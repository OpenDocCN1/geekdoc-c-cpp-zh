
<trustLevel name="Minimal" policyFile="web_minimaltrust.config" />

</securityPolicy>

<trust level="Full" originUrl="" />

</system.web>

<location>

<allowOverride="false" />

</location>

</configuration>

```

其他策略定义在特定的信任级别上。这些级别决定了 ASP.NET 允许的代码访问安全 (CAS)。要更改 ASP.NET 应用程序在服务器上运行的信任级别，你只需更改文档内或应用程序 `web.config` 文件实例中的 `<trust>` 元素即可。例如，你可以使用列表 33-3 所示的代码更改为中等信任级别。

# 列表 33-3：将信任级别更改为中等

```xml
<configuration>
  <location allowOverride="false">
    <system.web>
      <securityPolicy>
        <trustLevel name="internal" policyFile="internal" />
        <trustLevel name="High" policyFile="web_hightrust.config" />
        <trustLevel name="Medium" policyFile="web_mediumtrust.config" />
        <trustLevel name="Low" policyFile="web_lowtrust.config" />
        <trustLevel name="Minimal" policyFile="web_minimaltrust.config" />
      </securityPolicy>
      <trust level="Medium" originUrl="" />
    </system.web>
  </location>
</configuration>
```

在这种情况下，此代码不仅强制使用 `web_mediumtrust.config` 文件，而且（通过将 `allowOverride` 设置为 `false`）强制服务器上的每个 ASP.NET 应用程序使用此信任级别。单个实例无法通过在本地根 `web.config` 文件中覆盖来更改此设置，因为该设置是在根级别的 `web.config` 中。

如果你查看信任级别配置文件（例如 `web_mediumtrust.config` 文件），请注意它们定义了你可以通过代码操作执行的操作类型。例如，如列表 33-4 所示，`web_hightrust.config` 文件允许服务器上的任意点进行 FileIO 操作。

# 列表 33-4：web_hightrust.config 文件对 FileIO CAS 的定义

```xml
<Permission
  class="FileIOPermission"
  version="1*"
  Unrestricted="true"
/>
```

然而，如果查看中等信任的 web.config 文件 (`web_mediumtrust.config`)，你会发现此配置文件限制 ASP.NET 仅允许应用程序目录内的 FileIO 操作。列表 33-5 展示了此定义。

# 列表 33-5：web_mediumtrust.config 文件中的 FileIO 限制

```xml
<Permission
  class="FileIOPermission"
  version="1*"
  Read=\AppDir\$\$
  Write=\AppDir\$\$
  Append=\AppDir\$\$
  PathDiscovery=\AppDir\$\$
/>
```

在此目录中你可以运行 ASP.NET 应用程序，并更改 `<trust>` 部分以启用适当级别的 CAS 始终是一个好主意。

# 应用程序配置文件

与 `machine.config` 文件不同，每个 ASP.NET 应用程序都有一个存储在名为 `web.config` 文件中的配置设置副本。如果 Web 应用程序跨越多个子文件夹，每个子文件夹都可以有自己的 `web.config` 文件，继承或覆盖父文件的设置。

要用这些新设置更新你的服务器，你只需将此 `web.config` 文件复制到适当的应用程序目录中。ASP.NET 会处理其余工作——不需要重启，也不需要本地服务器访问——你的应用程序将继续正常运行，只是它现在使用了配置文件中应用了的新设置。

# 应用配置设置

当 ASP.NET 运行时为给定的 Web 请求应用配置设置时，`machine.config`（以及任何 `web.config` 文件的配置信息）将合并为一个单元，然后将该信息应用于该应用程序。配置设置继承自任何父 `web.config` 文件或 `machine.config`（它是根配置文件或最终父级）。图 33-1 展示了此的一个示例。

![](img/7040c21013b8e6c23c612d6da3599ff8_1302_0.png)

图 33-1

每个 Web 应用程序的配置都是唯一的；然而，设置继承自父级。例如，如果你的 根目录下的 `web.config` 文件定义了 10 分钟会话超时，那么子目录或子文件夹中继承自 `machine.config` 或根 `web.config` 文件的默认 ASP.NET 设置可以覆盖这些设置，或者继承这些设置（例如 10 分钟会话超时）。

> 虚拟目录的配置设置独立于物理目录结构。除非专门指定虚拟目录的组织方式，否则可能会出现配置问题。

注意，在大多数情况下，可以使用列表 33-3 所示的 `allowOverride = 'false'` 机制来阻止这些继承/覆盖规则。

# 检测配置更改文件

ASP.NET 自动检测配置文件（如 `machine.config` 或 `web.config`）的更改。此逻辑通过监听操作系统提供的文件更改通知事件来实现。

ASP.NET 自动检测配置文件（如 `machine.config` 或 `web.config`）的更改。此逻辑通过监听操作系统提供的文件更改通知事件来实现。

ASP.NET 自动检测配置文件（如 `machine.config` 或 `web.config`）的更改。此逻辑通过监听操作系统提供的文件更改通知事件来实现。

ASP.NET 自动检测配置文件（如 `machine.config` 或 `web.config`）的更改。此逻辑通过监听操作系统提供的文件更改通知事件来实现。

# 配置格式

`machine.config` 和 `web.config` 之间的主要区别在于。除此之外，它们的架构是相同的。配置文件被分为多个组。

## 列表 33-6：一个伪 web.config

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <configSections>
    <sectionGroup>
      <section name="sectionSettings" type="[Class]"/>
    </sectionGroup>
  </configSections>
</configuration>
```

配置中的根元素命名为 `<configuration>`。每个 Web 应用程序的配置都是唯一的；然而，设置继承自父级。例如，如果你的 Web 站点根目录下的 `web.config` 文件定义了 10 分钟会话超时，那么子目录或子文件夹中继承自 `machine.config` 或根 `web.config` 文件的默认 ASP.NET 设置可以覆盖这些设置，或者继承这些设置（例如 10 分钟会话超时）。

> 虚拟目录的配置设置独立于物理目录结构。除非专门指定虚拟目录的组织方式，否则可能会出现配置问题。

注意，在大多数情况下，可以使用列表 33-3 所示的 `allowOverride = 'false'` 机制来阻止这些继承/覆盖规则。

# 通用设置

ASP.NET 依赖于一些通用设置。这些设置对于 `machine.config` 和 `web.config` 文件都是通用的。在本节中，查看这些通用设置。

# 连接字符串

在 ASP.NET 1.0 和 1.1 中，连接字符串信息存储在 `<appSettings>` 部分。然而，从 ASP.NET 2.0 开始，引入了一个名为 `<connectionStrings>` 的部分，用于存储各种连接字符串信息。尽管将连接字符串存储在 `<appSettings>` 元素中是行的，但它带来了以下挑战：

- 当连接字符串存储在 appSettings 部分时，数据感知控件无法使用 `SqlCacheDependency` 或 `MembershipProvider` 来发现这些信息。
- 使用加密算法保护连接字符串是一个挑战。
- 最后，此功能不仅适用于 ASP.NET；它适用于所有的 .NET 类型，包括 Windows Forms、Web 服务等。

由于连接字符串信息独立于 appSettings 部分存储，因此可以通过强类型集合 `ConnectionStrings` 进行检索。列表 33-8 给出了如何存储连接字符串的示例。

# 列表 33-8：存储连接字符串

```xml
<configuration>
  <connectionStrings>
    <add
      name="ExampleConnection"
      connectionString="server=401kServer;database=401kDB;uid=WebUser;pwd=P$$$wOrD$ />
  </connectionStrings>
</configuration>
```

## 1246 | 第 33 章 配置

### 列表 33-9：检索连接字符串

```vb
Public Public Sub Page_Load(sender As Object, e As EventArgs)
    Dim dbConnection As New SqlConnection(ConfigurationManager.ConnectionStrings("ExampleConnection").ConnectionString)
End Sub
```

```csharp
public void Page_Load(Object sender, EventArgs e)
{
    SqlConnection dbConnection = new SqlConnection(ConfigurationManager.ConnectionStrings("ExampleConnection").ConnectionString);
}
```

这种类型的配置功能非常强大。你不再需要将连接字符串硬编码到 ASP.NET 应用程序中的每一个页面中，而是可以在集中存储一个连接字符串的实例（例如，在 web.config 文件中）。现在，如果你必须更改此连接字符串，可以在一处进行更改，而无需多处修改。

## 配置会话状态

由于 Web 应用程序使用无状态的 HTTP 协议，你必须将特定于应用程序的用户状态存储在可以持久化的地方。Session 对象基于键/值对。ASP.NET 1.0 和 1.1 要求你将会话数据持久化在 InProc（进程）、StateServer（状态服务器）和 SQLServer 中。从 ASP.NET 2.0 开始，你可以添加一个名为 Custom（自定义）的新功能。Custom 设置为开发者对会话状态的持久化方式提供了更多控制权。例如，ASP.NET 原生不支持在 Oracle、DB2 或 Sybase 等非微软数据库上的会话数据。如果你想将会话数据存储在这些任何一个数据库或自定义存储中，可以通过编写自定义提供程序来实现。（请参阅本章后文“自定义状态”部分以及第 2 章以了解更多关于 ASP.NET 4 会话状态的信息。）

你可以使用列表 33-10 所示的 `<sessionState>`元素来配置会话信息。

### 列表 33-10：配置会话状态

```xml
<sessionState mode="StateServer"
             cookieless="false"
             timeout="20"
             stateConnectionString="tcp://ExampleStore:4244"
             stateNetworkTimeout="60" />
```

以下列表描述了 `<sessionState>` 元素的一些属性：

- **mode**: 指定会话信息应该持久化的位置。mode 设置支持选项：Off（关闭）、InProc、StateServer 和 Custom。默认选项是 InProc。
- **cookieless**: 指定是否支持不使用 Cookie 的会话。
- **timeout**: 指定会话的周期。timeout 是一个滑动值；在每次请求时，超时时间都会重置为当前时间加上超时值。例如，如果超时值为 20 分钟，且在上午 10:10 接收到请求，则超时将在上午 10:30 发生。
- **stateConnectionString**: 当 mode 设置为 StateServer 时，此设置用于识别与状态服务通信的 TCP/IP 地址和端口。
- **stateNetworkNetworkTimeout**: 指定在尝试在 StateServer 这样的进程外会话中存储状态时的值（秒为单位）。
- **sqlConnectionString**: 当 mode 设置为 SQLServer 时，此设置用于连接到 SQL Server 数据库以存储和检索数据。

## Web 农场支持

多个服务器作为一个组工作被称为 Web 农场（Web Farm）。如果你希望将 ASP.NET 应用程序扩展到多个服务器，ASP.NET 原生支持这种部署。会话数据需要持久化在 StateServer 或 SQLServer 等进程外会话状态中。

## 状态服务器 (State Server)

StateServer 和 SQLServer 都支持进程外会话状态。然而，StateServer 将所有信息存储在 Windows 服务中，该服务将数据存储在内存中。这意味着如果 Web 农场中托管状态服务的服务器崩溃，访问网站的 ASP.NET 客户端将失败；没有办法恢复数据。

如果你使用的是 Windows XP 和 Windows 7，可以通过选择“控制面板 > 管理工具 > 服务”对话框来配置会话状态服务（如图 33-2 所示）。

![](img/7040c21013be6c23c612da3599ff8_1306_0.png)

图 33-2

或者，你可以通过使用命令提示符输入 `net start` 命令来启动状态服务：

```cmd
C:\Windows\Microsoft.NET\v4.0.30319\net start aspnet_state
```

ASP.NET 状态服务正在启动。

ASP.NET 状态服务已成功启动。

> 所有兼容版本的 ASP.NET 共享一个状态服务实例，该实例是随着最高版本的 ASP.NET 安装的服务。例如，如果你在已经在运行 ASP.NET 2.0 和 1.1 的服务器上安装了 ASP.NET 4，则 ASP.NET 4 安装将替换 ASP.NET 2.0 状态服务实例。ASP.NET 4 服务保证适用于所有之前的 ASP.NET 版本。

## SQL Server

当你选择 SQLServer 选项时，会话数据存储在 Microsoft SQL Server 数据库中。即使 SQL Server 崩溃，内置的 SQL Server 功能也能让你恢复所有数据。配置 ASP.NET 支持 SQL Server 会话就像配置 Windows 服务一样简单。唯一的区别在于你需要运行随 ASP.NET 附带的 T-SQL 脚本 `InstallSqlState`。还包含了用于卸载 ASP.NET SQL Server 支持的 T-SQL 脚本，称为 `UninstallSqlState`。安装和卸载脚本位于 Framework 文件夹中。列表 33-11 显示了使用 SQL Server 选项的示例。

```xml
<configuration>
  <system.web>
    <sessionState
      mode="SQLServer"
      connectionString="data source=ExampleSessionServer;
      user id=ExampleUser;password=P@sswordD"
      cookies="false"
      timeout="20"
    />
  </system.web>
</configuration>
```

### 列表 33-11：使用 SQL Server 选项

ASP.NET 通过存储过程访问存储在 SQL Server 数据。默认情况下，状态存储在 TempDB 中。然而，你可以修改存储过程使其存储在其他完整的数据库中。

> 尽管基于 SQL Server 的提供程序提供了可扩展的会话使用，但它可能是单点故障。这个问题在 ASP.NET 2.0 之后已经解决，你可以为每个应用程序配置不同的数据库。然而，如果你在为旧版框架寻找解决方案，可以在 http://support.microsoft.com/kb/83680 获取。

在之前的示例中，由于你在 `<connectionStrings>` 部分指定了连接字符串，因此可以在 `<sessionState>` 元素中指定该连接字符串的名称，如列表 33-12 所示。

### 列表 33-12：使用连接字符串配置会话状态

```xml
