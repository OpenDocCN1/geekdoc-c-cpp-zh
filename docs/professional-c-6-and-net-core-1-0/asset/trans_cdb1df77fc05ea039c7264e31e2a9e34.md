

http://localhost:8000/RoomReservation/Reservations?From=2012/1/1&To=2012/8/1

System.Data.Services.DataServiceHost 是另一个预配置了功能的类。这个类派生自 WebServiceHost。

## 客户端

客户端应用程序需要代理才能访问服务。有三种方式可以为客户端创建代理：

- **Visual Studio 添加服务引用**——该工具根据服务的元数据创建代理类。
- **ServiceModel 元数据实用工具（Svcutil.exe）**——你可以使用 `Svcutil` 实用工具创建代理类。该工具读取服务的元数据来创建代理类。
- **ChannelFactory 类**——这个类被由 `Svcutil` 生成的代理所使用；不过，它也可以用来以编程方式创建代理。

## 使用元数据

从 Visual Studio 添加服务引用需要访问 WSDL 文档。WSDL 文档由 MEX 终结点创建，该终结点需要与服务一起配置。使用以下配置，相对地址为 `mex` 的终结点使用 `mexHttpBinding` 并实现 `IMetadataExchange` 协定。要通过 HTTP GET 请求访问元数据，需要配置 `behaviorConfiguration MexServiceBehavior`。

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.serviceModel>
        <services>
            <service behaviorConfiguration="MexServiceBehavior" name="Wrox.ProCSharp.WCF.RoomReservationService">
                <endpoint address="Test" binding="wsHttpBinding" contract="Wrox.ProCSharp.WCF.IRoomService" />
                <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange" />
                <host>
                    <baseAddresses>
                        <add baseAddress="http://localhost:8733/Design_Time_Addresses/RoomReservationService/" />
                    </baseAddresses>
                </host>
            </service>
        </services>
        <behaviors>
            <serviceBehaviors>
                <behavior name="MexServiceBehavior">
<!-- To avoid disclosing metadata information,
    set the value below to false and remove the metadata endpoint above
    before deployment -->
                <serviceMetadata httpGetEnabled="True"/>
            </behavior>
            </serviceBehaviors>
        </behaviors>
    </system.serviceModel>
</configuration>
```

与 Visual Studio 的“添加服务引用”类似，`Svcutil` 实用工具需要元数据来创建代理类。`Svcutil` 实用工具可以从 MEX 元数据终结点、程序集的元数据或 WSDL 和 XSD 文档创建代理：

```
svcutil http://localhost:8080/RoomReservation?wsdl /language:C#
/out:proxy.cs
svcutil CourseRegistration.dll
svcutil CourseRegistration.wsdl CourseRegistration.xsd
```

生成代理类之后，只需要在客户端代码中实例化它，调用相应的方法，最后调用 `Close` 方法即可：

```
var client = new RoomServiceClient();
client.RegisterForCourse(roomReservation);
client.Close();
```

## 共享类型

生成的代理类派生自基类 `ClientBase<TChannel>`，该类包装了 `ChannelFactory<TChannel>` 类。除了使用生成的代理类之外，你也可以直接使用 `ChannelFactory<TChannel>` 类。构造函数需要绑定和终结点地址；接下来，你可以创建通道并调用服务协定中定义的方法。最后，必须关闭工厂：

```
var binding = new WSHttpBinding();
var address = new EndpointAddress("http://localhost:8080/RoomService");

var factory = new ChannelFactory<IRoomService>(binding, address);

IRoomService channel = factory.CreateChannel();
channel.ReserveRoom(roomReservation);

// etc.
factory.Close();
```

`ChannelFactory<TChannel>` 类有多个属性和方法，如下表所示。

| ChannelFactory 成员 | 描述 |
| --- | --- |
| `Credentials` | `Credentials` 是一个**只读**属性，用于访问分配给通道以便向服务进行身份验证的 `ClientCredentials` 对象。凭据可以随终结点一起设置。 |
| `Endpoint` | `Endpoint` 是一个**只读**属性，用于访问与通道关联的 `ServiceEndpoint`。终结点可以在构造函数中分配。 |
| `State` | `State` 属性的类型是 `CommunicationState`，用于返回通道的当前状态。`CommunicationState` 是一个枚举，其值包括 `Created`、`Opening`、`Opened`、`Closing`、`Closed` 和 `Faulted`。 |
| `Open` | `Open` 方法用于打开通道。 |
| `Close` | `Close` 方法关闭通道。 |
| `Opening`、`Opened`、`Closing`、`Closed`、`Faulted` | 你可以分配事件处理程序，以便获知通道状态的变化。在通道打开之前和之后、关闭之前和之后以及出现故障时，都会触发事件。 |

## 双工通信

下一个示例应用程序展示了如何在客户端和服务之间进行双工通信。客户端启动到服务的连接。客户端连接到服务后，服务可以回调客户端。前面也展示了使用 WebSocket 协议进行双工通信。除了使用 WebSocket 协议（自 Windows 8 和 Windows Server 2012 以来一直受支持）之外，还可以使用 `WSHttpBinding` 和 `NetTcpBinding` 来实现双工通信，如下所示。

### 双工通信的协定

对于双工通信，必须指定一个在客户端实现的协定。在这里，客户端的协定由接口 `IMyMessageCallback` 定义。客户端实现的方法是 `OnCallback`。该操作应用了操作协定设置 `IsOneWay=true`。这样，服务就不会等到方法在客户端成功调用。默认情况下，服务实例只能从一个线程调用。（请参阅服务行为的 `ConcurrencyMode` 属性，该属性默认设置为 `ConcurrencyMode.Single`。）

如果服务实现现在向客户端进行回调并等待从客户端获得答复，那么从客户端获取答复的线程必须等待获得服务对象的锁。由于服务对象已被对客户端的请求锁定，因此会发生死锁。WCF 会检测到死锁并抛出异常。为了避免这种情况，你可以将 `ConcurrencyMode` 属性改为 `Multiple` 或 `Reentrant`。使用 `Multiple` 设置时，多个线程可以同时访问该实例。在这种情况下，你必须自己实现锁定。使用 `Reentrant` 设置时，服务实例保持单线程，但允许来自回调请求的答复重新进入上下文。除了更改并发模式之外，你还可以在操作协定中指定 `IsOneWay` 属性。这样，调用方就不会等待答复。当然，只有在不期望返回值的情况下才能进行此设置。

服务的协定由接口 `IMyMessage` 定义。回调协定通过服务协定定义的 `CallbackContract` 属性映射到服务协定（代码文件 `DuplexCommunication/MessageService/IMyMessage.cs`）：

```
public interface IMyMessageCallback
{
    [OperationContract(IsOneWay=true)]
    void OnCallback(string message);
}
```

```
[ServiceContract(CallbackContract=typeof(IMyMessageCallback))]
public interface IMyMessage
{
    [OperationContract]
    void MessageToServer(string message);
}
```

### 用于双工通信的服务

`MessageService` 类实现了服务协定 `IMyMessage`。该服务将来自客户端的消息写入控制台。要访问回调协定，你可以使用 `OperationContext` 类。`OperationContext.Current` 返回与当前来自客户端的请求关联的 `OperationContext`。通过 `OperationContext`，你可以访问会话信息、消息头和属性，以及在双工通信的情况下访问回调通道。泛型方法 `GetCallbackChannel` 返回指向客户端实例的通道。然后可以使用该通道向客户端发送消息。

