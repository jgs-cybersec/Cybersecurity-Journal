# Security Orchestration, Automation, and Response (SOAR)

## Traditional SOC and Challenges

**The main advantage of an organisation having a SOC is to enhance its security incident handling through continuous monitoring and analysis.** 

1. Alert Fatigue: Numerous tolls= huge number of alerts. Many of these alerts are false positives or insufficient for an investigation, hence analyst may end up taking wrong decisions.
2. Manual Processes: SOC investigation procedures are often not documented, leading to inefficient means of addressing threats. Most rely on established tribal knowledge built by experienced analysts, and the processes are never documented. This results in slowing down the investigation and increasing response times.

## Overcoming SOC Challenges using SOAR

With SOAR, SOC analysts do not need to switch between SIEM, EDR, Firewall, and other security tools for their investigations. They **can operate all these tools within a single SOAR interface**. Along with unifying the security tools, it also provides ticketing and case management features to the analysts, through which they can document, track, and resolve their incidents in a structured way.

The Orchestration, Automation, and Response capabilities of SOAR solve the major challenges a SOC team faces. With SOAR, there is no more alert fatigue, most of the processes are automated, and all the different tools are connected for coordination.

**Orchestration**------------->Playbook creation--------------->**Automation using the playbook created**------------->**Automated reponse**

SOAR **Playbooks/Automation Workflows** are predefined workflows that tell the SOAR tool what actions to take during a specific investigation.

SOAR = To automate repitative tasks

SOC Analyst = Essential for taking critical decision and response, creating different type of playbooks.
