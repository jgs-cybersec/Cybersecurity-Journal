# Endpoint Detection and Response (EDR)

Endpoint Detection and Response (EDR) is a security solution designed to monitor, detect, and respond to advanced threats at the endpoint level. 
As a SOC analyst, it is essential for you to understand how the EDR works since it is a widely adopted solution in organizations to protect their endpoints.

As long as the endpoints are inside the organisation's network perimeter, the systems are secure and can be reponded to the threats that affects the system. 
But the adoption of remote work has exposed these devices as they are out of the perimeter protection deployed on the organization's network.

To ensure these endpoint devices are protected even out of the network, we need a security solution that guards all devices in different areas and is capable of fighting advanced threats. Endpoint Detection and Response (EDR) is a security solution that offers deep-level protection for endpoints. 
**No matter where the endpoints are, the EDR will make sure they are monitored constantly and threats are detected**.

Some of the EDRs-
1. CrowdStrike Falcon
2. Symantec EDR
3. SentinelOne EDR
4. Microsoft Defender for Endpoint


## Features of EDR

### 1. Visibility

It **collects detailed data from the endpoints, which includes process modifications, registry modifications, file and folder modifications, user actions, and much more.**
It then presents this information in a very structured format to the analyst. 
The analyst can see the whole process tree with a complete activity timeline of the sequence of actions. The analyst can also access the historical data of any endpoint for threat hunting or any other purpose. 
Any **detections in the EDR land with a whole context**.

### 2. Detection

It incorporates **signature-based detections as well as behavior-based detections**, such as unexpected user activities. 
With modern machine learning capabilities, it **identifies any deviation from the baseline behavior and instantly flags it**. 
It can also **detect fileless malware that resides in memory**. 
It also allows us to feed custom IOCs(Indicators of Compromise) for threat detections.

### 3. Response

EDR also empowers analysts to take action on detected threats. 
These **actions can be taken at any endpoint within the central EDR console**.
Imagine getting a detection on the EDR with full-fledged details on when, where, and what happened, and you have to opt for the best possible action for that detection. 
As an analyst, you may **decide to isolate a complete endpoint, terminate a process, or quarantine some files**. 
Also can  **connect to the host remotely and execute actions independently via EDR console**.

## Why do we need an EDR when we already have an Antivirus (AV) on the endpoints?

Both of these security solutions have the same motive of protecting the endpoint on which they are installed. 
However, **both differ in the level of protection they provide**.

The **Antivirus (AV) may detect some basic threats, but to detect advanced threats that evade normal detections, we need an EDR**. 
**Unlike antivirus software's basic signature-based detection, it monitors and records the behaviors of the endpoint**. 
An EDR also provides organization-wide visibility of any activity. 
For example, if a suspicious file is detected on one endpoint, the EDR will also check it across all the other endpoints.

Antivirus: signature based detection. check the signature(file hash etc.) of the file and compared with the blacklisted signature with it. 
So, if the malware is a new script then there will not be any signature, hence can't detect the malware.

EDR: Behavior based detection. Instead of checking what is it, these kind of detection solutions prefer to check what will this file do? 
Hence will monitor each action of this file and report security threats. 


## Detection and Response Capabilities

Some of the detection techniques are-
1. Behavioural Detection: Observes the complete behavior of a file.
2. Anomaly Detection:  deviates from this baseline behavior.
3. IOC matching: Except for zero-day attacks, most of the attacks have indicators published in the threat intelligence feeds.
4. MITRE ATT&CK Mapping: not only marked as malicious or suspicious but also mapped with the MITRE Tactic and Technique (attack stage) that the particular activity was on.
5. Machine Learning Algorithms: Modern EDRs have machine learning models trained by a large dataset of normal and malicious behaviors. This can detect complex patterns of an attack. Fileless attacks and multi-staged intrusions are often detected through this.

Some of the responses are-
1. Isolate Host:
2. Terminate Process: Instead of isolating an endpoint which may be the business core host, a particular process can be terminated by making sure that the termination of the process is not disrupting the endpoint on working.
3. Quarantine: Quarantine ensures that the file is moved to an isolated location where it can not be executed.
4. Remote Access: Remotely access the shell of any endpoint. Analysts can gain deeper visibility into the system or take custom actions within the endpoints. The analysts can also run scripts or collect their desired data from the host through remote access.
5. Artefacts Collection: extract some data from the endpoints for detailed forensic investigation or reporting for legal actions without physically accessing the device. details are- Event logs, Registry Hive, Memory Dump, Specific folder contents.
   
