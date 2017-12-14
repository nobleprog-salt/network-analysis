## ARP ANALYSIS EXERCISES

**arp-badpadding.pcapng**
  - ARP packets are minimum-sized packets and must be padded to meet the minimum 64-byte length for this Ethernet network.
  - What is in the ARP padding in these packets?
  - Why can’t we follow an ARP stream?
  - Could this padding be considered a security flaw?

**arp-bootup.pcapng**
  - This is a client boot up sequence.
  - What is the purpose of the ARP packets in this trace file?
  - Were the ARP requests answered?
  - What is the delay between each of the ARP packets seen?
  - Why is the delay necessary?

**arp-ping.pcapng**
  - What is the purpose of each of the ARP packets in this trace file?
  - Was each process successful?

**arp-poison.pcapng**
  - Follow the MAC and IP addresses in this trace file to diagram out what is happening.
  - What is the hardware address of the poisoner and the poisoned hosts?
