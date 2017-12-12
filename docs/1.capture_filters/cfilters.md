## Custom Capture filters
Create a new capture filter with following content

```
"Ethernet address 00:00:5e:00:53:00" ether host 00:00:5e:00:53:00
"Ethernet type 0x0806 (ARP)" ether proto 0x0806
"No Broadcast and no Multicast" not broadcast and not multicast
"No ARP" not arp
"IPv4 only" ip
"IPv4 address 192.0.2.1" host 192.0.2.1
"IPv6 only" ip6
"IPv6 address 2001:db8::1" host 2001:db8::1
"IPX only" ipx
"TCP only" tcp
"UDP only" udp
"__________NOC Team ____________________" Capture filters by Noc team
"TCP or UDP port 80 (HTTP)" port 80
"HTTP TCP port (80)" tcp port http
"No ARP and no DNS" not arp and port not 53
"Non-HTTP and non-SMTP to/from www.wireshark.org" not port 80 and not port 25 and host www.wireshark.org
"My MAC" ether host c4:b3:01:bd:ee:2f
"All Outgoing only" src host 192.168.1.2
"All Incoming only" dst host 192.168.1.2
"__________SG Team ____________________" Capture filters by Singapore team
"Not My MAC" not ether host c4:b3:01:bd:ee:2f
"ARP or DHCP (Passive Discovery)" arp or port 67 or port 68
"Broadcasts or Multicasts Only" broadcast or multicast
"ICMP Only" icmp
"IPv6 Only" ip6
```

### Primitive keywords that can be used
  - dst host ```host```
  - src host ```host```
  - host ```host```
  - ether dst ```ehost```
  - ether src ```ehost```
  - ether host ```ehost```
  - gateway ```host```
  - dst net ```net```
  - src net ```net```
  - net ```net```
  - net ```net``` mask ```netmask```
  - dst port ```port```
  - src port ```port```
  - less ```length```
  - greater ```length```
  - ip proto ```protocol```
  - ip6 proto ```protocol```
  - ip6 protochain ```protocol```
  - ip protochain ```protocol```
  - ip broadcast
  - ether multicast
  - ip multicast
  - ip6 multicast
  - ether proto ```protocol```
  - decnet src ```host```
  - decnet dst ```host```
  - decnet host ```host```
  - ip, ip6, arp, rarp, atalk, aarp, decnet, iso, stp, ipx, netbeui
  - lat, moprc, mopdl
  - vlan vlan_id
  - tcp, udp, icmp
  - portrange ```[startnum]-[endnum]```
  - tcp portrange ```[startnum]-[endnum]```
  - clnp, esis, isis
  - iso proto ```protocol```
  - ```proto[expr:size]```

### Filter incoming tcp connection attempts
```sh
tcp[tcpflags] & (tcp-syn) != 0
```

### Capture start and end packets (SYN and FIN) of each TCP conversation and to/from a non local host
```sh
tcp[tcpflags] & (tcp-syn|tcp-fin) != 0 and not src and dst net localnet
```
Refer to this manual for full scope : http://www.tcpdump.org/manpages/pcap-filter.7.html

### Creating Capture Filters to Look for Byte Values
Look for specific values at specific offsets of the packet. Get only TCP packets with window size 4096
```sh
"My Window Size Filter" tcp[14:2] = 4096
```

### Useful capture filters list  
 - https://wiki.wireshark.org/CaptureFilters
