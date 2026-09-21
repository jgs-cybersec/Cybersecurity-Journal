# Windows ICE

Exploitation of a windows OS.

The standard port number of MSRDP{Microsoft Remote Desktop}: 3389
When I ran a SYN scan only limited info related to open ports where displayed. But I did an Agressive scan to find out the ports in detail.
Then the output displayed a tcpwrapped detail on the 3389 port which means the scan tried to make a connection but was blocked.


An **impact score** measures the direct damage or consequences that would occur if a specific vulnerability is successfully exploited by an attacker.

## Meterpreter commands:

1. getuid: Host name
2. Sysinfo: details related to architecture, build etc.
   {This architecture boundary is exactly why you need **Privilege Escalation** in hacking. While exploiting, your initial shell landed inside a restricted User Mode space (Ring 3).
   To fully control the computer, you have to find an architecture exploit that forces the system to run your malicious code directly inside Kernel Mode or under a high-privilege system account (Ring 0).}
3. background: to background the session.
4. sessions: to list all the sessions.
5. getprivs: list the privilages enabled.
6. ps: to display the process
7. migrate -N PROCESS_NAME: to migrate to a running process.
8. load : to loas a tool.
   Mimikatz is a rather infamous password dumping tool that is incredibly useful. Kiwi is the updated version of Mimikatz.
   
