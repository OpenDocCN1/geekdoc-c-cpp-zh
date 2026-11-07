
> Unfortunately, there are two conflicting interpretations of out-of-band implementation. Internet RFC 793 introduced the concept of out-of-band data, and RFC 1122 provided the host requirements. The problem arises because the Berkeley implementation of out-of-band data handling does not follow RFC 1122. Most TCP/IP stack providers document their implementation so that you know which they use: BSD or RFC 1122. Because of this difference of opinion, it is best not to use out-of-band data in your applications. Of course, if your application must interoperate with an existing client or server, perhaps running on a UNIX computer, you have no choice.

The following demonstrates a typical call to `send()`:

```c
SOCKET s;             // socket to communicate over
char pszBuf[100];     // buffer to send
int nBufLen;          // number of bytes in buffer to send
int nBytesSent;       // bytes sent
int nError;           // error status

// create, bind, and connect socket s ...

lstrcpy(pszBuf, "Hello, World!");
nBufLen = lstrlen(pszBuf);

nBytesSent = send(s, pszBuf, nBufLen, 0);
if (nBytesSent == SOCKET_ERROR)
{
    nError = WSAGetLastError();
}
else
{
    // nBytesSent is the number of bytes successfully sent
}
```

The `send()` function has the same problem with blocking as the `accept()`, `connect()`, and `getXbyY` functions. If none of the data can be sent for some reason—because the receiving socket has too much incoming data spooled up, for example—`send()` blocks waiting for the receiver to read the spooled up data. While `send()` is blocking, the user loses control over your application. To prevent this problem, the `WSAAsyncSelect()` function is used to put the socket into nonblocking send mode. The event of interest in this scenario is `FD_WRITE`. An `FD_WRITE` message is posted when a socket is first connected with `connect()` or accepted with `accept()`, and then after a `send()` fails with `WSAEWOULDBLOCK` and buffer space becomes available. Therefore, an application can assume that sends are possible starting from the first `FD_WRITE` message and lasting until a send returns `WSAEWOULDBLOCK`. After such a failure, the application will be notified that sends are again possible with a new `FD_WRITE` message.

```c
{
    // ...
    return 0L;
}

// what event are we being notified of?
switch (WSAGETSELECTEVENT(lParam))
{
    case FD_CONNECT:
        // client made a connection

        // allocate some buffer space and fill
        // it with useful data to send
        nBufLen = 5000;
        pszBuf = (char *)malloc(nBufLen);
        if (pszBuf == NULL)
            nBufLen = 0;
        else
        {
            // this temporary pointer will be used
            // to move through the buffer
            pszBufTmp = pszBuf;

            // fill the buffer with some useful data to send ...
        }
        break; // case FD_CONNECT

    case FD_WRITE:
        // client can send data now

        // is there any data to send?
        if (nBufLen > 0)
        {
            // send as many bytes as possible
            do
            {
                // send data in 100 byte chunks
                if (nBufLen < 100)
                    nBytesSent = send(m_s, pszBufTmp, nBufLen, 0);
                else
                    nBytesSent = send(m_s, pszBufTmp, 100, 0);

                if (nBytesSent == SOCKET_ERROR)
                {
                    nError = WSAGetLastError();
                    if (nError == WSAEWOULDBLOCK)
                        // ok, we'll get another FD_WRITE eventually
                    else
                        // a real error ...
                }
            }
            else
            {
                // advance the pointer and decrement the byte count
                pszBufTmp += nBytesSent;
                nBufLen -= nBytesSent;

                if (nBufLen == 0)
                {
                    free(pszBuf);
                }
            }
        } while ((nBytesSent != SOCKET_ERROR) && (nBufLen > 0));
        break; // case FD_WRITE

} // switch

return 0L;
}
```

Notice that the asynchronous select message handler, CClientWindow::OnAsyncSelect(), handles multiple WinSock events, so a switch statement is used. As soon as the client's connect succeeds, the FD_CONNECT message is sent, telling you that the socket is connected. Immediately after that, the FD_WRITE message is sent, telling you that the socket is writable. In this example, there is only one call to WSAAsyncSelect() done in CClientWindow::DoConnect(). This single call registers interest in both the FD_CONNECT and the FD_WRITE events. You also could use two separate calls. The first call, in the DoConnect() member function, could simply register interest in FD_CONNECT. Then, in the OnAsyncSelect() member function's handling of FD_CONNECT, you could call WSAAsyncSelect() expressing interest in just the FD_WRITE event. Either technique gives the same result.

In this example, a buffer is allocated and filled with data to send in response to the FD_CONNECT event. The FD_WRITE handler sends the data in 100-byte pieces until the entire buffer is transmitted. I used 100-byte buffers in this example so that you could see the do-while loop in action. This loop is executed as long as there are bytes to send and there are no errors. If you get a WSAEWOULDBLOCK error, it doesn't pose a problem because the FD_WRITE handler will be called again as soon as the network subsystem can do it. Thanks to the use of the static variables, when the FD_WRITE handler gets called again, the rest of the buffer is sent from where it left off.

## Receiving Data

Sending is just half the battle. This section describes receiving data using the `recv()` function. Its prototype is as follows:

```c
int PASCAL FAR recv(SOCKET s, char FAR * buf, int len, int flags);
```

s is the connected socket from which to receive data. buf is a pointer to a buffer that will receive the data. len is the size of buf. flags specifies the way in which the recv() call is made. flags can be any of the following logically ORed together: 0 (zero) for no special receive options, MSG_PEEK to copy the data to buf but not remove it from the internal WinSock queues, and MSG_OOB to process out-of-band data. On success, recv() returns the number of bytes received. This could range from 0 (zero) to len.

A return value of 0 (zero) means the connection has been closed. On failure, SOCKET_ERROR is returned and WSAGetLastError() specifies: WSANOTINITIALIZED if WinSock wasn’t initialized with WSAStartup(); WSAENOTDOWN if the network subsystem is failing; WSAEINTR if the blocking call was canceled with WSAcancelBlockingCall(); WSAEINPROGRESS if a blocking call is in progress; WSAENOTCONN if the socket s isn’t connected; WSAENOTSOCK if the socket s isn’t a valid socket descriptor; WSAENOTSUP if MSG_OOB was specified by flags but the socket s isn’t a stream socket; WSAESHUTDOWN if the socket s has been shut down; WSAEWOULDBLOCK if the socket s is marked as nonblocking and the recv() would block; WSAEMSGSIZE if socket s is a datagram socket and the datagram was too large for buf; WSAEINVAL if the socket s hasn’t been bound; WSAECONNABORTED if the virtual circuit was aborted due to timeout or other failure; WSAECONNRESET if the virtual circuit was reset by the remote side.

The following demonstrates a typical call to recv():

```c
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

The `recv()` function has the same problem with blocking as the `accept()`, `connect()`, `getXbyY`, and `send()` functions. If there is no data waiting to be received, `recv()` blocks waiting for the sender to send some data. While `recv()` is blocking, the user loses control over your application. To prevent this problem, the `WSAAsyncSelect()` function is used to put the socket into nonblocking receive mode. The event of interest in this scenario is `FD_READ`. An `FD_READ` message is posted when a socket has data available to be read.

`FD_READ` works differently from `FD_WRITE`. For `FD_WRITE`, you get a single `FD_WRITE` when the socket is first connected. You must then send data until the `send()` results in a `WSAEWOULDBLOCK` error. You won’t get another `FD_WRITE` message until the condition that generated the `WSAEWOULDBLOCK` is cleared up. With `FD_READ`, you get the first `FD_READ` when data first arrives. If you then do a `recv()` and there is still more data waiting to be received, you will receive another `FD_READ` event notification. For example, suppose that the TCP/IP layer receives 100 bytes of data on a socket and WinSock posts a `FD_READ`
