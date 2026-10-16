
要终止的服务。

以下是自动生成的代码（代码文件 QuoteService/Program.cs）：

```csharp
static void Main()
{
    ServiceBase[] servicesToRun = new ServiceBase[]
    {
        new QuoteService()
    };
    ServiceBase.Run(servicesToRun);
}
```

如果进程中只有一个服务，则可以移除数组；`Run` 方法接受一个从 `ServiceBase` 类派生的单个对象，因此 `Main` 方法可以简化为：

```csharp
ServiceBase.Run(new QuoteService());
```

服务程序 `Services.exe` 包含多个服务。如果你有类似的服务，即在单个进程中运行多个服务，并且必须为多个服务初始化某些共享状态，那么共享初始化必须在 `Run` 方法之前完成。使用 `Run` 方法时，主线程会被阻塞，直到服务进程停止；在服务结束之前，任何后续指令都不会被执行。

初始化时间不应超过 30 秒。如果初始化代码耗时超过此限制，SCM 将假定服务启动失败。你需要考虑最慢的机器，确保此服务能在 30 秒限制内运行。如果初始化耗时较长，你可以在另一个线程中启动初始化，以便主线程及时调用 `Run`。然后可以使用事件对象来通知线程已完成其工作。

## 服务启动

在服务启动时，会调用 `OnStart` 方法。在此方法中，你可以启动之前创建的套接字服务器。你必须引用 `QuoteServer` 程序集才能使用 `QuoteService`。调用 `OnStart` 的线程不能被阻塞；此方法必须返回到调用方，即 `ServiceBase` 类的 `ServiceMainCallback` 方法。`ServiceBase` 类注册处理程序，并在调用 `OnStart` 后通知 SCM 服务已成功启动（代码文件 `QuoteService/QuoteService.cs`）：

```csharp
protected override void OnStart(string[] args)
{
    _quoteServer = new QuoteServer(Path.Combine(
        AppDomain.CurrentDomain.BaseDirectory, "quotes.txt"),
        5678);
    _quoteServer.Start();
}
```

`_quoteServer` 变量在类中声明为私有成员：

```csharp
namespace Wrox.ProCSharp.WinServices
{
    public partial class QuoteService : ServiceBase
    {
        private QuoteServer _quoteServer;
```

## 处理程序方法

当服务停止时，会调用 `OnStop` 方法。你应当在此方法中停止服务的功能（代码文件 `QuoteService/QuoteService.cs`）：

```csharp
protected override void OnStop() => _quoteServer.Stop();
```

除了 `OnStart` 和 `OnStop` 之外，你还可以在服务类中重写以下处理程序：

- `OnPause` — 当服务应暂停时调用。
- `OnContinue` — 当服务暂停后应恢复正常操作时调用。为了使重写的 `OnPause` 和 `OnContinue` 方法能被调用，必须将 `CanPauseAndContinue` 属性设置为 `true`。
- `OnShutdown` — 当 Windows 正在系统关闭时调用。通常，此方法的行为应与 `OnStop` 实现类似；如果关闭需要更多时间，你可以请求更多时间。与 `OnPause` 和 `OnContinue` 类似，必须设置一个属性才能启用此行为：`CanShutdown` 必须设置为 `true`。
- `OnPowerEvent` — 当系统电源状态改变时调用。关于电源状态变化的信息位于 `PowerBroadcastStatus` 类型的参数中。`PowerBroadcastStatus` 是一个枚举，其值包括 `Battery Low` 和 `PowerStatusChange`。在这里，如果系统想要挂起（`QuerySuspend`），你也会收到信息，你可以批准或拒绝。本章后面将详细介绍电源事件。
- `OnCustomCommand` — 这是一个可以为服务控制程序发送的自定义命令提供服务的处理程序。`OnCustomCommand` 的方法签名有一个 `int` 参数，你可以通过它获取自定义命令编号。该值可以在 128 到 256 的范围内；小于 128 的值是系统保留值。在你的服务中，你使用自定义命令 128 重新读取引文文件：

```csharp
protected override void OnPause() => _quoteServer.Suspend();

protected override void OnContinue() =>
    _quoteServer.Resume();

public const int CommandRefresh = 128;
protected override void OnCustomCommand(int command)
{
    switch (command)
    {
        case CommandRefresh:
            _quoteServer.RefreshQuotes();
            break;

        default:
            break;
    }
}
```

## 线程与服务

如本章前面所述，如果初始化时间过长，SCM 会假定服务失败。要处理这个问题，你需要创建一个线程。

你的服务类中的 `OnStart` 方法必须及时返回。如果你调用阻塞方法（如 `TcpListener` 类中的 `AcceptSocket`），则需要启动一个线程来执行此操作。对于处理多个客户端的网络服务器，线程池也非常有用。`AcceptSocket` 应接收调用，并将处理交给线程池中的另一个线程。这样，没有人会等待代码执行，系统看起来响应迅速。

## 服务安装

服务必须在注册表中配置。所有服务都位于 `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services`。你可以使用 `regedit` 查看注册表项。这里可以找到服务的类型、显示名称、可执行文件的路径、启动配置等。图 39.8 显示了 W3SVC 服务的注册表配置。

![](img/3d365b72b289213a91ade7eb366b8f35_1501_0.png)

图 39.8

你可以使用 `System.ServiceProcess` 命名空间中的安装程序类来完成此配置，如下一节所述。

## 安装程序

你可以通过切换到 Visual Studio 的设计视图，然后从上下文菜单中选择“添加安装程序”选项，向服务添加安装程序。使用此选项，将创建一个新的 `ProjectInstaller` 类，以及一个 `ServiceInstaller` 实例和一个 `ServiceProcessInstaller` 实例。

图 39.9 展示了服务的安装程序类的类图。

在我们查看使用“添加安装程序”选项创建的文件 `ProjectInstaller.cs` 中的源代码时，请记住此图。

### 安装程序类

`ProjectInstaller` 类派生自 `System.Configuration.Install.Installer`。这是所有自定义安装程序的基类。使用 `Installer` 类，可以构建基于事务的安装。对于基于事务的安装，如果安装失败，你可以回滚到先前状态，并且该安装到此为止所做的任何更改都将被撤消。如图 39.9 所示，`Installer` 类具有 `Install`、`Uninstall`、`Commit` 和 `Rollback` 方法，它们由安装程序调用。

![](img/3d365b72b289213a91ade7eb366b8f35_1502_0.png)

图 39.9

属性 `[RunInstaller(true)]` 表示在安装程序集时应调用 `ProjectInstaller` 类。自定义操作安装程序以及 `installutil.exe`（本章后面将使用）会检查此属性。

`InitializeComponent` 在 `ProjectInstaller` 类的构造函数内被调用（代码文件 `QuoteService/ProjectInstaller.cs`）：

```csharp
using System.ComponentModel;
using System.Configuration.Install;

namespace Wrox.ProCSharp.WinServices
{
    [RunInstaller(true)]
    public partial class ProjectInstaller : Installer
    {
        public ProjectInstaller()
        {
            InitializeComponent();
        }
    }
}
```

现在让我们转到由项目安装程序调用的安装程序中的其他安装器。

### 进程安装程序和服务安装程序

在 `InitializeComponent` 的实现中，创建了 `ServiceProcessInstaller` 类和 `ServiceInstaller` 类的实例。这两个类都派生自 `ComponentInstaller` 类，而 `ComponentInstaller` 类本身派生自 `Installer`。

从 `ComponentInstaller` 派生的类可用于安装过程。请记住，一个服务进程可以包含多个服务。`ServiceProcessInstaller` 类用于配置进程，该配置定义此进程中所有服务的值；`ServiceInstaller` 类用于配置服务，因此每个服务都需要一个 `ServiceInstaller` 实例。如果进程中有三个服务，则需要添加三个 `ServiceInstaller` 对象：

```csharp
partial class ProjectInstaller
{
    private System.ComponentModel.IContainer components = null;

    private void InitializeComponent()
    {
        this.serviceProcessInstaller1 =
            new System.ServiceProcess.ServiceProcessInstaller();
        this.serviceInstaller1 =
            new System.ServiceProcess.ServiceInstaller();

        this.serviceProcessInstaller1.Password = null;
        this.serviceProcessInstaller1.Username = null;

        this.serviceInstaller1.ServiceName = "QuoteService";
        this.serviceInstaller1.Description = "Sample Service for Professional C#";
        this.serviceInstaller1.StartType =
            System.ServiceProcess.ServiceStartMode.Manual;

        this.Installers.AddRange(
```
