## Email Analysis

**POP REQUEST COMMANDS**
```sh
USER: Used to indicate the user name
PASS: Used to indicate the password
QUIT: Terminate the connection
STAT: Obtain the server status
LIST: List message and message size
RETR: Retrieve a message
DELE: Delete a message
PIPELINING: Server can accept multiple commands at a time [RFC2449]
UIDL: Unique ID List—list all emails [RFC2449]
```

**POP Response Indicators**
```sh
+OK
-ERR
```

**Some POP filters**
```sh
pop
# Only pop command and email traffic

tcp port 110
# All pop traffic including TCP handshake

pop.response.indicator=="+OK"
# POP +OK responses

pop.response.indicator=="-ERR"
#POP –ERR responses

pop.request.command=="USER"
#POP USER commands

(pop.request.command=="USER") && (pop.request.parameter=="Fred")
#POP USER commands with the username Fred (the username is case sensitive)

(pop.response.indicator=="+OK") && (pop.response.description contains "octets")
#POP responses that contain email UIDL values and the length of each email message
#(good for spotting groups of spam messages with attachments)
```

**SMTP Client Commands**
```sh
HELO: Initiates an SMTP session
EHLO: Initiates an SMTP session from a sender that supports SMTP mail service extensions
MAIL: Initiates mail transfer
RCPT: Identifies mail recipient
DATA: Initiates mail data transfer
VRFY: Verifies recipient exists
RSET: Aborts mail transaction
NOOP: Tests connection to server
QUIT: Closes SMTP connection
EXPN: Expands mailing list
HELP: Lists help information
```

**SMTP Reply codes**
```sh
Code 211: System status
Code 214: Help message
Code 220: <domain> service ready
Code 221: <domain> service closing channel
Code 250: Requested action okay and completed
Code 251: User not local; will forward to <path>
Code 354: Start mail input
Code 421: <domain> service not available
Code 450: Mailbox unavailable
Code 451: Local error
Code 452: Insufficient storage
Code 500: Syntax error, command unrecognized
Code 501: Syntax error in parameters or arguments Code 502: Command not implemented
Code 503: Bad sequence of commands
Code 504: Command parameter not implemented
Code 521: <domain> does not accept mail (see rfc1846) Code 550: Mailbox unavailable
Code 551: User not local, please try <path>
Code 552: Exceeded storage allocation
Code 553: Mailbox name not allowed
Code 554: Transaction failed
```

**SMTP Filters**
```sh
smtp
# Only displays SMTP commands and data. Does not display TCP handshake

tcp.port==25
# Display all related packets. Correct port as required

smtp.req.command=="EHLO"
# User and server support mail extensions and are setting up an SMTP communication

(smtp.req.command=="MAIL") && (smtp.req.parameter=="FROM: <john@example.com>")
#An email is being sent from john@example.com

(smtp.req.command=="RCPT") && (smtp.req.parameter=="TO: <brenda@example.com>")
#An email is being sent to brenda@example.com

smtp.response.code > 399
#The email server indicates there is a problem with the email
```
