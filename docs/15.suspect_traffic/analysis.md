## Unacceptable Traffic

  - Maliciously malformed packets—intentionally malicious packets.
  - Traffic to invalid or unassigned IP or MAC addresses.
  - Flooding or denial of service traffic—traffic sent at a high packet per second rate.
  - Clear text passwords—passwords that are visible.
  - Clear text data. Data that is visible or able to be reconstructed
  - Phone home traffic. Traffic patterns indicating an application is checking in periodically with a remote host.
  - Unusual protocols and applications—protocols and applications that are not commonly seen or allowed on the network.
  - ARP poisoning. Altering target ARP tables for redirection of local traffic through another host—used for man-in-the-middle attacks.
  - IP fragmentation and overwriting—using the IP fragment offset field setting to overwrite previous data sent to a target.
  - TCP splicing—obscuring the actual TCP data to be processed at the peer.
  - Password cracking attempts—repeated attempts to guess an account password over a single connection or multiple connections.


### Example display filter for traffic to unknown addresses
  - 192.168.0.1-4 <-> routers
  - 192.168.0.100-112 <-> servers
  - 192.168.0.140-211 <-> clients

```sh
(ip.dst > 192.168.0.4 && ip.dst < 192.168.0.100) ||
(ip.dst > 192.168.0.112 && ip.dst < 192.168.0.140) ||
(ip.dst > 192.168.0.211 && ip.dst <= 192.168.0.255)
```

### IP header fields to identify package fragmentation
 - May Fragment field (one bit long): 0 = may fragment; 1 = don’t fragment.
 - More Fragments field (one bit long): 0 = no more fragments to come; 1 = more fragments to come.
 - Fragment Offset field (13 bits long): This field is used to reassemble the fragmented data in the correct order.
