# Cyber Kill  Chain

The framework defines the steps used by adversaries or malicious actors in cyberspace. To succeed, an adversary needs to go through all phases of the Kill Chain.
By understanding the Kill Chain as a SOC Analyst, Security Researcher, Threat Hunter, or Incident Responder be able to recognize the intrusion attempts and understand the intruder's goals and objectives. 

Stages:
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

