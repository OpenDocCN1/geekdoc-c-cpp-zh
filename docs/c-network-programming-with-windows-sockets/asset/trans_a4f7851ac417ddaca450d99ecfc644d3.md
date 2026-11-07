

作为服务器，它必须绑定到特定的端口或服务名。为此，可以通过以下方式之一调用该函数：

```c
int nPort;
char pszServiceName[100];
int nStatus;
```

```c
...assign port or service name...
```

```c
nStatus = m_ps->CreateSocket(nPort);
nStatus = m_ps->CreateSocket(pszServiceName);
```

如果这个套接字不是服务器，只需调用 `CreateSocket()`，如下所示：

```c
nStatus = m_ps->CreateSocket();
```

客户端必须先连接到服务器，然后才能发送或接收数据。连接是通过指定主机说明符来建立的。调用 `Connect()` 有以下五种方式：

```c
char pszHostName[100];
char pszHostIP[100];
int nPort;
char pszServiceName[100];
SOCKADDR_IN sin;
int nStatus;
```

```c
... assign destination specifiers ...
```

```c
nStatus = m_ps->Connect(pszHostName, nPort);
nStatus = m_ps->Connect(pszHostIP, nPort);
nStatus = m_ps->Connect(pszHostName, pszServiceName);
nStatus = m_ps->Connect(pszHostIP, pszServiceName);
nStatus = m_ps->Connect(&sin);
```

服务器必须先接受来自客户端的连接，然后才能进行数据传输。接受连接时，会使用一个新的 `CStreamSocket` 对象。`Accept()` 成员函数是响应来自服务器流套接字的 `CWINSOCK_READY_TO_ACCEPT_CONNECTION` 消息而调用的：

```c
CStreamSocket *psClient; // will communicate with the client
int nStatus;
```

```c
psClient = new CStreamSocket(this, WM_USER + 2);
```

```c
// m_ps is the server socket
nStatus = m_ps->Accept(psClient);
```

如果服务器希望知道已接受连接另一侧的客户端的 Internet 地址，可以使用 `GetPeerName()`。该函数从传给 `Accept()` 调用的套接字中调用，如下所示：

```c
SOCKADDR_IN sin; // address of client on other side of socket
int nStatus;
```

```c
nStatus = psClient->GetPeerName(&sin);
```

要发送数据，应用程序必须提供要发送的字节数以及指向数据的指针。在之前讨论的消息处理程序收到 `wParam` 被设置为 `CWINSOCK_DONE_WRITING` 或 `CWINSOCK_ERROR_WRITING` 的消息之前，数据必须保持已分配状态。在这种情况下，`lParam` 就是最初传给 `Write()` 的指针。如果 `Write()` 返回错误值，也可以释放该数据。以下代码展示了如何调用 `Write()`：

```c
int nLen;
LPVOID pData;
int nStatus;

... allocate data buffer ...

nStatus = m_ps->Write(nLen, pData);
```

数据缓冲区的分配方式有多种选择。你可以分配一个缓冲区并不断复用它。当写通知消息到达且 `wParam` 被设置为 `CWINSOCK_DONE_WRITING` 或 `CWINSOCK_ERROR_WRITING` 时，你就知道可以安全地复用该缓冲区。另一种选择是，每次要发送数据时都分配一个新缓冲区。在这种情况下，只需在 `CWINSOCK_DONE_WRITING` 或 `CWINSOCK_ERROR_WRITING` 消息到达时释放每个缓冲区。

要接收数据，应用程序必须提供一个指向整数的指针，以获取已读取的字节数。`Read()` 函数返回指向数据的指针，出错时返回 `NULL`。当消息处理程序被激活且 `wParam` 被设置为 `CWINSOCK_DONE_READING` 时，应调用 `Read()`。以下是调用 `Read()` 的两种方式：

```c
LPVOID pDataRead;
int nLen;

pDataRead = m_ps->Read(&nLen);
```

应用程序负责释放 `Read()` 返回的指针。

要结束流套接字对象的使用，请调用 `DestroySocket()`，如下所示：

```c
int nStatus;
nStatus = m_ps->DestroySocket();
```

## 小结

本章介绍了一个用于操作流套接字的类。该对象的目标是能够使用流通信快速开发网络应用程序。下一章将收尾这个类库。第 14 章到第 16 章将在功能完整的程序中使用 `CStreamSocket` 对象。

## 13 整合所有内容

本章讨论 WinSock 类库的最后几部分，包括一个用于显示 WinSock 错误消息的函数。

### CWinSockErrorBox()

到目前为止缺少的一项功能是：显示带有实际 WinSock 错误文本描述的错误消息的函数。`CWinSockErrorBox()` 函数正是做这件事的。

`CWinSockErrorBox()` 的第一个参数是一个整数，表示由 `WSAGetLastError()` 返回的 WinSock 错误。第二个参数是一个可选指针，指向包含你希望呈现给用户的附加信息的字符串。

该函数的原型如下：

```c
void CWinSockErrorBox(int nError, LPSTR pszMessage = NULL);
```

`CWinSockErrorBox()` 函数的实现如下：

```c
///////////////////////////////////////////////////////////////////////
// CWinSockErrorBox
//
void CWinSockErrorBox(int nError, LPSTR pszMessage/*= NULL*/)
{
#define ERROR_BUF_LEN (1000)
  char pszError[ERROR_BUF_LEN];

  wsprintf(pszError, "WinSock error %d: ", nError);

  switch (nError)
  {
    case WSAEINTR:
      lstrcat(pszError, "Interrupted system call");
      break;
    case WSAEBADF:
      lstrcat(pszError, "Bad file number");
      break;
    case WSAEACCES:
      lstrcat(pszError, "Permission denied");
      break;
    case WSAEFAULT:
      lstrcat(pszError, "Bad address");
      break;
    case WSAEINVAL:
      lstrcat(pszError, "Invalid argument");
      break;
    case WSAEMFILE:
      lstrcat(pszError, "Too many open files");
      break;
    case WSAEWOULDBLOCK:
      lstrcat(pszError, "Operation would block");
      break;
    case WSAEINPROGRESS:
      lstrcat(pszError, "Operation now in progress");
      break;
    case WSAEALREADY:
      lstrcat(pszError, "Operation already in progress");
      break;
    case WSAENOTSOCK:
      lstrcat(pszError, "Socket operation on non-socket");
      break;
    case WSAEDESTADDRREQ:
      lstrcat(pszError, "Destination address required");
      break;
    case WSAEMSGSIZE:
      lstrcat(pszError, "Message too long");
      break;
    case WSAEPROTOTYPE:
      lstrcat(pszError, "Protocol wrong type for socket");
      break;
    case WSAENOPROTOOPT:
      lstrcat(pszError, "Protocol not available");
      break;
    case WSAEPROTONOSUPPORT:
      lstrcat(pszError, "Protocol not supported");
      break;
    case WSAESOCKTNOSUPPORT:
      lstrcat(pszError, "Socket type not supported");
      break;
    case WSAEOPNOTSUPP:
      lstrcat(pszError, "Operation not supported on socket");
      break;
    case WSAEPFNOSUPPORT:
      lstrcat(pszError, "Protocol family not supported");
      break;
    case WSAEAFNOSUPPORT:
      lstrcat(pszError, "Address family not supported by protocol family");
      break;
    case WSAEADDRINUSE:
      lstrcat(pszError, "Address already in use");
      break;
    case WSAEADDRNOTAVAIL:
      lstrcat(pszError, "Can't assign requested address");
      break;
    case WSAENETDOWN:
      lstrcat(pszError, "Network is down");
      break;
    case WSAENETUNREACH:
      lstrcat(pszError, "Network is unreachable");
      break;
    case WSAENETRESET:
      lstrcat(pszError, "Network dropped connection on reset");
      break;
    case WSAECONNABORTED:
      lstrcat(pszError, "Software caused connection abort");
      break;
    case WSAECONNRESET:
      lstrcat(pszError, "Connection reset by peer");
      break;
    case WSAENOBUFS:
      lstrcat(pszError, "No buffer space available");
      break;
    case WSAISCONN:
      lstrcat(pszError, "Socket is already connected");
      break;
    case WSAENOTCONN:
      lstrcat(pszError, "Socket is not connected");
      break;
    case WSAESHUTDOWN:
      lstrcat(pszError, "Can't send after socket shutdown");
      break;
    case WSAETOOMANYREFS:
      lstrcat(pszError, "Too many references: can't splice");
      break;
    case WSAETIMEDOUT:
      lstrcat(pszError, "Connection timed out");
      break;
    case WSAECONNREFUSED:
      lstrcat(pszError, "Connection refused");
      break;
    case WSAELOOP:
      lstrcat(pszError, "Too many levels of symbolic links");
      break;
    case WSAENAMETOOLONG:
      lstrcat(pszError, "File name too long");
      break;
    case WSAEHOSTDOWN:
      lstrcat(pszError, "Host is down");
      break;
    case WSAEHOSTUNREACH:
      lstrcat(pszError, "No route to host");
      break;
    case WSAENOTEMPTY:
      lstrcat(pszError, "Directory not empty");
      break;
    case WSAEPROCLIM:
      lstrcat(pszError, "Too many processes");
      break;
    case WSAEUSERS:
      lstrcat(pszError, "Too many users");
      break;
    case WSAEDQUOT:
      lstrcat(pszError, "Disc quota exceeded");
      break;
    case WSAESTALE:
      lstrcat(pszError, "Stale NFS file handle");
      break;
    case WSAEREMOTE:
      lstrcat(pszError, "Too many levels of remote in path");
      break;
    case WSAEDISCON:
      lstrcat(pszError, "Disconnect");
      break;
    case WSASYSNOTREADY:
      lstrcat(pszError, "Network sub-system is unusable");
      break;
    case WSAVERNOTSUPPORTED:
      lstrcat(pszError, "WinSock DLL cannot support this application");
```

