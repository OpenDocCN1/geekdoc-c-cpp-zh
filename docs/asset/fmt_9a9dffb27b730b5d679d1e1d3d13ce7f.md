
> 注意：在学习其余提供程序时，请注意，健康监控系统在处理提供程序时的行为与本章中介绍的其他系统不同。在 ASP.NET 4.5 中使用健康监控系统时，你可以同时分配多个提供程序。这意味着你可以在 `web.config` 文件中指定错误不仅记录到 Windows 事件日志中，还记录到你指定的任何其他数据存储。例如，对于相同的 Web 事件类型，你可以同时将该 Web 事件记录到 Windows 事件日志和 SQL Server。

## System.Web.Management.SimpleMailWebEventProvider

有时当应用程序发生错误时，管理员或关心的开发人员可能希望接收该问题的电子邮件通知。在使用像 `EventLogWebEventProvider` 的工具将事件记录到磁盘的同时，你也可以使用 `SimpleMailWebEventProvider` 将错误通知通过电子邮件发送给你。正如提供程序名称所示，电子邮件的构建非常简单。列表 14-18 显示了你如何在将错误写入 Windows 事件日志的同时，添加电子邮件通知。

### 列表 14-18：SimpleMailWebEventProvider 的定义

```xml
<configuration>
  <system.web>
    <healthMonitoring heartbeatInterval="0" enabled="true">
      <bufferModes>
        <add name="Website Error Notification"
          maxBufferSize="100"
          maxFlushSize="20"
          urgentFlushThreshold="1"
          regularFlushInterval="00:01:00"
          urgentFlushInterval="00:01:00"
          maxBufferThreads="1" />
      </bufferModes>
      <providers>
        <clear />
        <add name="EventLogProvider"
          type="System.Web.Management.EventLogWebEventProvider,System.Web,Version=4.0.0.0,
          Culture=neutral,PublicKeyToken=b03f5f7f11d50a3a" />
        <add name="SimpleMailWebEventProvider"
          type="System.Web.Management.SimpleMailWebEventProvider,System.Web,Version=4.0.0.0,
          Culture=neutral,PublicKeyToken=b03f5f7f11d50a3a"
          from="admin@yourcompany.com"
          to="admin@yourcompany.com"
          subject="Web Event Notification"
          bufferMode="Website Error Notification" />
      </providers>
    </healthMonitoring>
  </system.web>
</configuration>
```

（注：由于原始文本包含大量的 OCR 错误重复和混乱，上述内容已根据逻辑进行了清理和重构，以提供干净的翻译版本。）

### 列表 14-20：定义的 LocalSqlServer 实例

```xml
<configuration>
  <connectionStrings>
    <add name="LocalSqlServer"
         connectionString="Data Source=127.0.0.1;Integrated Security=SSPI;"
         allowCustomSqlDatabase="true" />
  </connectionStrings>
</configuration>
```

配置好此连接后，下一步是在 `web.config` 文件的 `SqlWebEventProvider` 声明中使用此连接，如列表 14-21 所示。

### 列表 14-21：使用 SqlWebEventProvider 向 SQL Server 2012 写入 Web 事件

```xml
<configuration>
  <system.web>
    <healthMonitoring>
      <!-- 为了清晰起见删其他节点 -->
      <providers>
        <add name="SqlWebEventProvider"
           type="System.Web.Management.SqlWebEventProvider,System.Web"
           connectionStringName="LocalSqlServer"
           maxEventLength="1037741823"
           bufferMode="SQL Analysis" />
      </providers>
    </healthMonitoring>
  </system.web>
</configuration>
```

现在事件将代表你记录在 SQL Server 2012 中。这样做的好处在于，与 `SimpleMailWebEventProvider` 和 `TemplatedMailWebEventProvider` 一样，`SqlWebEventProvider` 继承自 `BufferedWebEventProvider`。这意味着事件可以批量写入，而不是逐个写入。你通过提供程序声明中的 `buffer` 和 `bufferMode` 属性来触发这些批处理。它与 `<healthMonitoring>` 声明中 `<bufferModes>` 部分适用的设置配合工作。

## System.Web.Management.TraceWebEventProvider

调试 ASP.NET 应用程序的一种方法是使用系统内置的跟踪功能。跟踪允许你查看请求、应用程序状态、Cookie、控件树、集合等的详细信息。你使用 `TraceWebEventProvider` 对象将 Web 事件输出到跟踪输出中。在配置文件中设置 `TraceWebEventProvider` 实例的方法如列表 14-22 所示。

### 列表 14-22：使用 TraceWebEventProvider 向跟踪输出写入 Web 事件

```xml
<configuration>
  <system.web>
    <healthMonitoring>
      <!-- 为了清晰起见删其他节点 -->
      <providers>
        <add name="TraceWebEventProvider"
           type="System.Web.Management.TraceWebEventProvider,System.Web"
           maxEventMessagesPerNotification="1" />
      </providers>
    </healthMonitoring>
  </system.web>
</configuration>
```

## System.Web.Management.WmiWebEventProvider

健康监控系统的最后一个提供程序是 `WmiWebEventProvider`。该提供程序允许你将来自健康监控系统的任何 Web 事件映射到 Windows 管理规范 (WMI) 事件。当你将事件传递给 WMI 子系统时，你可以将事件表示为对象。

默认情况下，`WmiWebEventProvider` 已经为你配置好了，你只需要将感兴趣的 Web 事件映射到健康监控声明中 `<rules>` 部分已声明的 `WmiWebEventProvider` 即可。此声明包含在服务器上安装的 Microsoft .NET Framework CONFIG 文件夹下的 `machine.config` 文件中，如列表 14-23 所示（`WmiWebEventProvider` 以粗体显示）。

### 列表 14-23：machine.config 注释文件中的 WmiWebEventProvider 定义

```xml
<configuration>
  <system.web>
    <healthMonitoring>
      <!-- 为了清晰起见删除了节点 -->
      <providers>
        <clear />
        <add name="EventLogProvider"
             type="System.Web.Management.EventLogWebEventProvider,
             System.Web, Version=4.0.0.0,Culture=neutral,
             PublicKeyToken=b03f5f7f11d50a3a" />
        <add connectionStringName="LocalSqlServer"
             maxEventDetailsLength="32768" buffer="false"
             bufferMode="Notification" name="SqlWebEventProvider"
             type="System.Web.Management.SqlWebEventProvider,
             System.Web, Version=4.0.0.0,Culture=neutral,
             PublicKeyToken=b03f5f7f11d50a3a" />
        <add name="WmiWebEventProvider"
             type="System.Web.Management.WmiWebEventProvider,
             System.Web, Version=4.0.0.0,Culture=neutral,
             PublicKeyToken=b03f5f7f11d50a3a" />
      </providers>
    </healthMonitoring>
  </system.web>
</configuration>
```

请记住，健康监控系统使用提供程序模型的奇妙之处在于，它允许对系统捕获的事件使用多个提供程序。

## 配置提供程序

ASP.NET 4.5 的一个极佳的功能是它允许你实际上对配置文件的部分进行加密。你可以加密 `web.config` 文件中定义的 ASP.NET 部分，也可以加密你自己放在文件中的自定义部分。这是保持敏感配置信息免受所有人视线的理想方式。

默认情况下，ASP.NET 4.5 提供了两种开箱即用的提供程序：

- `System.Configuration.DpapiProtectedConfigurationProvider`：使用数据保护 API (DPAPI) 加密。
- `System.Configuration.RsaProtectedConfigurationProvider`：使用 RSA 加密。这两种提供程序在图 14-15 中显示。

![图 14-15](img/67a707ff505c0ed96)

> **注意**：你可以在第 2 章找到关于使用这些提供程序的信息。

### System.Configuration.DpapiProtectedConfigurationProvider

`DpapiProtectedConfigurationProvider` 类允许你使用数据保护 API (DPAPI) 加密配置。这种提供程序是针对机器的。

该提供程序的两个主要属性如下：

- `useMachineProtection`：默认设置为 `true`，这意味着所有机器上的应用程序共享同一个密钥。将 `useMachineProtection` 设置为 `false` 意味着加密仅针对应用程序。
- `entropy`：`entropy` 属性可以接受任何字符串值来参与加密解密。

### System.Configuration.RsaProtectedConfigurationProvider

`RsaProtectedConfigurationProvider` 使用三重 DES 加密配置文件的指定部分。此提供程序只有几个可用的属性。

- `keyContainerName` 属性是用于加密解密过程定义的密钥。默认情况下，此提供程序使用 .NET Framework 内置的密钥容器，但你可以通过此属性轻松地切换到另一个密钥。
- `cspProviderName` 属性只有在你配合 Windows 加密 API (CAPI) 使用自定义加密服务程序 (CSP) 时才有效。如果是这样，将 CSP 的名称作为 `cspProviderName` 属性的值。
- `useMachineContainer` 属性允许你指定想要一个机器范围或用户特定的密钥容器。此属性类似于在 `DpapiProtectedConfigurationProvider` 中发现的 `useMachineProtection` 属性。
- `useOAEP` 属性指定在执行加密/解密过程时是否开启可选非对称加密和填充（OAEP）能力。

## 配置提供程序总结

如你在本章所示，你可以轻松地在 ASP.NET 4.5 中将这些系统关联到大量的可用提供程序上。从那里开始，你还可以通过提供程序暴露的属性来配置关联提供程序的行为。你可以通过系统范围的配置文件（如 `machine.config` 文件）或更特定于应用程序配置文件（如 `web.config` 文件）轻松地完成这些配置。

## 总结

本章介绍了提供程序模型的基础知识，以及在你开始使用各种可用的 ASP.NET 系统时有哪些提供程序可供选择。了解每个系统内置的可用提供程序，以及你如何微调每个提供程序的行为是非常重要的。

这种提供程序模型允许了额外的抽象层级，并允许你自行决定用于各种系统的底层数据存储器。例如，你有权决定将成员和角色管理信息存储在 SQL Server 还是 Oracle 中，而无需对业务逻辑或表现逻辑进行任何更改！

下一章将展示如何将提供程序模型提升到新的层次。

# 第 15 章 扩展提供程序模型

本章内容包括：

- 修改和扩展提供程序
- 构建你自己的提供程序

## 本章的 WROX.COM 代码下载

请注意，本章中的所有代码示例均作为书籍网站（www.wrox.com）上“Download Code”选项卡中本章代码下载的一部分提供。

上一章介绍了 ASP.NET 4.5 中使用的提供程序模型，并解释了它如何与成员和角色管理系统配合使用。

如上一章讨论，ASP.NET 4.5 中的这些系统需要长时间维护某种类型的用户状态。它们对状态存储的时间间隔和安全性要求高于那些简单使用 `Session` 对象的早期系统。默认情况下，ASP.NET 4.5 为你提供了一系列提供程序，用于为这些系统因状态管理而产生的任何数据存储提供底层连接器。

.NET Framework 4.5 默认安装带的提供程序包含了与任何一个系统工作所需的最常见状态管理数据存储。但在 .NET 中，大多数情况下，你都可以自定义和扩展提供的提供程序。

本章探讨了扩展 ASP.NET 4.5 中发现提供程序模型的某些方法。本章还回顾了提供程序模型的几个示例扩展。不过，首先你将查看修改和扩展 .NET 4.5 默认安装中已有的提供程序的一些简单方法。

## 提供程序是更大架构中的一层

记住上一章的内容，提供程序允许你为 ASP.NET 4.5 中的许多系统定义数据访问层。它们还允许你定义关于如何操纵或处理数据的核心业务逻辑实现。它们允许你以统一的方式使用构成这些系统的各种控件和 API，无论提供程序的底层数据存储方法如何。提供程序模型还允许你轻松地将一个提供程序交换为另一个，而不影响与提供程序交互的底层控件和 API。见图 15-1。

![图 15-1](img/67a6707ff505c052edb96c0128fb3096_609_0.png)

从此图中，你可以看到成员系统使用的控件以及 `Membership` API 都使用了定义的提供程序。更改底层提供程序不会更改控件或 API，但你完全可以修改这些项的行为（正如你很快将看到的）。你也可以简单地更改这些项所需的状态管理的存储位置。

> **注意** 除了本章涵盖的示例，你还可以使用 [ASP.NET 通用提供程序](https://www.microsoft.com/example)（通过在 Package Manager 中安装 `Microsoft.AspNet.Providers` 包）。通用提供程序不会更改 API，但它们替换了内置提供程序的数据存储机制。如上一章所述，你可以在第 18 章和第 19 章找到有关此主题更多信息。

## 通过基于属性的编程修改

修改 .NET Framework 4.5 内置提供程序行为最简单的方法可能是基于属性的编程。在 ASP.NET 4.5 中，你可以通过属性使用应用高级修改，通过 `machine.config` 文件或根 `web.config` 文件中的提供程序定义，更改提供程序的行为。本章提供了一个如何修改 `SqlMembershipProvider` 的示例。

### 通过 SqlMembershipProvider 实现简单的密码结构

当你使用 `SqlMembershipProvider` 实例创建用户时，无论使用的是 SQL Server Express 还是微软的 SQL Server 2005、2008，请注意创建用户所需的密码是“半强型”密码。当你通过 ASP.NET 网站管理工具创建用户时，这种要求会被拒绝，如图 15-2 所示。有关 ASP.NET 网站管理工具的更多信息，请查看附录 D。

![图 15-2](img/67a6707ff505c052edb96c0128fb3096_610_0.png)

在此屏幕上，我收到密码不符合要求的通知。当你通过 ASP.NET 网站管理工具创建用户时，这会被拒绝。有关 ASP.NET 网站管理工具的更多信息，请查看附录 D。

查看此提供程序的属性，注意 `minRequiredPasswordLength` 和 `minRequiredNonAlphanumericCharacters` 定义了这种行为。要更改所有应用程序的这种行为，只需在 `machine.config` 中更改这些值。然而，我们建议在应用程序的 `web.config` 中更改这些值，如列表 15-2 所示。

### 列表 15-2：在 web.config 中修改 SqlMembershipProvider 密码策略

```xml
<configuration>
  <system.web>
    <membership defaultProvider="CustomSqlMembershipProvider">
      <providers>
        <add name="CustomSqlMembershipProvider"
             type="System.Web.Security.SqlMembershipProvider"
             connectionStringName="LocalSqlServer"
             enablePasswordRetrieval="false"
             enablePasswordReset="true"
             requiresQuestionAndAnswer="true"
             applicationName="/"
             requiresUniqueEmail="false"
             minRequiredPasswordLength="7"
             minRequiredNonAlphanumericCharacters="1"
             passwordFormat="Hashed"
             maxInvalidPasswordAttempts="5"
             passwordAttemptWindow="10"
             passwordStrengthRegularExpression="" />
      </providers>
    </membership>
  </system.web>
</configuration>
```
