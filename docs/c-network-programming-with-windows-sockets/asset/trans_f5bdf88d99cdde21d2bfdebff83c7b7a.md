
> 不幸的是，对于带外实现存在两种相互冲突的解释。Internet RFC 793 引入了带外数据的概念，RFC 1122 则给出了主机要求。问题之所以出现，是因为伯克利对带外数据处理的实现并不遵循 RFC 1122。大多数 TCP/IP 协议栈提供商都会记录其实现，以便你了解他们使用的是哪一种：BSD 还是 RFC 1122。由于这种观点分歧，最好在应用程序中不要使用带外数据。当然，如果你的应用程序必须与现有的客户端或服务器（可能运行在 UNIX 计算机上）互操作，那你就别无选择。

下面演示一次典型的 `send()` 调用：

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

`send()` 函数与 `accept()`、`connect()` 和 `getXbyY` 函数一样存在阻塞问题。如果由于某种原因无法发送任何数据——例如，接收套接字已缓存了太多传入数据——`send()` 会阻塞，等待接收方读取这些已缓存的数据。当 `send()` 阻塞时，用户会失去对应用程序的控制。为防止这个问题，可使用 `WSAAsyncSelect()` 函数将套接字置于非阻塞发送模式。此场景中关注的事件是 `FD_WRITE`。当套接字首次通过 `connect()` 连接或通过 `accept()` 接受时，会投递一个 `FD_WRITE` 消息；此后，当 `send()` 因 `WSAEWOULDBLOCK` 失败并且缓冲区空间变得可用时，也会投递该消息。因此，应用程序可以假定：从第一条 `FD_WRITE` 消息开始，发送就是可能的，直到某次发送返回 `WSAEWOULDBLOCK` 为止。发生此类失败后，应用程序将通过一条新的 `FD_WRITE` 消息收到再次可以发送的通知。

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

请注意，异步选择消息处理程序 CClientWindow::OnAsyncSelect() 会处理多个 WinSock 事件，因此使用了 switch 语句。客户端的连接一旦成功，就会发送 FD_CONNECT 消息，告诉你套接字已连接。紧接着会发送 FD_WRITE 消息，告诉你套接字可写。在此示例中，CClientWindow::DoConnect() 中只调用了一次 WSAAsyncSelect()。这一次调用同时注册了对 FD_CONNECT 和 FD_WRITE 事件的关注。你也可以使用两次单独的调用。第一次调用在 DoConnect() 成员函数中，可以只注册对 FD_CONNECT 的关注。然后，在 OnAsyncSelect() 成员函数处理 FD_CONNECT 时，你可以调用 WSAAsyncSelect() 只表达对 FD_WRITE 事件的关注。两种方法的结果相同。

在此示例中，响应 FD_CONNECT 事件时会分配一个缓冲区，并填入要发送的数据。FD_WRITE 处理程序以 100 字节为单位发送数据，直到整个缓冲区被传输完毕。我在这个示例中使用了 100 字节的缓冲区，以便你能看到 do-while 循环的实际运行。只要还有字节要发送且没有错误，这个循环就会执行。如果遇到 WSAEWOULDBLOCK 错误，这不会造成问题，因为只要网络子系统能够处理，FD_WRITE 处理程序就会再次被调用。由于使用了静态变量，当 FD_WRITE 处理程序再次被调用时，会从上次中断的地方继续发送缓冲区剩余部分。

## 接收数据

发送只是战斗的一半。本节介绍使用 `recv()` 函数接收数据。其原型如下：

```c
int PASCAL FAR recv(SOCKET s, char FAR * buf, int len, int flags);
```

s 是已连接、用于接收数据的套接字。buf 是指向将接收数据的缓冲区的指针。len 是 buf 的大小。flags 指定调用 recv() 的方式。flags 可以是以下任意值的逻辑或组合：0（零）表示没有特殊的接收选项，MSG_PEEK 表示将数据复制到 buf 但不从内部 WinSock 队列中移除，MSG_OOB 表示处理带外数据。成功时，recv() 返回接收到的字节数。该值范围可以从 0（零）到 len。

返回值为 0（零）表示连接已关闭。失败时，会返回 SOCKET_ERROR，并由 WSAGetLastError() 指明具体错误：如果 WinSock 未通过 WSAStartup() 初始化，则为 WSANOTINITIALIZED；如果网络子系统发生故障，则为 WSAENOTDOWN；如果阻塞调用被 WSAcancelBlockingCall() 取消，则为 WSAEINTR；如果阻塞调用正在进行，则为 WSAEINPROGRESS；如果套接字 s 未连接，则为 WSAENOTCONN；如果套接字 s 不是有效的套接字描述符，则为 WSAENOTSOCK；如果 flags 指定了 MSG_OOB，但套接字 s 不是流式套接字，则为 WSAENOTSUP；如果套接字 s 已关闭，则为 WSAESHUTDOWN；如果套接字 s 被标记为非阻塞且 recv() 会阻塞，则为 WSAEWOULDBLOCK；如果套接字 s 是数据报套接字且数据报对于 buf 来说太大，则为 WSAEMSGSIZE；如果套接字 s 尚未绑定，则为 WSAEINVAL；如果虚电路因超时或其他故障而中止，则为 WSAECONNABORTED；如果虚电路被远程端重置，则为 WSAECONNRESET。

下面演示一次典型的 recv() 调用：

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

`recv()` 函数与 `accept()`、`connect()`、`getXbyY` 和 `send()` 函数一样存在阻塞问题。如果没有等待接收的数据，`recv()` 会阻塞，等待发送方发送一些数据。当 `recv()` 阻塞时，用户会失去对应用程序的控制。为防止这个问题，可使用 `WSAAsyncSelect()` 函数将套接字置于非阻塞接收模式。此场景中关注的事件是 `FD_READ`。当套接字有数据可供读取时，会投递一个 `FD_READ` 消息。

`FD_READ` 的工作方式与 `FD_WRITE` 不同。对于 `FD_WRITE`，当套接字首次连接时，你会收到一个 `FD_WRITE`。然后你必须发送数据，直到 `send()` 导致 `WSAEWOULDBLOCK` 错误。在产生 `WSAEWOULDBLOCK` 的条件被清除之前，你不会收到另一个 `FD_WRITE` 消息。对于 `FD_READ`，当数据首次到达时，你会收到第一个 `FD_READ`。如果你随后执行 `recv()`，并且仍有更多数据等待接收，你将收到另一个 `FD_READ` 事件通知。例如，假设 TCP/IP 层在某个套接字上收到 100 字节数据，并且 WinSock 投递了一个 `FD_READ`
