
```csharp
{
    greeting = d.EndInvoke(ar);
}

Console.WriteLine(greeting);
}
}
}
```

您可以在第 8 章“Delegates, Lambdas, and Events”中了解有关委托的更多信息，以及在第 20 章“Threads, Tasks, and Synchronization”中了解有关异步使用委托的信息。

## OneWay 属性

具有 void 返回值且仅有输入参数的方法可以用 OneWay 属性进行标记。OneWay 属性（在命名空间 System.Runtime.Remoting.Messaging 中定义）会使方法自动变为异步，无论客户端如何调用它。将方法 TakeAWhile() 添加到远程对象类 RemoteHello 中会创建一个即发即忘的方法。如果客户端通过代理调用它，代理会立即返回给客户端。在服务器上，该方法会在稍后完成：

```csharp
[OneWay]
public void TakeAWhile(int ms)
{
    Console.WriteLine("TakeAWhile started");
    System.Threading.Thread.Sleep(ms);
    Console.WriteLine("TakeAWhile finished");
}
```

## .NET Remoting 的安全性

.NET Remoting 自 .NET 2.0 起已支持安全性。.NET Remoting 提供了传输数据在电线上的保密性以及用户身份验证。

每个通道都可以配置安全性。TCP、HTTP 和 IPC 通道都支持安全配置。使用服务器配置，您必须定义通信的最低安全要求，而客户端配置则定义有关安全性的功能。如果客户端定义的安全配置低于服务器定义的最低要求，则通信会失败。

让我们从服务器配置开始。以下配置文件的摘录显示了如何为服务器定义安全性。

使用 XML 属性 protectionLevel，您可以指定服务器是否要求在网络上传输加密数据。可以使用 protectionLevel 属性设置的可选值有 None、Sign 和 EncryptAndSign。使用值 Sign 会创建签名，用于验证发送的数据在跨网络传输过程中是否未被更改。但是，仍然可以使用读取网络上所有数据的嗅探器读取数据。使用值 EncryptAndSign，发送的数据也会被加密，以使未正式参与消息传输的系统无法读取数据。

属性 impersonate 可以设置为 true 或 false。如果 impersonate 设置为 true，服务器可以冒充客户端用户以其名义访问资源：

```xml
<channels>
    <channel ref="tcp" port="9001"
        secure="true"
        protectionLevel="EncryptAndSign"
        impersonate="false" />
</channels>
```

## 服务器

服务器在控制台应用程序中实现。使用 RemotingConfiguration.Configure()，读取配置文件，从而设置通道和远程对象。使用 Console.ReadLine()，服务器会等待用户停止应用程序：

```csharp
using System;
using System.Runtime.Remoting;
namespace Wrox.ProCSharp.Remoting
{
    class Server
    {
        static void Main()
        {
            RemotingConfiguration.Configure("Server.exe.config", true);
            Console.WriteLine("press return to exit");
            Console.ReadLine();
        }
    }
}
```

代码片段 RemotingAndEvents/RemoteServer/Program.cs

## 服务器配置文件

服务器配置文件 Server.exe.config 也已创建，如前所述。只有一个重要点：远程对象必须为客户端保留状态，因为客户端首先注册事件处理程序，然后再调用远程方法。事件不能使用单次调用对象，因此 RemoteObject 类被配置为客户端激活类型。此外，为了支持委托，您必须通过为 <provider> 元素指定 typeFilterLevel 属性来启用完全序列化：

```xml
<configuration>
    <system.runtime.remoting>
        <application name="CallbackSample">
            <service>
                <activated type="Wrox.ProCSharp.Remoting.RemoteObject, RemoteObject" />
            </service>
            <channels>
                <channel ref="tcp" port="6791">
                    <serverProviders>
                        <provider ref="binary" typeFilterLevel="Full" />
                    </serverProviders>
                </channel>
            </channels>
        </application>
    </system.runtime.remoting>
</configuration>
```

代码片段 RemotingAndEvents/RemoteServer/app.config

## 事件接收器

客户端需要事件接收器库，服务器会调用它。事件接收器实现了与委托一起定义的处理器 StatusHandler()。如前所述，该方法

```
RemoteObject: LongWorking() Ending
RemoteObject: LongWorking() Started
RemoteObject: LongWorking() Ending
```

通过客户端输出，您可以看到跨网络传递的事件：

```
wait for server...

EventSink: Event occurred: Message for Client: LongWorking() Started
EventSink: Event occurred: Message for Client: LongWorking() Ending
```

## 调用上下文

客户端激活对象可以为特定客户端保存状态。使用客户端激活对象，服务器为每个客户端分配资源。使用服务器激活的 SingleCall 对象，每次实例调用都会创建一个新实例，并且服务器上不保留资源；这些对象无法为客户端保存状态。对于状态管理，您可以在客户端保留状态；状态信息会随每次方法调用发送到服务器。要实现这种状态管理，不必更改所有方法签名以包含额外的参数来将状态传递给服务器；这是由调用上下文自动完成的。

调用上下文会随逻辑线程流动，并在每次方法调用时传递。逻辑线程从调用线程启动，并流经从调用线程启动的所有方法调用，穿过不同的上下文、不同的应用程序域和不同的进程。

您可以使用 CallContext.SetData() 将数据分配给调用上下文。用于 SetData() 方法的数据对象的类必须实现接口 ILogicalThreadAffinitive。您可以使用 CallContext.GetData() 在同一逻辑线程中（但可能是不同的物理线程）再次获取此数据。

对于调用上下文的数据，创建一个新的 C# 类库，其中包含类 CallContextData。此类将用于在每次方法调用时将一些数据从客户端传递到服务器。使用调用上下文传递的类必须实现 System.Runtime.Remoting.Messaging.ILogicalThreadAffinitive 接口。此接口没有方法；它只是运行时的一种标记，用于定义此类实例应随逻辑线程流动。CallContextData 类还必须标记为 Serializable 属性，以便可以通过通道传输：

```csharp
using System;
using System.Runtime.Remoting.Messaging;
namespace Wrox.ProCSharp.Remoting
{
    [Serializable]
    public class CallContextData : ILogicalThreadAffinitive
    {
        public CallContextData()
        {
        }
        public string Data { get; set; }
    }
}
```

在远程对象类 Hello 中，修改 Greeting() 方法以访问调用上下文。要使用 CallContextData 类，您必须引用之前创建的程序集 CallContextData.dll。要使用 CallContext 类，必须打开命名空间 System.Runtime.Remoting.Messaging。变量 cookie 保存从客户端发送到服务器的数据。选择名称“cookie”是因为上下文的工作方式类似于基于浏览器的 cookie，其中客户端会自动将数据发送到 Web 服务器：

```csharp
public string Greeting(string name)
{
    Console.WriteLine("Greeting started");
    CallContextData cookie = (CallContextData)CallContext.GetData("mycookie");
```
