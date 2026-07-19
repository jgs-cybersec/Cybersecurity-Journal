================================================================================
📝 DEEP DIVE MASTER NOTES: LAYER 4 PROTOCOLS (TCP VS. UDP)
================================================================================

1. ## TCP MECHANICS & EXPLOITATION
   - Stateful protocol that uses Sequence/Acknowledgment numbers to ensure 
     ordered and error-free data delivery.
   - Attack vector: SYN Floods target the connection allocation state during the 
     3-way handshake, exhausting memory (TCB buffers) on the target host.

 ### The 3-way TCP Handshake
 ```
 CLIENT                                                  SERVER
  │                                                       │
  │ ─── 1. SYN (seq=1000) ──────────────────────────────> │ [Allocates TCB Memory]
  │                                                       │
  │ <─── 2. SYN-ACK (ack=1001, seq=5000) ───────────────  │ 
  │                                                       │
  │ ─── 3. ACK (ack=5001) ──────────────────────────────> │ [Connection Established]
  ▼                                                       ▼
```

  **SYN Flood DoS**: 
  
  The exact millisecond the server receives the initial SYN packet (Step 1), it must allocate space in its physical RAM—known as a **Transmission Control Block (TCB)** buffer—to remember this pending connection.  
  An **attacker can send millions of spoofed SYN packets from non-existent IP addresses**. The server dutifully responds with a SYN-ACK and sits waiting for the final ACK (Step 3) that will never come. 
  The server's RAM buffer fills up entirely with "half-open" connections, causing it to crash or refuse legitimate users.

  **TCP Session Hijacking**:
  
  Once the handshake is done, the server validates the user solely by checking if the sequence numbers in incoming packets match what it expects. 
  If an attacker is on the same network path and can read or guess the next sequence numbers, **they can inject a malicious command packet with the exact expected sequence number**. 
  The server accepts it blindly, effectively hijacking the authenticated session.

  

2. ## UDP MECHANICS & EXPLOITATION
   - Stateless, unreliable protocol prioritizing raw speed and low overhead.
   - Attack vector: The absence of a handshake permits trivial source IP spoofing, 
     serving as the structural foundation for DNS/NTP Amplification DDoS attacks.

   **No Head-of-Line Blocking**:
   
   - In TCP, if packet #2 is lost, packets #3, #4, and #5 must sit in memory waiting for #2 to be retransmitted.
 
   - UDP does not care—if packet #2 drops, packet #3 is processed instantly by the application.

   - This makes it perfect for live streaming, gaming, and real-time DNS.


   **IP Spoofing**:
   
   If an attacker crafts a raw TCP packet with a fake source IP, the 3-way handshake breaks because the server sends the SYN-ACK to the fake IP, neutralizing the attack.
   In UDP, because there is no verification return loop, forging the source IP address is trivial.

   **DDoS Amplification Attacks (DNS)**:
   
   Attackers exploit UDP to launch massive Distributed Denial of Service (DDoS) attacks:
   
   -The attacker sends a tiny UDP request (like a DNS query asking for all records) to an open server on the internet.
   
   -The attacker spoofs the source IP address, modifying it to match the IP address of their victim.
   
   -The server generates a massive response payload (often 50 to 100 times larger than the request) and fires it directly at the unsuspecting victim.
   By utilizing thousands of open UDP reflectors, an attacker can easily flood a target enterprise completely offline. 
================================================================================
