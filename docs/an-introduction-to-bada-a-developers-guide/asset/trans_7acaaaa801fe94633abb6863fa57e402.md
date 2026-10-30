

2. CreateSecureSocket 方法执行以下操作：

+   a. 创建安全套接字。
+   b. 添加套接字侦听器，以侦听套接字事件。
+   c. 初始化安全套接字服务器的端口和 IP。
+   d. 创建对等端点。
+   e. 连接服务器套接字。

```
void
SocketsSecureExample::CreateSecureSocket(void)
{
    result r = E_SUCCESS;

    // Create a Secure(based on TCP) socket
    pSocket = new SecureSocket();
    pSocket->Construct(NET_SOCKET_AF_IPV4, NET_SOCKET_TYPE_STREAM,
        NET_SOCKET_PROTOCOL_SSL);

    // Add a Socket Listener to listen to socket event
    pSocket->AddSecureSocketListener(*this);

    // Set the socket as select an interested event.
    pSocket->AsyncSelectByListener(
        NET_SOCKET_EVENT_CONNECT|NET_SOCKET_EVENT_WRITE
        |NET_SOCKET_EVENT_READ|NET_SOCKET_EVENT_CLOSE);

    // Connect to a Secure Server
    IpAddress peerAddr("127.0.0.1");
    // server socket address
    unsigned short peerPort = 8080;
    // port
    NetEndPoint peerEndPoint(peerAddr, peerPort);

    pSocket->Connect(peerEndPoint);
}
```

3. 在 SecureSendDataMethod 中发送数据。

```
void
SocketsSecureExample::SecureSendData(void)
{
    result r = E_SUCCESS;

    const char* pSendData = "Send";
    ByteBuffer txBuffer;
    txBuffer.Construct(strlen(pSendData) + 1);
    txBuffer.SetArray((byte*)pSendData, 0, strlen(pSendData));
```

```
txBuffer.Flip();

r = pSocket->Send(txBuffer);

if (r == E_SUCCESS)
{
    // Release resource
    txBuffer.Clear();
}
```

+   4. 接收安全数据：
+       a. 准备一个用于接收数据的缓冲区。
+       b. 获取待接收数据的大小。
+       c. 接收数据。
+       d. 从 OnSecureSocketReadyToReceive 方法中调用下方所示的 SecureReceiveData 函数来接收数据。

```
void
SocketsSecureExample::SecureReceiveData(void)
{
    result r = E_SUCCESS;

    ByteBuffer rxBuffer;
    int capacity = MAX_BUFFER_SIZE;
    char data[MAX_BUFFER_SIZE];

    rxBuffer.Construct(capacity);

    // Receive data
    r = pSocket->Receive(rxBuffer);

    if(r == E_SUCCESS)
    {
        // Release resource
        rxBuffer.Flip();
        rxBuffer.GetArray((byte*)data, 0, capacity);
        data[capacity]='\0';
        AppLog(data);
        rxBuffer.Clear();
    }
}
```

5. 使用 Close() 方法关闭安全套接字服务。

```
void
SocketsSecureExample::CloseSecureSocket(void)
{
```

```
result r = E_SUCCESS;

// Close socket
r = pSocket->Close();

if(r == E_SUCCESS)
{
    //Release resource
    delete pSocket;
    pSocket = null;
}
```

## 提示、注意事项及相关主题

SecureSocket 实例只能在异步（非阻塞）模式下创建和使用，并且只能用于 TCP 客户端套接字功能。bada 的安全套接字功能支持 CipherSuite 机制，该机制由特定的证书类型、密码算法、MAC、密钥交换算法和压缩方法组合而成。

## 配方 5.3：为 HTTP 会话建立普通和流水线连接模式

### 问题描述

你想要建立 HTTP 普通连接模式和流水线连接模式。

### 配方

此配方需要以下配置：

| 使用的命名空间： | Osp::Base、Osp::Net::Http、Osp::Net |
| 要包含的头文件： | FBase.h、FNet.h |
| 所需库： | FNet |
| 所需权限级别： | 普通 |
| 所需权限组： | NET |

HTTP 客户端架构为运行在各种传输方式之上的类 HTTP 协议提供了一种通用机制。使用此命名空间，客户端可以选择 HTTP 协议、对数据进行编码，然后传输数据。默认操作是在 TCP/IP 连接上运行纯文本 HTTP。

Net::Http 提供 HTTP 数据通信协议的实现。正确使用此命名空间，可使应用程序成为符合 HTTP 1.1 标准的客户端。

HTTP 会话封装了客户端在其运行期间的 HTTP 活动。它由一组使用相同连接设置（例如代理或主机）的事务组成。HTTP 会话有两种模式（见图 R5.3）：

+   - 普通模式；
+   - 流水线模式。

在普通模式下，会话中的所有事务共享同一个连接。一个会话只有一个连接，并且一次只处理一个事务。

流水线模式与普通模式类似，同样共享连接，但可以并发提交多个请求，而无需等待每个请求的响应。

![](img/a257d5fd53a79a244a20e587cd2f08f6_407_0.png)

本配方介绍创建 HTTP 连接的步骤，如下所示：

+   1. 从 IHttpTransactionEventListener 派生一个类。
+   2. 创建 HttpSession，打开一个事务并发送请求。
+   3. 在 OnTransactionReadyToRead 中响应请求。

现在来看代码。

### 1. 从 IHttpTransactionEventListener 派生，以便在应用程序中接收 HTTP 事务事件。

```
class MyHttpClass :
    public Osp::Net::Http::IHttpTransactionEventListener
{
public:
    MyHttpClass();
    virtual ~MyHttpClass();

    void SendRequestGet(Osp::Base::String requestUrl);

private:
    void OnTransactionReadyToRead(Osp::Net::Http::HttpSession& httpSession,
        Osp::Net::Http::HttpTransaction& httpTransaction,
        int availableBodyLen);

    void OnTransactionAborted(Osp::Net::Http::HttpSession& httpSession,
        Osp::Net::Http::HttpTransaction& httpTransaction, result r);

    void OnTransactionReadyToWrite(Osp::Net::Http::HttpSession& httpSession,
        Osp::Net::Http::HttpTransaction& httpTransaction,
        int recommendedChunkSize);

    void OnTransactionHeaderCompleted(Osp::Net::Http::HttpSession&
        httpSession,
        Osp::Net::Http::HttpTransaction& httpTransaction,
        int headerLen, bool rs);

    void OnTransactionCompleted(Osp::Net::Http::HttpSession& httpSession,
        Osp::Net::Http::HttpTransaction& httpTransaction);

    void OnTransactionCertVerificationRequired(Osp::Net::Http::HttpSession&
        httpSession, Osp::Net::Http::HttpTransaction&
        httpTransaction,
        String* pCert);

private:
    Osp::Net::Http::HttpSession* pSession;
};
```

在此类中，我们创建了一个指向 HttpSession 的指针。会话封装了客户端在其运行期间的 HTTP 活动。

+   2. 发起 HTTP 请求：
+      a. 创建一个 `HttpSession` 实例。
+      b. 构造一个 `HttpSession` 实例，并指定普通模式或流水线模式。
+      c. 为 `HttpSession` 打开事务。
+      d. 添加一个 `HttpTransactionListener`。
+      e. 调用 `GetRequest` 获取 `HTTPRequest` 指针。使用该指针设置实际 URI、方法、请求头等。
+      f. 提交 HTTP 请求。

```
void
MyHttpClass::SendRequestGet(Osp::Base::String requestUrl)
{
    result r = E_SUCCESS;
    HttpTransaction* pTransaction = null;
    HttpRequest* pRequest = null;

    String hostAddr(requestUrl);

    if (null != pSession)
    {
        delete pSession;
        pSession = null;
    }

    pSession = new HttpSession();
    r = pSession->Construct(NET_HTTP_SESSION_MODE_NORMAL, null,
            hostAddr, null);

    if (IsFailed(r))
    {
        AppLog("Fail to HttpSession::Construct. [%s]",
                GetErrorMessage(r));
        return;
    }

    pTransaction = pSession->OpenTransactionN();

    if (pTransaction)
    {
        pTransaction->AddHttpTransactionListener(*this);
        pRequest = pTransaction->GetRequest();

        if (pRequest)
```

在 NORMAL 和 PIPELINING 会话模式下，此会话中的所有事务都通过同一个连接提交。普通模式下，一次只处理一个事务；流水线模式下则可以对多个事务进行流水线处理。在普通模式下，必须等待前一个事务结束后才能提交下一个事务。每个应用程序最多可以构造六个 HttpSession。

## 配方 5.4：使用蓝牙配置文件

### 问题描述

根据连接类型或需求使用不同的蓝牙配置文件。

### 配方

此配方需要以下配置：

**使用的命名空间：**  
Osp::UI、Osp::Base、Osp::Net

**要包含的头文件：**  
FUI.h、FBase.h、FNet.h

**所需库：**  
FUI、FBase、FNet

**所需权限级别：**  
普通

**所需权限组：**  
BLUETOOTH

蓝牙可以快速、轻松地连接其他设备，并支持多种使用场景，包括一次性文件传输，以及无线连接耳机、键盘等外围设备。标准使用场景通过蓝牙配置文件进行定义。

bada 支持的蓝牙配置文件包括：

+   - 通用访问配置文件（GAP）
+   - 对象推送配置文件（OPP）

GAP 是最基础的蓝牙配置文件，也是所有其他配置文件的基础。包括 OPP 在内的所有其他配置文件都构建于 GAP 之上。GAP 的目的是确保所有设备都能成功建立基带链路。

