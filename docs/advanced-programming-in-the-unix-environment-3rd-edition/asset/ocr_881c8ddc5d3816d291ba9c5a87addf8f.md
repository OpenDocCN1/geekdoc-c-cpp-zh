If the socket descriptor is in nonblocking mode, which we discuss further in Section 16.8, connect will return −1 with errno set to the special error code EINPROGRESS if the connection can’t be established immediately. The application can use either poll or select to determine when the file descriptor is writable. At this point, the connection is complete.

The connect function can also be used with a connectionless network service (SOCK_DGRAM). This might seem like a contradiction, but it is an optimization instead. If we call connect with a SOCK_DGRAM socket, the destination address of all messages we send is set to the address we specified in the connect call, relieving us from having to provide the address every time we transmit a message. In addition, we will receive datagrams only from the address we’ve specified.

A server announces that it is willing to accept connect requests by calling the listen function.

```
#include <sys/socket.h>
int listen(int sockfd, int backlog);

Returns: 0 if OK, −1 on error
```

The backlog argument provides a hint to the system regarding the number of outstanding connect requests that it should enqueue on behalf of the process. The actual value is determined by the system, but the upper limit is specified as SOMAXCONN in <sys/socket.h>.

> On Solaris, the SOMAXCONN value in <sys/socket.h> is ignored. The particular maximum depends on the implementation of each protocol. For TCP, the default is 128.

Once the queue is full, the system will reject additional connect requests, so the backlog value must be chosen based on the expected load of the server and the amount of processing it must do to accept a connect request and start the service.

Once a server has called listen, the socket used can receive connect requests. We use the accept function to retrieve a connect request and convert it into a connection.

```
#include <sys/socket.h>
int accept(int sockfd, struct sockaddr *restrict addr,
    socklen_t *restrict len);

Returns: file (socket) descriptor if OK, −1 on error
```

The file descriptor returned by accept is a socket descriptor that is connected to the client that called connect. This new socket descriptor has the same socket type and address family as the original socket (sockfd). The original socket passed to accept is not associated with the connection, but instead remains available to receive additional connect requests.

If we don’t care about the client’s identity, we can set the addr and len parameters to NULL. Otherwise, before calling accept, we need to set the addr parameter to a buffer large enough to hold the address and set the integer pointed to by len to the size of the buffer in bytes. On return, accept will fill in the client’s address in the buffer and update the integer pointed to by len to reflect the size of the address.