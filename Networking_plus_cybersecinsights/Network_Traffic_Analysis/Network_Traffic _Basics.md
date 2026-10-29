# Network Traffic Basics

Network Traffic Analysis (NTA) is a process that encompasses capturing, inspecting, and analyzing data as it flows in a network. 
Its goal is to have complete visibility and understand what is communicated inside and outside the network.

**NTA != Wireshark Tool**

## Why do we need to analyze network traffic?

The devices like Firewall and others only captures or identifies only the query but not the query content. 
The knowledge of the content of the query is essential to determine whether the query id malicious.
There may be a possibility of data exfiltration via DNS- which is smuggling C2 commands in the query. This technique is called DNS Tunneling. 
Therefore network traffic need to be analyzed.

As a SOC Analyst, the network Traffic analysis helps in-
1. Detecting malicious/ suspicious activities.
2. Reconstructing the attack during incidence Response.
3. Verifying and validating alerts.

