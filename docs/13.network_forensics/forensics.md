### Network Forensics

**Some useful coloring rules**
```sh
(icmp.type==8) && !(icmp.code==0x00)
#Highlights the unusual ICMP Echo Request used by NetScanTools.

(tcp.flags==0x00) || (tcp.options.wscale_val==10) || (tcp.options.mss_val < 1460) || (tcp.flags==0x29) && tcp.urgent_pointer==0 || (tcp.flags==0x02 && frame[42:4] != 00:00:00:00) || (tcp.flags==0x02 && tcp.window_size < 65535 && tcp.options.wscale_val > 0)
#Nmap general traffic (a long filter looking for unusual traffic patterns)

tcp.window_size < 65535 && tcp.flags.syn==1
#Small WinSize SYN (Suboptimal setting or discovery packet?)

tcp.port==6666 || tcp.port==6667 || tcp.port==6668 || tcp.port==6669
#Default IRC TCP Ports 6666-6669 (IRC traffic—bot issue? Could also be created with > and < operators)

dns.count.answers > 5
#DNS Answers > 5 (Bot C&C servers listed in this packet? Not always a problem, but suspect. Look for a
#number of dissimilar IP addresses in the response.)

icmp.type==3 && icmp.code==2
#ICMP Protocol Unreachable (IP scan underway?)

(icmp) && (tcp)
#ICMP Response to TCP Packet (Sender firewalled?)

icmp.type==3 && icmp.code==4
#ICMP Type 3/Code 4 (Black hole detection?)

icmp.type==13 || icmp.type==15 || icmp.type==17
#ICMP Types 13, 15 or 17 (OS fingerprinting?)

icmp.type==8 && !icmp.code==0
#NonStandard ICMP Echo Request (Can we detect the application used?)

tcp.window_size < 1460 && tcp.flags.reset==0
#TCP Window Size < 1460 (Receiver stopping data transfer?)

(tcp.window_size==0) && (tcp.flags.reset==0)
#TCP Zero Window (Receiver stopping data transfer.)

http.request.method =="GET" && http matches "\(?i)(exe|zip|jar|tar)"
#Look for any HTTP GET packets that have exe, zip, jar or tar files
```

### Complementary Forensics Tools
```sh
# Nmap is a security scanner, originally written by Gordon Lyon, used to discover
# hosts and services on a computer network, thus building a "map" of the network.
Nmap (https://nmap.org/)

# Nessus is a proprietary vulnerability scanner developed by Tenable Network Security.
Nessus (www.nessus.org)

# Snort is a free and open source network intrusion prevention system and network
# intrusion detection system created by Martin Roesch in 1998.
Snort (www.snort.org)

# Netcat is a featured networking utility which reads and writes data across
# network connections, using the TCP/IP protocol.
Netcat (netcat.sourceforge.net)

# Penetration testing framework
Metasploit Framework (www.metasploit.com)

# hping is a command-line oriented TCP/IP packet assembler/analyzer.
Hping2 (www.hping.org)

# Kismet is a wireless network detector, sniffer, and intrusion detection system.
# Kismet works predominately with Wi-Fi (IEEE 802.11) networks
Kismet (www.kismetwireless.net)

# powerful command-line packet analyzer
Tcpdump (www.tcpdump.org)

# Ettercap is a comprehensive suite for man in the middle attacks.
# It features sniffing of live connections, content filtering.
Ettercap (http://ettercap.github.io/ettercap/)

# Nikto is an Open Source (GPL) web server scanner which performs
# comprehensive tests against web servers
Nikto (www.cirt.net/nikto2)
```
