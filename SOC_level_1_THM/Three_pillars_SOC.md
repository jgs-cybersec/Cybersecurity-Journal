# The Three Pillars

## **People-**

**People in a SOC** will always be important.In a SOC, with security solutions in place without human intervention, you'll end up focusing on more irrelevant issues. There are always the People who help the security solution to identify truly harmful activities and enable a prompt response.

<img width="1562" height="627" alt="image" src="https://github.com/user-attachments/assets/913b8fa5-cc40-4ab8-92ed-735fd30444ac" />

SOC Analyst (Level 1): 

These are the first responders to any detection. SOC Level 1 Analysts **perform basic alert triage** to determine if a specific detection is harmful. They also report these detections through proper channels.
 
SOC Analyst (Level 2): 

While Level 1 does the first-level analysis, some detections may require **deeper investigation**. Level 2 Analysts help them dive deeper into the investigations and correlate the data from multiple data sources to perform a proper analysis.

SOC Analyst (Level 3): 

Level 3 Analysts are experienced professionals who proactively look for any threat indicators and support in the incident response activities. The critical severity detection reported by Level 1 and Level 2 Analysts are often security incidents that need detailed responses, including containment, eradication, and recovery. This is where Level 3 analysts’ experience comes in handy.

Security Engineer: 

All analysts work on **security solutions**. These solutions need deployment and configuration. Security Engineers deploy and configure these security solutions to ensure their smooth operation.

Detection Engineer: 

**Security rules are the logic built behind security solutions** to detect harmful activities. Level 2 and 3 Analysts often create these rules, while the SOC team can sometimes also utilize the detection engineer role independently for this responsibility.

SOC Manager:

The SOC Manager manages the processes the SOC team follows and provides support. The SOC Manager also remains in contact with the organization’s **CISO (Chief Information Security Officer)** to provide him with updates on the SOC team’s current security posture and efforts.


## **Process-**

Each role in the SOC team have their own process to carry out. The process that need to be done by SOC Analyst level 1 is -**Alert Triage**

### Alert Triage

<img width="1601" height="717" alt="image" src="https://github.com/user-attachments/assets/5f7762d2-97e6-4d2d-985a-093f91f41d69" />

<img width="1597" height="592" alt="image" src="https://github.com/user-attachments/assets/c5ff2e70-db83-4501-b4ac-61b0820f3457" />

After carrying out this process SOC Analyst L1 should make a report based on this triage and give it to higher level people.

### Incident Response and Forensics:

By inspecting the detection deeply the higher-ups suggests to the incident response team if the alert is critical in nature.


## **Technology-**

The Technology portion in the SOC pillars refers to the **security solutions**. 
These security solutions efficiently minimize the SOC team's manual effort to detect and respond to threats.

Security solutions:-------> Centralizes the all the information of the devices or applications present in the network
                  --------> Automates the detection and response capabilities.


Some of the security solutions are-
1. SIEM: collects logs from various network devices----> detect after correlating them with multiple log sources----->alerts us in case of a match with any of the rules

2. EDR:  provides the SOC team with detailed real-time and historical visibility of the devices’ activities. 
It operates on the endpoint level and can carry out automated responses. 

3. Firewall: For network security----> acts as a barrier between your internal and external networks (such as the Internet)-----> monitors incoming and outgoing network traffic and filters any unauthorized traffic.
 has some detection rules deployed------>  helps to identify and block suspicious traffic. 
