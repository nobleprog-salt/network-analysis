## HTTP ANALYSIS EXERCISES

**http-espn2011.pcapng**
  - How many GET requests were required to launch the main page when browsing to www.espn.com?
  - Is it better than 2007

**http-espn2012.pcapng**
  - How many GET requests were required to launch the main page in 2012?
  - How many sites did we have to connect to when loading the page?
  - Were there any redirections?

**http-facebook.pcapng**
  - How many GET requests were required to launch the main page when browsing to www.facebook.com?
  - Why did the client have to send another DNS query so late in the process?
  - What was the last item to load?
  - Would this have slowed down the page loading process?     

**https-justlaunchpage.pcapng**
  - In this trace file we have simply opened a website. You’ll see the HTTPS handshake after the TCP handshake.
  - Look at the 95 second delay in this trace file.
  - What type of packet follows the delay? This packet is encrypted so we don’t know what the alert message is, but likely it is a close_notify. We can somewhat infer that by looking at the FIN that follows.
  - What site did we connect to?
  - How many cipher suites were offered to the HTTPS server?
  - Which cipher suite was chosen for this HTTPS connection?
  - How long did it take the load the website? (Do not include the FIN process.)  

**https-ssl3session.pcapng**
  - There appears to be a problem during the establishment of this SSL connection (HTTPS). Hint: Disable Preferences | Protocols | TCP | Allow subdissector to reassemble TCP streams when examining the SSL/TLS handshake process.
  - What problems occur during the HTTPS connection?
  - How many cipher suites were offered to the HTTPS server?
  - Which cipher suite was chosen for this HTTPS connection?

**http-winpcap.pcapng**
  - This trace contains a web browsing session to www.winpcap.org.
  - Does this client have any of the website elements in cache?
  - What is the largest delay in the trace file?
  - Should you troubleshoot this delay?
  - What operating system is running on the WinPcap server?
  - What is the size of the new.gif file?
  - What image does the new.gif file contain?
  - Will this connection support window scaling?  

  _If an HTTP client has visited a page recently and that page is cached locally, the client may send the IfModified-Since parameter and provide a date and time of the previous page download. If the server responds with a 304 Not Modified—the server will not resend the page that is already cached._
