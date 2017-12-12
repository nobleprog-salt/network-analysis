##HTTP/HTTPS display filters

```sh
http.request.method=="GET" or http.request.method=="POST"
#HTTP GET or POST requests

http.response.code > 399
#HTTP 4xx or 5xx (client or server errors)

http contains "IfModified-Since"
#Determine if a client has cached a page already

http.host=="www.wireshark.org"
#Target host is www.wireshark.org

http.user_agent contains "Firefox"
#HTTP client is using Firefox browser

http.referer contains "wireshark.org"
#HTTP client has reached the current location from a link on wireshark.org

tcp.port==443
#HTTPS

ssl
#Secure Socket Layer (secure browsing session) - consider using tcp.port==443

ssl.record.content_type==22
#TLSv1 handshake

ssl.handshake.type==1
#TLSv1 Client Hello in handshake

ssl.handshake.type==16
#TLSv1 Client Key exchange
```


**Request Header/Modifier**
The request-header fields allow the client to pass additional information about the request, and about the client itself, to the server. These fields act as request modifiers, with semantics equivalent to the parameters on a programming language method invocation.

```sh
Accept: Acceptable content types
Accept-Charset: Acceptable character sets
Accept-Encoding: Acceptable encodings
Accept-Language: Acceptable languages
Accept-Ranges: Server can accept range requests
Authorization: Authentication credentials for HTTP authentication Cache-Control: Caching directives
Connection: Type of connection preferred by user agent
Cookie: HTTP cookie
Content-Length: Length of the request body (bytes)
Content-Type: Mime type of body (used with POST and PUT requests)
Date: Date and time message sent
Expect : Defines server behavior expected by client
If-Match: Perform action if client-supplied information matches IfModified-Since: Provide date/time of cached data; 304 Not Modified if current If-Range: Request for range of missing information
If-Unmodified-Since: Only send if unmodified since certain date/time Max-Forwards : Limit number of forwards through proxies or gateways Proxy-Authorization: Authorization credentials for proxy connection
Range: Request only part of an entity
Referer[110]: Address of previous website linking to current one
TE: Transfer encodings accepted
UserAgent: User agent—typically browser and operating system
Via: Proxies traversed
```

**HTTPS Alert Types**
```sh
close_notify (0)
unsupported_certificate (43)
decrypt_error (51)
unexpected_message (10)
certificate_revoked (44)
export_restriction (60)
bad_record_mac (20)
certificate_expired (45)
protocol_version (70)
decryption_failed (21)
certificate_unknown (46)
insufficient_security (71)
record_overflow (22)
illegal_parameter (47)
internal_error (80)
decompression_failure (30)
unknown_ca (48)
user_canceled (90)
handshake_failure (40) 
```
