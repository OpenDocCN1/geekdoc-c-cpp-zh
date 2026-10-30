

我们需要实现 IBluetoothOppServerEventListener，以便从远程 OPP 客户端获取文件。当 OPP 服务器收到来自远程客户端的请求时，会调用 OnOppPushRequested 方法。
下面的代码片段展示了 IBluetoothOppServerEventListener。

```
void
BtServer::OnOppPushRequested(const Osp::Net::Bluetooth::BluetoothDevice&
device)
{
    // show the status of receiving a file.
    String title = L"Receiving....";
    ShowTransferProgress(title);

    pBtOppServer->AcceptPush();
}
```

如果想要接受文件，请调用 AcceptPush()；如果想要拒绝文件，请调用 RejectPush()。与接收文件时一样，向用户显示进度并允许取消操作是很有帮助的。

## 方案 5.5：使用非阻塞与阻塞的 TCP 和 UDP 套接字

### 问题描述

你想要使用套接字。

### 方案步骤

本方案需要以下配置：

-   使用的命名空间：Osp::Net::Sockets
-   需要 #include 的头文件：FNet.h
-   所需库：FNet
-   所需特权级别：Normal
-   所需特权组：SOCKET

Net::Sockets 命名空间为 TCP（传输控制协议）或 UDP（用户数据报协议）套接字编程提供了一组类、方法和属性。

Socket 类是在网络上连接、发送和接收数据的基类。默认情况下，Socket 以异步（非阻塞）模式创建和使用。要接收异步套接字事件，你需要注册并维护一个 ISocketEventListener。

本方案演示了：

-   1. 创建服务器套接字。
-   2. 创建客户端套接字。
-   3. 通过套接字进行通信。

让我们逐步完成实现这一目标的代码：

-   1. 实现 ISocketEventListener。

```
#include <FNet.h>

class MyClass:
  public Osp::Net::Sockets::ISocketEventListener
{
Osp::Net::Sockets::Socket* pServerSocket;
Osp::Net::Sockets::Socket* pCommunicatorSocket;
Osp::Net::Sockets::Socket* pClientSocket;
Osp::Base::ByteBuffer* pByteBuffer;

CreateServerSocket(void);
CreateClientSocket(Osp::Base::String serverIP);
SendData();
ReceiveData();
CreateBlockingSocket();

// ISocketEventListener

void OnSocketConnected(Osp::Net::Sockets::Socket& socket);
void OnSocketClosed(Osp::Net::Sockets::Socket& socket,
    Osp::Net::Sockets::NetSocketClosedReason reason);
void OnSocketReadyToReceive(Osp::Net::Sockets::Socket& socket);
void OnSocketReadyToSend(Osp::Net::Sockets::Socket& socket);
void OnSocketAccept(Osp::Net::Sockets::Socket& socket);
};
```

-   2. 创建服务器套接字。服务器绑定到一个网络端点——即 IP 地址和端口号。当客户端连接到服务器时，响应由 OnSocketAccept() 事件处理程序接收。创建服务器套接字的代码包括以下步骤：
    -   a. 创建套接字实例。
    -   b. 在 TCP 套接字的构造方法中，提供 NET_SOCKET_TYPE_STREAM 作为网络套接字类型，提供 NET_SOCKET_PROTOCOL_TCP 作为网络套接字协议。
    -   c. 如果你想使用 UDP 套接字，则在构造方法中提供 NET_SOCKET_TYPE_DATAGRAM 作为网络套接字类型，提供 NET_SOCKET_PROTOCOL_UDP 作为网络套接字协议。
    -   d. 要创建非阻塞套接字，请通过调用 AddSocketListener 向 ISocketEventListener 注册。
    -   e. 通过调用 AsyncSelectByListener 将套接字设置为异步模式。监听器接收的事件包括：Write、Read、Close、Accept、Connect，以及 SecureSocket 的 Certificate failed 事件。
    -   f. 将此套接字绑定到网络端点，指定服务器将要监听的端口。
    -   g. 调用 Listen() 函数以监听连接。

```
void
MyClass::CreateServerSocket(void)
{
    result r = E_SUCCESS;

    //Create socket instance
    pServerSocket = new Socket();
    r = pServerSocket->Construct (
        NET_SOCKET_AF_IPV4, NET_SOCKET_TYPE_STREAM,
        NET_SOCKET_PROTOCOL_TCP);

    if (E_SUCCESS!= r)
    {
        AppLog("Construct Failed %d ", r);
    }

    //Register with ISocketListener
    pServerSocket->AddSocketListener(*this);

    //Sets the socket in asynchronous mode, also listener will listen
    //to the specified events as passed in the argument
    r = pServerSocket->AsyncSelectByListener
        (NET_SOCKET_EVENT_ACCEPT|NET_SOCKET_EVENT_CLOSE );

    if (E_SUCCESS!= r)
    {
        AppLog("AsyncSelectByListener Failed %d",r);
    }

    //NetEndPoint holds the IP address and Port number
    Ip4Address peerAddr(NET_SOCKET_INADDR_ANY);
    unsigned short peerPort = 9000;
    NetEndPoint peerEndPoint(peerAddr, peerPort);

    //The socket will bind to a port, on which it will listen for
    //connection
    r = pServerSocket->Bind(peerEndPoint);
    if (E_SUCCESS!= r)
    {
        AppLog("CreateServerSocket Bind Failed %d",r);
    }

    //The socket will listen to the incoming connections, the maximum
    //number of incoming connections that can be queued for acceptance
    //can be specified as argument to this function
    r = pServerSocket->Listen(1);

    if (E_SUCCESS!= r)
    {
        AppLog("CreateServerSocket Listen Failed %d",r);
    }
}
```

-   3. 按如下方式创建客户端套接字：
    -   a. 创建套接字实例。
    -   b. 与客户端套接字一样，在 TCP 套接字的构造方法中，提供 NET_SOCKET_TYPE_STREAM 作为网络套接字类型，提供 NET_SOCKET_PROTOCOL_TCP 作为网络套接字协议。
    -   c. 要创建非阻塞套接字，请通过调用 AddSocketListener 向 ISocketEventListener 注册。
    -   d. 通过调用 AsyncSelectByListener 将套接字设置为异步模式。
    -   e. 调用 Connect 函数，并指定该客户端要连接的服务器的 NetEndPoint。

```
void
MyClass::CreateClientSocket(String serverIP)
{
    result r = E_SUCCESS;

    //Create socket instance
    pClientSocket = new Socket;
    pClientSocket->Construct(NET_SOCKET_AF_IPV4, NET_SOCKET_TYPE_STREAM, NET_SOCKET_PROTOCOL_TCP);

    //Register with ISocketListener
    pClientSocket->AddSocketListener(*this);

    //Sets the socket in asynchronous mode, also listener will listen
    //to the specified events as passed in the argument
    pClientSocket->AsyncSelectByListener(
        NET_SOCKET_EVENT_CONNECT | NET_SOCKET_EVENT_WRITE
        | NET_SOCKET_EVENT_READ | NET_SOCKET_EVENT_CLOSE);

    //NetEndPoint holds the IP address and Port number, here IP Address
    //and port is that of server to which the client wishes to connect
    Ip4Address peerAddr(serverIP);      // For Testing
    unsigned short peerPort = 9000;     // port
    NetEndPoint peerEndPoint(peerAddr, peerPort);

    //Establishes a connection to a remote host for a connection-oriented
    //socket
    r = pClientSocket->Connect(peerEndPoint);
}
```

-   4. 套接字在 OnSocketAccept() 中收到来自对端的新连接通知。调用 AcceptN 函数，该函数将返回一个可用于发送和接收数据的套接字实例。你需要将此套接字注册到监听器，并按上述方式将其设置为异步模式。

```
void
MyClass::OnSocketAccept(Osp::Net::Sockets::Socket& socket)
{
    AppLog("OnSocketAccept");
    Socket* pSocket = const_cast<Socket*>(&socket);

    if (null != pCommunicatorSocket)
    {
        delete pCommunicatorSocket;
        pCommunicatorSocket = null;
    }

    pCommunicatorSocket = pSocket->AcceptN();

    pCommunicatorSocket->AddSocketListener(*this);

    pCommunicatorSocket->AsyncSelectByListener(
        NET_SOCKET_EVENT_CONNECT | NET_SOCKET_EVENT_WRITE
        | NET_SOCKET_EVENT_READ | NET_SOCKET_EVENT_CLOSE);
}
```

-   5. 现在你可以通过套接字发送和接收数据。调用 Send() 方法将 pByteBuffer 中的数据发送到远程主机。

```
void
MyClass::SendData()
{
    r = pCommunicatorSocket->Send(this->pByteBuffer);
    // pByteBuffer contains the data to be sent
}
```

-   6. 要接收数据，我们首先调用 Ioctl() 方法检查有多少字节可读，然后利用此信息构造缓冲区，再使用 Receive() 方法将数据读入其中。

```
void
MyClass::ReceiveData()
{
    ByteBuffer rxBuffer;
    unsigned long arg =0;
    if (null != pCommunicatorSocket)
    {
        pCommunicatorSocket->Ioctl(NET_SOCKET_FIONREAD, arg);
        rxBuffer.Construct(arg);
        r = pCommunicatorSocket->Receive(rxBuffer);
    }
}
```

-   7. ISocketEventListener 是你处理套接字相关事件的地方：

//Notifies a connecting socket that the connection attempt has been completed
//successfully

void
MyClass::OnSocketConnected(Osp::Net::Sockets::Socket& socket)
{
    AppLog("OnSocketConnected");
}

//Notifies the registered socket that the peer socket has been closed
//or if the connection attempt has not been completed successfully

void
MyClass::OnSocketClosed(Osp::Net::Sockets::Socket& socket,
    Osp::Net::Sockets::NetSocketClosedReason reason)
{
    // Do necessary cleanup if required
}

//Notifies a socket that data is ready to be retrieved
void

