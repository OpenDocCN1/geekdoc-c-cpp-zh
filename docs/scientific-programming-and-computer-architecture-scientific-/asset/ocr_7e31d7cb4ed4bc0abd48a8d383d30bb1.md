# Chapter 6. Special Topic: Networks and Message Passing

described in section 6.4.4.

In all probability, the reader's computer can run servers or clients. To run the example in this section in real time, it is enough to have an ssh connection to some remote site that the client and server may be run at different locations.

Section 6.4.5 is a discussion of Internet latency, which we define as the round-trip time. The path that packets take from a destination to the source can be different from the path they take from the source to the destination. A significant fraction of Internet latency can be due to the finite speed of light. During their journey between source and destination, TCP/IP packets spend in buffers maintained by enormous routers. The buffers are typically linked lists and are therefore exposed to latency to DRAM memory. Buffering is another source of latency.

On a good day, the bandwidth between Michigan and Texas can be 2 MB/s. That figure is lower than the bandwidth to hard disk by a factor of 100. The bandwidth to hard disk can be lower than the bandwidth to bandwidth by a factor of nearly 1000. The gap between Internet bandwidth and the bandwidth to hard disk may narrow in the coming years. In section 6.4.6, we relate Internet bandwidth to congestion windows.

On the whole, the aim of this section is to give a view of the Internet from inside a computer program. The discussion is illustrated using programs throughout. Algorithms for flow control and congestion control internal to the Internet are not discussed.

Our discussion is based on functions in the sockets API, such as getaddrinfo(), bind(), listen(), accept(), connect(), recv(), and send(). The prototypes of these functions are in various header files.¹18 Here we list all the header files to be included in our programs.

```
#include <unist.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/tcp.h>
#include <netdb.h>
```

> ¹18 A readable introduction to the sockets API is given by Hall (2009). See http://beej.us/guide/bgnet/. Peterson and Davie (2010) and Tanenbaum and Wetherall (2010) are two well-known textbooks on computer networks.