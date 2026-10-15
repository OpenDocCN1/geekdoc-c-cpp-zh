
`Default.aspx`页面的设计视图出现，如图 19.45 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1040_0.png)

图 19.45：显示 `Default.aspx` 文件的设计视图

- 2. 将 `MyAjaxEnableWCFService` 网站的 `Default.aspx` 文件设为你的主页。
- 3. 按 `F5` 键或从菜单栏中选择 `Debug→Start Debugging` 选项来运行应用程序。`MyAjaxEnableWCFService` 网站的输出出现，如图 19.46 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1041_0.png)

图 19.46：显示 `MyAjaxEnableWCFService` 网站的输出

现在，你可以执行 `OperationService` 服务中指定的操作，例如加法、减法、乘法和除法。

## 摘要

在本章中，你学习了 `WCF` 服务。你还学习了 `WCF` 服务的实例化模型。接下来，你学习了 `WCF` 架构。此外，你学习了 `WCF` 端点，包括端点地址、绑定、服务契约、行为、`WCF` 服务配置、`WCF` 客户端、`WCF` 服务标识以及 `WCF` 与 `ASP.NET AJAX` 的集成。最后，你学习了如何创建 `WCF` 服务并使用 `ASP.NET AJAX` 调用它。

在下一章中，你将学习 Windows 服务。

# 20 Windows 服务

| 如果你需要即时解决方案： | 参见页面： |
|---|---|
| 创建 Windows 服务应用程序 | 1008 |
| 使用 `Installutil.exe` 安装 Windows 服务 | 1012 |
| 使用 Windows Installer 安装 Windows 服务 | 1013 |
| 使用 SCM 管理 Windows 服务 | 1018 |
| 使用 `Installutil.exe` 和 Windows Installer 卸载 Windows 服务 | 1021 |

## 深入解析

当 Windows 操作系统启动时，与操作系统相关的各种服务也会自动启动。这些服务称为 Windows 服务，它们执行特定功能，不需要用户干预。Windows 服务没有用户界面，也不会产生任何可视化输出。此外，当系统启动时，这些服务会在后台自动运行，并且不需要用户登录系统。Windows 服务的一些示例包括服务器产品，如 Microsoft Exchange、`SQL Server` 和其他应用程序；例如，设置计算机时钟的 Windows 日期和时间服务。当 Windows 服务启动时，它会在事件日志中创建一条日志条目，指示该服务已启动。该服务还会在运行期间按指定间隔创建日志条目，最后在停止时也创建日志条目。

`Visual Studio 2010` 使您能够将 Windows 服务创建为应用程序，并允许您定义代码，以控制在向服务发送 `start`、`pause`、`resume` 和 `stop` 等命令时要执行的操作。您可以使用 `ServiceBase`、`ServiceInstaller`、`ServiceProcessInstaller` 和 `EventLog` 类来创建 Windows 服务应用程序。在 Windows 服务应用程序中，您还可以将服务配置为在操作系统启动时自动启动，或者配置为手动启动服务。由于 Windows 服务没有任何界面，因此它不能像普通应用程序那样进行调试，而是作为进程进行调试。此外，您可以使用 `Installutil.exe` 实用工具或 Windows Installer 从目标 Windows 系统安装或卸载 Windows 服务应用程序。

在本章中，您将学习使用 `ServiceBase`、`ServiceInstaller`、`ServiceProcessInstaller` 和 `EventLog` 类，在 `Visual Studio 2010` 中创建 Windows 服务的各种类。`ServiceBase` 类允许您定义 Windows 服务的行为以及 `Start`、`Pause` 和 `Stop` 等命令。`ServiceInstaller` 和 `ServiceProcessInstaller` 类分别用于安装 Windows 服务以及服务中的特定进程。接下来，将介绍 `EventLog` 类，它使您能够从 Windows 服务访问 Windows 事件日志。最后，您将学习使用 `Installutil.exe` 和 Windows Installer 安装和卸载 Windows 服务。

让我们从 `ServiceBase` 类开始。

## ServiceBase 类

`ServiceBase` 类是创建 Windows 服务的基类。它继承自 `Component` 类。`ServiceBase` 类的继承层次结构如下：

```
System.Object

    System.MarshalByRefObject

        System.ComponentModel.Component

            System.ServiceProcess.ServiceBase
```

`ServiceBase` 类提供了各种属性、方法和命令来控制 Windows 服务的行为。向 Windows 服务发出的命令包括 `Start`、`Pause` 和 `Stop`。这些命令由服务控制管理器 `SCM` 处理，`SCM` 充当 Windows 服务的中央组织者。

表 20.1 中列出了 `ServiceBase` 类的一些重要公共属性：

**表 20.1：ServiceBase 类的重要公共属性**

| 属性 | 描述 |
|---|---|
| `AutoLog` | 指定是否在事件日志中记录 `Start`、`Stop`、`Pause` 和 `Continue` 命令 |
| `CanHandlePowerEvent` | 确定 Windows 服务能否处理计算机电源状态更改的通知 |
| `CanHandleSessionChangeEvent` | 确定 Windows 服务能否处理终端服务器会话返回的会话更改事件 |
| `CanPauseAndContinue` | 确定是否可以暂停和继续 Windows 服务 |
| `CanShutdown` | 确定当系统关闭时是否应通知 Windows 服务 |
| `CanStop` | 确定 Windows 服务是否可以停止 |
| `EventLog` | 获取一个事件日志，您可以使用它向应用程序事件日志写入信息 |
| `ExitCode` | 确定 Windows 服务的退出代码 |
| `ServiceName` | 指定 Windows 服务的名称 |

表 20.2 描述了 `ServiceBase` 类的一些重要公共方法：

**表 20.2：ServiceBase 类的重要公共方法**

| 方法 | 描述 |
|---|---|
| `Dispose` | 释放 `ServiceBase` 类使用的资源 |
| `RequestAdditionalTime` | 请求额外时间以完成挂起的操作 |
| `Run` | 向 `SCM` 注册 Windows 服务的可执行文件 |
| `ServiceMainCallback` | 向 Windows 操作系统注册命令处理程序并启动相应的 Windows 服务 |
| `Stop` | 停止 Windows 服务 |

现在让我们探索另一个类：`ServiceInstaller`。

## ServiceInstaller 类

`ServiceInstaller` 类用于安装 Windows 服务应用程序。此类用于将与 Windows 服务关联的注册表值写入 `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services` 注册表项。Windows 服务通过分配给 `ServiceInstaller` 类的 `ServiceName` 属性的名称来标识。您可以通过创建继承自 `Installer` 类的项目安装程序类来安装 Windows 服务。

`ServiceInstaller` 类的继承层次结构如下：

```
System.Object

  System.MarshalByRefObject

    System.ComponentModel.Component

      System.Configuration.Install.Installer

        System.Configuration.Install.ComponentInstaller

          System.ServiceProcess.ServiceInstaller
```

表 20.3 描述了 `ServiceInstaller` 类的一些重要公共属性：

**表 20.3：ServiceInstaller 类的重要公共属性**

| 属性 | 描述 |
|---|---|
| `Description` | 指定 Windows 服务的描述 |
| `DisplayName` | 指定 Windows 服务的显示名称 |
| `ServiceName` | 指定用于标识 Windows 服务的名称 |
| `ServicesDependedOn` | 指定为支持主 Windows 服务而必须运行的服务 |
| `StartType` | 指定 Windows 服务的启动类型 |

表 20.4 描述了 `ServiceInstaller` 类的重要公共方法：

**表 20.4：ServiceInstaller 类的重要公共方法**

| 方法 | 描述 |
|---|---|
| `CopyFromComponent` | 在重写时，将属性从 `ServiceBase` 实例复制到 `ServiceInstaller` 类 |
| `Install` | 安装关联的 Windows 服务 |
| `IsEquivalentInstaller` | 确定两个安装程序是否可以安装同一服务 |
| `Rollback` | 回滚安装过程写入注册表的服务应用程序信息 |
| `Uninstall` | 卸载 Windows 服务 |

> 注意
> 安装 Windows 服务时，会自动创建 `EventLogInstaller` 类，以安装与该特定服务相关的事件日志。

让我们探索 `ServiceProcessInstaller` 类。

## ServiceProcessInstaller 类

`ServiceProcessInstaller` 类用于安装在 Windows 服务中的特定进程。它还执行可执行文件中所有服务共有的任务，例如提供系统信息和打印文档。与 `ServiceInstaller` 类类似，`ServiceProcessInstaller` 类也用于在计算机上写入与服务相关的注册表值，服务必须安装在该计算机上。`ServiceProcessInstaller` 类还允许您指定服务在 Windows 操作系统上运行时应使用的特定用户名和密码、计算机系统帐户、本地或网络服务帐户或用户帐户。

`ServiceProcessInstaller` 类继承自 `ComponentInstaller` 类。`ServiceProcessInstaller` 类的继承层次结构如下：

```
System.Object

  System.MarshalByRefObject

    System.ComponentModel.Component

      System.Configuration.Install.Installer

        System.Configuration.Install.ComponentInstaller

          System.ServiceProcess.ServiceProcessInstaller
```

表 20.5 中列出了 `ServiceProcessInstaller` 类的一些重要公共属性：

**表 20.5：ServiceProcessInstaller 类的重要公共属性**

| 属性 | 描述 |
|---|---|
| `Account` | 获取服务的帐户类型 |
| `HelpText` | 获取服务选项的帮助文本 |
| `Password` | 获取用户帐户的密码 |
| `Username` | 获取服务应用程序运行所使用的用户帐户 |

表 20.6 描述了 `ServiceProcessInstaller` 类的重要公共方法：

表 20.6：`ServiceProcessInstaller` 类的重要公共方法

| 方法 | 描述 |
|---|---|
| `CopyFromComponent` | 将当前组件的信息复制以便在服务安装时稍后使用。 |
| `Install` | 将服务信息写入注册表 |
| `Rollback` | 回滚已写入注册表的服务信息 |

让我们现在来探索 `EventLog` 类。

## EventLog 类

`EventLog` 类用于访问 Windows 事件日志，该日志记录与硬件和软件安装相关的事件信息。此类可帮助您读取和写入现有日志中的条目、删除日志以及响应日志条目。您还可以通过创建事件源来创建新的日志，如果与 `EventLog` 实例关联的事件日志的源不存在。此事件源在事件日志中注册您应用程序的条目。`EventLog` 类需要日志名称和机器名称才能从日志中读取。

> 注意
> 您需要在 Windows Vista、Windows XP Professional 或 Windows Server 2003 中拥有管理员权限才能创建事件源。

`EventLog` 类的继承层次结构如下：

```
System.Object

    System.MarshalByRefObject

        System.ComponentModel.Component

            System.Diagnostics.EventLog
```
