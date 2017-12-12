### Detection and discovery

Some general filters to tcp scans
```sh
tcp.flags==0x000
# null scan

tcp.flags==0x029
# xmas scan URG (URGENT),FIN and PUSH Flags are set

```

###Some popular UDP based services
**DNS**: UDP Port Number 53
**SNMP**: UDP Port Number 161/162
**DHCP**: UDP Port Number 67/68
**SIP**: UDP Port Number 5060
**NetBIOS Name Service**: UDP Port Number 137/139 # Generally same purpose as DNS



###Port Status
**Closed Port**: If you send a SYN to a closed port, it will respond back with a RST.
**Filtered Port**: Presumably, the host is behind some sort of firewall. Here, the packet is simply dropped and you receive no response (not even a RST).
**Open Port**: If you send a SYN to an open port, you would expect to receive SYN/ACK.


### Services running directly over IP
**ICMP**: IP Protocol Number 1
**IGMP**: IP Protocol Number 2
**TCP**: IP Protocol Number 6
**EGP**: IP Protocol Number 8
**IGP**: (used for IGRP): IP Protocol Number 9
**UDP**: IP Protocol Number 17

### Example of FTP mappings in nmap
```sh
match ftp m|^220[- ]FileZilla Server version (\d[-.\w ]+)\r\n| p/FileZilla ftpd/ v/$1/ o/Windows/15579
match ftp m|^220 ([-\w_.]+) running FileZilla Server version (\d[-.\w ]+)\r\n| p/FileZilla ftpd/ v/$2/ h/$1/ o/Windows/15579
match ftp m|^220 FTP Server - FileZilla\r\n| p/FileZilla ftpd/ o/Windows/15579
match ftp m|^220-Welcome to ([A-Z]+) FTP Service\.\r\n220 All unauthorized access is logged\.\r\n| p/FileZilla ftpd/ h/$1/ o/Windows/15579
match ftp m|^220.*\r\n220[- ]FileZilla Server version (\d[-.\w ]+)\r\n|s p/FileZilla ftpd/ v/$1/ o/Windows/15579
match ftp m|^220-.*\r\n220-\r\n220 using FileZilla FileZilla Server version ([^\r\n]+)\r\n|s p/FileZilla ftpd/ v/$1/ o/Windows/15579
match ftp m|^431 Could not initialize SSL connection\r\n| p/FileZilla ftpd/ i/Mandatory SSL/ o/Windows/15579
match ftp m|^550 No connections allowed from your IP\r\n| p/FileZilla ftpd/ i/IP blocked/ o/Windows/15579
```

### Some common user agent definitions
```sh
Mozilla/5.0 (Windows; U; Windows NT 6.0; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
# [likely a Vista host with .NET framework running Firefox v3.5.5]

Mozilla/5.0 (Windows; U; Windows NT 5.1; de; rv:1.9.1.4) Gecko/20091016 Firefox/3.5.4 (.NET CLR 3.5.30729)
# [likely a Windows XP host running Firefox v3.5.4]

Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; GTB6.3; .NET CLR 2.0.50727; InfoPath.2)
# [likely a Windows XP host running Internet Explorer v6.0 and Service Pack 2]

Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; .NET CLR 1.1.4322; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; InfoPat
# [likely a Windows XP host with the .NET framework running Internet Explorer v7.0]

Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .N
# [likely a Windows 7 host with .NET framework running 32-bit version of Internet Explorer v8.0 compatibility view on a 64-bit Windows OS]

Mozilla/5.0 (Windows; U; Windows NT 6.0; en-US) AppleWebKit/532.0 (KHTML, like Gecko) Chrome/3.0.195.33 Safari/532.0
# [likely a Vista host running Chrome v3.0.195.33]

Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; Media Center PC 5.0; OfficeLiveConnector.1
# [likely a Vista Media Center Edition host with .NET framework running Internet Explorer v7.0 with Office Live Workspace installed]

vodafone/1.0/SFR_v3650/1.25.163.3 (compatible; MSIE 6.0; Windows CE; IEMobile 7.6)
# [likely Windows CE running Internet Explorer v7.6 on a mobile device (Vodafone)]

Mozilla/5.0 (X11; U; Linux i686; en-US) AppleWebKit/532.5 (KHTML, like Gecko) Chrome/4.0.251.0 Safari/532.5
# [likely a Linux host running Chrome v4.0.251.0]

Mozilla/5.0 (webOS/1.3.1; U; en-US) AppleWebKit/525.27.1 (KHTML, like Gecko) Version/1.0 Safari/525.27.1 Pre/1.0
# [likely a Palm Pre 1.0 running Safari v1.0]

Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; Trident/4.0; SLCC1; .NET CLR 2.0.50727; InfoPath.2; .NET CLR 3.5.3072
# [likely a Windows Vista host with .NET framework running Internet Explorer v8.0 compatibility view]

javascript:alert(navigator.userAgent)
# check your browser user agent
```


### Nmap Active OS fingerprinting signatures
```sh
ICMP Echo Request (Type 8) with no payload
ICMP Echo Request (Type 8) with 120 or 150 byte payload of 0x00s
ICMP Timestamp Request with Originate Timestamp value set to 0
TCP SYN with 40 byte options area
TCP SYN with Window Scale Shift Count set to 10
TCP SYN with Maximum Segment Size set to 256
TCP SYN with Timestamp Value set to 0xFFFFFFFF
TCP packet with options and SYN, FIN, PSH and URG bits set
TCP packet with options and no flags set
TCP Acknowledgment Number field non-zero without the ACK bit set TCP packets with unusual TCP Window Size field values
```

### Some useful filters to spot NMAP fingerprinting
```sh
(tcp.flags==0x02) && (tcp.window_size < 1025)
#TCP SYN/ACK with a TCP Window Size field value less than 1025

tcp.flags==0x2b
#TCP SYN, FIN, PSH and URG bits set

tcp.flags==0x00
#No TCP flags set

(icmp.type==13) && (frame[42:4]==00:00:00:00)
#ICMP Timestamp Request with Originate Timestamp Value set to 0 (Ethernet II header structure)

tcp.options.wscale_val==10
#TCP Window Scale Option set to 10

tcp.options.mss_val < 1460
#TCP Maximum Segment Size value set to less than 1460 
```
