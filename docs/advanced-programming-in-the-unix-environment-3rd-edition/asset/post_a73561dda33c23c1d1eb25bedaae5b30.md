
Figure 20.9 is a graph of the data from Figure 20.8 for advisory fine-grained locking. We plot the clock time as the number of processes goes from 1 to 16. We also plot the user CPU time divided by the number of processes and the system CPU time divided by the number of processes.

![](img/244bf0c3b6d0288ae397336907e37851_819_0.png)

Figure 20.9 Values from Figure 20.8 for advisory fine-grained locking

Note that both CPU times, divided by the number of processes, are linear but that the plot of the clock time is nonlinear. The probable reason is the added amount of CPU time used by the operating system to switch between processes as the number of processes increases. This operating system overhead would show up as an increased clock time, but shouldn't affect the CPU times of the individual processes.

The reason the user CPU time increases with the number of processes is that there are more records in the database. Each hash chain is getting longer, so it takes the _db_find_and_lock function longer, on average, to find a record.

## 20.10 Summary

This chapter has taken a long look at the design and implementation of a database library. Although we’ve kept the library small and simple for presentation purposes, it contains the record locking required to allow concurrent access by multiple processes.

We’ve also looked at the performance of this library with various numbers of processes using no locking, advisory locking (fine-grained and coarse-grained), and mandatory locking. With a single process, we saw that advisory locking adds between

29% and 59% to the clock time over no locking and that mandatory locking adds about another 15% over advisory locking.

## Exercises

20.1 The locking in _db_dodelete is somewhat conservative. For example, we could allow more concurrency by not write locking the free list until we really need to; that is, the call to writew_lock could be moved between the calls to _db_writedat and _db_readptr. What happens if we do this?

20.2 If _db_nextrec did not read lock the free list and a record that it was reading was also in the process of being deleted, describe how _db_nextrec could return the correct key but an all-blank (hence incorrect) data record. (Hint: Look at _db_dodelete.)

20.3 At the end of Section 20.8, we described the locking performed by _db_writeidx and _db_writedat. We said that this locking didn’t interfere with other readers and writers except those making calls to db_store. Is this true if mandatory locking is being used?

20.4 How would you integrate the fsync function into this database library?

20.5 In db_store, we write the data record before the index record. What happens if you do it in the opposite order?

20.6 Create a new database and write some number of records to the database. Write a program that calls db_nextrec to read each record in the database, and call _db_hash to calculate the hash value for each record. Print a histogram of the number of records on each hash chain. Is the hashing function in _db_hash adequate?

20.7 Modify the database functions so that the number of hash chains in the index file can be specified when the database is created.

20.8 Compare the performance of the database functions when the database is (a) on the same host as the test program and (b) on a different host accessed via NFS. Does the record locking provided by the database library still work?

20.9 The database reuses free list records only if the sizes of the key buffer and data buffer match the needed sizes exactly. Modify the database to allow larger buffer sizes on the free list to satisfy the request. How do you have to change the persistent format of the database to support this feature?

20.10 After implementing a solution to Exercise 20.9, write a tool to convert one database format to the other.

This page intentionally left blank

## Communicating with a Network Printer

### 21.1 Introduction

We now develop a program that can communicate with a network printer. These printers are connected to multiple computers via Ethernet and often support PostScript files as well as plain text files. Applications generally use the Internet Printing Protocol (IPP) to communicate with these printers, although some support alternative communication protocols.

We are about to describe two programs: a print spooler daemon that sends jobs to a printer and a command to submit print jobs to the spooler daemon. Since the print spooler has to do multiple things (e.g., communicate with clients submitting jobs, communicate with the printer, read files, scan directories), this gives us a chance to use many of the functions from earlier chapters. For example, we use threads (Chapters 11 and 12) to simplify the design of the print spooler and sockets (Chapter 16) to communicate between the program used to schedule a file to be printed and the print spooler, and also between the print spooler and the network printer.

### 21.2 The Internet Printing Protocol

IPP specifies the communication rules for building network-based printing systems. By embedding an IPP server inside a printer with an Ethernet card, the printer can service requests from many computer systems. These computer systems need not be located on the same physical network, however. IPP is built on top of standard Internet protocols, so any computer that can create a TCP/IP connection to the printer can submit a print job.

IPP is specified in a series of documents (Requests For Comments, or RFCs) available at .../.../.../.../www.ietf.org/rfc.html. Draft standards are developed by the Printer Working Group, which is associated with the IEEE. These drafts are available at .../.../.../.../www.pwg.org/ipp. Documents are listed in Figure 21.1, although many other documents are available to further specify administrative procedures, job attributes, and the like.

| Document | Title |
|---|---|
| RFC 2567 | Design Goals for an Internet Printing Protocol |
| RFC 2568 | Rationale for the Structure of the Model and Protocol for the Internet Printing Protocol |
| RFC 2911 | Internet Printing Protocol 1/1: Model and Semantics |
| RFC 2910 | Internet Printing Protocol 1/1: Encoding and Transport |
| RFC 3196 | Internet Printing Protocol 1/1: Implementor's Guide |
| Candidate Standard 5100.12-2011 | Internet Printing Protocol Version 2.0, Second Edition |

Figure 21.1 Primary IPP documents

Candidate Standard 5100.12-2011 specifies all features that implementations must support to conform to different versions of the IPP standard. There are many proposed extensions to the IPP protocol (specific features are defined in other IPP-related documents). These features are divided into groups to create different conformance levels; each level is a different protocol version. For compatibility, each higher level of conformance requires that implementations meet most of the requirements defined by lower versions of the standard. In this chapter, we will use IPP version 1.1 in our simple example.

IPP is built on top of HTTP, the Hypertext Transfer Protocol (Section 21.3). HTTP, in turn, is built on top of TCP/IP. Figure 21.2 shows the structure of an IPP message.

| Ethernet header | IP header | TCP header | HTTP header | IPP header | data to be printed |

Figure 21.2 Structure of an IPP message

IPP is a request-response protocol. A client sends a request message to a server, and the server answers with a response message. The IPP header contains a field that indicates the requested operation. Operations are defined to submit print jobs, cancel print jobs, get job attributes, get printer attributes, pause and restart the printer, place a job on hold, and release a held job.

![](img/244bf0c3b6d0288ae397336907e37851_824_0.png)

# Figure 21.3 Structure of an IPP header

The next 4 bytes contain an integer identifying the request, which allows requests to be matched up with responses. Optional attributes follow this, terminated by an end-of-attributes tag. Any data that might be associated with the request follows immediately after the end-of-attributes tag.

In the header, integers are stored as signed, two’s-complement, binary values in big-endian byte order (i.e., network byte order). Attributes are stored in groups. Each group starts with a single byte identifying the group. Within each group, an attribute is generally represented as a 1-byte tag, followed by a 2-byte name length, followed by the name of the attribute, followed by a 2-byte value length, and finally by the value itself. The value can be encoded as a string, a binary integer, or a more complex structure, such as a date/timestamp.

Figure 21.4 shows how the attributes-charset attribute would be encoded with a value of utf-8.

![](img/244bf0c3b6d0288ae397336907e37851_824_1.png)

# Figure 21.4 Sample IPP attribute encoding

Depending on the operation requested, some attributes are required to be provided in the request message, whereas others are optional. For example, Figure 21.5 shows the attributes defined for a print-job request.
