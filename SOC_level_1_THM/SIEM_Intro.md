# Security Information and Event Management system (SIEM)

This is the core security solution that a SOC analyst uses in the security operations center.

Log sources are of two types-
1. Host-Centric Logs:  Devices that generate host-centric logs include Windows, Linux, servers, etc. Some examples of host-centric logs are:
- A user accessing a file
- A user attempting to authenticate.
- A process execution activity
- A process adding/editing/deleting a registry key or value.
- PowerShell execution
2. Network-Centric Logs: Devices that generate network-centric logs are firewalls, IDS/IPS, routers, etc. Some examples of network-centric logs are:
- SSH connection
- A file being accessed via FTP
- Web traffic
- A user accessing the company's resources through VPN.
- Network file sharing Activity


## Challenges while analysing Logs

-  A network has many log sources, which generate hundreds of events per second.
-  As logs reside on the machines on which they are generated,  you may need to connect with each log source via SSH, RDP, etc., to analyze logs from multiple log sources. This is very inefficient and can waste a lot of your valuable time during the investigations.
-  Difficult to correlate logs.
-  Numerous logs per second from multiple sources result in inefficient analysis of the logs.
-  Different logs have different formats and it is difficult for analysts to learn all formats.


 **Security Information and Event Management (SIEM) is a security solution that collects logs from various types of log sources, standardizes their format into a consistent one, correlates them, and detects malicious activities using detection rules.**
 
 ### Features of SIEM 

- SIEM collects logs from all sources (endpoints, servers, firewalls, etc.) and centralizes them in one place. These logs are pulled through lightweight agents or APIs and populated into the SIEM solution. This solves the problem of jumping on every machine individually to analyze its logs.
- Breaking down a log into several fields for ease of understanding is known as **Parsing**, and converting all the logs of various log sources into one consistent format is known as **Normalization**
- Individual logs are not very useful. SIEM correlates the logs of different sources and finds any relationship between them.
- Analysts make new detection rules based on their requirements to mature future detections. When the conditions for these detection rules are satisfied, alerts are triggered, and the analysts are notified. Analysts can then investigate these alerts within the SIEM platform.
-  The summary of this analysis is presented in the form of actionable insights with the help of multiple dashboards.


## Log Ingestion

Each SIEM solution has its own way of ingesting the logs. Some common methods used by these SIEM solutions are-
1. Agent / Forwarder: a lightweight tool called an agent (forwarder by Splunk) that gets installed on the Endpoint. It is configured to capture and send all the important logs to the SIEM server.
2. Syslog: a widely used protocol to collect data from various systems like web servers, databases, etc., and send real-time data to the centralized destination.
3. Manual Upload: Some SIEM solutions, like Splunk, ELK, etc., allow users to ingest offline data for quick analysis. Once the data is ingested, it is normalized and made available for analysis.
4. Port-Forwarding: SIEM solutions can also be configured to listen on a certain port, and then the endpoints forward the data to the SIEM instance on the listening port.






 
