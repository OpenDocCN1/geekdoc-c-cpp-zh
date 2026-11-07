
最初传递给 `Write()`。如果 `Write()` 返回错误值，数据也可能被释放。目标说明符有几种选项。以下代码展示了调用 `Write()` 的多种方式：

```cpp
int nLen;
LPVOID pData;
char pszHostName[100];
char pszHostIP[100];
int nPort;
char pszServiceName[100];
SOCKADDR_IN sin;
int nStatus;

... allocate data buffer and assign destination specifiers...

nStatus = m_pdg->Write(nLen, pData, pszHostName, nPort);
nStatus = m_pdg->Write(nLen, pData, pszHostIP, nPort);
nStatus = m_pdg->Write(nLen, pData, pszHostName, pszServiceName);
nStatus = m_pdg->Write(nLen, pData, pszHostIP, pszServiceName);
nStatus = m_pdg->Write(nLen, pData, &sin);
```

你还可以选择数据缓冲区的分配方式。你可以分配一个缓冲区并持续重复使用。当写通知消息到达且 `wParam` 设置为 `CWINSOCK_DONE_WRITING` 或 `CWINSOCK_ERROR_WRITING` 时，你就知道可以安全地重用该缓冲区了。另一种选择是每次要发送时都分配一个新缓冲区。在这种情况下，只需在 `CWINSOCK_DONE_WRITING` 或 `CWINSOCK_ERROR_WRITING` 消息到达时释放每个缓冲区即可。

要接收数据，应用程序必须提供一个指向整数的指针，以获取读取的字节数。还可以选择提供一个指向 `SOCKADDR_IN` 结构的指针，以获取数据报发送方的地址。`Read()` 函数返回指向数据的指针，出错时返回 NULL。当消息处理程序被激活且 `wParam` 设置为 `CWINSOCK_DONE_READING` 时，应调用 `Read()`。以下是调用 `Read()` 的两种方式：

```cpp
LPVOID pDataRead;
int nLen;
SOCKADDR_IN sin;

pDataRead = m_pdg->Read(&nLen);
pDataRead = m_pdg->Read(&nLen, &sin);
```

释放 `Read()` 返回的指针是应用程序的责任。

要结束数据报套接字对象的使用，请调用 `DestroySocket()`，如下所示：

```cpp
int nStatus;
nStatus = m_pdg->DestroySocket();
```

## 总结

本章介绍了一个用于操作数据报套接字的类。该对象的目标是支持使用数据报通信快速开发网络应用程序。下一章将介绍一个处理流式套接字通信的类。第 14 章和第 15 章将在完整程序中使用 `cDatagramSocket` 对象。

![](img/5e551abe6e0cb0588043ee757a235ddb_218_0.png)

## 12 CStreamSocket

本章讨论 `CStreamSocket` 类。该类简化了应用程序与流式套接字的交互。该类负责以下工作：创建流式套接字；可选地将套接字绑定到名称；侦听客户端连接请求并接受客户端连接；发送和接收数据；以及销毁套接字。

类声明如下：

```cpp
///////////////////////////////////////////////////////////////
// CStreamSocket
//
class CStreamSocket : public CWnd
{
private:
    CWnd *m_pParentWnd;       // window to receive event notification
    UINT m_uMsg;              // message to send to m_pParentWnd on event
    SOCKET m_s;               // socket handle
    SOCKADDR_IN m_sinLocal;   // name bound to socket m_s
    SOCKADDR_IN m_sinRemote;  // name on other side of m_s
    int m_nLastError;         // last WinSock error
    BOOL m_bServer;           // TRUE if socket m_s is bound to a name
    CPtrList m_listWrite;     // data waiting to be sent
    CPtrList m_listRead;      // data read

public:
    CStreamSocket(CWnd *pParentWnd, UINT uMsg);
    virtual ~CStreamSocket();
    int CreateSocket(int nLocalPort);
    int CreateSocket(LPCTSTR pszLocalService = NULL);
    int DestroySocket();
    int Connect(LPCTSTR pszRemoteName, int nRemotePort);
    int Connect(LPCTSTR pszRemoteName, LPCTSTR pszRemoteService);
    int Connect(LPSOCKADDR_IN psinRemote);
    int Accept(CStreamSocket *pStreamSocket);
    int Write(int nLen, LPVOID pData);
    LPVOID Read(LPINT pnLen);
    int GetPeerName(LPSOCKADDR_IN psinRemote);
    int LastError() { return m_nLastError; }

private:
    void InitVars(BOOL bInitLastError = TRUE);
    LONG HandleRead(WPARAM wParam, LPARAM lParam);
    LONG HandleWrite(WPARAM wParam, LPARAM lParam);

    // message map functions
protected:
    //{{AFX_MSG(CStreamSocket)
    //}}AFX_MSG
    LONG OnWinSockEvent(WPARAM wParam, LPARAM lParam);
    DECLARE_MESSAGE_MAP()
};
```

该类包含几个私有成员变量，这些变量在类实现之外不可访问。特别值得关注的是 `m_listWrite` 和 `m_listRead` 成员变量。这些派生自 `CObject` 的对象维护指向传入和传出数据的指针。这些列表所维护的数据具有以下结构：

```cpp
// structure used for stream socket read/write queue
typedef struct tagSTREAMDATA
{
    LPVOID pData;
    int    nLen;
} STREAMDATA, FAR * LPSTREAMDATA;
```

### CStreamSocket 构造函数

CStreamSocket 对象的构造函数初始化类的成员变量。m_pParentWnd 变量是创建此流式套接字对象的窗口对象。此参数是必需的，因为 CStreamSocket 对象使用 Windows 消息将某些状态信息传回给该对象的用户。类似地，m_uMsg 变量是当流式套接字需要通知应用程序某些信息时，m_pParentWnd 接收到的实际 Windows 消息。该类的构造函数如下所示：

```cpp
///////////////////////////////////////////////////////////////
// CStreamSocket constructor()
//
// Constructs the CStreamSocket object. Initializes member variables
//
CStreamSocket::CStreamSocket(CWnd *pParentWnd, UINT uMsg)
{
    m_pParentWnd = pParentWnd;
    ASSERT(m_pParentWnd != NULL);
    m_uMsg = uMsg;
    ASSERT(m_uMsg != 0);
    InitVars();
}
```

### CStreamSocket::InitVars()

`InitVars()` 成员函数初始化几个私有成员变量。其实现如下所示：

```cpp
///////////////////////////////////////////////////////////////
// CStreamSocket::InitVars()
//
// Initialize class member variables.
//
void CStreamSocket::InitVars(BOOL bInitLastError /* TRUE */)
{
    if (bInitLastError)
        m_nLastError = 0;

    m_s = INVALID_SOCKET;
    memset(&m_sinLocal, 0, sizeof(SOCKADDR_IN));
    memset(&m_sinRemote, 0, sizeof(SOCKADDR_IN));
    m_bServer = FALSE;
}
```

### CStreamSocket::CreateSocket()

CreateSocket() 成员函数创建一个隐藏窗口，用于接收 WinSock 消息（即 FD_READ、FD_WRITE、FD_ACCEPT、FD_CONNECT 和 FD_CLOSE）。该函数还会创建一个流式套接字，并可选地将套接字绑定到名称。CreateSocket() 成员函数有两种实现。一种实现接受一个整数参数，表示应以主机字节序绑定到套接字的端口号。另一种 CreateSocket() 版本接受一个字符串，其中包含要绑定到套接字的数字端口号或服务名称，或者为 NULL。如果指定 NULL，或者调用该函数时完全不提供参数，则套接字不会绑定到名称。此参数仅对服务器类型套接字指定。

接受整数端口号的 CreateSocket() 版本只是将整数转换为字符串，并调用另一个版本的 CreateSocket()。其实现如下所示：

```cpp
////////////////////////////////////////////////////////////
// CStreamSocket::CreateSocket()
//
// Create a hidden window that will receive asynchronous messages
// from WinSock.  Also creates a socket and optionally binds it to
// a name if the socket is a server socket.
//
// This version of the CreateSocket() function takes a
// port number, in host order, as input.  A port number
// should only be specified if the socket is to be bound
// to a certain port.  If you don't care which port is
// assigned to the socket, just call CreateSocket() without
// any parameter, causing CreateSocket(NULL) to be called.

int CStreamSocket::CreateSocket(int nLocalPort)
{
    // if this version of the function is being called,
    // a valid port number must be specified
    if (nLocalPort <= 0)
        return WSAEINVAL;

    // convert the port number into a string and
    // call the version of CreateSocket() which
    // accepts a string
    char pszLocalService[18];
    _itoa(nLocalPort, pszLocalService, 10);
    return CreateSocket(pszLocalService);
}
```
