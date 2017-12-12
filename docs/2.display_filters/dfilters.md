### Examples of very simple display filters  
```sh
tcp
ip  
udp
ssl
arp  
dns  
```

### Display filters based on packet characteristics (not actual fields)
```sh
tcp.analysis.flags
ip.checksum_bad
```

### Display filters with Comparison Operators
```sh
http.request.method=="GET"
tcp.flags==0x010
tcp.window_size < 4096
tcp.stream eq 2
```

### Complex display filters with with multiple conditions

Display ARP requests except ARP requests from the MAC address 00:01:5c:22:a5:82.
```sh
(arp.opcode==0x0001) && !(arp.src.hw_mac==00:01:5c:22:a5:82)
```

Display any BOOTP/DHCP packets to or from 74.31.51.150 that lists 73.68.136.1 as the relay agent.
```sh
bootp.ip.relay==73.68.136.1 && bootp.ip.your==74.31.51.150
```

Displays packets that have the TCP ACK bit set but not packets that have the TCP SYN bit set.
[http://packetlife.net/blog/2010/jun/7/understanding-tcp-sequence-acknowledgment-numbers/]
```sh
(tcp.flags.ack==1) && !(tcp.flags.syn==1)
```

Display ICMP Destination Unreachable packets that indicate the host is unreachable or the protocol is unreachable.
```sh
(icmp.type==3) && ((icmp.code==0x01) || (icmp.code==0x02))
```

### Using Expressions for Filter Assistance
  - Expression assist in creating complex Filters
  - These help with syntax and identifying all the available fields for us to use.

### Some examples  
Filter: expert.severity==1536
```sh
Expression Path: Expert | Expert Severity | == | Warn
```
Filter: expert.message
```sh
Expression Path: Expert | Expert Message | is present
```

Filter: bootp.type==1
```sh
Expression Path: BOOTP or DHCP | bootp.type | == | Boot Request
```

Filter: dns.flags.opcode==1
```sh
Expression Path: DNS | dns.flags.opcode | == | Inverse Query  
```

### Regular Expression Matches
HTTP requests for files ending in .zip or .exe
```sh
http.request.method=="GET" && (http matches "\.(?i)(zip|exe)"
```

Look for email addresses anywhere in the frame
```sh
frame matches "(?i)[A-Z0-9._%-]+@[A-Z0-9.-]+\.[A-Z\>]{2,4}"
```

Look for someone using HTTP to connect to a website ending in a string other than ".com":
```sh
http.host && !http.host matches "\.com$"
```

###Display Filter Macros
Create a macro to get traffic from 5 ports.     

Without Display filter macro
```sh
tcp.dstport==5600 || tcp.dstport==5603 || tcp.dstport==6400 || tcp.dstport==6500 || tcp.dstport==6700
```

Create a new macro
```sh
name : 5ports
string : tcp.dstport==$1 or tcp.dstport==$2 or tcp.dstport==$3 or tcp.dstport==$4 or tcp.dstport==$5
```

With Display filter
```sh
${5ports:5600;5603;6400;6500;6700}
```

The variables are substituted as follows
```sh
    $1 tcp.dstport==5600
    $2 tcp.dstport==5603
    $3 tcp.dstport==6400
    $4 tcp.dstport==6500
    $5 tcp.dstport==6700
```

Focus on a specific conversation by building a macro (we'll call it tcp_conv)
```sh
(ip.src==$1 and ip.dst==$2 and tcp.srcport==$3 and tcp.dstport==$4) or (ip.src==$2 and ip.dst==$1 and tcp.srcport==$4 and tcp.dstport==$3)
```

Apply the display filter like so
```sh
${tcp_conv:192.168.1.1;192.168.1.99;1201;2401}
```

Create custom dfilter file with the following contents
```sh
"__________Wireshark Default Display Filters____________________" WS Default Filter
"    Ethernet address 00:08:15:00:08:15" eth.addr == 00:08:15:00:08:15
"    Ethernet type 0x0806 (ARP)" eth.type == 0x0806
"    Ethernet broadcast" eth.addr == ff:ff:ff:ff:ff:ff
"    No ARP" not arp
"    IP only" ip
"    IP address 192.168.0.1" ip.addr == 192.168.0.1
"    IP address isn't 192.168.0.1, don't use != for this!" !(ip.addr == 192.168.0.1)
"    IPX only" ipx
"    TCP only" tcp
"    UDP only" udp
"    UDP port isn't 53 (not DNS), don't use != for this!" !(tcp.port == 53)
"    TCP or UDP port is 80 (HTTP)" tcp.port == 80 || udp.port == 80
"    HTTP" http
"    No ARP and no DNS" not arp and !(udp.port == 53)
"    Non-HTTP and non-SMTP to/from 192.168.0.1" not (tcp.port == 80) and not (tcp.port == 25) and ip.addr == 192.168.0.1
"__________SG Team ____________________" Display filters by Singapore team
"    Default IRC TCP Ports 6666-6669 (IRC Traffic - Bot Issue)" tcp.port == 6666 || tcp.port == 6667 || tcp.port == 6668 || tcp.port == 6669
"    DHCP NACK (DHCP Server Does Not Like Target)" (bootp.option.type == 53) && (bootp.option.value == 06)
"    ICMP Protocol Unreachable (IP Scan Underway)" icmp.type==3 && icmp.code==2
"    ICMP Response to TCP Packet (Sender Firewalled)" (icmp) && (tcp)
"__________AU Team ____________________" Display filters by Australia team
"    ICMP Types 13, 15 or 17 (OS Fingerprinting)" icmp.type==13 || icmp.type==15 || icmp.type==17
"    Non-Standard ICMP Echo Request" icmp.type==8 && !icmp.code==0
"__________NY Team ____________________" Display filters by New York team
"    TCP Handshake Packets (Connection Process/Attempt)" tcp.flags.syn == 1
"    TCP Length = 536 (MTU Issue Along Path)" tcp.len==536
"    TCP Window Size < 1460 (Receiver Stopping Data Xfer)" tcp.window_size < 1460 && tcp.flags.reset == 0
"    TCP Zero Window (Receiver Stopping Data Xfer)" (tcp.window_size == 0) && (tcp.flags.reset == 0)


```
