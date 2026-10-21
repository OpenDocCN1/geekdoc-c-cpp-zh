Before we send an email using an Arduino and an Ethernet shield, you should learn how to send an email from a command line using the telnet command. To do so, you have to find out the address of an SMTP server you can use first. The following instructions assume you’re using a Google Mail account (http://gmail.com). If you use a different email provider, you have to adjust the domain names accordingly. In any case, don’t abuse their service! When in doubt, read their usage terms!

Open a terminal, and enter the following:

```
maik> nslookup
> set type=mx
> gmail.com
Server:  192.168.2.1
Address:  192.168.2.1#53
Non-authoritative answer:
gmail.com mail exchanger = 5 gmail-smtp-in.l.google.com.
gmail.com mail exchanger = 10 alt1.gmail-smtp-in.l.google.com.
gmail.com mail exchanger = 20 alt2.gmail-smtp-in.
> exit
```

This command returns a list of all the Google Mail exchange servers (MX) available on your network. Take the first server name, and open a connection to the SMTP standard port 25 (replace the server name gmail-smtp-in.l.google.com and all email addresses accordingly):

```
⇒ maik> telnet gmail-smtp-in.l.google.com 25
⇒ Trying 74.125.77.27...
Connected to gmail-smtp-in.l.google.com.
Escape character is '^]'.
220 mx.google.com ESMTP q43si10820020eeh.100
⇒ HELO
⇒ 250 mx.google.com at your service
⇒ MAIL FROM: <arduino@example.com>
⇒ 250 2.1.0 OK q43si10820020eeh.100
⇒ RCPT TO: <info@example.com>
⇒ 250 2.1.5 OK q43si10820020eeh.100
⇒ DATA
⇒ 354 Go ahead q43si10820020eeh.100
⇒ from: arduino@example.com
⇒ to: info@example.com
⇒ subject: This is a test
⇒ 
⇒ Really, this is a test!
⇒ .
⇒ 250 2.0.0 OK 1286819789 q43si10820020eeh.100
⇒ QUIT
⇒ 221 2.0.0 closing connection q43si10820020eeh.100
Connection closed by foreign host.
```