

### 清单 15.6（续）

```cpp
    HandleRead();
    break;

case CWINSOCK_ERROR_READING:
    break;

case CWINSOCK_YOU_ARE_CONNECTED:
    // print out client information
    nStatus = m_pStream->GetPeerName(&sin);
    if (nStatus == CWINSOCK_ERROR)
    {
        memcpy(&in, &sin.sin_addr.s_addr, 4);
        wsprintf(szMessage, "Connected to client %s, %d",
            inet_ntoa(in), ntohs(sin.sin_port));
        plb->InsertString(0, szMessage);
    }
    else
        plb->InsertString(0, "Error getting client name");
    break;

case CWINSOCK_LOST_CONNECTION:
    // client closed the connection
    m_pStream->DestroySocket();
    delete m_pStream;
    m_pStream = NULL;
    m_pDatagram->DestroySocket();
    delete m_pDatagram;
    m_pDatagram = NULL;
    plb->InsertString(0, "Client closed connection");
    break;

default:
    break;
}

return 0L;
}

///////////////////////////////////////////////////////////////
// CServerView::HandleRead()
//
// Receives data from the connected stream object.
//
void CServerView::HandleRead()
{
    char pszMessage[1000]; // informational message
    LPVOID pDataRead;       // pointer to data read
    int nLen;               // length
    DBCOMMAND dbcmd;        // database command structure

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // read the data
    pDataRead = m_pStream->Read(nLen);
    plb->InsertString(0, "Received command from client");

// verify that the data represented an entire
// database command structure
if (nLen != sizeof(DBCOMMAND))
{
    plb->InsertString(0, "This server cannot handle partial blocks");
    free(pDataRead);
    return;
}

// copy the data to a database command structure
memcpy(&dbcmd, pDataRead, sizeof(DBCOMMAND));
free(pDataRead);

// verify database command
if ((dbcmd.nCommand != DB_READ) && (dbcmd.nCommand != DB_WRITE))
{
    plb->InsertString(0, "Invalid database command");
    return;
}

// perform the database request and format a response
LPDBCOMMAND pdbcmd = (LPDBCOMMAND)malloc(sizeof(DBCOMMAND));
if (pdbcmd == NULL)
{
    plb->InsertString(0, "Cannot allocate memory for response");
    return;
}
memcpy(pdbcmd, &dbcmd, sizeof(DBCOMMAND));
pdbcmd->nCommand = DB_OK;
if (dbcmd.nCommand == DB_READ)
    ::GetPrivateProfileString(dbcmd.szSection, dbcmd.szEntry, "NOT FOUND",
        pdbcmd->szValue, DBBUFSIZE, dbcmd.szFile);
else
    ::WritePrivateProfileString(dbcmd.szSection, dbcmd.szEntry,
        dbcmd.szValue, dbcmd.szFile);

// send the response to the client
if (m_pStream->Write(sizeof(DBCOMMAND), pdbcmd) != CWINSOCK_NOERROR)
{
    wsprintf(szMessage, "Error sending data (ID %d)", pdbcmd->nID);
    plb->InsertString(0, szMessage);
    free(pdbcmd);
}
}

//////////////////////////////////////////////////////////////////////
// CServerView::OnDatagram()
//
// Receives messages from the datagram object.
//
LONG CServerView::OnDatagram(WPARAM wParam, LPARAM lParam)
{
    LPVOID pDataWritten;   // pointer to data that is completely written
    LPVOID pDataRead;      // pointer to data just read
    int nLen;              // length
    char pszMessage[1000]; // informational message

// make sure we are not sending out of a bad datagram socket
if (m_pDatagram == NULL)
    return;

// get pointer to list box used for status messages
CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

// send the buffer unless the previous send hasn't completed yet
if ((*m_pszHeartbeat) == '\0')
{
    lstrcpy(m_pszHeartbeat, HEARTBEAT_STRING);
    // be sure to send terminating NULL character
    if (m_pDatagram->Write(lstrlen(m_pszHeartbeat) + 1, m_pszHeartbeat,
        &m_sinClient) != CWINSOCK_NOERROR)
    {
        (*m_pszHeartbeat) = '\0';
        wsprintf(pszMessage, "Error sending heartbeat");
        plb->InsertString(0, pszMessage);
    }
}

CFormView::OnTimer(nIDEvent);
}
```

图 15.1 和图 15.2 展示了客户端和服务器的运行情况。

**图 15.1。**  
*客户端 INICLNT。*

![](img/5e551abe6e0cb0588043ee757a235ddb_298_0.png)

### 总结

本章演示了 `CWinSock`、`CDatagramSocket` 和 `CStreamSocket` 对象的使用方法。同时还展示了如何借助 WinSock 类库轻松构建一个能够同时处理多个客户端的服务器。

**图 15.2。**  
*服务器 INISRV。*

![](img/5e551abe6e0cb0588043ee757a235ddb_299_0.png)

不过，客户端和服务器程序仍有很大的改进空间。其中一项重要的增强功能可能是处理未在一个连续数据块中到达的数据库命令和响应。目前，客户端和服务器无法处理这种情况。不过幸运的是，要传输的数据块相对较小，因此在负载较轻的网络中几乎不会发生碎片化。要实现这项增强功能，需要修改流套接字对象的 CWINSOCK_DONE_READING 处理程序，将收到的字节缓冲起来，直到接收到一个完整的 DBCOMMAND 结构。

下一章将在异构 UNIX 环境中的 finger 应用程序中使用 WinSock 类库对象。

![](img/5e551abe6e0cb0588043ee757a235ddb_300_0.png)

## 16 异构 UNIX 环境中的 Finger 应用程序

### Finger 客户端设计

Finger 客户端应用程序 FINGER 使用由 CFormView 派生的经典对象作为其主界面。CMainView 对象的头文件如清单 16.1 所示，其实现如清单 16.2 所示（这两个清单将在本节后面给出）。该对象负责完成 FINGER 应用程序的大部分工作。

对象创建后不久就会调用 OnInitialUpdate()。该函数首先强制输出所使用的列表框采用等宽字体。这样可以确保为 ASCII 终端设置格式的任何数据都能正确显示。接下来，该函数启动 WinSock 子系统，然后初始化用于接收用户名的数据输入字段。

当 Finger 客户端的操作员选择标有 Finger 的按钮时，将调用 OnClickedButtonFinger()。首先检查主机名和用户名字段，确保其中包含有效数据。如果用户名有效，则对 Finger 请求字符串进行格式化。如果用户名输入的是通配符星号（*），请求字符串就只包含一个回车符，后跟一个换行符。否则，请求字符串就是用户名后跟回车符和换行符。接下来创建一个流套接字，并异步连接到所选主机的 79 端口。最后，禁用 Finger 按钮，以便通过视觉反馈告知用户程序正处于忙碌状态。

连接成功后，将调用 OnStream()，并将 wParam 设置为 CWINSOCK_YOU_ARE_CONNECTED。作为对此事件的响应，将发送在 OnClickedButtonFinger() 函数中格式化的 Finger 请求。发送 Finger 请求后，将调用 OnStream()，并将 wParam 设置为 CWINSOCK_DONE_WRITING。对此事件的响应是清空用于输出的列表框，使其准备接收 Finger 请求的响应。

数据到达后，将调用 OnStream()，并将 wParam 设置为 CWINSOCK_DONE_READING。CWINSOCK_DONE_READING 处理程序调用 DisplayData()，先缓冲由回车符标识的完整文本行，然后再将该行添加到输出列表框中。之所以需要缓冲，是因为数据可能分成多个片段接收，有些行可能只接收了一部分。

Finger 服务器完成 Finger 请求的响应发送后，会关闭流连接的另一端，从而导致调用 OnStream()，并将 wParam 设置为 CWINSOCK_LOST_CONNECTION。这会使客户端销毁流套接字。Finger 按钮将被重新启用，表示可以再次使用相同或不同的主机/用户名组合。

### 清单 16.1。FINGER 的 MAINVIEW.H。

```cpp
// mainview.h : header file
//
```

