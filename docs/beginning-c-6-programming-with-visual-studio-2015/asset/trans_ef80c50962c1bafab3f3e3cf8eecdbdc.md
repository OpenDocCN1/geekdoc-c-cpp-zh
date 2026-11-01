

这种实现方式的一个结果是，服务可以同时向多个客户端广播消息。

- **命名管道** — 使你能够与调用代码位于同一台计算机上、但在独立进程中运行的 WCF 服务进行通信。
- **MSMQ** — Microsoft 消息队列（MSMQ）是一种队列技术，它使应用程序发送的消息能够通过队列进行路由，最终到达目的地。MSMQ 是一种可靠的消息传递技术，可确保发送到队列的消息能够到达该队列。MSMQ 在本质上也是异步的，因此只有当队列中位于它前面的消息已被处理，并且有可用的处理服务时，排队的消息才会被处理。

这些协议通常使你能够建立安全连接。例如，可以使用 HTTPS 协议在 Internet 上建立 SSL 连接。TCP 通过使用 Windows 安全框架，在局域网中提供了丰富多样的安全可能性。UDP 不支持安全性。

为了连接 WCF 服务，你必须知道它的位置。实际上，这意味着要了解终结点的地址。

## 地址、终结点和绑定

你为服务使用的地址类型取决于你正在使用的协议。本章介绍的三种协议（不包括 MSMQ）的服务地址格式如下：

- **HTTP** — HTTP 协议的地址是常见的 URL 形式：http://<server>:<port>/<service>。对于 SSL 连接，还可以使用 https://<server>:<port>/<service>。如果你在 IIS 中托管服务，<service> 将是一个扩展名为 .svc 的文件。IIS 地址可能包含比此示例更多的子目录——也就是说，在 .svc 文件之前会有更多用 / 字符分隔的部分。
- **TCP** — TCP 地址的形式为 net.tcp://<server>:<port>/<service>。
- **UDP** — UDP 地址的形式为 soap.udp://<server>:<port>/<service>。某些 <server> 值是多播通信所必需的，但这超出了本章的范围。
- **命名管道** — 命名管道连接的地址与此类似，但没有端口号。其形式为 net.pipe://<server>/<service>。

服务的地址是一个基地址，你可以使用它来创建表示操作的终结点的地址。例如，你可以在 net.tcp://<server>:<port>/<service>/operation1 上有一个操作。

例如，假设你创建一个 WCF 服务，它只有一个操作，并为这里列出的所有三种协议配置了绑定。你可以使用以下基地址：

```
http://www.mydomain.com/services/amazingservices/mygreatservice.svc
net.tcp://myhugserver:8080/mygreatservice
net.pipe://localhost/mygreatservice
```

在 Web 服务中实现起来要困难得多。你还可以与 IIS 功能（例如 IIS 安全性）集成。

- 可执行文件 — 你可以在 .NET 中能创建的任何应用程序类型中托管 WCF 服务，例如控制台应用程序、Windows 窗体应用程序和 WPF 应用程序。
- Windows 服务 — 你可以在 Windows 服务中托管 WCF 服务，这意味着你可以使用 Windows 服务提供的实用功能。这些功能包括自动启动和故障恢复。
- Windows 激活服务 (WAS) — WAS 专门用于托管 WCF 服务，它基本上是 IIS 的简化版本，可在无法使用 IIS 的地方使用。

前面列表中的两个选项——IIS 和 WAS——为 WCF 服务提供了有用的功能，例如激活、进程回收和对象池。如果你使用另外两个托管选项中的任意一个，则该 WCF 服务被称为自托管。你偶尔会出于测试目的而自托管服务，但创建自托管的生产级服务也可能有非常充分的理由。例如，你可能遇到这样的情况：不允许在服务应该运行的计算机上安装 Web 服务器。如果服务在域控制器上运行，或者组织本地策略禁止运行 IIS，就会出现这种情况。在这种情况下，你可以在 Windows 服务中托管服务，其运行效果与其他方式完全一样。

## WCF 编程

既然你已经掌握了所有基础知识，是时候编写一些代码了。在本节中，你将首先查看一个简单的、由 Web 服务器托管的 WCF 服务和一个控制台应用程序客户端。在查看了所创建代码的结构之后，你将了解 WCF 服务和客户端应用程序的基本结构。然后，你将更详细地了解一些关键主题：

- 定义 WCF 服务契约
- 自托管 WCF 服务

### 试一试：一个简单的 WCF 服务和客户端：Ch22Ex01Client

1. 在目录 C:\BegVCSharp\Chapter22 中创建一个名为 Ch22Ex01 的新 WCF 服务应用程序项目。
2. 向解决方案中添加一个名为 Ch22Ex01Client 的控制台应用程序。
3. 在“生成”菜单上，单击“生成解决方案”。
4. 在 Ch22Ex01Client 项目中，右键单击“解决方案资源管理器”中的“引用”，然后选择“添加服务引用”。
5. 在“添加服务引用”对话框中，单击“发现”。
6. 当开发 Web 服务器已启动并加载有关 WCF 服务的信息后，展开该引用以查看其详细信息。请注意，服务中有两个方法：GetData 和 GetDataUsingDataContract。
7. 单击“确定”以添加服务引用。
8. 按如下方式修改 Ch22Ex01Client 应用程序中 Program.cs 的代码：

```csharp
using Ch22Ex01Client.ServiceReference1;
using static System.Console;

namespace Ch22Ex01Client
{
    class Program
    {
        static void Main(string[] args)
        {
            Title = "Ch22Ex01Client";
            string numericInput = null;
            int intParam;
            do
            {
                WriteLine("Enter an integer and press enter to call the WCF service.");
                numericInput = ReadLine();
            }
            while (!int.TryParse(numericInput, out intParam));
            ServiceClient client = new ServiceClient();
            WriteLine(client.GetData(intParam));
            WriteLine("Press a key to exit.");
            ReadKey();
        }
    }
}
```

9. 在“解决方案资源管理器”中右键单击 Ch22Ex01Client 项目，然后选择“设置为启动项目”。
10. 运行应用程序。在控制台应用程序窗口中输入一个数字，然后按 Enter。结果如图 22-1 所示。

    ![](img/cf72ea860016d2d680fc085fc06f265a_712_0.png)

    图 22-1

11. 退出应用程序，在“解决方案资源管理器”中右键单击 Ch22Ex01 项目中的 Service1.svc 文件，然后点击“在浏览器中查看”。
12. 查看窗口中的信息。
13. 单击网页顶部服务的链接以查看 WSDL。不要惊慌——你不需要理解 WSDL 文件中的所有内容！

### 工作原理

在此示例中，你创建了一个简单的、由 Web 服务器托管的 WCF 服务和一个控制台应用程序客户端。你使用了 WCF 服务项目的默认 Visual Studio 模板，这意味着你不必添加任何代码。相反，你使用了该默认模板中定义的操作之一。

这种配置使你可以将几乎任何能想到的配置应用于服务，甚至可以扩展此语法。

WCF 配置代码包含在 Web.config 或 app.config 文件的 <system.serviceModel> 配置节中。在此示例中，由于使用默认值，服务配置并不多。在 Web.config 文件中，配置节由一个子节组成，该子节提供对服务行为 <behaviors> 默认值的覆盖。Web.config 中 <system.serviceModel> 配置节的代码（为清晰起见，已移除注释）如下：

```
<system.serviceModel>
  <behaviors>
    <serviceBehaviors>
      <behavior>
        <serviceMetadata httpGetEnabled="true" httpsGetEnabled="true" />
        <serviceDebug includeExceptionDetailInFaults="false" />
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```

此节可以在 <behavior> 子节中定义一个或多个行为，这些行为可以在多个其他元素上重用。<behavior> 节可以指定名称以方便重用（以便可以从其他地方引用），也可以不使用名称（如本示例所示），以指定对默认行为设置的覆盖。

> 注意 如果使用非默认配置，你应会看到 <system.serviceModel> 内有一个 <services> 节，其中包含一个或多个 <services> 子节。相应地，<service> 节可以包含 <endpoint> 子节，每个子节（你猜对了）都为服务定义一个终结点。事实上，所定义的终结点是服务的基终结点。操作的终结点就是根据这些基终结点推断出来的。

Web.config 中的默认行为覆盖之一如下：

```
<serviceDebug includeExceptionDetailInFaults="false"/>
```

此设置可以设置为 true，以便在传输到客户端的任何错误中公开异常详细信息，这通常只在开发时才会允许。

