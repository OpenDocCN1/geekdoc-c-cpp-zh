
## 代码清单 8.21. 续

```cpp
else
{
    // try to make the connection
    // if it doesn't succeed it may still be ok as long
    // as the error was that the connection would block
    if (connect(m_s, (LPSOCKADDR)&m_addr, sizeof(m_addr)) == SOCKET_ERROR)
    {
        int nError = WSAGetLastError();
        if (nError != WSAEWOULDBLOCK)
            plb->InsertString(0, "Stream echo client could not connect");
        SetTimer(1, 5000, NULL);
    }
}

///////////////////////////////////////////////////////////////
// CMainView::OnAsyncSelect()
//
LONG CMainView::OnAsyncSelect(WPARAM wParam, LPARAM lParam)
{
    char pszMessage[100];        // informational message
    static char pBuf[101];       // send/recv buffer
    int nBytesRecv;              // number of bytes received
    int nBytesSent;              // number of bytes sent
    int nError;                  // WinSock error

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // check for an error
    if (WSAGETSELECTERROR(lParam) != 0)
    {
        wsprintf(pszMessage, "Datagram echo client async select got error %d",
                 WSAGETSELECTERROR(lParam));
        plb->InsertString(0, pszMessage);
        return 0L;
    }

    // what event are we being notified of?
    switch (WSAGETSELECTEVENT(lParam))
    {
        case FD_CONNECT:
            // the connection has been completed

            plb->InsertString(0, "Stream echo client connected");

            if (WSAAsyncSelect(m_s, m_hWnd, WM_USER_ASYNC_SELECT,
                FD_READ | FD_WRITE | FD_CLOSE) == SOCKET_ERROR)
                plb->InsertString(0, "Stream echo client could not do async select");
            break;

        case FD_CLOSE:
            // close the socket

            closesocket(m_s);
            m_s = INVALID_SOCKET;
            plb->InsertString(0, "Server closed connection");
            break;

        case FD_WRITE:
            plb->InsertString(0, "FD_WRITE");

            // is there any data to send?
            if (m_nBytesToSend != 0)
            {
                // send the data
                nBytesSent = send(m_s, &m_pBuf[m_nTotalBytesToSend - m_nBytesToSend],
                    m_nBytesToSend, 0);

                // check for send error
                if (nBytesSent == SOCKET_ERROR)
                {
                    // if the error is just that the send would block,
                    // I don't do anything...we'll get another FD_WRITE soon
                    nError = WSAGetLastError();
                    if (nError != WSAEWOULDBLOCK)
                    {
                        wsprintf(pszMessage, "Error %d sending data to %s, %d",
                            nError, inet_ntoa(m_in), ntohs(m_addr.sin_port));
                        plb->InsertString(0, pszMessage);

                        m_nBytesToSend = m_nTotalBytesToSend = 0;
                    }
                }
                else
                {
                    wsprintf(pszMessage, "Data sent (%s) to %s, %d",
                        m_pBuf, inet_ntoa(m_in), ntohs(m_addr.sin_port));
                    plb->InsertString(0, pszMessage);

                    m_nBytesToSend = m_nBytesToSend - nBytesSent;
                    if (m_nBytesToSend == 0)
                        m_nTotalBytesToSend = 0;
                    else
                        // there are more bytes to send so we'll trigger
                        // the FD_WRITE event again
                        PostMessage(WM_USER_ASYNC_SELECT, m_s,
                            WSAMAKESELECTREPLY(FD_WRITE, 0));
                }
            }
            break;

        case FD_READ:
            plb->InsertString(0, "FD_READ");

            // receive data
            nBytesRecv = recv(m_s, pBuf, 100, 0);

            // check for receive error
            if (nBytesRecv == SOCKET_ERROR)
            {
```

### 2.2.1 单线图

单线图（SLD）是电力系统或其一部分的简化图形表示。它使用单线和标准符号来表示三相（有时为单相）电力系统。单线图是电力工程中最常用的电气图类型。

下图展示了一个简单电力系统的典型单线图。它包括发电机、变压器、母线、断路器以及通过输电线路连接的负载。

![](img/5e551abe6e0cb0588043ee757a235ddb_186_0.png)

在单线图中，每个设备都用标准符号表示。例如，发电机用带十字的圆圈表示，变压器用两个圆圈或一对绕组表示，断路器用开关符号表示。各组件通过一条单线连接，这条单线代表系统的所有三相。

单线图广泛用于电力系统研究，例如潮流分析、短路分析和保护配合。它们提供了一种清晰简洁的方式来理解电力系统的整体结构和运行方式。

- **组件：** 发电机、变压器、母线、断路器、负载
- **连接：** 输电线路、电缆
- **符号：** 每个组件的标准化图形符号

连接成功。SECLIENT 的 `CMainView::OnAsyncSelect()` 会因 `FD_CONNECT` 事件被调用。
SESERV 的 `CMainView::OnAsyncSelect()` 会因 `FD_ACCEPT` 事件被调用；如果 `m_sClient` 套接字尚未连接，则会建立连接。

五秒后，SECLIENT 中的定时器会触发，导致 `CMainView::OnTimer()` 被调用。此时还没有待发送的字节，因此会填充发送缓冲区，并伪造一个 WinSock `FD_WRITE` 消息来触发数据发送。必须这样做，因为真正的 `FD_WRITE` 可能已被错过，或者它可能在还没有任何数据可发送时就已经发生。

SECLIENT 中的 `CMainView::OnAsyncSelect()` 会因 `FD_WRITE` 事件被调用。此时有字节要发送，因此会尝试将它们传输到流式回显服务器。如果尝试成功，则待发送的字节数会减少。如果发送时出错，但错误仅仅是发送操作会阻塞，则待发送字节数会保留，因为最终会收到真正的 `FD_WRITE`。如果无法在一次 `send()` 调用中传输所有待发送字节（鉴于示例中的数据大小，这种情况不太可能），则会继续生成 `FD_WRITE` 事件，并减少字节计数，直到最终变为 0（零）。

假设 SECLIENT 发送了一个缓冲区，SESERV 中的 `CMainView::OnAsyncSelect()` 会因 `FD_READ` 通知被调用。SESERV 只有一个用于接收和发送数据的缓冲区，因此如果还有任何字节需要回显给客户端，就会忽略 `FD_READ`。如果数据读取成功，则会记录字节计数，并生成一个伪造的 `FD_WRITE` 消息，以强制将刚接收到的数据发送回发起方（SECLIENT）。

SESERV 中的 `CMainView::OnAsyncSelect()` 会因 `FD_WRITE` 事件被调用。此时有字节要发送，因此会尝试将它们传输到流式回显客户端。如果尝试成功且写入了字节，则待发送字节数会按成功写入的字节数减少。如果发送时出错，但错误仅仅是发送操作会阻塞，则待发送字节数会保留，因为最终会收到真正的 `FD_WRITE`。在整个缓冲区被回显之前，可能会生成多个 `FD_WRITE` 事件（不过鉴于本例中的缓冲区很小，这种情况极不可能发生）。

假设 SESERV 发送了一个缓冲区，SECLIENT 中的 `CMainView::OnAsyncSelect()` 会因 `FD_READ` 通知被调用，客户端会读取回显的数据。SECLIENT 中的另一个定时器会触发，然后重复该过程。

图 8.10 显示了在同一台计算机上运行的 SESERV 和 SECLIENT，该计算机的 IP 地址为 166.78.16.150。服务器和客户端分别被分配了端口 1067 和 1068。请注意，与基于数据报的示例相比，这里多了与连接有关的状态消息。

**图 8.10.**  
*SESERV 和*  
*SECLIENT 运行*  
*在同一台计算机上。*

![](img/5e551abe6e0cb0588043ee757a235ddb_188_0.png)

## 小结

本章演示了在完整应用程序中使用许多重要 WinSock 函数的方法。演示的函数包括初始化 WinSock、提供有关计算机上 WinSock TCP/IP 协议栈的详细信息、执行数据库查询，以及通过流式套接字和数据报套接字传输数据。

可以对这里说明的程序进行若干增强，使其更加健壮。你可能想自行探索的一项修改是：让 DECLIENT 和 SECLIENT 应用程序能够输入主机名，而不仅仅是 IP 地址。可以为此尝试使用 WSAAsyncGetHostByName()，但不要忘记先调用 `inet_addr()`，以防用户确实输入了 IP 地址。

第 9 章至第 13 章介绍若干 C++ 类，这些类封装了 WinSock 功能，使编写网络应用程序变得更加容易。

