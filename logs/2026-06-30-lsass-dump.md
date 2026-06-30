Daily Log Analysis Lab: June 30, 2026

Topic: **Credential Dumping via LSASS Memory Access (Sysmon Event ID 10)**

**Question:** The Scenario
You are a Tier 1 SOC Analyst at AuraGrid Power & Light, a metropolitan electric utility.
At 9:12 AM, your EDR (Endpoint Detection and Response) console triggers a high-severity alert on an engineering computer:

CRITICAL: LSASS Memory access handle opened by anomalous system utility on ENG-WORKSTATION-04.
Your Goal:
Analyze the raw Sysmon JSON log below, isolate the key indicators of compromise (IoCs), calculate the operational risk score, and decide on containment playbooks.

The Raw Sysmon JSON Log
```
{
  "timestamp": "2026-06-30T09:12:01.442Z",
  "event_id": 10,
  "provider_name": "Microsoft-Windows-Sysmon",
  "computer_name": "ENG-WORKSTATION-04",
  "security_channel": "Microsoft-Windows-Sysmon/Operational",
  "event_data": {
    "SourceImage": "C:\\Windows\\System32\\rundll32.exe",
    "TargetImage": "C:\\Windows\\System32\\lsass.exe",
    "GrantedAccess": "0x1410",
    "CallTrace": "C:\\Windows\\SYSTEM32\\ntdll.dll+0xa7240|C:\\Windows\\System32\\comsvcs.dll+0x1842d|C:\\Windows\\System32\\rundll32.exe+0x5442",
    "SourceUser": "AURAGRID\\engineering_admin"
  }
}
```






**Technical Explanation**

**?** What is LSASS? 
The **Local Security Authority Subsystem Service (lsass.exe)** is a critical Windows system process responsible for enforcing security policies, verifying users logging in, and handling password changes.

**?** Why do attackers target it? 
To make Windows fast, LSASS temporarily stores active user passwords (in plain text or encrypted NTLM hash form) directly inside the computer's RAM.

**?** What is the attack vector? 
Attackers use administrative tools to read the memory space of lsass.exe and dump it into a .dmp file. They then copy this dump file to their own system and use tools like Mimikatz to extract plain-text administrative passwords from it.

**?** What is the **"Living off the Land" trick** here? 
The attacker didn't download a virus binary. They used rundll32.exe (a safe, built-in Windows utility) and pointed it at comsvcs.dll (a built-in Windows mini-program used to dump crashed processes). They hijacked safe Windows tools to bypass security detection!

 
 
 
 
 **Applying Your "Who, What, How" Filter**

**WHO** is the user? Look at SourceUser. ***AURAGRID\\engineering_admin (An extremely high-privilege account).***

**WHAT** was the target? Look at TargetImage. ***Sysmon Event ID 10 (Process Access) targeting lsass.exe (Credential Dumping).***

**HOW** did they execute it? Look at SourceImage and the CallTrace (look specifically for the .dll being used). ***Executed using the built-in Windows binary rundll32.exe leveraging comsvcs.dll (Mini-dump function) to read memory. This is confirmed by the access mask 0x1410 (which stands for PROCESS_VM_READ and PROCESS_QUERY_INFORMATION).***

**WHY** is this highly dangerous? (Hint: Think about ***the credentials being targeted*** and the computer classification).




**THE VERDICT:** 
**True Positive (Credential Harvesting Attempt). This is a signature lateral-movement and privilege-escalation technique used by advanced actors.**



**Playbook Containment Actions:**

EDR Isolation: Isolate ENG-WORKSTATION-04 from the network immediately to prevent password export.

Credential Revocation: Reset the passwords for engineering_admin and any other user logged into that workstation immediately across Active Directory.

Forensic Sweeping: Check the workstation disk for .dmp or .tmp files in C:\Windows\Temp\ or C:\Users\Public\ created at the exact timestamp to locate the dumped credentials.





**Detailed Study notes**

1.Living off the Land Binary (LOLBin):
Instead of downloading a suspicious virus file that antivirus programs would instantly block, the attacker hijacked native, trusted Windows tools to steal credentials directly from RAM.This is why "Living off the Land" is so incredibly stealthy—to the computer, it just looks like a normal administrator doing normal system troubleshooting.
(note: Living off the Land means- instead of buying something, surviving by using the nature like hunting, growing cropsetc.)

2.Sysmon (System Monitor):
An advanced Windows logging service. Unlike standard security logs, Sysmon is highly detailed and tells us exactly when programs read other programs' memory.
