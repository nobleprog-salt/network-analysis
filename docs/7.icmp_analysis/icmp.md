## Why do we need ICMP
  - Used as messaging system for errors, alerts and general notifications on an IP network
  - ICMP message types :
    - Echo messages : used by Ping and traceroute to test connectivity.
    - Redirect messages : used by routers to let the source know there is a better path to a destination. (note: if this message is not sent by router than it is suspect)
    - Destination unreachable messages: used to tell source host that destination could not be delivered.
    - ICMP traffic monitoring can determine how well the traffic is defined, spot security breaches and functional problems.

###ICMP Type
Type 0: Echo Reply [RFC 792]
Type 1: Unassigned
Type 2: Unassigned
Type 3: Destination Unreachable [RFC 792]
Type 4: Source Quench [RFC 792]
Type 5: Redirect [RFC 792]
Type 6: Alternate Host Address
Type 7: Unassigned
Type 8: Echo [RFC 792]
Type 9:Router Advertisement [RFC 1256]
Type 10:Router Solicitation [RFC 1256]
Type 11: Time Exceeded [RFC 792]
Type 12: Parameter Problem [RFC 792]

###Type 3 Destination Unreachable Codes
  - Code 0: Net Unreachable—the ICMP sender knows about the network, but believes it is not up at this time—perhaps it is too far away or only available through an unknown route.
  - Code 1: Host Unreachable—the ICMP sender knows about the host, but doesn’t get an ARP reply, indicating the host is not up at this time.
  - Code 2: Protocol Unreachable—the protocol defined in the IP header cannot be processed for some reason.
  - Code 3: Port Unreachable—the ICMP sender does not support the port number you are trying to reach—a large number of these packets indicates a configuration problem or possibly a UDP port scan; if these packets are sent in response to a TCP handshake attempt, they indicate the target port is likely firewalled.
  - Code 4: Fragmentation Needed and Don't Fragment was Set—a Router needed to fragment to forward the packet across a link that supports a smaller MTU size, but the application set the Don’t Fragment bit
  - Code 5: Source Route Failed—the ICMP sender cannot use the strict or loose source routing path specified in the original packet.
  - Code 6: Destination Network Unknown—the ICMP sender does not have a route entry for the destination network, indicating it may never have been an available network.
  - Code 7: Destination Host Unknown—the ICMP sender does not have a host entry indicating it may never have been available on the connected network.
  - Code 8: Source Host Isolated—the ICMP sender (router) has been configured to not forward packets from the source. Most routers will not generate this response code—they will generate a code 0 (network unreachable) and code 1 (host unreachable)—whichever one is appropriate.
  - Code 9: Communication with Destination Network is Administratively Prohibited—the ICMP sender (router) has been configured to block access to the desired destination network.
  - Code 10: Communication with Destination Host is Administratively Prohibited—the ICMP sender (router) has been configured to block access to the desired destination host.
  - Code 11: Destination Network Unreachable for Type of Service—the Type of Service (TOS) indication used by the original sender is not available through this router for that specific network—note that more current networks may not use TOS or Precedence—they may use DiffServ instead.
  - Code 12: Destination Host Unreachable for Type of Service—the TOS indication used by the original sender is not available through this router for that specific host—note that more current networks may not use TOS or Precedence—they may use DiffServ instead.
  - Code 13: Communication Administratively Prohibited—the ICMP sender is not available for communications at this time; this might be sent by a verbose firewall.
  - Code 14: Host Precedence Violation—the Precedence value defined in sender’s original IP header is not allowed (for example, using Flash Override precedence)—note that more current networks may not use TOS or Precedence—they may use DiffServ instead.
  - Code 15: Precedence Cutoff in Effect—the Network administrator has imposed a minimum level of precedence to be serviced by a router, but a lower precedence packet was received.

### Type 5 Redirect Codes
  - Code 0: Redirect Datagram for the Network (or subnet)—the ICMP sender (router) is not the best way to get to the desired network. Reply contains IP address of best router to destination. Dynamically adds a network entry in original sender’s route tables
  - Code 1: Redirect Datagram for the Host—the ICMP sender (router) is not the best way to get to the desired host. Reply contains IP address of best router to destination. Dynamically adds a host entry in original sender’s route tables
  - Code 2: Redirect Datagram for the Type of Service and Network—the ICMP sender (router) does not offer a path to the destination network using the TOS requested. Dynamically adds a network entry in original sender’s route tables—note that more current networks may not use TOS or Precedence—they may use DiffServ instead
  - Code 3: Redirect Datagram for the Type of Service and Host—the ICMP sender (router) does not offer a path to the destination host using the TOS requested. Dynamically adds a host entry in original sender’s route tables—note that more current networks may not use TOS or Precedence—they may use DiffServ instead.


###Type 11 Time Exceeded Codes
  - Code 0: Time to Live Exceeded in Transit—the ICMP sender (router) indicates that originator’s packet came in with a TTL of 1. Routers cannot decrement the TTL value to 0 and forward a packet on
  - Code 1: Fragment Reassembly Time Exceeded—the ICMP sender (destination host) did not receive all fragment parts before the expiration (in seconds of holding time) of the TTL value of the first fragment received

###Type 12 Parameter Problem Codes
  - Code 0: Pointer indicates the Error—this error is defined in greater detail within the ICMP packet.
  - Code 1: Missing a Required Option—the ICMP sender expected some additional information in the Option field of the original packet.
  - Code 2: Bad Length—the original packet structure had an invalid length.

**Full List of Codes** : https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol
**Wireshark ICMP Bug** : https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=11414

###Filtering ICMP
```sh
icmp.type==8
#ICMP ping—echo request

icmp.type==8 || icmp.type==0
#ICMP ping request or response

(icmp.type==8) && !(icmp.code==0)
#Unusual ICMP ping packets (code field is not set at 0)

icmp.type==13 || icmp.type==15 || icmp.type==17
#ICMP Timestamp Request, Information Request or Address Mask Request (possible OS fingerprinting)

tcp && icmp.type==3 && (icmp.code==1 || icmp.code==2 || icmp.code==3 || icmp.code==9 || icmp.code==10 || icmp.code==13)
#ICMP Destination Unreachable response to a TCP handshake (possible firewalled TCP target)—this is a unique
#filter as it looks for a TCP header embedded after the ICMP header

icmp.type==11
#ICMP Time to Live Exceeded (traceroute underway?)

icmp.type==3 and icmp.code==4
#Fragmentation Needed, but Don’t Fragment Bit Set (path MTU discovery packet—don’t block this packet!)
```  
