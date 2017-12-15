**arp-recon.pcapng**
  - This trace depicts an ARP reconnaissance process.
  - What would explain the non-sequential target IP addresses?
  - Can you determine the subnet mask of the transmitter by the ARP target addresses?

**icmp-routersolicitation.pcapng**
  - This trace file contains numerous discovery packets.
  - How can ICMP Router Solicitation be used to alter the default gateway setting of 10.1.22.2?

**sec-nmap-ackscan.pcapng**
  - This trace file depicts the default Nmap scan process.
  - How many different discovery processes can you detect?

**sec-nmap-robots-plus.pcapng**
  - Nmap is scanning a site for a robots.txt file (a file defining how web robots should behave when visiting the site).
  - In particular, Nmap is interested in what might be disallowed. Apply a filter for http.request.method.
  - What else is Nmap doing?

**sec-nst-osfingerprint.pcapng**
  - This trace shows an OS fingerprinting operation from NetScanTools Pro.
  - Create a display for ICMP Echo packets that have a non-zero code value.
  - This filter will help you discover what NetScanTools Pro’s signature is in this trace.

**sec-spoofedhost.pcapng**
  - Using Nmap, IP address is hidden among other source addresses.
  - This trace was taken on the host performing the scan.
  - Can you detect the true IP address of the host ?

**sec-strangescan.pcapng**
  - What is the scanner doing?
  - Look at the TCP Flag settings in the scan packets.
  - What is triggering the "TCP ACKed lost segment" expert notification in Wireshark?
