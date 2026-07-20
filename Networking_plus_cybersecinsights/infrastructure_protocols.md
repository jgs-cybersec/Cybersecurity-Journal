================================================================================
📝 DEEP DIVE MASTER NOTES: INFRASTRUCTURE & RESOLUTION PROTOCOLS
================================================================================

1. ### DNS VARIATIONS & ATTACK VECTORS
   - Legacy DNS (UDP 53) is highly vulnerable to injection and cache poisoning.
   - DNSSEC adds data integrity via cryptographic signatures (RRSIG).
   - DoT (Port 853) and DoH (Port 443) wrap queries in TLS to enforce privacy.
  


#### Domain Name System (DNS) 

- DNS **maps human-readable names (target.com) to machine-routable IP addresses** (192.0.2.1). 
- By default, traditional DNS operates completely in the clear over UDP port 53, making it highly vulnerable to exploitation.

#### The Classical Vulnerability: DNS Cache Poisoning (Kaminsky Attack)
Because UDP is stateless and lacks source verification, a remote attacker can trick a local DNS resolver into caching a fraudulent IP address for a legitimate domain name.

#### Defence Remedies:


**DNSSEC (DNS Security Extensions)**:

Addresses authenticity. It adds cryptographic digital signatures (RRSIG) to existing DNS records. When a resolver receives a response, it requests the public key (DNSKEY) of the zone to cryptographically verify that the record was not altered in transit. 
Crucial note: DNSSEC provides integrity, but it does not provide privacy; data is still sent in plaintext.

**DoT (DNS over TLS)**:

Addresses privacy on the wire. It wraps standard DNS queries inside a secure **TLS tunnel over TCP port 853**. This blinds intermediate ISPs or eavesdroppers on local networks from seeing what domains a user is looking up.





2. ### LOCAL & GLOBAL ROUTING SECURITY (DHCP)
   - DHCP has zero inherent trust boundaries; mitigate Rogue Gateways using 
     Switch-level DHCP Snooping.
   

#### DHCP (Dynamic Host Configuration Protocol)
- DHCP **automates the assignment of IP addresses, subnet masks, default gateways, and DNS servers to endpoints on a local area network (LAN)**. 
- It uses a four-step lease process known as DORA operating over **UDP ports 67 and 68**.

##### The DORA Handshake

**Discover**: The newly connected client broadcasts a request looking for a DHCP server.

**Offer**: Any listening DHCP server broadcasts or unicasts an available IP configuration.

**Request**: The client selects the first offer it receives and requests to lease that IP.

**Acknowledge (ACK)**: The server finalizes the lease commitment.

#### The Cybersecurity Angle: Resource Starvation & Rogue Gateways

DHCP features absolutely **no native authentication; it trusts any device connected to the physical layer or VLAN switch port**.

A. **DHCP Starvation Attacks**

- An attacker runs a tool (like Yersinia) that generates thousands of fake MAC addresses and floods the network with DHCP Discover packets. 
- The legitimate DHCP server responds to each, exhausting its entire pool of available IP addresses. New corporate laptops connecting to the network are denied an IP and cannot access network resources.

B. **Rogue DHCP Server (Man-in-the-Middle)**

- While the real DHCP server is starved, the attacker stands up a fake DHCP server on their own machine. 
- When a legitimate client broadcasts a Discover packet, the attacker answers first.
- The attacker assigns the client a valid IP, but sets the Default Gateway and DNS Server settings to point directly to the attacker's machine. 
- Every packet destined for the internet is now funneled through the attacker's machine for full packet capture decryption and manipulation.

**Enterprise Defense**: 

Network engineers implement **DHCP Snooping on Layer 2 switches**. 
This hardcodes specific physical switch ports (connected directly to the real server) as "Trusted", while instantly dropping any DHCP Offer packets seen originating from untrusted employee-facing switch ports.



```
Protocol, |  Default Transport, |   Primary Vulnerability,        |  Core Enterprise Mitigation
------------------------------------------------------------------------------------------------
DNS,      |    UDP 53,          |     Cache Poisoning / Spoofing, |  DNSSEC Validation, DoT / DoH Deployment
DHCP,     |   UDP 67/68,        |    Rogue Servers / Starvation,  |  DHCP Snooping on Switch Ports

```
================================================================================
