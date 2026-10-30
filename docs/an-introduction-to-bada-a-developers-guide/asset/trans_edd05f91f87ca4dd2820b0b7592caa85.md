

MyClass::OnSocketReadyToReceive(Osp::Net::Sockets::Socket& socket)
{
    ReceiveData();
}

// Notifies a socket that it can send data
void
MyClass::OnSocketReadyToSend(Osp::Net::Sockets::Socket& socket)
{
    SendData();
}
```

## Hints, Pitfalls, and Related Topics

bada 也支持阻塞模式。要使用阻塞套接字，请不要实现 `ISocketEventListener`，并且不要将套接字设置为异步模式。使用 `NET_SOCKET_FIONBIO` 和 `0` 作为参数调用 `Ioctl` 函数。

```
void
MyClass::CreateBlockingSocket()
{
    pClientSocket = new Socket();
    pClientSocket->Construct(NET_SOCKET_AF_IPV4,
        NET_SOCKET_TYPE_DATAGRAM, NET_SOCKET_PROTOCOL_UDP);

    // Enable synchronous (blocking) mode
    unsigned long arg = 0;
    pClientSocket->Ioctl(NET_SOCKET_FIONBIO, arg);
}
```

使用阻塞模式的应用在事务处理期间可能会冻结或变得无响应，因此最好使用非阻塞模式。

## Recipe 5.6: Set Up an Ad Hoc Wi-Fi Network

## Problem Description

你需要建立一个 ad hoc Wi-Fi 网络，例如用于多人游戏。

## The Recipe

本配方需要以下配置：

Namespaces used:

Osp::Base, Osp::Net, Osp::Wifi, Osp::Base::Collection

Header files to `#include`:

FBase.h, FUi.h, FNet.h

Required libraries:

FBase, FNet

Required privilege level:

Normal

Required privilege groups:

NET, WIFI

独立模式或 ad hoc 模式允许 Wi-Fi 网络在没有中央无线路由器或接入点的情况下运行。ad hoc 网络上的所有无线对等方必须使用相同的 SSID（服务集标识符）和信道号。目前，信道不能由应用程序开发人员配置；Wi-Fi 设备会自行扫描并选择合适的信道。

本配方向你展示如何使用 `Net::Wifi` 命名空间中的类和方法执行以下操作：

- 建立一个 ad hoc Wi-Fi 网络。
- 在建立 ad hoc 网络时获取对等方信息。
- 与对等方交换消息。

在图 R5.5 中，设备 1 的用户将其名称设为 Jerry，设备 2 的用户将其名称设为 Tom。然后他们按下 Search，建立了 Wi-Fi 网络并可以看到彼此作为对等方。

![](img/a257d5fd53a79a244a20e587cd2f08f6_425_0.png)

Figure R5.5 Establishing an ad hoc Wi-Fi network.

在图 R5.6 中，Tom 和 Jerry 之间建立了 ad hoc 连接。

![](img/a257d5fd53a79a244a20e587cd2f08f6_426_0.png)

Figure R5.6 An ad hoc Wi-Fi connection is established.

下面是从你的应用程序中建立 ad hoc Wi-Fi 网络需要遵循的步骤。

1. 使你的类派生自 `IAdhocServiceEventListener`。

```
#include <FNet.h>

class MyWiFiClass :
  public Osp::Net::Wifi::IAdhocServiceEventListener
{
  Osp::Net::Wifi::AdhocService* pAdhocService;

  void Initialize();
  void StopService();
  void SendBroadcastMessage(Osp::Base::String msg);
  void SendMessageToPeer(Osp::Base::String peerName,
    Osp::Base::String message);

  void OnAdhocServiceStarted(const Osp::Net::NetConnection*
    pNetConnection, result r);
  void OnAdhocServiceStopped(result r);
  void OnMessageReceived(const Osp::Base::String& peerName,
    const Osp::Base::String& message);
};
```

2. 创建一个 `AdhocService` 的实例。

```
{
    IEnumerator* pEnum;
    pEnum = pNeighborPeerInfo->GetEnumeratorN();
    while (pEnum->MoveNext() == E_SUCCESS)
    {
        pAdhocPeerInfo = (AdhocPeerInfo*) pEnum->GetCurrent();
        name = pAdhocPeerInfo->GetName();
        pAddr = pAdhocPeerInfo->GetAddress();
        String ip = pAddr->ToString();
    }
    pAdhocService->SendBroadcastMessage("Hello All");
    delete pNeighborPeerInfo;
    delete pEnum;
}
```

7. 一旦你的 ad hoc 服务启动，你可以通过调用 `SendBroadcastMessage()` 向所有对等方广播消息。

```
void
MyWiFiClass::SendBroadcastMessage(String msg)
{
    pAdhocService->SendBroadcastMessage(msg);
}
```

8. 你也可以通过调用 `SendUnicastMessage()` 向你的任何对等方发送专用消息。

```
void
MyWiFiClass::SendMessageToPeer(String peerName, String message)
{
    pAdhocService->SendUnicastMessage(peerName, message);
}
```

9. 完成 ad hoc 服务后，调用 `StopService()`。

```
void
MyWiFiClass::StopService()
{
    if (pAdhocService)
    {
        pAdhocService->StopAdhocService();
        delete pAdhocService;
    }
}
```

## Hints, Pitfalls, and Related Topics

一次最多可以看到八个对等方。

你不能在模拟器中测试 `Net::WiFi` 的功能；你需要在设备硬件上进行测试。

## Recipe 5.7: Query a DNS Server

## Problem Description

你想要查询一个域名系统（DNS）服务器。

## The Recipe

本配方需要以下配置：

| Item | Details |
|---|---|
| Namespaces used | Osp::UI, Osp::UI::Controls, Osp::Net, Osp::Base::Collection |
| Header files to `#include` | FUI.h, FNet.h |
| Required libraries | FUI, FUIControls, FNet |
| Required privilege level | Normal |
| Required privilege groups | NET |

`Dns` 是由 `Osp::Net` 命名空间提供的类。该类提供简单的域名解析功能，可将主机名转换为 IP 地址，反之亦然。

要使用 `Dns` 获取查询的答案，必须使用 `IDnsEventListener`。

`Dns` 类封装了从 DNS 服务器请求信息的请求。DNS 请求可以是两种类型之一：

- 从用户友好的主机名查找 IP 地址。
- 从 IP 地址查找主机名。

本配方解释了如何创建 `Dns` 实例，如何发送名称解析查询以及如何获取响应。发送 DNS 查询的 UI 由一个带有 Host by Name 和 Host by IP 按钮的表单提供，如图 R5.7 所示。本配方将集中于发送 DNS 查询的细节。我们的代码包括以下步骤：

1. 从接口 `IDnsEventListener` 派生一个类以获取 DNS 查询的结果。
2. 重写函数 `OnDnsResolutionCompletedN`。该函数作为查询的响应被调用。
3. 使用 `Dns` 类方法 `GetHostByName()` 或 `GetHostByAddress()` 中的任一个查询 DNS 服务器。

![](img/a257d5fd53a79a244a20e587cd2f08f6_430_0.png)

Figure R5.7 Our UI allows us to query the DNS server by name or IP address.

让我们看一下代码。

首先我们从接口 `IDnsEventListener` 派生一个类。

```
#include <FBase.h>
#include <FUi.h>
#include <FNet.h>

class FormDns :
    public Osp::Ui::Controls::Form,
    public Osp::Ui::IActionEventListener,
    public Osp::Net::IDnsEventListener
{
public:
    FormDns(void);
    virtual ~FormDns(void);
    bool Initialize(void);
protected:
    static const int ID_BUTTON_BY_NAME = 101;
    static const int ID_BUTTON_BY_IP = 102;
    Osp::Ui::Controls::Button* pButtonHostByName;
    Osp::Ui::Controls::Button* pButtonHostByIP;
    Osp::Ui::Controls::Label* pLabelHostDetails;
private:
    Osp::Net::Dns* pDns;
public:
    result OnInitializing(void);
    result OnTerminating(void);
    void OnActionPerformed(const Osp::Ui::Control& source, int actionId);
    void OnDnsResolutionCompletedN(Osp::Net::IpHostEntry* ipHostEntry, result r);
private:
    void DnsRequestIP(Osp::Base::String hostName);
    void DnsRequestHostName(Osp::Net::IpAddress& ipAddress);
};
```

`OnDnsResolutionCompletedN` 是作为异步 DNS 查询的响应而被调用的回调函数，即 `GetHostByName()` 或 `GetHostByAddress()`。

```
void FormDns::OnDnsResolutionCompletedN(IpHostEntry* ipHostEntry, result r)
{
    if (r == E_SUCCESS && ipHostEntry != null)
    {
        // Get IP Addresses
        // Gets the address list of a domain name.
        IList* addressList = ipHostEntry->GetAddressList();
        pLabelHostDetails->SetText(L"");
        String strTemp = L"";

        if (addressList != null)
        {
            // Get the count of IpAddress object in address list
            int count = addressList->GetCount();
            strTemp += L"IP:\n";
            for (int index = 0; index < count; index++)
            {
```

