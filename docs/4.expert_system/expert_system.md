##TCP Expert Information
The Expert system can speed up the process of locating potential problems in a trace file. See a list of some major TCP Expert notifications below.

###TCP Retransmissions
Retransmissions are the result of packet loss and are triggered when the sender’s TCP retransmission timeout (RTO) timer expires or a receiver sends Duplicate Acknowledgments to request a missing segment. If a TCP segment contains data and it uses the same sequence number as a previous packet, it must be a TCP retransmission or a fast retransmission. To filter on all retransmissions (fast or regular), use ```tcp.analysis.retransmission```.

###Previous Segment Lost
Wireshark tracks the TCP sequence numbers of each packet as well as the number of data bytes in the packets. Wireshark, therefore, knows the next expected sequence number in a TCP stream. When an expected sequence number is skipped, Wireshark indicates a previous segment has been lost on the packet immediately following the missing packet in the stream.

###ACKed Lost Packet
When Wireshark detects an acknowledgment, but it has not seen the packet that is being acknowledged, an ACKed Lost Packet warning is triggered. The ACKed Lost Packet can also be an indication that your capture process is faulty. For example, if you spanned a switch port and the switch is overloaded, it may not forward all the traffic down the monitor port.

###TCP Keep Alive
Each side of a TCP connection maintains a keep alive timer. When the keep alive timer expires, a TCP host sends a keep alive probe to the remote host. If the remote host responds with a keep alive ACK (or any TCP packet, for that case), it is assumed the connection is still valid. If no response is received, it is assumed the connection is broken.

###Duplicate ACK
A receiver tracks the incoming TCP sequence numbers. If a packet is detected as missing (the expected sequence number is skipped), the receiver generates an ACK indicating the next expected sequence number in the Acknowledgment Number field.A TCP host that supports a feature called Fast Recovery will continue to generate Duplicate ACKs—requesting the missing segment. When the host sending the TCP segments receives three identical ACKs (the original ACK and two Duplicate ACKs), it assumes there is packet loss and it resends the missing packet—regardless of whether the RTO expired or not. A high number of Duplicate ACKs may be an indication of high latency between TCP hosts as well as packet loss. A receiver continues to generate Duplicate ACKs until the situation is resolved.

###Zero Window
When a receiver has no receive buffer space available, it sends Zero Window packets indicating the TCP window size is zero. This, in effect, shuts down data transfer to the receiver. The data transfer will not resume until that receiver sends a packet with a window size sufficient to accept the next amount of queued data from the sender.

###Zero Window Probe
A Zero Window Probe packet may be sent by a TCP host when the remote host advertises a window size of zero. By specification, a zero window probe may contain one byte of the next segment of data. If the zero window condition has been resolved, the receiver sends an acknowledgment for the new byte received. If the zero window condition has not been resolved, the receiver sends an ACK, but does not acknowledge the new byte.

###Zero Window Probe ACK
This packet is a response to the Zero Window Probe packet. If the zero window condition has been resolved, the Zero Window Probe ACK will acknowledge the new byte received. If the zero window condition has not been resolved, the Zero Window Probe ACK will not acknowledge the new byte received.

###Keep Alive ACK
 Keep Alive ACKs are sent in response to a Keep Alive. If the Keep Alive ACK contains a window size of zero, the zero window condition has not been resolved.

###Out-of-Order
If a packet contains data and does not advance the sequence number, it is either a retransmission or fast retransmission (using the same sequence number as the previous one) or an Out-of-order packet. An out-of-order packet contains a lower sequence number than a previous packet. Out-of-order packets often indicate that data traffic travels along multiple paths to get to the destination. Data streams traveling along multiple paths may encounter different latency times, thus triggering unnecessary retransmissions if a receiver times out waiting for a packet.
These Out-of-order indications can also be seen when a queuing device along a path does not forward packets in the same order in which they arrived. For example, packets arrive at the queuing device in 1-2-3-4 order, but are queued and forwarded in 1-3-2-4 order.

###Fast Retransmission
A Fast Retransmission occurs within 20ms of a Duplicate ACK.
To filter on all retransmissions (fast or regular), use ```tcp.analysis.retransmission```.
Fast Retransmissions are similar to Retransmissions. The only difference is who noticed the packet loss first. In this case, the receiver noticed packet loss and began to complain through Duplicate ACKs. You need to find out the location of packet loss to fix this issue.

###Window Update
A Window Update packet contains no data, but indicates that the sender’s TCP window size field value has increased[78].
These are actually good packets. A client just advertised a larger receive buffer space indicating an application just picked up some data from the receive buffer. These packets are the only recovery for a Window Zero condition and do not require any action.


###Window is Full
Wireshark tracks a receiver’s window size and notes when a data packet is sent that will fill up the remaining buffer space. This packet itself will not have the Window size value of 0. This packet is an indication that a window size value of 0 may come from the other side if their receive window size is not updated.

###TCP Ports Reused
This Expert notification is triggered when a new TCP session begins using the same IP addresses and port number combination as an earlier conversation in the trace file. This is often seen during a vulnerability scan or reconnaissance process. These packets should be investigated to see if there is a security issue to address.

### Display filters based on Exert Severity levels
```sh
expert.severity==error
expert.severity==warn
expert.severity==note
expert.severity==chat
```
