# Cyber Kill  Chain

The framework defines the steps used by adversaries or malicious actors in cyberspace. To succeed, an adversary needs to go through all phases of the Kill Chain.
By understanding the Kill Chain as a SOC Analyst, Security Researcher, Threat Hunter, or Incident Responder be able to recognize the intrusion attempts and understand the intruder's goals and objectives. 

Stages(7):
1. Reconnaissance: research and planning phase of an attack. Adversaries use this phase to gather information about their target. A valuable piece of recon is OSINT (Open-Source Intelligence). Some public sources where OSINT data can be collected from include:

- Search engines
- Print and online media
- Social media accounts
- Online forums and blogs
- Online public record databases
- WHOIS and technical data

Reconnaissance type:-
- Passive: no direct interaction. Include WHOIS lookups, social media scraping, or reviewing breach data.
- Active: direct interaction. Activities such as social engineering, port scanning, banner grabbing (a reconnaissance technique used to gather information about computer systems, operating systems, and services running on open network ports. Nmap can be used), or probing for open services.

  

Tools used for reconnaissance are 
- theHarvester: other than gathering emails, this tool is also capable of gathering names, subdomains, IPs, and URLs using multiple public data sources.
- Hunter.io: this is an email hunting tool that will let you obtain contact information associated with the domain.
- OSINT Framework: OSINT Framework provides the collection of OSINT tools based on various categories.

2. Weaponization: After a successful reconnaissance stage, attacker would work on turning the raw information into actionable attack tools- **through crafting malware and exploits into a payload**.
- Most attackers usually use automated tools to generate the malware or
- refer to the DarkWeb to purchase the malware.
- More sophisticated actors or nation-sponsored APT (Advanced Persistent Threat Groups) would write their custom malware to make the malware sample unique and evade detection on the target.

Weaponization Phase Tactics:

- Create an infected Microsoft Office document containing a malicious **macros or VBA (Visual Basic for Applications) scripts**.
- Create a **malicious payload or a very sophisticated worm**, implant it on USB drives, and then distribute them in public.
- Set up **Command and Control (C2) infrastructure** for executing the commands on the victim's machine or deliver more payloads.
- Infect the victim's host with a **backdoor**, which would provide a way to access the computer system, and bypass the security mechanisms.
- Tailoring **phishing templates or OAuth-consent apps** to look legitimate and dupe the victim.

3. Delivery: The decision to choose the method for transmitting the payload or the malware onto the target environment. There are plenty of options: 

- Phishing email: The email would contain a malicious link or email attachment that would result into a compromise.

- USB drops: offer the attacker a physical delivery medium into public places like coffee shops, car parks, or on the street. 

- **Watering hole attacks** are targeted and designed to aim at a specific group of people by compromising the website they are usually visiting, redirecting them to a malicious website of the attacker's choice or creation. Victims would unintentionally download malware or a malicious application to their computer, resulting in a drive-by download. **An example can be a malicious pop-up asking to download a fake Browser extension**.

4.  Exploitation: The attacker's code executes on the target, taking advantage of a known vulnerability. key techniques to gain access:

- Malicious macro execution: This may have been delivered through a phishing email, that would execute ransomware when the victim opens it.
- Zero-day exploits: These leverages on unknown and unpatched flaws in a system. These exploits leave no opportunity for detection at the beginning.
- Known CVEs: The attacker can choose to exploit unpatched public vulnerabilities found on the target environment.

Signs of exploitation to look out for include:

- Unexpected process spawns.
- Registry changes or new services created.
- Suspicious command-line arguments found in system logs.
5. Installation: The attacker can install a persistent backdoor that will let the attacker access the system he compromised in the past. This can be achieved by-
  - Installing a web shell on the webserver. A web shell is a malicious script written in web development programming languages such as ASP, PHP, or JSP.
  - Installing a backdoor on the victim's machine. For example, the attacker can use Meterpreter(opens in new tab) to install a backdoor on the victim's machine.
  - Creating or modifying Windows services. An attacker can create or modify the Windows services to execute the malicious scripts or payloads regularly as a part     of the persistence.
  - Adding the entry to the "run keys" for the malicious payload in the Registry or the Startup Folder. By doing that, the payload will execute each time the user     logs in to the computer.

6. Command & Control: Opens up the C2 (Command and Control) channel through the malware to remotely control and manipulate the victim. This term is also known as C&C or C2 Beaconing as a type of malicious communication between a C&C server and malware on the infected host. The infected host will consistently communicate with the C2 server; that is also where the beaconing term came from. The most common C2 channels used by adversaries include:

- HTTP on port 80 and HTTPS on port 443, where this type of beaconing blends the malicious traffic with the legitimate traffic and can help the attacker evade firewalls.

- DNS (Domain Name Server), where the infected machine makes constant DNS requests to the DNS server that belongs to an attacker, this type of C2 communication is also known as DNS Tunneling
7. Exfilteration(Actions On Objectives): can finally achieve his goals, which means taking action on the original objectives. With hands-on keyboard access, the attacker can achieve the following: 

- Collect the credentials from users.
- Perform privilege escalation. 
- Internal reconnaissance (for example, an attacker gets to interact with internal software to find its vulnerabilities).
- Lateral movement through the company's environment.
- Collect and exfiltrate sensitive data.
- Deleting the backups and shadow copies. **Shadow Copy is a Microsoft technology that can create backup copies, snapshots of computer files, or volumes**. 
- Overwrite or corrupt data.
