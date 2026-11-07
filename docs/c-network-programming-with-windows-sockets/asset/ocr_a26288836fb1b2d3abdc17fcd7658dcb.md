A return value of 0 (zero) means the connection has been closed. On failure, SOCKET_ERROR is returned and WSAGetLastError() specifies: WSANOTINITIALIZED if WinSock wasn’t initialized with WSAStartup(); WSAENOTDOWN if the network subsystem is failing; WSAEINTR if the blocking call was canceled with WSAcancelBlockingCall(); WSAEINPROGRESS if a blocking call is in progress; WSAENOTCONN if the socket s isn’t connected; WSAENOTSOCK if the socket s isn’t a valid socket descriptor; WSAENOTSUP if MSG_OOB was specified by flags but the socket s isn’t a stream socket; WSAESHUTDOWN if the socket s has been shut-down; WSAEWOULDBLOCK if the socket s is marked as nonblocking and the recv() would block; WSAEMSGSIZE if socket s is a datagram socket and the datagram was too large for buf; WSAEINVAL if the socket s hasn’t been bound; WSAECONNABORTED if the virtual circuit was aborted due to timeout or other failure; WSAECONNRESET if the virtual circuit was reset by the remote side.

The following demonstrates a typical call to recv():

```
    SOCKET s;                 // socket to communicate over
    #define BUFSIZE (100)      // receive buffer size
    char pszBuf[BUFSIZE];      // buffer to receive data
    int nBytesRecv;            // number of bytes received
    int nError;                // error status

    // create, bind, and connect socket s ...

    nBytesRecv = recv(s, pszBuf, BUFSIZE, 0);
    if (nBytesRecv == SOCKET_ERROR)
    {
        nError = WSAGetLastError();
    }
    else
    {
        // nBytesRecv is the number of bytes successfully received
    }
```

The recv() function has the same problem with blocking as the accept(), connect(), getXByY, and send() functions. If there is no data waiting to be received, recv() blocks waiting for the sender to send some data. While recv() is blocking, the user loses control over your application. To prevent this problem, the WSAAsyncSelect() function is used to put the socket into nonblocking receive mode. The event of interest in this scenario is FD_READ. An FD_READ message is posted when a socket has data available to be read.

FD_READ works differently from FD_WRITE. For FD_WRITE, you get a single FD_WRITE when the socket is first connected. You must then send data until the send() results in a WSAEWOULDBLOCK error. You won’t get another FD_WRITE message until the condition that generated the WSAEWOULDBLOCK is cleared up. With FD_READ, you get the first FD_READ when data first arrives. If you then do a recv() and there is still more data waiting to be received, you will receive another FD_READ event notification. For example, suppose that the TCP/IP layer receives 100 bytes of data on a socket and WinSock posts a FD_READ