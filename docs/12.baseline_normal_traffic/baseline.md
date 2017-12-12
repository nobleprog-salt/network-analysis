## Baselining Normal Traffic Patterns

**Baseline Broadcast and Multicast Types and Rates**
```sh
Who is broadcasting?
What application is using broadcasts?
What is the typical broadcast rate in packets per seconds? Who is multicasting?
What application is using multicasts?
What is the typical multicast rate in packets per seconds?
```

**Baseline Protocols and Applications**
```sh
Which applications are running on the network?
What protocols are used for these applications?
What UDP ports are in use?      
What TCP ports are in use?
What routing protocol is in use?
What does a routing update process look like?
What ICMP traffic is seen on the network?
```

**Baseline Traffic during Idle Times**
```sh
What protocols or applications are seen during idle time?
What hosts are contacted (IP address, host name)?
How frequently does the idle traffic occur?
What are the signatures of this traffic that you can filter out when removing this traffic from a trace file?
```

**Baseline Application Launch Sequences and Key Tasks**
```sh
What discovery process is the application dependent upon?
Is the application TCP-based or UDP-based?
If TCP-based, what are the TCP options set in the handshake packets?
What port(s) does the application use?
What hosts are contacted when the application starts (interdependencies)?
How many packets/how much time until the launch is complete?
What is the IO rate during the launch sequence?
What happens during application idle time?
Are any portions of the login visible in clear text?
What is the round trip latency during the application launch?
Are there any failures or retries during the application launch?
Are there any server delays upon receipt of requests?
Are there any client delays preceding requests?
Are there lost packets, retransmissions or out-of-order packets during the launch?
Analyze key tasks (application-dependent) individually.
```

**Baseline Web Browsing Sessions**
```sh
What browser is used for the analysis?
What is the target (if any) for the name resolution process?
What is the name resolution response time?
What is the round trip latency time between the client and the target server?
What is the application response time for a page request?
What other hosts do you communicate with during the web browsing session?
Are there any HTTP errors in the trace file?
```

**Baseline Name Resolution Sessions**
```sh
What application is being used to test the name resolution process? What name and type is being resolved?
What is the IP address of the target name server?
What is the round trip response time for the name resolution process?
```

**Baseline Throughput Tests**
```sh
What application is being used to perform the throughput test?
What are the configurations of host 1 and host 2?
What is the packet size used for the throughput test?
What transport was used for the test?
What is the Kbytes per second rate from host 1 to host 2?
What is the Kbytes per second rate from host 2 to host 1?
What was the packet loss rate in each direction?
What was the latency (if measurable) in each direction?
```

**Baseline VoIP Communications**
```sh
What protocol is used for the call setup procedure?
What is the round trip latency time for the call setup procedure?
What is the average call setup time (Telephony | SIP)?
What codec is used for the compression (e.g., payload type G.711)
Are there any SIP error responses (Telephony | SIP)?
What is the jitter rate?
Is there any packet loss in the communication (Telephony | RTP | Stream Analysis)?
```
