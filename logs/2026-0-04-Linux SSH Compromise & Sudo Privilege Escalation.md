# Linux SSH Compromise & Sudo Privilege Escalation

## The scenario

`ALERT: Successful SSH login followed immediately by high-privilege sudo execution from a non-standard IP.`

## Goal

Analyze the raw `/var/log/auth.log` entries below, apply your security filters, identify the exact sequence of events, and explain what commands you would use on the terminal to investigate the active threat.

## The Raw `/var/log/auth.log` Snippet

 Jul  4 15:22:10 volt-db-prod sshd[18402]: Failed password for invalid user admin from 198.51.100.72 port 49210 ssh2

Jul  4 15:22:15 volt-db-prod sshd[18405]: Failed password for invalid user root from 198.51.100.72 port 49214 ssh2

Jul  4 15:22:21 volt-db-prod sshd[18410]: Accepted password for web_developer from 198.51.100.72 port 49218 ssh2

Jul  4 15:22:22 volt-db-prod sshd[18410]: pam_unix(sshd:session): session opened for user web_developer(uid=1003) by (uid=0)

Jul  4 15:23:02 volt-db-prod sudo: web_developer : TTY=pts/1 ; PWD=/tmp ; USER=root ; COMMAND=/usr/bin/apt-get install -y netcat-traditional

Jul  4 15:23:45 volt-db-prod sudo: web_developer : TTY=pts/1 ; PWD=/tmp ; USER=root ; COMMAND=/usr/bin/nc.traditional -lvnp 8888 -e /bin/bash 

## Analyst Answer

1. **Initial Attack Pattern**: A Credential **Brute-Force (Password Guessing) Attack**. The attacker tried logging in as admin and root but failed.

2. The **Compromised User**: **web_developer (UID 1003)**. The attacker guessed this user's password correctly, resulting in an Accepted password log entry.

3. **Attack Source IP**: 198.51.100.72.

4. **Privilege Escalation & Backdoor**:

The attacker leveraged **sudo** to run commands as root (administrative context).

They operated from the world-writable directory **/tmp** (a classic malware landing pad).

They installed **Netcat** and executed nc.traditional -lvnp 8888 -e **/bin/bash** to open a root-level backdoor shell listening on **Port 8888**.

## Active Troubleshooting Command:

To verify if the backdoor is still active, you would run:

`ss -tulnp | grep ":8888"`

## Incident Response Actions Required:

1.Run `kill -9 [PID]` to instantly terminate the running Netcat listener.

2.**Isolate the server network interface from the corporate segment immediately**.

3.**Lock the account web_developer and audit `/etc/sudoers` to remove their high-level permissions**.

## Output Of the command `ss -tulnp | grep ":8888"`

If  the backdoor is active, the terminal will print an output line that looks like this:

`tcp   LISTEN 0      10         0.0.0.0:8888       0.0.0.0:* users:(("nc.traditional",pid=18415,fd=3))`

1. **tcp** (The Protocol)
This confirms the port is using the TCP (Transmission Control Protocol) standard, which is connection-oriented and perfect for interactive hacker shell sessions.

2. **LISTEN** (The State)
This is the red alert! It means the port is actively open and "listening," waiting for someone from the outside world to connect to it.

3. **0.0.0.0:8888** (The Local Address & Port)
0.0.0.0 means the program is listening on every network interface card on the machine (local network, internet, loopback). :8888 is the port number we searched for.

4. **0.0.0.0:*** (The Peer Address)
This means anyone (*) from any IP address in the world is allowed to connect to this listening port.

5. **users:(("nc.traditional",pid=18415,fd=3))** (The Program & PID)
*This is the most important forensic clue:*

**nc.traditional**: This is the exact name of the program holding the port open. It tells you Netcat is the culprit!

**pid=18415**: This is the unique Process ID assigned by the Linux kernel.









