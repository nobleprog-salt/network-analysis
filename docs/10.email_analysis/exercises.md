## EMAIL ANALYSIS EXERCISES

**smtp-prob.pcapng**
  - A user (10.1.0.1) complains that they cannot send email to the SMTP server (10.2.23.11).
  - Look at the trace file! It contains a ping process and FTP session before the attempt to communicate with the SMTP server. Now look for any indication that the client is trying to reach the SMTP server (10.2.23.11).
  - Does the fault lie with the client, the server or the network?

**smtp-sendone.pcapng**
  - This trace shows a standard single email being sent through SMTP. What email application is the client using?
