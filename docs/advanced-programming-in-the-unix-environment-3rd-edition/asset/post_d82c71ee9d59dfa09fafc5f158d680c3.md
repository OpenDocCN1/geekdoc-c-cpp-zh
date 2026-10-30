
| Attribute | Status | Description |
|---|---|---|
| attributes-charset | required | the character set used by attributes of type text or name |
| attributes-natural-language | required | the natural language used by attributes of type text or name |
| printer-uri | required | the printer's Universal Resource Identifier |
| requesting-user-name | optional | name of user submitting job (used for authentication, if enabled) |
| job-name | optional | name of job used to distinguish between multiple jobs |
| ipp-attribute-fidelity | optional | if true, tells printer to reject job if all attributes can't be met; otherwise, printer does its best to print the job |
| document-name | optional | the name of the document (suitable for printing in a banner, for example) |
| document-format | optional | the format of the document (e.g., plaintext, PostScript) |
| document-natural-language | optional | the natural language of the document |
| compression | optional | the algorithm used to compress the document data |
| job-k-octets | optional | size of the document in 1,024-octet units |
| job-impressions | optional | number of impressions (images imposed on a page) submitted in this job |
| job-media-sheets | optional | number of sheets printed by this job |

Figure 21.5 Attributes of print-job request

The IPP header contains a mixture of text and binary data. Attribute names are stored as text, but sizes are stored as binary integers. This complicates the process of building and parsing the header, since we need to worry about such things as network byte order and our host processor's ability to address an integer on an arbitrary byte boundary. A better alternative would have been to design the header to contain text only. This simplifies processing at the cost of slightly larger protocol messages.

## 21.3 The Hypertext Transfer Protocol

Version 1.1 of HTTP is specified in RFC 2616. HTTP is also a request-response protocol. A request message contains a start line, followed by header lines, a blank line, and an optional entity body. The entity body contains the IPP header and data in this case.

HTTP headers are ASCII, with each line terminated by a carriage return (\r) and a line feed (\n). The start line consists of a method that indicates which operation the client is requesting, a Uniform Resource Locator (URL) that describes the server and protocol, and a string indicating the HTTP version. The only method used by IPP is POST, which is used to send data to a server.

The header lines specify attributes, such as the format and length of the entity body. A header line consists of an attribute name followed by a colon, optional white space, and the attribute value, and is terminated by a carriage return and a line feed. For example, to specify that the entity body contains an IPP message, we include the header line

```
Content-Type: application/ipp
```

The following is a sample HTTP header for a print request submitted to the author’s Xerox Phaser 8560 printer:

```
POST /ipp HTTP/1.1^M
Content-Length: 21931^M
Content-Type: application/ipp^M
Host: phaser8560:631^M
^M
```

The Content-Length line specifies the size in bytes of the amount of data in the HTTP message. This excludes the size of the HTTP header, but includes the size of the IPP header. The Host line specifies the host name and port number of the server to which the message is being sent.

The ^M at the end of each line is the carriage return that precedes the line feed. The line feed doesn’t show up as a printable character. Note that the last line of the header is empty, except for the carriage return and line feed.

The start line in an HTTP response message contains a version string followed by a numeric status code and a status message, terminated by a carriage return and a line feed. The remainder of the HTTP response message has the same format as the request message: headers followed by a blank line and an optional entity body.

In response to a print request, the printer might send us the following message:

```
HTTP/1.1 200 OK^M
Content-Type: application/ipp^M
Cache-Control: no-cache, no-store, must-revalidate^M
Expires: THU, 26 OCT 1995 00:00:00 GMT^M
Content-Length: 215^M
Server: Allegro-Software-RomPager/4.34^M
^M
```

As far as our print spooler is concerned, all we care about in this message is the first line: it tells us whether the request succeeded or failed using a numeric error code and a short string. The remainder of the message contains additional information to control caching by nodes that might sit in between the client and the server and to indicate the software version running on the server.

## 21.4 Printer Spooling

The programs that we develop in this chapter form the basis of a simple printer spooler. A simple user command sends a file to the printer spooler; the spooler saves it to disk, queues the request, and ultimately sends the file to the printer.

All UNIX Systems provide at least one print spooling system. FreeBSD ships LPD, the BSD print spooling system (see lpd(8) and Chapter 13 of Stevens [1990]). Linux and Mac OS X include CUPS, the Common UNIX Printing System (see cups(8)). Solaris ships with the standard System V printer spooler (see lp(1) and lpsched(1M)). In this

chapter, our interest is not in these spooling systems per se, but rather in communicating with a network printer. We need to develop a spooling system to solve the problem of multiple access to a single resource (the printer).

We use a simple command that reads a file and sends it to the printer spooler daemon. The command has one option to force the file to be treated as plaintext (the default assumes that the file is PostScript). We call this command `print`.

In our print spooler daemon, `printd`, we use multiple threads to divide up the work that the daemon needs to accomplish.

- One thread listens on a socket for new print requests arriving from clients running the `print` command.
- A separate thread is spawned for each client to copy the file to be printed to a spooling area.
- One thread communicates with the printer, sending it queued jobs one at a time.
- One thread handles signals.

Figure 21.6 shows how these components fit together.

![](img/244bf0c3b6d0288ae397336907e37851_827_0.png)

**Figure 21.6** Printer spooling components

The print configuration file is `/etc/printer.conf`. It identifies the host name of the server running the printer spooling daemon and the host name of the network printer. The spooling daemon is identified by a line starting with the `printserver` keyword, followed by white space and the host name of the server. The printer is identified by a line starting with the `printer` keyword, followed by white space and the host name of the printer.

A sample printer configuration file might contain the following lines:

```
printserver    fujin
printer        phaser8560
```

where `fujin` is the host name of the computer system running the printer spooling daemon, and `phaser8560` is the host name of the network printer. We assume these

names are listed in /etc/hosts or registered with whatever name service we are using, so that we can translate the names to network addresses.

We can run the print command on the same machine where the printer spooling daemon is running, or we can run it from any machine on the same network. We only need to configure the printserver field in /etc/printer.conf in the latter case, because only the daemon needs to know the name of the printer.

## Security

Programs that run with superuser privileges have the potential to open a computer system up to attack. Such programs usually aren’t more vulnerable than any other program, but when compromised can lead to attackers obtaining full access to your system.

The printer spooling daemon in this chapter starts out with superuser privileges in this example to be able to bind a socket to a privileged TCP port number. To make the daemon less vulnerable to attack, we can

- Design the daemon to conform to the principles of least privilege (Section 8.11). After we obtain a socket bound to a privileged port address, we can change the user and group IDs of the daemon to something other than root (1p, for example). All the files and directories used to store queued print jobs should be owned by this nonprivileged user. This way, the daemon, if compromised, will provide the attacker with access only to the printing subsystem. This is still a concern, but it is far less serious than an attacker getting full access to your system.
- Audit the daemon’s source code for all known potential vulnerabilities, such as buffer overruns.
- Log unexpected or suspicious behavior so that an administrator can take note and investigate further.

## 21.5 Source Code

The source code for this chapter comprises five files, not including some of the common library routines we’ve used in earlier chapters:

| ipp.h | Header file containing IPP definitions |
| print.h | Header containing common constants, data structure definitions, and utility routine declarations |
| util.c | Utility routines used by the two programs |
| print.c | The C source file for the command used to print a file |
| printd.c | The C source file for the printer spooling daemon |

We will study each file in the order listed.
