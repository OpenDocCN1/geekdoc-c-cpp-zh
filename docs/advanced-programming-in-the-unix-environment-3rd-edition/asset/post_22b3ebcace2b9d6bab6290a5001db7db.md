
## 16.8 Nonblocking and Asynchronous I/O

Normally, the recv functions will block when no data is immediately available. Similarly, the send functions will block when there is not enough room in the socket’s output queue to send the message. This behavior changes when the socket is in nonblocking mode. In this case, these functions will fail instead of blocking, setting errno to either EWOULDBLOCK or EAGAIN. When this happens, we can use either poll or select to determine when we can receive or transmit data.

The Single UNIX Specification includes support for a general asynchronous I/O mechanism (recall Section 14.5). The socket mechanism has its own way of handling asynchronous I/O, but this isn’t standardized in the Single UNIX Specification. Some texts refer to the classic socket-based asynchronous I/O mechanism as “signal-based I/O” to distinguish it from the general asynchronous I/O mechanism found in the Single UNIX Specification.

With socket-based asynchronous I/O, we can arrange to be sent the SIGIO signal when we can read data from a socket or when space becomes available in a socket’s write queue. Enabling asynchronous I/O is a two-step process.

- 1. Establish socket ownership so signals can be delivered to the proper processes.
- 2. Inform the socket that we want it to signal us when I/O operations won’t block.

We can accomplish the first step in three ways.

- 1. Use the F_SETOWN command with fcntl.
- 2. Use the FIOSETOWN command with ioctl.
- 3. Use the SIOCSPGRP command with ioctl.

To accomplish the second step, we have two choices.

- 1. Use the F_SETFL command with fcntl and enable the O_ASYNC file flag.
- 2. Use the FIOASYNC command with ioctl.

We have several options, but they are not universally supported. Figure 16.23 summarizes the support for these options provided by the platforms discussed in this text.

| Mechanism | POSIX.1 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|
| fcntl(fd, F_SETOWN, pid) | • | • | • | • | • |
| ioctl(fd, FIOSETOWN, pid) |  | • | • | • | • |
| ioctl(fd, SIOCSPGRP, pid) |  | • | • | • | • |
| fcntl(fd, F_SETFL, flags|O_ASYNC) |  | • | • | • |  |
| ioctl(fd, FIOASYNC, &n); |  | • | • | • | • |

Figure 16.23 Socket asynchronous I/O management commands

## 16.9 Summary

In this chapter, we looked at the IPC mechanisms that allow processes to communicate with other processes on different machines as well as within the same machine. We discussed how socket endpoints are named and how we can discover the addresses to use when contacting servers.

We presented examples of clients and servers that use connectionless (i.e., datagram-based) sockets and connection-oriented sockets. We briefly discussed asynchronous and nonblocking socket I/O and the interfaces used to manage socket options.

In the next chapter, we will look at some advanced IPC topics, including how we can use sockets to pass file descriptors between processes running on the same machine.

## Exercises

- 16.1 Write a program to determine your system's byte ordering.
- 16.2 Write a program to print out which stat structure members are supported for sockets on at least two different platforms, and describe how the results differ.
- 16.3 The program in Figure 16.17 provides service on only a single endpoint. Modify the program to support service on multiple endpoints (each with a different address) at the same time.
- 16.4 Write a client program and a server program to return the number of processes currently running on a specified host computer.
- 16.5 In the program in Figure 16.18, the server waits for the child to execute the uptime command and exit before accepting the next connect request. Redesign the server so that the time to service one request doesn't delay the processing of incoming connect requests.
- 16.6 Write two library routines: one to enable asynchronous (signal-based) I/O on a socket and one to disable asynchronous I/O on a socket. Use Figure 16.23 to make sure that the functions work on all platforms with as many socket types as possible.

## Advanced IPC

### 17.1 Introduction

In the previous two chapters, we discussed various forms of IPC, including pipes and sockets. In this chapter, we look at an advanced form of IPC—the UNIX domain socket mechanism—and see what we can do with it. With this form of IPC, we can pass open file descriptors between processes running on the same computer system, server processes can associate names with their file descriptors, and client processes running on the same system can use these names to rendezvous with the servers. We’ll also see how the operating system provides a unique IPC channel per client.

### 17.2 UNIX Domain Sockets

UNIX domain sockets are used to communicate with processes running on the same machine. Although Internet domain sockets can be used for this same purpose, UNIX domain sockets are more efficient. UNIX domain sockets only copy data; they have no protocol processing to perform, no network headers to add or remove, no checksums to calculate, no sequence numbers to generate, and no acknowledgements to send.

UNIX domain sockets provide both stream and datagram interfaces. The UNIX domain datagram service is reliable, however. Messages are neither lost nor delivered out of order. UNIX domain sockets are like a cross between sockets and pipes. You can use the network-oriented socket interfaces with them, or you can use the socketpair function to create a pair of unnamed, connected, UNIX domain sockets.

```
#include <sys/socket.h>
int socketpair(int domain, int type, int protocol, int sockfd[2]);
Returns: 0 if OK, -1 on error
```

Although the interface is sufficiently general to allow socketpair to be used with other domains, operating systems typically provide support only for the UNIX domain.

![](img/244bf0c3b6d0288ae397336907e37851_663_0.png)

A pair of connected UNIX domain sockets acts like a full-duplex pipe: both ends are open for reading and writing (see Figure 17.1). We’ll refer to these as “fd-pipes” to distinguish them from normal, half-duplex pipes.

## Example — fd_pipe Function

Figure 17.2 shows the fd_pipe function, which uses the socketpair function to create a pair of connected UNIX domain stream sockets.

```
#include "apue.h"
#include <sys/socket.h>

/*
 * Returns a full-duplex pipe (a UNIX domain socket) with
 * the two file descriptors returned in fd[0] and fd[1].
 */
int
fd_pipe(int fd[2])
{
    return(socketpair(AF_UNIX, SOCK_STREAM, 0, fd));
}
```

Figure 17.2 Creating a full-duplex pipe

Some BSD-based systems use UNIX domain sockets to implement pipes. But when pipe is called, the write end of the first descriptor and the read end of the second descriptor are both closed. To get a full-duplex pipe, we must call socketpair directly.

```
{ int i, n, err; int fd[2]; int qid[NQ]; struct pollfd pfd[NQ]; struct threadinfo ti[NQ]; pthread_t tid[NQ]; char buf[MAXMSZ]; for (i = 0; i < NQ; i++) { if ((qid[i] = msgget((KEY)+1, IPC_CREAT|0666)) < 0) err_sys("msgget error"); printf("queue ID %d is %d\n", i, qid[i]); if (socketpair(AF_UNIX, SOCK_DGRAM, 0, fd) < 0) err_sys("socketpair error"); pfd[i].fd = fd[0]; pfd[i].events = POLLIN; ti[i].qid = qid[i]; ti[i].fd = fd[1]; if ((err = pthread_create(&tid[i], NULL, helper, &ti[i])) != 0) err_exit(err, "pthread_create error"); } for (;;) { if (poll(pfd, NQ, -1) < 0) err_sys("poll error"); for (i = 0; i < NQ; i++) { if (pfd[i].revents & POLLIN) { if ((n = read(pfd[i].fd, buf, sizeof(buf))) < 0) err_sys("read error"); buf[n] = 0; printf("queue id %d, message %s\n", qid[i], buf); } } exit(0); }
```

# Figure 17.3 Poll for XSI messages using UNIX domain sockets

Note that we use datagram (SOCK_DGRAM) sockets instead of stream sockets. This allows us to retain message boundaries so when we read from the socket, we read only one message at a time.

This technique allows us to use either poll or select (indirectly) with message queues. As long as the costs of one thread per queue and copying each message two extra times (once to write it to the socket and once to read it from the socket) are acceptable, this technique will make it easier to use XSI message queues.

Well use the program shown in Figure 17.4 to send messages to our test program from Figure 17.3.
