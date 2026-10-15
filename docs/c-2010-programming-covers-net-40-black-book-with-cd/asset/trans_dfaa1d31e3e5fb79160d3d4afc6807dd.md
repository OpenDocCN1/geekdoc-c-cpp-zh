

表 20.6：ServiceProcessInstaller 类的重要公共方法

| 方法 | 描述 |
|---|---|
| CopyFromComponent | 将当前组件的信息复制以便在服务安装时稍后使用。 |
| Install | 将服务信息写入注册表 |
| Rollback | 回滚已写入注册表的服务信息 |

让我们现在来探索 EventLog 类。

## EventLog 类

EventLog 类用于访问 Windows 事件日志，该日志记录与硬件和软件安装相关的事件信息。此类可帮助您读取和写入现有日志中的条目、删除日志以及响应日志条目。您还可以通过创建事件源来创建新的日志，如果与 EventLog 实例关联的事件日志的源不存在。此事件源在事件日志中注册您应用程序的条目。EventLog 类需要日志名称和机器名称才能从日志中读取。

> 注意
> 您需要在 Windows Vista、Windows XP Professional 或 Windows Server 2003 中拥有管理员权限才能创建事件源。

EventLog 类的继承层次结构如下：

```
System.Object
    System.MarshalByRefObject
        System.ComponentModel.Component
            System.Diagnostics.EventLog
```

表 20.7 描述了 EventLog 类值得注意的公共类方法：

表 20.7：EventLog 类的重要公共类（静态）方法

| 方法 | 描述 |
|---|---|
| CreateEventSource | 使应用程序能够将事件数据写入事件日志 |
| Delete | 删除事件日志 |
| DeleteEventSource | 删除应用程序的事件源注册 |
| Exists | 指定日志是否存在 |
| GetEventLogs | 返回事件日志数组 |
| LogNameFromSourceName | 获取源所注册的日志的名称 |
| SourceExists | 指定特定事件源是否存在 |
| WriteEntry | 向事件日志写入条目 |
| WriteEvent | 向事件日志写入本地化事件条目 |

表 20.8 描述了 EventLog 类的一些重要公共属性：

表 20.8：EventLog 类的值得注意的公共属性

| 属性 | 描述 |
|---|---|
| EnableRaisingEvents | 确定事件日志是否接收 EntryWritten 事件通知 |
| Entries | 获取事件日志的内容 |
| Log | 获取事件日志的名称 |
| LogDisplayName | 获取日志的显示名称 |
| MachineName | 获取日志计算机的名称 |
| MaximumKilobytes | 指定最大事件日志大小 |
| MinimumRetentionDays | 获取在事件日志中保留条目的天数 |
| OverflowAction | 获取当事件日志达到最大日志文件大小时存储新条目的配置行为 |
| Source | 获取写入日志时使用的源名称 |
| SynchronizingObject | 获取用于封送事件处理程序调用的对象 |

表 20.9 描述了 EventLog 类的值得注意的公共方法：

表 20.9：EventLog 类的值得注意的公共方法

| 方法 | 描述 |
|---|---|
| BeginInit | 开始事件日志的初始化操作 |
| Clear | 清除事件日志中的所有条目 |
| Close | 关闭事件日志 |
| Dispose | 释放事件日志使用的资源 |
| EndInit | 结束事件日志的初始化操作 |
| ModifyOverflowPolicy | 更改事件日志存储新条目的配置行为 |
| RegisterDisplayName | 指定事件日志的本地化名称，该名称在服务器事件查看器中显示 |

表 20.10 描述了 EventLog 类的值得注意的公共事件：

表 20.10：EventLog 类的值得注意的公共事件

| 事件 | 描述 |
|---|---|
| EntryWritten | 当向事件日志写入数据时发生 |

要写入事件日志，您可以使用 WriteEntry() 和 WriteEvent() 方法。在这些方法中，您需要使用 Source 属性指定事件日志的事件源。这些方法允许您指定在服务启动、停止或暂停时要显示的消息。

> **注意**
> Application 事件日志是默认事件日志，即，如果您未设置 Log 属性，则条目将写入 Application 事件日志。
> 如果您有一个并不经常需要的事件日志，那么建议在此期间暂停或停止该事件日志。这使您可以节省事件日志占用的内存和其他资源。

让我们现在学习如何安装和卸载 Windows 服务。

## 安装和卸载 Windows 服务

Windows 服务应用程序可以通过转换为安装程序组件在目标计算机上安装。您需要使用 installutil.exe 命令将 Windows 服务应用程序转换为安装组件。通过在 Windows 服务项目中添加默认类 Installer1 来创建安装组件。添加 Installer1 类后，您需要构建应用程序以创建 dll 或可执行文件（exe）。创建 dll 或 exe 文件后，您可以使用 installutil.exe 实用程序或 Windows 安装程序安装 Windows 服务。

### Installutil.exe

installutil.exe 实用程序是一个安装工具，允许您使用命令行语句安装和卸载 Windows 服务。它通过在目标计算机中安装与服务相关的 dll 文件来安装 Windows 服务。installutil.exe 实用程序以事务方式安装 Windows 服务，这意味着如果在安装服务时发生错误或由于其他原因安装失败，installutil.exe 实用程序将回滚服务的整个安装。

### Windows 安装程序

Windows 安装程序为您的应用程序创建部署包，并将项目的 dll 作为自定义操作添加到此部署包中。它使用安装项目创建 Windows 安装程序文件（.msi），这些文件用于使用安装向导安装 Windows 服务。当您开始部署 Windows 服务应用程序时，部署过程会识别 Installer1 类应运行并启动安装组件的安装过程。

让我们在 Immediate 部分学习创建、安装或卸载 Windows 服务应用程序。

## 即时解决方案

### 创建 Windows 服务应用程序

在 Visual C# 2010 中，Windows 服务是通过使用 ServiceBase 类创建的。要创建 Windows 服务，您应重写 OnStart 或 OnStop 事件处理程序，服务启动或停止时分别调用它们。您还可以重写 OnPause 和 OnContinue 事件处理程序以处理服务暂停和恢复时的事件。

> 提示
> 您可以使用 ServiceBase 类的 CanPauseAndContinue 属性暂停和恢复服务；默认情况下，此属性设置为 False。

让我们采取以下总体步骤来创建 Windows 服务：

- 1. 创建新的 Windows 服务项目
- 2. 写入事件日志
- 3. 向 Windows 服务应用程序添加安装程序

### 创建新的 Windows 服务项目

在本节中，您将学习创建名为 MyWindowsService 的 Windows 服务应用程序（也可在 CD 上获得）。

执行以下步骤创建 MyWindowsService 应用程序：

- 1. 打开 Visual Studio 2010 IDE。
- 2. 选择 File→New→Project。New Project 对话框出现（图 20.1）。
- 3. 从 Installed Templates 窗格中选择 Visual C#→Windows 并在 New Project 对话框中选择 Windows Service 模板（图 20.1）。
- 4. 在 Name 文本框和 Location 组合框中分别输入项目的名称和位置。在我们的例子中，项目名称为 MyWindowsService，项目位置为 D:\Black Books\C# 2010\Chapter 20\，如图 20.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1049_0.png)

MyWindowsService 应用程序在 Visual Studio 2010 IDE 中打开。

- 5. 在 Solution Explorer 中右键单击 Service1.cs 文件并选择 View Code 选项以打开 Service1.cs 代码隐藏文件。

