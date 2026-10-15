

## 安装服务

安装服务的实用工具 `InstallUtil.exe` 必须从命令行运行。`InstallUtil.exe` 位于 .NET 实用工具目录中，在 Windows 2000 和 NT 系统上位于 `C:\WINNT\Microsoft.NET\Framework\v4.0.xxxxx`，或在 Windows XP、Windows Vista、Windows 7、Windows Server 2003 和 Windows Server 2008 上位于 `C:\Windows\Microsoft.NET\Framework\v4.0.xxxxx`（“xxxxx” 是已安装的 .NET Framework 版本号的占位符）。

您需要一个命令窗口来访问此实用工具。可以通过选择 Microsoft Visual Studio 2010 → Visual Studio Tools → Visual Studio 命令提示符（2010）获得。根据您的安全设置，您可能希望右键单击命令窗口的链接，并选择以管理员身份运行。

在命令窗口中，切换到包含 `FileWatcherService.exe` 的目录。默认情况下，使用 Visual Studio 2010 时，如果您当前在 Visual Studio 中使用的是 Debug 配置，您会在 `C:\Users\[ user ]\Documents\Visual Studio 2010\Projects\FileWatcherService\FileWatcherService\obj\Debug` 找到此可执行文件，或如果您当前使用的是 Release 配置，则在 `C:\Users\[ user ]\Documents\Visual Studio 2010\Projects\FileWatcherService\FileWatcherService\obj\Release` 中找到。找到后，运行以下命令：

```
InstallUtil FileWatcherService.exe
```

检查 `InstallUtil.exe` 生成的消息以确保服务安装成功。该实用工具会生成几行信息；如果成功，最后两行如下：

```
The Commit phase completed successfully.
The transacted install has completed.
```

如果前两行未出现，则需要阅读实用工具生成的所有信息以找出安装失败的原因。原因可能包括可执行文件的路径错误，或尝试在服务已安装时安装服务（必须先卸载服务，然后才能重新安装；卸载过程将在后面描述）。此外，如果您未为命令窗口选择以管理员身份运行，您可能会收到与安全权限不足相关的错误。

> 如果您的服务将 ServiceProcessInstaller 的 Account 属性设置为 User，则在安装期间需要安排用户名和密码。使用的用户名和密码作为参数传递给 InstallUtil 命令。然后在 ServiceProcessInstaller 内部的代码中使用 `InstallContext` 类来设置 UserName 和 Password 属性。`InstallContext` 类的文档包含一个示例。

## 启动服务

本章后面，您将创建自己的“控制面板”屏幕来启动和停止服务。现在，为了测试新的 Windows 服务，您将使用 Windows 内置的服务控制管理器来启动 FileWatcherService 服务。它先前已在图 30-1 中显示。打开服务控制管理器并找到 FileWatcherService 服务。如果您在安装 FileWatcherService 后已打开服务控制管理器，您需要刷新它。

如果 FileWatcherService 服务未出现在列表中，则安装失败。重试安装并检查错误消息。右键单击 FileWatcherService 服务并选择开始菜单选项。

要测试服务，请在 `C:/TEMP` 目录（或您决定使用的任何其他目录）中复制或创建 `.TXT` 文件。您应该能够使用前面描述的事件查看器在计算机的事件日志中看到相应的事件。

图 30-3 显示了事件查看器，其中包含服务创建的几个示例消息。如果您右键单击 FileWatcherService 的其中一个事件，您将看到详细信息屏幕。请注意，该消息对应于您在服务中 FileSystemWatcher 控件的 Created 事件中构建的事件日志消息，如图 30-4 所示。

### 图 30-3

![](img/d99870e80390742f93963da7be0b2e61_993_0.png)

## 卸载服务

卸载服务与安装服务非常相似。服务必须处于停止状态后才能卸载，但卸载操作会尝试在服务运行时停止服务。卸载操作在与安装操作相同的命令窗口中进行，使用命令与安装时相同，只是服务名称前加上了选项 /u。请记住，您需要导航到 C:\Users\[ user ]\Documents\Visual Studio 2010\Projects\FileWatcherService\FileWatcherService\obj\Debug（或根据当前配置等效的 Release 目录）来运行此命令：

```
InstallUtil.exe /u FileWatcherService.exe
```

如果实用工具显示的信息包含以下行，则可以判断卸载成功：

```
Service FileWatcherService was successfully removed from the system.
```

如果卸载不成功，则阅读其余信息以确定原因。除了输入错误的路径名外，另一个常见失败原因是尝试卸载处于运行状态且未能及时停止的服务。

一旦您卸载了 FileWatcherService，它将不再显示在可启动和停止的服务列表中（至少在刷新后不会）。

![](img/d99870e80390742f93963da7be0b2e61_993_1.png)

### 图 30-4

> 每次对 Windows 服务进行更改时，都必须卸载并重新安装它。

## 与服务通信

到目前为止，您已学习如何执行以下操作：

- 使用 Visual Basic 创建 Windows 服务
- 使用控制面板中的服务控制管理器启动和停止服务
- 使服务与系统级功能（如 FileSystemWatcher）一起工作

如果这些过程足以通过 Server Explorer 或服务控制管理器启动、停止并检查服务，并且无需与服务进行任何其他通信，则这就是您需要做的全部工作。但是，通常创建专门的应用程序来操作您的服务会很有帮助。此应用程序通常能够启动和停止服务，并检查其状态。应用程序可能还需要与服务通信以更改其配置。此类应用程序通常被称为服务的控制面板，即使它不一定驻留在操作系统的控制面板中。一个常用的此类应用程序示例是 SQL Server 服务管理器，其图标如果您安装了 SQL Server，则会出现在任务栏托盘中（通常在屏幕右下角）。

此类应用程序需要一种与服务通信的方式。用于此类通信的 .NET Framework 基类是 ServiceController。它位于 System.ServiceProcess 命名空间中。在项目可以使用 ServiceController 类之前，您需要添加对 System.ServiceProcess.dll（包含此命名空间）的引用。

ServiceController 类提供对服务控制管理器的接口，服务控制管理器协调与 Windows 服务的所有通信。但是，使用 ServiceController 类时，您不必了解任何有关服务控制管理器的知识。您只需操作 ServiceController 类的属性和方法，任何必要的与服务控制管理器的通信都会在幕后为您完成。

由于与同一服务通信的多个 ServiceController 实例可能存在时序冲突，因此最好为每个控制的服务使用恰好一个 ServiceController 实例。通常，这意味着使用模块级对象变量来保存对活动 ServiceController 的引用，并在应用程序的初始化逻辑期间实例化 ServiceController。以下示例使用了此技术。

### ServiceController 类

ServiceController 的构造函数需要它将要通信的 Windows 服务的名称。这与定义服务的类中 ServiceName 属性中放置的名称相同。您将很快看到如何实例化 ServiceController 类。

ServiceController 类有几个用于操作服务的成员。表 30-2 描述了最重要的<|message|> 方法，其后是表 30-3 中的最重要的属性。

### 表 30-2：重要的 ServiceController 方法

| 方法 | 描述 |
|---|---|
| Start | 用于启动服务的方法 |
| Stop | 用于停止服务的方法 |
| Refresh | 用于确保 ServiceController 对象包含服务的最新状态的方法（因为服务可能由另一个程序操作） |
| ExecuteCommand | 用于向服务发送自定义命令的方法。此方法将在“自定义命令”部分中介绍。 |

