## VOIP Analysis

**SIP Commands**

```sh
INVITE: Invites a user to a call
ACK:Acknowledgement is used to facilitate reliable message exchange for INVITEs.
BYE:Terminates a connection between users
CANCEL:Terminates a request, or search, for a user. It is used if a client sends an INVITE and then changes its decision to call the recipient.
OPTIONS:Solicits information about a server's capabilities.
SUBSCRIBE: Requests state change information regarding another host
REGISTER:Registers a user's current location
INFO:Used for mid-session signaling
```

**SIP Response Codes Groups**
```sh
1xx: Provisional—request received, continuing to process the request
2xx: Success—the action was successfully received, understood, and accepted
3xx: Redirection—further action needs to be taken in order to complete the request
4xx: Client Error — the request contains bad syntax or cannot be fulfilled at this server
5xx: Server Error — the server failed to fulfill an apparently valid request
6xx: Global Failure — the request cannot be fulfilled at any server
```

**SIP Response Codes**
```sh
100: Trying
180: Ringing
181: Call is Being Forwarded 182: Queued
183: Session Progress
199: Early Dialog Terminated 200: OK
202: Accepted (used for referrals) 204: No Notification
300: Multiple Choices
301: Moved Permanently
302: Moved Temporarily 305: Use Proxy
380: Alternative Service 400: Bad Request
401: Unauthorized: Used only by registrars. Proxies should use proxy authorization 407
402: Payment Required (Reserved for future use)
403: Forbidden
404: Not Found: User not found
405: Method Not Allowed
406: Not Acceptable
407: Proxy Authentication Required
408: Request Timeout: Couldn't find the user in time
410: Gone: The user existed once, but is not available here anymore.
412: Conditional Request Failed [RFC3903]
413: Request Entity Too Large
414: Request-URI Too Long
415: Unsupported Media Type
416: Unsupported URI Scheme
417: Unknown Resource –Priority [RFC4412]
420: Bad Extension: Bad SIP Protocol Extension used, not understood by the server 421: Extension Required
422: Session Interval Too Small
423: Interval Too Brief
428: Use Identity Header [RFC4474]
429: Provide Referrer Identity [RFC3892]
430: Flow Failed [RFC5626]
433: Anonymity Disallowed [RFC5079]
436: Bad Identity Info [RFC4474]
437: Unsupported Certificate [RFC4474]
438: Invalid Identity Header [RFC4474]
439: First Hop Lacks Outbound Support [RFC5626]
440: Max-Breadth Exceeded [RFC5393]
469: Bad Info Package [RFC6086]
470: Consent Needed [RFC5360]
480: Temporarily Unavailable
481: Call/Transaction Does Not Exist
482: Loop Detected
483: Too Many Hops
484: Address Incomplete
485: Ambiguous
486: Busy Here
487: Request Terminated
488: Not Acceptable Here
489: Bad Event [RFC3265]
491: Request Pending
493: Undecipherable: Could not decrypt S/MIME body part
494: Security Agreement Required [RFC3329]
500: Server Internal Error
501: Not Implemented: The SIP request method is not implemented here
502: Bad Gateway
503: Service Unavailable
504: Server Timeout
505: Version Not Supported: The server does not support this version of the SIP protocol
513: Message Too Large
580: Precondition Failure [RFC3312]
600: Busy Everywhere
603: Decline
604: Does Not Exist Anywhere
```

**VOIP Filters**
```sh
sip
#SIP traffic only

rtp
#RTP traffic only

rtcp
#Realtime Transport Control Protocol

sip.Method=="INVITE"
#SIP Invites[127]

sip.Method=="BYE"
#SIP Connection closings

sip.Method=="NOTIFY"
#SIP Notify packets

sip.Status-Code > 399
#SIP response codes indicating client, server or global faults

sip.resend==1
#Detect when a SIP packet had to be resent[128]

rtp.p_type==0
#G.711 codec definition for payload type

rtpevent.event_id==4
#Dual-tone multifrequency—a 4 was pushed on the phone keypad

(sip.r-uri.user=="0")
#The SIP packet is used to establish a session with the operator (0) or ACK to the operator (0)

rtcp.pt==200
#RTCP sender report
```
