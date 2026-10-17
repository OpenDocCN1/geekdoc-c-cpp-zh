
宿主服务的构建方式与之前的示例相同，因此此处不再展示。然而，对于双工通信，必须配置一个支持双工通道的绑定。支持双工通道的绑定之一是 `wsDualHttpBinding`，它在应用程序的配置文件中进行配置（配置文件 `DuplexCommunication/DuplexHost/app.config`）：

```xml
<?xml version="1.0" encoding="utf-8" ?>

<configuration>

    <system.serviceModel>

        <services>

            <service name="Wrox.ProCSharp.WCF.MessageService">

                <endpoint address="" binding="wsDualHttpBinding" contract="Wrox.ProCSharp.WCF.IMyMessage" />

                <host>

                    <baseAddresses>

                        <add baseAddress="http://localhost:8733/Design_Time_Addresses/MessageService/Serv..." />

                    </baseAddresses>

                </host>

            </service>

        </services>

    </system.serviceModel>

</configuration>
```

#### 双工通信的客户端应用程序

在客户端应用程序中，必须实现回调契约，如下面的类 `ClientCallback` 所示，该类实现了接口 `IMyMessageCallback`（代码文件 `DuplexCommunication/MessageClient/Program.cs`）：

```csharp
class ClientCallback: IMyMessageCallback

{

    public void OnCallback(string message)

    {

        WriteLine($"message from the server: {message}");

    }

}
```

对于双工通道，不能像之前那样使用 `ChannelFactory` 来发起与服务的连接。要创建双工通道，可以使用 `DuplexChannelFactory` 类。这个类有一个构造函数，除了绑定和地址配置之外，还多一个参数。该参数指定了一个 `InstanceContext`，它包装了 `ClientCallback` 类的一个实例。将这个实例传递给工厂后，服务就可以通过该通道调用该对象。客户端只需要保持连接打开。如果连接关闭，服务将无法通过它发送消息。

```csharp
private async static void DuplexSample()

{

    var binding = new WSDualHttpBinding();

    var address = new EndpointAddress("http://localhost:8733/Service1");

    var clientCallback = new ClientCallback();

    var context = new InstanceContext(clientCallback);

    var factory = new DuplexChannelFactory<IMyMessage>(context, binding, address);

    IMyMessage messageChannel = factory.CreateChannel();

    await Task.Run(() => messageChannel.MessageToServer("From the client"));

}
```

通过启动服务宿主和客户端应用程序即可实现双工通信。

#### 路由

使用 SOAP 协议相比于带有 REST 的 HTTP GET 请求有一定的优势。SOAP 可以实现的高级功能之一是路由。通过路由，客户端不直接寻址服务，而是寻址中间的路由器，由路由器转发请求。

使用此功能有几种不同的场景。一种是用于故障转移（见图 44.10）。如果服务无法访问或返回错误，路由器会调用另一台主机上的服务。这对客户端来说是透明的；客户端只会收到结果。

![](img/3d365b72b289213a91ade7eb366b8f35_1738_0.png)

图 44.10

路由也可以用于更改通信协议（见图 44.11）。客户端可以使用 HTTP 协议调用请求并将其发送到路由器。路由器充当 net.tcp 协议的客户端，并调用服务来转发消息。

![](img/3d365b72b289213a91ade7eb366b8f35_1738_1.png)

图 44.11

使用路由实现可伸缩性是另一种场景（见图 44.12）。根据消息头中的某个字段或消息内容中的信息，路由器可以决定将请求转发到某一台服务器。来自客户的请求，若名称以 A–F 开头，则发送到第一台服务器，G–N 发送到第二台服务器，O–Z 发送到第三台服务器。

![](img/3d365b72b289213a91ade7eb366b8f35_1738_2.png)

图 44.12

#### 示例路由应用程序

在示例路由应用程序中，定义了一个简单的服务契约，调用者可以调用 `IDemoService` 接口中的 `GetData` 操作（代码文件 `RoutingSample/DemoService/IDemoService.cs`）：

### 第45章 部署网站和服务

#### 本章内容

- 部署准备
- 部署到 Internet Information Server
- 部署到 Microsoft Azure
- 使用 Docker 部署

#### Wrox.com 本章代码下载

本章的 wrox.com 代码下载可在 [www.wrox.com/go/professionalcsharp6](http://www.wrox.com/go/professionalcsharp6) 的 Download Code 选项卡中找到。本章的代码位于以下示例中：

- WebDotnetFramework
- WebDotnetCore

#### 部署 Web 应用程序

ASP.NET Web 应用程序传统上一直部署在 Internet Information Server（IIS）上。并且，服务器上必须安装与开发期间使用的相同版本的 .NET Framework，这一点曾非常重要。而使用 .NET Core 后，情况不再如此。.NET Core 不仅可以在 Windows 上运行，也可以在 Linux 上运行。此外，应用程序所需的运行时也作为应用程序的一部分提供。这些变化为你提供了更多的部署选项来运行应用程序。

本章展示了部署 Web 应用程序的不同选项。当然，其中之一是将应用程序部署到本地 Internet Information Server。部署到 Microsoft Azure 也很容易。使用 Microsoft Azure，你可以轻松扩展应用程序，并且不需要预先购买可能需要使用的所有系统。你还可以根据需求添加其他系统，并且只为使用这些系统的时间付费。

> **注意** 本书并未涵盖 IIS 和 Microsoft Azure 的所有不同配置选项，也没有涵盖 Docker 可以做的所有事情。请参阅其他书籍以获取更多详细信息。本章仅为你提供作为开发人员需要了解的关于这些主题的最重要信息。

#### 部署准备

Web 应用程序需要部署哪些内容？静态文件（如 HTML、CSS、JavaScript 和图像文件）、由 C# 源文件编译生成的二进制程序集，以及数据库。配置文件也是必需的。配置文件包含应用程序设置，包括用于连接数据库的连接字符串。很可能，应用程序设置在测试环境和生产环境之间会有所不同。你可能还会有一个预发布环境，以便在迁移到生产环境之前进行一些最终测试。你也需要在不同环境之间更改配置。

为了部署示例应用程序，你将创建两个应用程序：一个使用 .NET Framework 4.6 的应用程序，另一个使用 ASP.NET Core 1.0 和 .NET Core 的应用程序。这两个应用程序都使用一个通过 Entity Framework Core 访问的数据库。

> **注意** 请参阅第 38 章以获取有关 Entity Framework Core 的更多信息。

#### 创建 ASP.NET 4.6 Web 应用程序

使用 Visual Studio 项目模板 ASP.NET Web Application 创建第一个应用程序，命名为 `WebDotnetFramework`。选择 ASP.NET 4.6 模板 MVC，并选择身份验证为“单个用户帐户”（见图 45.1）。

#### 图 45.1

运行此应用程序时，会出现几个屏幕，你可以注册一个新用户（参见图 45.2）。此注册会在随 Visual Studio 安装的 SQL LocalDB 实例上创建一个数据库。

![](img/3d365b72b289213a91ade7eb366b8f35_1748_0.png)

#### 图 45.2

### 创建 ASP.NET Core 1.0 Web 应用程序

再次使用 Visual Studio 项目模板 “ASP.NET Web Application” 创建名为 `WebDotnetCore` 的第二个应用程序，但现在选择 ASP.NET Core 1.0 模板 “Web Application”，并且仍然使用“个人用户帐户”进行身份验证（参见图 45.3）。

选择一个模板：

ASP.NET 4.5.1 模板

- 空
- Web 窗体
- MVC
- Web API
- 单页应用程序

ASP.NET 5 模板

- 空
- Web API
- Web 应用程序

用于创建 ASP.NET 5 应用程序的项目模板。该模板使用 ASP.NET MVC，可用于构建 Web 应用程序和 RESTful HTTP 服务。

了解更多

更改身份验证

身份验证：个人用户帐户

Microsoft Azure

托管在云中

应用服务

为以下项添加文件夹和核心引用：

- Web 窗体
- MVC
- Web API

添加单元测试

测试项目名称：`WebDotNetCore.Tests`

![](img/3d365b72b289213a91ade7eb366b8f35_1750_0.png)

#### 图 45.4

同时拥有这两个应用程序用于部署，可以满足不同的场景：使用运行 .NET 4.6 的 Web 应用程序时，在部署应用程序之前，需要在目标系统上安装 .NET Framework。你需要一个具备 .NET 4.6 的系统；通常使用 IIS（也可在 Microsoft Azure 上）进行部署。

使用 ASP.NET Core 1.0，你可以使用 .NET 4.5 或更高版本托管应用程序，也可以使用 .NET Core 1.0。使用 .NET Core 1.0，你还可以在非 Windows 系统上托管应用程序，并且不需要在部署应用程序之前在目标系统上安装 .NET 运行时。.NET 运行时可以随应用程序一起交付。

使用 ASP.NET Core 1.0，你仍然可以决定使用 .NET 4.6 托管应用程序，这与第一个应用程序的部署方式类似。但是，ASP.NET Core 1.0 的 Web 配置文件与 ASP.NET 4.6 的 Web 配置文件看起来非常不同；因此，我决定在本章中向你提供 ASP.NET 4.6 和 ASP.NET Core 1.0 两个选项，以便你了解应用程序的典型部署需求。

让我们开始在本地 Internet 信息服务（IIS）上部署 Web 应用程序。

### 使用 ASP.NET 4.6 的配置文件

Web 应用程序的一个重要部分是配置文件。在 ASP.NET 4.6 中，配置文件（`Web.config`）采用 XML 格式，包含应用程序设置、数据库连接字符串、ASP.NET 配置（如身份验证和授权、会话状态等）以及程序集重定向配置。

在部署方面，你必须考虑此文件的不同版本。例如，如果你为在本地系统上运行的 Web 应用程序使用不同的数据库，暂存服务器有特殊的测试数据库，当然生产服务器也有一个实际数据库。这些服务器的连接字符串不同。此外，调试配置也不同。如果你为这些场景创建单独的 `Web.config` 文件，然后向本地 `Web.config` 文件添加新的配置值，则很容易忽略更改其他配置文件。

Visual Studio 提供了一个特殊功能来处理此问题。你可以创建一个配置文件，并定义该文件应如何转换到暂存服务器和部署服务器。默认情况下，对于 ASP.NET Web 项目，在解决方案资源管理器中，你会看到 `Web.config` 文件以及 `Web.Debug.config` 和 `Web.Release.config`。后两个文件只包含转换。你还可以添加其他配置文件，例如用于暂存服务器的配置文件。操作方法是在解决方案资源管理器中选择解决方案，打开配置管理器，然后添加一个新配置（例如，一个 Staging 配置，如图 45.5 所示）。一旦新配置可用，你就可以选择 `Web.config` 文件，并从上下文菜单中选择“添加配置转换”选项。然后，这会添加一个以配置名称命名的配置转换文件，例如 `Web.Staging.config`。

1.0. 这里，使用文件名中包含环境名称的 JSON 文件来定义不同的设置（代码文件 `WebCoreFramework/Startup.cs`）：

```csharp
public Startup(IHostingEnvironment env)

{

    var builder = new ConfigurationBuilder()

        .AddJsonFile("appsettings.json")

        .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true);

    if (env.IsDevelopment())

    {

        builder.AddUserSecrets();

    }

    builder.AddEnvironmentVariables();

    Configuration = builder.Build();

}

public IConfigurationRoot Configuration { get; set; }
```
