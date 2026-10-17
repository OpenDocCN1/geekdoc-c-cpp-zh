
```xml
<configuration>
  <system.web>
    <authentication mode="Windows" />
    <roleManager defaultProvider="WindowsProvider"
      enabled="true" cacheRolesInCookie="false">
      <providers>
        <add name="WindowsProvider"
          type="System.Web.Security.WindowsTokenRoleProvider" />
      </providers>
    </roleManager>
  </system.web>
</configuration>
```

记住，你必须在 `<roleManager>` 元素中使用 `defaultProvider` 属性声明默认提供程序，以便将分配的提供程序从 `SqlRoleProvider` 关联更改。

## System.Web.Security.AuthorizationStoreRoleProvider

ASP.NET 默认安装后提供的最后一种角色提供程序是 `AuthorizationStoreRoleProvider`。该角色类允许你在授权管理程序策略内部存储角色。这些类型的存储也被称为 AzMan 存储。`WindowsTokenRoleStoreRoleProvider` 比较有限，因为它无法支持任何 AzMan 业务规则。

要使用 `AuthorizationStoreRoleProvider`，你必须首先在 `web.config` 文件中建立到 AzMan XML 数据存储的连接，如列表 14-10 所示。

## 列表 14-10: 与 AzMan 策略存储建立连接

```xml
<configuration>
  <connectionStrings>
    <add name="LocalPolicyStore"
      connectionString="xml://-//App_Data\SampleStore.xml" />
  </connectionStrings>
</configuration>
```

注意，当你处理这些基于 XML 的策略文件时，将它们存储在 `App_Data` 文件夹是最佳策略。存储在 `App_Data` 文件夹中的文件无法被浏览器调用。

连接字符串到位后，下一步是配置你的 `AuthorizationStoreRoleProvider` 实例。这需要列表 14-11 中定义的语法。

## 列表 14-11: 定义 AuthorizationStoreRoleProvider 实例

```xml
<configuration>
  <connectionStrings>
    <add name="MyLocalPolicyStore"
      connectionString="xml://-//App_Data\datafilename.xml" />
  </connectionStrings>
  <system.web>
    <authentication mode="Windows" />
    <identity impersonate="true" />
    <roleManager defaultProvider="AuthorizationStoreRoleProvider"
      enabled="true"
      cacheInCookie="true"
      cookieName="ASPROLES"
      cookieTimeout="30"
      cookiePath="/"
      cookieRequireSSL="false"
      cookieSlidingExpiration="true"
      cookieProtection="All" />
    <providers>
      <clear />
      <add name="System.Web.Security.AuthorizationStoreRoleProvider"
        connectionName="MyLocalPolicyStore"
        applicationName="SampleApplication"
        cacheRefreshInterval="60"
        scopeName="" />
    </providers>
    </roleManager>
  </system.web>
</configuration>
```

（注：由于严重的 OCR 损坏和逻辑不一致，第 593 页和 594 页已省略。）

# 第 14 节 提供模型简介

# 列表 14-13（续）

```
type=System.Web.XmlMapProvider,System.Web,Version=4.0.0.0,
Culture=neutral,PublicKeyToken=b03f5f7f11d50a3a
sitemapFile="AnotherWeb.sitemap" />
<providers>
  <siteMap>
  </system.web>
</configuration>
```

`XmlMapProvider` 在严格设计的 `web.sitemap` 文件中仅允许单个根元素。它所查找的 XML 默认文件名为 `web.sitemap`，尽管你可以使用 `web.config` 文件提供程序声明中的 `siteMapFile` 属性更改此默认设置（如列表 14-13 所示）。

## 会话提供程序 (Session Providers)

为用户存储会话状态的可用模式有 InProc、StateServer、SQLServer 甚至 Custom。每种模式都有其特定的优缺点，在决定使用哪种会话模式时，你应该彻底地检查每个选项。

> 注意：关于会话和 SessionState 的更多信息可以在第 21 章中找到。

此提供程序与本章目前为止讨论的其他提供程序略有不同。`SessionStateModule` 类是一个用于加载可用会话状态模式之一的处理器。这些模式均都定义在这里：

- `System.Web.SessionState.InProcSessionStateStore`: 提供你将会话存储在与 ASP.NET 工作进程相同进程中的能力。这是会话状态管理中性能最好的方法。

- `System.Web.SessionState.OutOfProcSessionStateStore`: 提供你将会话存储在与 ASP.NET 工作进程分离的进程中的能力。这种方法更安全一些，但性能低于 InProc 模式。

- `System.Web.SessionState.SQLSessionStateStore`: 提供你将会话存储在 SQL 中的能力。这是存储会话最安全的方法，但在三种可用方法中性能最差。

图 14-13 显示了这三种会话状态管理模式。

接下来，本章将回顾你可以在 ASP.NET 4.5 应用中开箱即用的三种模式模式。

`System.Web.SessionState.InProcSessionStateStore` 是 ASP.NET 的默认模式。在此模式下，会话保留在与 ASP.NET 工作进程（`aspnet_wp.exe` 或 `w3wp.exe`）相同的进程中。这种模式性能最好，但也存在一些问题。由于会话存储在相同进程中，每当工作进程回收时，所有的会话都会被销。

![](img/67a6707ff505c052edb96c0128fb3096_595_0.png)

![](img/67a6707ff505c052edb96c0128fb3096_595_1.png)

图 14-13

工作进程可能由于许多原因被回收（例如更改了 `web.config` 文件、`Global.asax` 文件，或 IIS 中要求在设定时间段后回收进程的设置）。

列表 14-14 显示了 `web.config` 文件中运行 InProc 模式的配置示例。

# 列表 14-14：在 web.config 中定义会话状态管理的 InProc 模式

```xml
<configuration>
  <system.web>
    <sessionState mode="InProc">
    </sessionState>
  </system.web>
</configuration>
```

如你所示，这非常简单。接下来回顾的方法是进程外模式（out-of-process mode），也称为 SessionServer 模式。

### System.Web.SessionState.OutOfProcessSessionState

除了 InProc 模式外，SessionServer 模式是一种存储会话状态的进程外方法。这种方法的性能不如将会话存储在与 ASP.NET 工作进程相同进程中的方法。这是合理的，因为该方法必须跨越进程边界来处理你正在使用的会话。虽然性能低于 InProc 模式，但 `OutOfProcessSessionState` 方法比使用 `InProcSessionState` 的会话更可靠。如果你的应用程序工作进程回收，该应用程序中的会话仍然会被维持。这种能力对于关键依赖会话的应用程序非常重要。

列表 14-15 显示了使用 `OutOfProcessSessionState` 的示例。

# 列表 14-15：使用 OutOfProcessSessionState 在进程外运行会话

```xml
<configuration>
  <system.web>
    <sessionState mode="SessionServer"
      connectionString="tcp://127.0.0.1:42424*>
    </sessionState>
  </system.web>
</configuration>
```

使用 SessionServer 模式时，你还必须使用 `connectionString` 属性定义会话存储的位置。这意味着会话存储在同一台机器上，但在完全独立的进程中。你可以通过为此属性提供相应的 IP 地址值，轻松地将会话存储在不同的服务器上。除了 IP 地址外，还使用了端口 42424。在对会话使用 SessionServer 模式时，这是要求的。第 21 章涵盖了 SessionServer 的端口。

### System.Web.SessionState.SqlSessionStore

ASP.NET 可为你提供的最后一种会话状态管理提供程序是 `SqlSessionStore`。这种方法无疑是三种方法中最安全的。尽管如此，它的性能最差。如果你使用这种方法，妥善设置数据库是非常重要的。第 21 章将向如何设置数据库。要配置应用程序与 `SqlStore` 工作，你需要如列表 14-16 所示配置 `web.config`。

# 列表 14-16：在 web.config 中定义 SqlStore

```xml
<configuration>
  <system.web>
    <sessionState mode="SQLServer"
      connectionString="Data Source=127.0.0.1;database=MyDatabase;Integrated Security=SSPI">
    </sessionState>
  </system.web>
</configuration>
```

接下来，你将回顾 Web Web 提供程序。

## 事件提供程序

在 ASP.NET 提供的所有系统中，健康系统的提供程序比其他系统都多。健康监控系统允许 ASP.NET 管理员评估运行应用程序的健康状况。默认情况下，ASP.NET 4.5 为健康系统提供了多种提供程序。这比其他系统都多。这些提供程序定义在列表中：

- `System.Management.LogEventProvider`: 提供你使用 ASP.NET 健康监控系统将事件和所有错误记录到 Windows 事件日志的能力。

- `System.Management.SimpleMailEventProvider`: 提供你使用 ASP.NET 健康监控系统通过电子邮件发送错误信息的能力。

- `System.Management.TemplatedMailEventProvider`: 与 `SimpleMailEventProvider` 类似，`TemplatedMailEventProvider` 类提供你通过模板化电子邮件发送错误信息的能力。这些模板使用标准的 `.aspx` 页面定义。

- `System.Management.SqlEventProvider`: 提供你使用 ASP.NET 健康监控系统在 SQL Server 中存储错误信息的能力。对于其他系统的所有 SQL 提供程序，`SqlEventProvider` 默认将错误信息存储在 SQL Server 中。

- `System.Management.TraceEventProvider`: 提供你使用 ASP.NET 健康监控系统将错误信息发送到 ASP.NET 页面跟踪系统的能力。

- `System.Management.IisTraceEventProvider`: 提供你使用 ASP.NET 健康监控系统将错误信息发送到 IIS 跟踪系统的能力。

- `System.Management.WmiEventProvider`: 提供你连接 ASP.NET 健康监控系统与 Windows 管理 (WMI) 事件提供程序的能力。

这七种用于 ASP.NET 健康系统的提供程序要么继承自 `WebEventProvider` 基类，要么继承自 `BufferedWebEventProvider`（后者继承自 `WebEventProvider`），如图 14-14 所示。

# ASP.NET 4.5 中的 Provider 模型 | 549

![](img/67a6707ff505c052edb96c0128fb3096_598_0.png)

图 14-14

`WebEventProvider` 类和 `BufferedWebEventProvider` 之间有什么区别？主要的区别在于，`WebEventProvider` 会在事件发生时立即写入事件，而 `BufferedWebEventProvider` 则持有事件直到收集成一个集合。然后，该集合将以批量的形式写入数据库或通过电子邮件。如果你使用 `SqlEventProvider` 类，你实际上希望进行这种批处理，而不是让提供程序为发生的每个 Web 事件都连接一次数据库并进行写入。

接下来，本章列出了健康监控系统最主要的七个提供程序。

## System.Web.Management.EventLogEventProvider

传统上，管理员和开发人员习惯在内置的 Windows 事件日志中查看系统和应用程序错误。事件日志中的项可以通过“事件查看器”（Event Viewer）查看。你可以通过选择控制面板中的“管理工具”，然后选择“事件查看器”来找到这个基于 GUI 的事件查看工具。

默认情况下，健康监控系统使用 Windows 事件日志来记录服务器配置文件已指定的项，或者你在应用程序的 `web.config` 文件中指定的项。如果你查看服务器上安装的 Microsoft .NET Framework 中 CONFIG 文件夹下的 `web.config` 注释文件，你会发现 `EventLogEventProvider` 在此位置有详细说明。列表 14-17 展示了相关代码。

# 列表 14-17：在 web.config 注释文件中声明的 EventLogEventProvider

# 列表 14-17（续）

```xml
System.Web.Version=4.0.0.0,Culture=neutral,
  PublicKeyToken=b035f7f11d50a3a3" />
<!-- Removed for clarity -->
</profiles>
<profiles>
  <!-- Removed for clarity -->
</profiles>
<rules>
  <add name="All Errors Default" eventName="All Errors"
    minInstances="1"
    provider="EventLogProvider" profile="Default" maxlimit="Infinite" minInterval="00:01:00" custom="" />
  <add name="Failure Audits Default" eventName="Failure Audits"
    minInstances="1"
    provider="EventLogProvider" profile="Default" maxlimit="Infinite" minInterval="00:01:00" custom="" />
</rules>
<eventMappings>
  <!-- Removed for clarity -->
</eventMappings>
<healthMonitoring>
</system.web>
</configuration>
```

如列表 14-17 所示，健康监控系统中可以应用一组可能的设置。项被记录在托管应用程序的服务器日志中。仔细观察列表中的 `<rules>` 部分，你可以看到特定的错误类型被分配进行监控。在这一部分中，健康监控系统捕获了两种类型的错误：`All Errors Default` 和 `Failure Audits Default`。

当 `<rules>` 部分中定义的错误之一被触发并被健康监控系统捕获时，它就会被记录。记录在何处取决于指定的。`<rules>` 部分中 `<add>` 元素使用的 `Provider` 属性决定了这一点。在列表 14-17 示例的两种情况下，都可以看到分配的提供程序是 `EventLogProvider`。这意味着 Windows 错误日志被用于记录这两类型的错误。
