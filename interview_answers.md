# Interview Questions — Answers

1. What is an open port?**  
   An open port is a network port where an application or service is listening and ready to accept incoming connections.

2. How does Nmap perform a TCP SYN scan?**  
   Nmap sends a TCP SYN packet to a port. If the target replies with SYN/ACK the port is considered open (scanner typically responds with RST to avoid completing the handshake), if it replies RST then the port is closed. No reply or ICMP unreachable suggests the port is filtered.

3. What risks are associated with open ports?**  
   They expose running services that can be exploited if they have vulnerabilities or weak authentication, leading to unauthorized access, data theft, or lateral movement.

4. Explain the difference between TCP and UDP scanning.**  
   TCP scanning uses the TCP handshake responses to determine port state. UDP is connectionless—absence of response is inconclusive (open|filtered), so UDP scans need more time and generate more ambiguous results.

5. How can open ports be secured?**  
   Close unused services, restrict access with firewalls, patch software, use strong credentials and MFA, limit exposure via VPNs, and apply network segmentation.

6. What is a firewall's role regarding ports?**  
   It allows or blocks traffic to/from specific ports and IPs, reducing exposure by enforcing network access policies.

7. What is a port scan and why do attackers perform it?**  
   It's the act of probing ports on a host to find available services. Attackers scan to discover potential attack vectors and vulnerable services.

8. How does Wireshark complement port scanning?**  
   Wireshark captures packet-level traffic so you can inspect protocol exchanges, confirm how a service responds, and analyze suspicious traffic that a port scan reveals.
