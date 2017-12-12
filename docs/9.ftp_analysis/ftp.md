## FTP Analysis

**Client Commands**
```sh
USER: Identifies the user accessing the FTP server PASS: Indicates the user’s password
CWD: Change working directory
QUIT: Terminates the connection
PORT: Sets up a data connection IP address and port number at the client (active mode FTP)
PASV: Requests the server to listen on a non-default data port for the client to establish a data connection (passive mode FTP)
TYPE: Indicates the type of data to be transferred 
RETR: Retrieve a file from the FTP server
STOR: Send a file to the FTP server
DELE: Delete a file
RMD: Remove a directory
MKD: Make a directory
NSLT: Name list—displays directory on server
PWD: Print (display) working directory contents NSLT: Name list—displays directory on server HELP: Shows commands supported by the server
```

**Server response codes**
```sh
120: Service ready in nnn minutes.
125: Data connection already open; transfer starting. 150: File status okay; about to open data connection.
200: Command okay.
202: Command not implemented, superfluous at this site.
211: System status or system help reply.
212: Directory status.
213: File status.
214: Help message. On how to use the server or the meaning of a particular nonstandard command. This reply is useful only to the human user.
215: NAME system type. Where NAME is an official system name from the list in the Assigned Numbers document.
220: Service ready for new user.
221: Service closing control connection. Logged out if appropriate.
225: Data connection open; no transfer in progress.
226: Closing data connection. Requested file action successful (for example, file transfer or file abort).
227: Entering Passive Mode (h1,h2,h3,h4,p1,p2) where h1,h2,h3,h4 indicates the IP address and p1,p2 indicates the port number
230: User logged in, proceed.
250: Requested file action okay, completed.
257: "PATHNAME" created.
331: User name okay, need password.
332: Need account for login.
350: Requested file action pending further information.
421: Service not available, closing control connection. This may be a reply to any command if the service knows it must shut down.
425: Can't open data connection.
426: Connection closed; transfer aborted.
450: Requested file action not taken. File unavailable (e.g., file busy).
451: Requested action aborted: local error in processing.
452: Requested action not taken. Insufficient storage space in system.
500: Syntax error, command unrecognized. This may include errors such as command line too long.
501: Syntax error in parameters or arguments.
502: Command not implemented.
503: Bad sequence of commands.
504: Command not implemented for that parameter.
530: Not logged in.
532: Need account for storing files.
550: Requested action not taken. File unavailable (e.g., file not found, no access).
551: Requested action aborted: page type unknown.
552: Requested file action aborted. Exceeded storage allocation (for current directory or dataset).
553: Requested action not taken. File name not allowed.
```

### Some FTP filters  
```sh
ftp.request.command=="USER"
#FTP USER packets

ftp.request.command=="USER" || ftp.request.command=="PASS"
#FTP USER or PASS packets

ftp.request.command=="USER" && ftp.request.arg=="Fred"
#FTP USER command with the user name Fred (the user name argument is case sensitive)

ftp.request.command=="PASS" && ftp.request.arg=="Krueger"
#FTP PASS command with the password Krueger (the password argument is case sensitive)

ftp.request.command=="PASS" && ftp.request.arg matches "(?i)krueger"
#FTP PASS command with the password Krueger (the password argument is not case sensitive and we are
#using matches with a regular expression)

ftp.response.code==230
#Successful FTP logins

ftp.request.command=="PASV"
#FTP passive mode requests

ftp.request.command=="MKD" && ftp.request.arg=="dir01"
#FTP MKD (make directory) command for a directory named dir01 (the directory name argument is case
#sensitive)

ftp.response.code==257
#Successful directory creation response
```
