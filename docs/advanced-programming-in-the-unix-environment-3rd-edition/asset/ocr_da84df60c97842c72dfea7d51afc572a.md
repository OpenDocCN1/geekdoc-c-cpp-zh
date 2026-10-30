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