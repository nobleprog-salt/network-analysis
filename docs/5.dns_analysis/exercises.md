## DNS ANALYSIS EXERCISES

**misc-dns.pcapng**
  - Compare the DNS lookups required to access www.winpcap.org, www.msnbc.com and www.espn.com.
  - Were all of the DNS requests successful? We can see that some of these sites use Akamai to offer edge services to feed elements from local servers.
  - How does the roundtrip time look between DNS queries and replies?

**dns-serverfailure.pcapng**
  - DNS server failures indicate that the server couldn't offer a positive or negative response.
  - Perhaps the upstream DNS server didn't respond in a timely manner (or at all) ?
  - Were these recursive requests?
  - Consider building a display filter for dns.flags.rcode==2 to view these DNS server failure responses.

**http-espn2007.pcapng**
  - How many DNS queries were generated to load this website (espn)?
  - Were any DNS queries unsuccessful?
  - What was the typical round trip time between DNS requests and responses?
  - Select Statistics | HTTP | HTTP Packet Counter to view the number of redirections (Code 301 and 302) and client errors (Code 404).
  - It takes a lot of hosts to load the www.espn.com website.
  - This trace file contains A record queries, and A and CNAME responses to those queries.
  - Are there any DNS errors?  

**http-espn2010.pcapng**
  - ESPN website in 2010.
  - Are there too many DNS queries ?

**http-espn2011.pcapng**
  - We are now using a dual-stack client.
  - Observe number of times client requests the AAAA records.  

**http-msnbc.pcapng**
  - Filter on the DNS traffic in this trace file to see the A and AAAA record queries.
  - We are using a dual stack client now and the number of DNS queries is doubled.
  - Are we benefiting from these AAAA record queries?
  - What response do we receive for these AAAA record queries?  
