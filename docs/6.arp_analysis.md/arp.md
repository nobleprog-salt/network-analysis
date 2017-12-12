## ARP Traffic Analysis
  - ARP is used to associate a hardware address with and IP address on a local network.
  - ARP is defined in RFC 826, Ethernet Address Resolution Protocol.
  - ARP is not used in IPv6 communications.
  - ARP packets unique compared to the majority of traffic on a TCP network because they do not have an IP header.
  - They are non-routable packets.

### ARP Storm
ARP storm is an attack situation intentionally created by an attacker from within the local network. In ARP packet storm the attacker keeps generating broadcast packets, with IP addresses within a subnet range or even to IP addresses not present in the local subnet.

## ARP Packet Structure
**Hardware Type**
This defines the hardware or data link type in use. Hardware type 1 is assigned to Ethernet and defines a 6- byte hardware address length. The complete Hardware Type field value listing is available at www.iana.org.

**Protocol Type**
This field defines the protocol address type in use. This field uses the standard protocol ID values that are also used in the Ethernet II frame structures. These protocol types are defined at www.iana.org/assignments/protocol-numbers.

**Length of Hardware Address**
This field defines the length (in bytes) of the hardware addresses used in this packet.

**Length of Protocol Address**
This field defines the length (in bytes) of the protocol (network) addresses used in this packet.

**Opcode**
This defines whether this is a request or reply packet and the type of address resolution taking place. RARP is a process that enables a device to learn a network address from a MAC address. RARP is defined in RFC 903, A Reverse Address Resolution Protocol. We do not see RARP in use except in really old network environments where they used RARP as an early address assignment protocol.
The following lists the ARP and RARP (reverse ARP) operation codes:
  - Opcode 1: ARP request
  - Opcode 2: ARP reply
  - Opcode 3: RARP request
  - Opcode 4: RARP reply

**Sender’s Hardware Address**
This field indicates the hardware address of the device that is sending this request or reply.

**Sender’s Protocol Address**
This field indicates the protocol (network) address of the device that is sending this request or reply.

**Target Hardware Address**
This field indicates the desired target hardware address, if known. In ARP requests, this field is typically filled with all 0s. In ARP replies, this field contains the hardware address of the device that sent the ARP request.

**Target Protocol Address**
This field indicates the desired target protocol (network) address in a request. In the reply it contains the address of the device that issued the request.  

### Some display filters
```sh
arp.opcode==0x0001
#ARP request

arp.opcode==0x0002
#ARP reply

arp.src.hw_mac==00:13:46:cc:a3:ea
#ARP source hardware address is 00:13:46:cc:a3:ea (request or reply)

(arp.src.hw_mac==00:21:97:40:74:d2) && (arp.opcode==0x0001)
#ARP request with source hardware address 00:21:97:40:74:d2
```

Multicast
```sh
From one source to multiple destinations stating an interest in receiving the traffic i.e. One-to-Many
```

Broadcast
```sh
Any packet destined for all stations on a network segment is considered broadcast traffic. One-to-All
```
