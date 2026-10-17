
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <sections>
    <section name="[sectionSettings]" type="[Class]" />
    <sectionGroup name="[sectionGroup]">
      <section name="[sectionSettings]" type="[Class]" />
    </sectionGroup>
  </sections>
</configuration>
```

> 方括号 `[ ]` 内的值在真实的配置文件中具有唯一的值。

XML 配置文件中的根元素始终是 `<configuration>`。每个节处理器和设置都可以选择封装在 `<sectionGroup>` 中。`<sectionGroup>` 在配置文件内部提供了一种组织功能。它允许你将配置组织成唯一的组——例如，`<system.web>` 节组用于识别配置文件中特定于 ASP.NET 的区域。

`<sections>` 节是与每个配置节关联的配置节处理器分组的机制。当你想要创建自己的节处理器时，必须在 `<sections>` 节中声明它们。`<httpModules>` 节有一个配置处理器，被设置为 `System.Web.Caching.HttpModulesSection`，而 `<sessionState>` 节有一个配置处理器被设置为 `System.Web`。

### 列表 28-7：machine.config 文件中的 HTTP 模块配置设置

```xml
<sections>
  <sectionGroup>
    <section name="httpModules"
             type="System.Web.Configuration.HttpModulesSection,
                   System.Web.Version=4.0.0.0, Culture=neutral,
                   PublicKeyToken=b0d3f5f7fi3d50a3a" />
  </sectionGroup>
</sections>
```

## 通用配置设置

ASP.NET 应用程序依赖于几个通用配置设置。这些设置在 web.config 和 machine.config 文件中通用的。在本节中，你将查看这些常用配置设置。

### 连接字符串

在 ASP.NET 早期版本中，所有的连接字符串信息都存储在 `<appSettings>` 节中。最新版本的 ASP.NET 包含名为 `<connectionStrings>` 的节，存储各种连接字符串信息。尽管将连接字符串存储在 `<appSettings>` 元素中可行，但它会带来以下挑战：

- 当连接字符串存储在 appSettings 节中时，像 `SqlCacheDependency` 或 `MembershipProvider` 这样具有数据感知能力的控件无法发现这些信息。
- 使用加密算法保护连接字符串是一个挑战。
- 最后，此功能不仅适用于 ASP.NET；它适用于所有 .NET 类型，包括 Windows Forms、Web 服务等。

由于连接字符串信息是独立于 appSettings 节存储的，因此可以使用强类型集合方法 `ConnectionStrings` 进行检索。列表 28-8 给出了如何存储连接字符串的示例。

### 列表 28-8：存储连接字符串

```xml
<configuration>
  <connectionStrings>
    <add name="ExampleConnection" connectionString="server=401kserver;database=401db;uid=Web;pwd=$$wordD9" />
  </connectionStrings>
</configuration>
```

列表 28-9 显示了如何在你的代码中检索连接字符串（ExampleConnection）。

### 列表 28-9：检索连接字符串

VB

```vb
Protected Sub Page_Load(sender As Object, e As EventArgs)
  Dim dbConnection As New SqlConnection(
    ConfigurationManager.ConnectionStrings("ExampleApplication")
    .ConnectionString);
End Sub
```

C#

```csharp
protected void Page_Load(Object sender, EventArgs e)
{
  SqlConnection dbConnection = new
  SqlConnection(ConfigurationManager.ConnectionStrings["ExampleApplication"]
  .ConnectionString);
}
```

这种构造方式具有很大的威力。你不需要将连接字符串硬编码到 ASP.NET 应用程序中的每个页面中，而是可以集中存储一个连接字符串实例（例如在 web.config 文件中）。现在，如果你必须对此连接字符串进行更改，你只需要在一个地方进行此更改，而不是在多个处进行。

### 配置会话状态

由于 Web 应用程序使用 HTTP 协议，你必须将应用程序特定的状态或用户特定的状态存储在可以持久化的地方。`Session` 对象是持久化用户特定信息的常用存储处。Session 存储实现为 Hashtable，并根据键值对存储数据。

ASP.NET 有能力在 InProc 中持久化会话数据，也可以使用 StateServer、SQLServer 或 Custom。Custom 设置为开发者对于如何持久化会话数据提供了更多控制。开箱即用的 ASP.NET 不支持在 XML 存储数据。如果你想将会话数据存储在任何这些 XML 文件中，可以通过编写自定义提供程序来实现（参见本章后文“自定义状态存储”部分）。

你可以使用列表 28-10 所示的 `<sessionState>` 元素配置会话状态。

### 列表 28-10：配置会话状态

```xml
<sessionState mode="StateServer" cookieless="false" timeout="20" stateConnectionString="*"
```

以下列表描述了 `<sessionState>` 元素的某些属性：

- `mode`：指定是否持久化。支持的模式有 InProc、StateServer、SQLServer 和 Custom。
- `cookieless`：指定是否支持无 Cookie。
- `timeout`：指定会话生命周期。例如，每次请求的超时值为 20 分钟，超时将重置。
- `stateConnectionString`：当设置为 StateServer 时，此设置用于标识与服务通信的 TCP/IP 地址。
- `stateNetworkTimeout`：指定尝试存储时的超时（秒）。
- `sqlConnectionString`：当设置为 SQLServer 时，此设置用于连接 SQL 数据库。

## Web 集群支持

作为一组工作的多个 Web 服务器称为 Web 集群。如果你想将你的 ASP.NET 应用程序扩展到多个服务器形成 Web 集群，ASP.NET 开箱支持此。但是，会话数据需要持久化在进程外状态，例如 StateServer 或 SQLServer。

### State Server

StateServer 和 SQLServer 都支持进程外状态。StateServer 将会话信息存储在内存中。使用此选项时，如果托管会话的服务器崩溃，访问网站的所有 ASP.NET 客户端将失败；无法恢复数据。

### SQL Server

当你选择 SQLServer 选项时，会话数据存储在 Microsoft SQL Server 数据库中。即使 SQL Server 崩溃，内置的 SQL Server 恢复功能也能让你恢复所有会话数据。配置 ASP.NET 以支持 SQL Server 会话状态与配置 Windows 服务器一样简单。区别在于你需要运行随 ASP.NET 提供的 T-SQL 脚本 `InstallState.sql`。卸载 ASP.NET SQL Server 支持的 T-SQL 脚本也包含在内。安装和卸载脚本框架中可用。

### 列表 28-11：使用 SQLServer 选项

```xml
<sessionState mode="SQLServer" cookieless="false" timeout="20" stateConnectionString="Data Source=ServerName;Database=DBName;" />
```

## 列表 28-11：使用 SQLServer 选项会话状态

```xml
<configuration>
  <system.web>
    <sessionState
      mode="SQLServer"
      connectionString="data source=ExampleSessionServer;
      user id=ExampleWebUser;password=P@5ssword"
      cookieless="false"
      timeout="20"
    />
  </system.web>
</configuration>
```

ASP.NET 通过存储过程访问存储在 SQL Server 中的会话状态数据。默认情况下，所有会话数据都存储在 Temp DB 数据库中。然而，你可以修改存储过程，使其存储在 Temp DB 之外的完整数据库的表中。

> 尽管基于 SQL Server 的会话状态提供了可扩展的会话使用，但它可能会成为单点故障。这是因为 SQL Server 为同一个 ASP.NET 进程中的所有应用程序使用同一个 SQL Server 数据库。这个问题从 ASP.NET 2.0 之后已经得到了修复，你可以为每个应用程序配置不同的数据库。现在，你可以使用 `aspnet_regsql.exe` 工具为你的所有应用程序配置基于 SQL Server 的会话状态。如果你在使用旧版本的 .NET，可以在 http://support.microsoft.com/kb/836680 处获取修复。

由于连接字符串存储在强类型模式中，因此连接字符串可以在配置文件的其他部分进行引用。例如，在配置将会话状态存储在 SQL Server 时，你可以在 `<connectionStrings>` 部分中指定连接字符串，然后在 `<sessionState>` 元素中指定连接字符串的名称，如列表 28-12 所示。

## 列表 28-12：使用连接字符串配置会话状态

```xml
<configuration>
  <connectionStrings>
    <add name="ExampleSqlSessionState"
      connectionString="data source=ExampleSessionServer;
      user id=ExampleWebUser;password=P@5ssword" />
  </connectionStrings>
  <system.web>
    <sessionState
      mode="SQLServer"
      sqlConnectionString="ExampleSqlSessionState"
      cookieless="false"
      timeout="20"
    />
  </system.web>
</configuration>
```

## 自定义状态存储

ASP.NET 4.5 中的会话状态基于可插的架构，具有继承自 `SessionStateProviderBase` 类的不同提供程序。如果你想创建自己的自定义提供程序或使用第三方提供程序，必须将 `mode` 设置为 `Custom`。

你需要指定继承 `SessionStateProviderBase` 类的自定义程序，如列表 28-13 所示。

## 列表 28-13：使用你自己的会话状态提供程序

```xml
<configuration>
  <system.web>
    <sessionState mode="Custom" customProvider="CustomStateProvider">
      <providers>
        <add name="CustomStateProvider"
             type="CustomStateProviderAssembly,CustomStateProviderNamespace.CustomStateProvider"/>
      </providers>
    </sessionState>
  </system.web>
</configuration>
```

在上一个示例中，你将会话状态模式配置为 `Custom`，因为你指定了提供程序名为 `CustomStateProvider`。从那里开始，你添加了提供程序元素并包含了带有命名空间和类名的提供程序类型。

> 注意 你可以在第 14 章和第 15 章中阅读更多关于提供程序模型和自定义提供程序的内容。

## 编译配置

ASP.NET 支持 ASP.NET 页面、Web 服务、HttpHandlers、ASP.NET 应用程序文件（例如 `Global.asax` 文件）、源文件等的动态编译。这些文件在 ASP.NET 应用程序首次需要它们时会自动编译。

对动态编译文件的任何更改都会导致所有受影响的资源自动失效并重新编译。这使得开发者能够以最小的进程开销快速开发应用程序，因为他们只需点击“保存”即可立即缓存代码更改，使其在应用程序中生效。

你可以使用 `web.config` 或 `config.file` 中的 `<compilation>` 节来配置 ASP.NET 编译设置。ASP.NET 引擎会在需要时编译页面并将生成的代码保存在缓存中。在执行 ASP.NET 页面时会使用这些缓存代码。列表 28-14 显示了 `<compilation>` 节的语法。

## 列表 28-14：<compilation> 节

```xml
<!-- compilation 属性 -->
<compilation
  tempDirectory="[String]"
  debug="false" [true|false]
  cookieieless="false"
  timeout="20"
  mode="SQLServer"
  sqlConnectionString="ExampleSqlSessionState"
  mode="Custom"
  customProvider="CustomStateProvider">
  <providers>
    <add name="CustomStateProvider"
             type="CustomStateProviderAssembly,CustomStateProviderNamespace.CustomStateProvider"/>
  </providers>
</compilation>
```

*(注：此处原文示例 XML 块内容存在重复或不完整，根据指令“不翻译代码块”原则，保持原样)*

现在详细查看这些 `<compilation>` 属性：

- `tempDirectory`: `[String]`
- `debug`: `"false"` [true|false]
- `cookieieless`: `"false"`
- `timeout`: `"20"`
- `mode`: `"SQLServer"`
- `sqlConnectionString`: `"ExampleSqlSessionState"`
- `mode`: `"Custom"`
- `customProvider`: `"CustomStateProvider"`

*(由于提供的原文文本中列表 28-14 之后的描述部分较为杂乱，以下按提供的文本逻辑进行翻译)*

## 自定义错误

当 ASP.NET 应用程序失败时，ASP.NET 页面可以显示带有源代码和错误行的默认错误页面。然而，这种方法存在一些问题：

- 源代码和错误消息对于经验较少的终端用户可能没有任何意义。
- 如果将相同的源代码和错误消息显示给黑客，可能会导致损害。

显示过多的错误信息可能会提供你在大多数情况下不想向公众公开的重要实现细节。图 28-3 显示了一个示例。

![](img/67a6707ff505c052edb96c0128fb3096_1089_0.png)

图 28-3

然而，ASP.NET 良好的基础设施来防止此类错误。`<customErrors>` 节提供了在 ASP.NET 应用程序中定义自定义错误消息的方法。语法如下：

```xml
<customErrors defaultRedirect="[url]" mode="on/off/remote]">
  <error statusCode="[status]" redirect="[url]" />
</customErrors>
```

- `defaultRedirect`: 指定发生错误时将客户端浏览器重定向的 URL。此设置是可选的。
- `mode`: 指定自定义错误的状态是启用、禁用或仅显示给远程机器。可能的值表示自定义错误启用状态的是 On、Off 和 RemoteOnly。RemoteOnly 表示仅向远程客户端显示自定义错误。

# 身份认证
