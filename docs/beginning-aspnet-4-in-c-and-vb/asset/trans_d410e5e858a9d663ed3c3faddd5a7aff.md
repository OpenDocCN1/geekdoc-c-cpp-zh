
## 绑定

一个绑定描述了服务希望如何通信。通过绑定，您可以指定以下功能：

- 传输协议
- 安全
- 编码格式
- 事务流
- 可靠性
- 形状更改
- 传输升级

一个绑定由多个绑定元素组成，这些元素描述了所有绑定要求。您可以创建自定义绑定或使用下表中显示的预定义绑定之一。

| 标准绑定 | 描述 |
|---|---|
| BasicHttpBinding | BasicHttpBinding 是最广泛互操作性的绑定，属于第一代 Web 服务。使用的传输协议为 HTTP 或 HTTPS；安全仅来自传输协议。 |
| WSHttpBinding | WSHttpBinding 是下一代 Web 服务的绑定，平台实现用于安全、可靠性和事务的 SOAP 扩展。使用的传输为 HTTP 或 HTTPS；对于安全实现了 WS-Security 规范；事务得到支持，如所述，使用 WS-Coordination、WS-AtomicTransaction 和 WS-BusinessActivity 规范；可靠消息传递通过 WS-ReliableMessaging 的实现得到支持。WS-Profile 还支持 MTOM（Message Transmission Optimization Protocol）编码用于发送附件。您可以在 http://www.oasis-open.org 找到 WS-* 标准的规范。 |
| WS2007HttpBinding | WS2007HttpBinding 派生自基类 WSHttpBinding，并支持 OASIS（Organization for the Advancement of Structured Information Standards）定义的 安全、可靠性和事务规范。 |
| WSHttpContextBinding | WSHttpContextBinding 派生自基类 WSHttpBinding 并增加了在不使用 cookie 的情况下支持上下文的功能。此绑定添加了一个 ContextBindingElement 用于交换上下文信息。 |
| WebHttpBinding | 此绑定用于通过 HTTP 请求而不是 SOAP 请求公开的服务。这对于脚本客户端很有用——例如 ASP.NET AJAX。 |
| WSFederationHttpBinding | WSFederationHttpBinding 是一个安全且可互操作的绑定，支持在多个系统之间共享身份以进行身份验证和授权。 |
| WSDualHttpBinding | 与 WSHttpBinding 相比，绑定 WSDualHttpBinding 支持双工消息传递。 |
| NetTcpBinding | 所有以 Net 为前缀的标准绑定都使用用于 .NET 应用程序之间通信的二进制编码。这种编码比 WSxxx 绑定中的文本编码更快。绑定 NetTcpBinding 使用 TCP/IP 协议。 |
| NetTcpContextBinding | 类似于 WSHttpContextBinding，NetTcpContextBinding 添加了一个 ContextBindingElement 用于通过 SOAP 头交换上下文。 |
| NetPeerTcpBinding | NetPeerTcpBinding 为点对点通信提供绑定。 |

要使用简单的 HTTP GET 请求接收预订，方法 GetRoomReservation 需要一个 WebGet 属性来将方法参数映射到 GET 请求的输入。在以下代码中，定义了一个 UriTemplate，要求在基本地址后添加 Reservations，然后是 From 和 To 参数。From 和 To 参数依次映射到 fromDate 和 toDate 变量。

```csharp
[WebGet(UriTemplate="Reservations?From={fromDate}&To={toDate}")]
public RoomReservation[] GetRoomReservations(DateTime fromDate, DateTime toDate)
{
    var data = new RoomReservationData();
    return data.GetReservations(fromDate, toDate);
}
```

*代码片段 RoomReservationService/RoomReservationService.cs*

现在服务可以用如下所示的简单请求调用。指定时间段内的所有预订都将被返回。

`http://localhost:8000/RoomReservation/Reservations?From=2010/1/16&To=2010/8/1`

## 客户端

客户端应用程序需要代理来访问服务。创建客户端代理有三种方法：

- Visual Studio 添加服务引用 — 此实用工具从服务的元数据创建代理类。
- ServiceModel 元数据实用工具 (Svcutil.exe) — 您可以使用 Svcutil 实用工具创建代理类。此实用工具从服务读取元数据以创建代理类。
- ChannelFactory 类 — 此类由 Svcutil 生成的代理使用；但是，它也可以用于以编程方式创建代理。

从 Visual Studio 添加服务引用需要访问 WSDL 文档。WSDL 文档由需要与服务一起配置的 MEX 端点创建。通过以下配置，相对地址为 mex 的端点使用 mexHttpBinding 并实现契约 IMetadataExchange。为了通过 HTTP GET 请求访问元数据，behaviorConfiguration MexServiceBehavior 已配置。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service behaviorConfiguration="MexServiceBehavior" name="Wrox.ProCSharp.WCF.RoomReservationService">
        <endpoint address="Test" binding="wsHttpBinding" contract="Wrox.ProCSharp.WCF.IRoomService" />
        <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange" />
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost:8732/Design_Time_Addresses/RoomReservationService/" />
          </baseAddresses>
        </host>
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior name="MexServiceBehavior">
        <!-- To avoid disclosing metadata information,
```

## 双工通信

下一个示例应用程序展示了客户端和服务之间如何进行双工通信。客户端启动与服务的连接。客户端连接到服务后，服务可以回调到客户端。

对于双工通信，必须指定在客户端实现的契约。这里客户端的契约由接口 IMyMessageCallback 定义。客户端实现的方法是 OnCallback()。该操作应用了操作契约设置 IsOneWay=true。这样，服务不会等待该方法在客户端上成功调用。默认情况下，服务实例只能由一个线程调用（请参阅服务行为的 ConcurrencyMode 属性，默认情况下设置为 ConcurrencyMode.Single）。

如果服务实现现在对客户端进行回调并等待从客户端获取答案，则获取客户端回复的线程必须等待直到它获得对服务对象的锁。因为服务对象已被对客户端的请求锁定，所以会发生死锁。WCF 检测到死锁并抛出异常。为了避免这种情况，您可以将 ConcurrencyMode 属性更改为值 Multiple 或 Reentrant。使用设置 Multiple，多个线程可以并发访问实例。在这里，您必须自行实现锁定。使用设置 Reentrant，服务实例保持单线程，但允许来自回调请求的答案重新进入上下文。代替更改并发模式，您可以指定操作契约中的 IsOneWay 属性。这样，调用者不会等待回复。当然，此设置仅在不期望返回值时才可能。

服务的契约由接口 IMyMessage 定义。回调契约通过服务契约定义的 CallbackContract 属性映射到服务契约：

```csharp
public interface IMyMessageCallback
{
    [OperationContract(IsOneWay=true)]
    void OnCallback(string message);
}

[ServiceContract(CallbackContract=typeof(IMyMessageCallback))]
public interface IMyMessage
{
    [OperationContract]
    void MessageToServer(string message);
}
```

代码片段 MessageService/IMyMessage.cs

类 MessageService 实现服务契约 IMyMessage。服务将来自客户端的消息写入控制台。要访问回调契约，您可以使用 OperationContext 类。OperationContext.Current 返回与来自客户端的当前请求关联的 OperationContext。通过 OperationContext，您可以访问会话信息、消息头和属性，以及在双工通信的情况下，回调通道。通用方法 GetCallbackChannel() 返回到客户端实例的通道。然后可以使用该通道通过调用方法 OnCallback() 向客户端发送消息，该方法由回调接口 IMyMessageCallback 定义。为了证明也可以独立于方法的完成从服务使用回调通道，会创建一个接收回调通道的新线程。新线程使用回调通道向客户端发送消息。

```csharp
public class MessageService: IMyMessage
{
    public void MessageToServer(string message)
    {
        Console.WriteLine("message from the client: {0}", message);
        IMyMessageCallback callback =
            OperationContext.Current.
```
