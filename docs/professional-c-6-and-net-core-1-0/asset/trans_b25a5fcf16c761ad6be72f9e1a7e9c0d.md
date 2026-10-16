
{
    [DataMember]
    public string Message { get; set; }
}

必须使用操作契约中的 FaultContractAttribute 定义 SOAP 错误的类型：

```
[FaultContract(typeof(RoomReservationFault))]
[OperationContract]
bool ReserveRoom(RoomReservation roomReservation);
```

在实现中，会抛出 FaultException<TDetail>。通过构造函数，你可以分配一个新的 TDetail 对象，在示例中即 RoomReservationFault。此外，可以在构造函数中分配 FaultReason 中的错误信息。FaultReason 支持多语言的错误信息。

```
FaultReasonText[] text = new FaultReasonText[2];
text[0] = new FaultReasonText("Sample Error", new CultureInfo("en"));
text[1] = new FaultReasonText("Beispiel Fehler", new CultureInfo("de"));
FaultReason reason = new FaultReason(text);

throw new FaultException<RoomReservationFault>(
    new RoomReservationFault() { Message = m }, reason);
```

在客户端应用程序中，可以捕获 FaultException<RoomReservationFault> 类型的异常。异常的原因由 Message 属性定义；可通过 Detail 属性访问 RoomReservationFault：

```
try
{
    // etc.
}
catch (FaultException<RoomReservationFault> ex)
{
    WriteLine(ex.Message);
    RoomReservationFault detail = ex.Detail;
    WriteLine(detail.Message);
}
```

除了捕获强类型的 SOAP 错误外，客户端应用程序还可以捕获 FaultException<Detail> 的基类异常：FaultException 和 CommunicationException。通过捕获 CommunicationException，还可以捕获与 WCF 通信相关的其他异常。

> 注意：在开发期间，你可以将异常返回给客户端。要启用异常的传播，需要使用 serviceDebug 元素配置服务行为配置。serviceDebug 元素具有属性 IncludeExceptionDetailInFaults，可将其设置为 true 以返回异常信息。

## 服务行为

服务的实现可以用 `ServiceBehavior` 特性标记，如类 `RoomReservationService` 所示：

```
[ServiceBehavior]
public class RoomReservationService: IRoomService
{
    public bool ReserveRoom(RoomReservation roomReservation)
    {
        // implementation
    }
}
```

`ServiceBehavior` 特性用于描述 WCF 服务提供的行为，以拦截所需功能的代码，如下表所示。

| ServiceBehavior 属性 | 描述 |
|---|---|
| `TransactionAutoCompleteOnSessionClose` | 当当前会话无错误地完成时，事务会自动提交。这类似于 Enterprise Services 中使用的 `AutoComplete` 属性。 |
| `TransactionIsolationLevel` | 要定义服务内事务的隔离级别，可以将属性 `TransactionIsolationLevel` 设置为 `IsolationLevel` 枚举中的一个值。 |
| `ReleaseServiceInstanceOnTransactionComplete` | 当事务完成时，服务的实例会被回收。 |
| `AutomaticSessionShutdown` | 如果不希望在客户端关闭连接时关闭会话，可以将属性 `AutomaticSessionShutdown` 设置为 `false`。默认情况下，会话会关闭。 |
| `InstanceContextMode` | 通过属性 `InstanceContextMode`，你可以定义是使用有状态还是无状态的对象。默认设置为 `InstanceContextMode.PerCall`，即每次方法调用时创建一个新对象。其他可能的设置为 `PerSession` 和 `Single`。使用这两种设置时，都会使用有状态的对象。但是，使用 `PerSession` 时会为每个客户端创建一个新对象。`Single` 允许多个客户端共享同一个对象。 |
| `ConcurrencyMode` | 由于有状态的对象可以被多个客户端（或单个客户端的多个线程）使用，因此你必须注意此类对象类型的并发问题。如果将属性 `ConcurrencyMode` 设置为 `Multiple`，则多个线程可以访问该对象，你必须处理同步问题。如果将该选项设置为 `Single`，则同一时间只有一个线程访问该对象。这里你无需进行同步，但在客户端数量较多时可能会出现可伸缩性问题。值 `Reentrant` 意味着仅从外部调用返回的线程可能访问该对象。对于无状态对象，此设置没有意义，因为每次方法调用都会实例化新对象，因此不会共享任何状态。 |
| `UseSynchronizationContext` | 对于用户界面代码，控件的成员只能从创建线程调用。如果服务托管在 Windows 应用程序中，并且服务方法调用了控件成员，请将 `UseSynchronizationContext` 设置为 `true`。这样，服务将在由 `SynchronizationContext` 定义的线程中运行。 |
| `IncludeExceptionDetailInFaults` | 在 .NET 中，错误以异常的形式出现。SOAP 定义：如果服务器出现问题，则向客户端返回 SOAP 错误。出于安全原因，将服务器端异常的详细信息返回给客户端并不是一个好主意。因此，默认情况下，异常会被转换为未知的错误。要返回特定的错误，请抛出类型为 `FaultException` 的异常。出于调试目的，返回真实的异常信息可能会很有帮助。将 `IncludeExceptionDetailInFaults` 设置为 true 时就是这种情况。此时会抛出 `FaultException<TDetail>`，其中原始异常包含详细信息。 |

- **MaxItemsInObjectGraph**：使用属性 `MaxItemsInObjectGraph`，你可以限制序列化的对象数量。如果序列化一个对象树，默认限制可能太低。
- **ValidateMustUnderstand**：将属性 `ValidateMustUnderstand` 设置为 true 意味着必须理解 SOAP 头（这是默认设置）。

为了演示服务行为，接口 `IStateService` 定义了一个服务契约，其中包含两个用于设置和获取状态的操作。对于有状态的服务契约，需要会话。这就是为什么服务契约的 `SessionMode` 属性被设置为 `SessionMode.Required`。服务契约还通过将 `IsInitiating` 和 `IsTerminating` 属性应用于操作契约来定义启动和关闭会话的方法：

```
[ServiceContract(SessionMode=SessionMode.Required)]
public interface IStateService
{
    [OperationContract(IsInitiating=true)]
    void Init(int i);

    [OperationContract]
    void SetState(int i);

    [OperationContract]
    int GetState();

    [OperationContract(IsTerminating=true)]
    void Close();
}
```

服务契约由类 `StateService` 实现。服务实现定义了 `InstanceContextMode.PerSession`，以在实例中保持状态：

```
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]
public class StateService: IStateService
{
    int _i = 0;

    public void Init(int i)
    {
        _i = i;
    }

    public void SetState(int i)
    {
        _i = i;
    }

    public int GetState()
    {
        return _i;
    }

    public void Close()
    {
    }
}
```

现在必须定义与地址和协议的绑定。这里，将 `basicHttpBinding` 分配给服务的终结点：

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.serviceModel>
        <services>
            <service behaviorConfiguration="StateServiceSample.Service1Behavior"
                name="Wrox.ProCSharp.WCF.StateService">
                <endpoint address="" binding="basicHttpBinding"
                    bindingConfiguration=""
                    contract="Wrox.ProCSharp.WCF.IStateService">
                </endpoint>
                <endpoint address="mex" binding="mexHttpBinding"
                    contract="IMetadataExchange" />
                <host>
                    <baseAddresses>
                        <add baseAddress="http://localhost:8731/Design_Time_Addresses/StateServiceSample/Service1/" />
                    </baseAddresses>
                </host>
            </service>
        </services>
    </system.serviceModel>
```
