
如果 `AppDomain` 卸载失败，新线程将处理 `CannotUnloadAppDomainException`，但由于你没有编写该新线程执行的代码，因此无法捕获此异常。

回调无法以任何方式处理或吞掉异常；它们接收的是异常已发生的通知。要注册回调方法，只需添加到 `AppDomain` 的 `FirstChanceException`。

如果 `AppDomain` 卸载失败，新线程将处理。

> 注意：如果线程在 `AppDomain` 内部调用 `AppDomain.Unload`，CLR 会创建另一个线程来尝试卸载该 `AppDomain`。第一个线程将强制抛出 `ThreadAbortException` 并回溯。新线程将用于卸载该 `AppDomain`，然后新线程将终止。如果 `AppDomain` 卸载失败，新线程将处理 `CannotUnloadAppDomainException`，但由于你没有编写该新线程执行的代码，因此无法捕获此异常。

当线程调用 `AppDomain.Unload` 时，CLR 会等待 10 秒让正在卸载的 `AppDomain` 中的线程离开它。如果 10 秒后，调用 `AppDomain.Unload` 的线程没有返回，它将抛出 `CannotUnloadAppDomainException`，且该 `AppDomain` 以后可能无法被卸载。

应用程序可以监控 `AppDomain` 消耗的资源。某些宿主使用这些信息来决定当 `AppDomain` 的内存或 CPU 消耗超过宿主认为合理的范围时何时卸载该 `AppDomain`。监控也可以用于比较不同算法的资源消耗，以确定哪种算法使用的资源更少。由于 `AppDomain` 监控会产生额外的开销，宿主必须通过将 `AppDomain` 的静态属性 `MonitoringEnabled` 设置为 `true` 来显式开启监控。这将开启所有 `AppDomain` 的监控。一旦开启监控，就无法关闭；尝试将 `MonitoringEnabled` 属性设置为 `false` 会导致抛出 `ArgumentException`。

一旦开启监控，你的代码就可以查询 `AppDomain` 类提供的四个只读属性：

- *MonitoringSurvivedProcessMemorySize*：`Int64` 属性，返回当前由 CLR 实例控制的所有 `AppDomain` 正在使用的字节数。该数字自上一次垃圾回收以来是准确的。
- *MonitoringTotalAllocatedMemorySize*：实例 `Int64` 属性，返回特定 `AppDomain` 分配的字节数。该数字自上一次垃圾回收以来是准确的。
- *MonitoringSurvivedMemorySize*：实例 `Int64` 属性，返回特定 `AppDomain` 正在使用的字节数。该数字自上一次垃圾回收以来是准确的。
- *MonitoringTotalProcessorTime*：实例 `TimeSpan` 属性，返回特定 `AppDomain` 产生的 CPU 使用量。

# 第 22 章 CLR 托管与 AppDomains 611

下面的类展示了如何使用这些属性三个来查看两个时间点之间 `AppDomain` 内部发生了变化：

```csharp
private sealed class AppDomainMonitorDelta : IDisposable {
    private AppDomain m_appDomain;
    private TimeSpan m_thisADCPU;
    private Int64 m_thisMemoryInUse;
    private Int64 m_thisMemoryAllocated;

    static AppDomainMonitorDelta() {
        // 确保 AppDomain 监控已开启
        AppDomain.MonitoringIsEnabled = true;
    }
```

```csharp
public AppDomainMonitorDelta(AppDomain ad) {
    m_appDomain = ad ?? m_appDomain.CurrentDomain;
    m_thisADCPU = m_appDomain.MonitoringTotalProcessorTime;
    m_thisMemoryInUse = m_appDomain.MonitoringTotalSurvivedMemorySize;
    m_thisMemoryAllocated = m_appDomain.MonitoringTotalAllocatedMemorySize;
}
```

```csharp
public void Dispose() {
    Console.WriteLine("Friendly={0}, CPU={1}ms", m_appDomain.FriendlyName,
        m_appDomain.MonitoringTotalProcessorTime - m_thisADCPU.TotalMilliseconds);
    Console.WriteLine(" Allocated {0:N} bytes of {1:N} survived GCs",
        m_appDomain.MonitoringTotalAllocatedMemorySize - m_thisMemoryAllocated,
        m_appDomain.MonitoringTotalSurvivedMemorySize - m_thisMemoryInUse);
}
```

下面的代码展示了如何使用 `AppDomainMonitor` 类：

```csharp
private static void AppDomainResourceMonitoring() {
    // 分配 1000 万字节将会在回收中存
    var list = new List<byte>();
    for (int x = 0; x < 1000; x++) list.Add(new byte[10000]);
    // 分配 2000 万字节将不会在回收中存
    for (int x = 0; x < 2000; x++) new byte[10000].GetType();
    // 运行 CPU 大 5 秒
    Int64 stop = Environment.TickCount + 5000;
    while (Environment.TickCount < stop);
}
```

当我执行这段代码时，我得到以下输出：

FriendlyName=0-Ch22-1-Appdomains.exe, CPU=5031.25ms

Allocated 30,159,496 bytes of 10,085,080 survived GCs

# AppDomain 首次异常通知

每个 `AppDomain` 都可以关联一系列回调方法，当 CLR 开始在 `AppDomain` 内部执行 `catch` 块时，这些方法会被调用。这些方法可以执行日志记录，或者宿主可以使用此机制监控 `AppDomain` 内部抛出的异常。回调无法以任何方式处理或吞掉异常；它们接收的是异常已发生的通知。要注册回调方法，只需添加到 `AppDomain` 的 `FirstChanceException`。

以下是 CLR 如何初始化一个托管 EXE：在 CLR 加载并初始化后，执行继续。

如果 `AppDomain` 卸载失败，新线程将处理 `CannotUnloadAppDomainException`，但由于你没有编写该新线程执行的代码，因此无法捕获此异常。

回调无法以任何方式处理或吞掉异常；它们接收的是异常已发生的通知。要注册回调方法，只需添加到 `AppDomain` 的 `FirstChanceException`。

当线程调用 `AppDomain.Unload` 时，CLR 会等待 10 秒让正在卸载的 `AppDomain` 中的线程离开它。如果 10 秒后，调用 `AppDomain.Unload` 的线程没有返回，它将抛出 `CannotUnloadAppDomainException`，且该 `AppDomain` 以后可能无法被卸载。

> 注意：如果线程在 `AppDomain` 内部调用 `AppDomain.Unload`，CLR 会创建另一个线程来尝试卸载该 `AppDomain`。第一个线程将强制抛出 `ThreadAbortException` 并回溯。新线程将用于卸载该 `AppDomain`，然后新线程将终止。如果 `AppDomain` 卸载失败，新线程将处理 `CannotUnloadAppDomainException`，但由于你没有编写该新线程执行的代码，因此无法捕获此异常。

# 宿主使用 AppDomain

所以我已经讨论了不同的应用程序类型以及它们如何管理 `AppDomain`。为了使讨论更具体，我将描述一些常见的托管场景。

## 可执行程序

控制台应用程序、NT 服务应用程序、Windows Forms 应用程序以及 Windows Presentation Foundation 应用程序 `WPF` 都是托管 EXE 示例。当 Windows 初始化一个托管 EXE 文件时，Windows 加载 `shim`，`shim` 检查程序中的 CLR 头部。头部指示用于构建和测试应用程序的 CLR 版本。在 CLR 加载并初始化后，执行继续。

# 第 22 章 CLR 托管与 AppDomains 613

当代码运行时，它访问其他类型。当引用另一个程序集中的类型时，CLR 定位必要的程序集并加载到同一个 `AppDomain`。任何附加的程序集也会加载到同一个 `AppDomain`。当应用程序的 `Main` 方法返回时，Windows 进程终止（销毁默认 `AppDomain` 和所有其他 `AppDomain`）。

> 顺便提一下，你可以调用 `System.Environment.Exit()` 来关闭 Windows 进程，包括它所有的 `AppDomain`。`Exit` 是终止进程最优雅的方法，因为它首先调用托管堆上所有对象的 `Finalize` 方法，并释放 CLR 持有的所有未托管 COM 对象。最后，`Exit` 调用 Win32 `ExitProcess` 函数。

## Microsoft Silverlight 丰富互联网应用程序

`Silverlight` 运行时使用一种特殊的 CLR，与桌面版本的 .NET Framework 不同。一旦安装了 `Silverlight` 运行时，导航到使用 `Silverlight` 的网站会导致 CLR `CoreClr.dll` 加载到你的浏览器中（浏览器可能是 Windows Explorer——你可能不是在使用 Windows ）。页面上的每个 `Silverlight` 控件运行在自己的 `AppDomain` 中。当用户关闭标签或导航到另一个网站时，不再使用的 `Silverlight` 控件将卸载其 `AppDomain`。在 `AppDomain` 中运行的 `Silverlight` 代码在一个限制的安全沙箱中运行，不会以任何方式危害用户或机器。

## Microsoft ASP.NET Web Forms 和 XML Web 服务应用程序

`ASP.NET` 实现为 ISAPI DLL（实现在 `ASPNet_ISAPI.dll` 中）。当客户端第一次请求由 `ASP.NET` ISAPI DLL 处理的 URL 时...

当后续客户端对已经运行的 Web 应用程序提出请求时，`ASP.NET` 不创建新的 `AppDomain`；而是使用现有的 `AppDomain`，创建 Web 应用程序类型的新实例，并开始调用方法。这些方法已经通过 JIT 编译为本地代码，因此处理所有后续客户端请求的性能非常出色。

如果客户端对不同的 Web 应用程序提出请求，`ASP.NET` 会调用 CLR 创建一个新的 `AppDomain`。这个新的 `AppDomain` 通常与其它 `AppDomain` 一样，是在工作进程内部被创建的。这意味着许多 Web 应用程序运行在单个 Windows 进程中，这提高了系统的整体效率。再次，每个 Web 应用程序所需的程序集被加载到一个 `AppDomain` 中，其唯一目的是将该 Web 应用程序的代码和对象与其他 Web 应用程序隔离开。

`ASP.NET` 的一个非常棒的功能是，可以在不关闭 Web 服务器的情况下更改 Web 站点的代码。当磁盘上的 Web 站点文件发生变化时，`ASP.NET` 会检测到该变化，卸载包含旧版本文件的 `AppDomain`（在最后一个当前正在运行的请求完成后），并创建一个新的 `AppDomain`，加载新版本的文件。为了实现这一点，`ASP.NET` 使用了 `AppDomain` 的一项功能：**影子拷贝（shadow copying）**。

## Microsoft SQL Server

`SQL Server` 是一个非托管应用程序，因为它的大部分代码是用非托管的 C++ 编写的。`SQL Server` 允许开发者使用托管代码创建存储过程。当请求第一次到达数据库以运行用托管代码编写的存储过程时，`SQL Server` 会加载 CLR。存储过程在它们自己的 `AppDomain` 中运行，防止存储过程对数据库服务器产生不利影响。

这种功能绝对是不可思议的！这意味着开发者将能够使用他们选择的编程语言编写存储过程。存储过程可以在其代码中使用强类型数据对象。代码在执行时也将会被 JIT 编译为本地代码，而不是被解释。开发者还可以利用框架类库 `FCL` 或任何程序集中的定义的任何类型。结果是，我们的工作变得简单得多，我们的应用程序运行得也快得多。一个开发者还能要求什么呢？

## 挥洒你的想象力

像文字处理器和电子表格之类的生产力应用程序也允许用户使用选择的任何编程语言编写宏。这些宏将访问所有与 CLR 工作的程序集和类型。它们将经过编译，因此执行速度很快，最重要的是，这些宏将在安全的 `AppDomain` 中运行，这样用户就不会遇到任何意外的惊喜。你自己的应用程序也可以以你想要的方式使用这种能力。

# 高级主机控制

在本节中，我将提到一些与托管 CLR 相关的更高级的话题。我的意图是让你体验一下可能的功能，这将帮助你更多地了解 CLR 的能力。如果你发现这些内容特别感兴趣，我鼓励你寻找其他书籍。

## 使用托管代码管理 CLR

`System.AppDomainManager` 类允许主机使用托管代码而不是非托管代码来覆盖 CLR 的默认设置。当然，使用托管代码使得实现变得更加容易。你只需要定义你的类，并派生自 `System.AppDomainManager` 类，在你想要接管的地方覆盖任何虚方法。你的类然后应该被构建到它自己的程序集中，并安装到全局程序集缓存 `GAC` 中，因为该程序集需要被授予完全信任，而 `GAC` 中的所有程序集始终被授予完全信任。

然后，你需要告诉 CLR 使用你派生自 `AppDomainManager` 的类。在代码中，实现此点的方法方法创建 `AppDomainSetup` 对象的属性，这两者的类型都是 String。将 `AppDomainManagerAssembly` 属性设置为定义你派生自 `AppDomainManager` 类的程序集的字符串标识名称和标识。或者，将 `AppDomainManagerType` 属性设置为你派生自 `AppDomainManager` 类的全名。这可以在你应用程序的 XML 配置文件中通过 `AppDomainManagerAssembly` 和 `AppDomainManager-Type` 元素进行设置。此外，主机还可以查询 `ICLRControl` 接口并调用此接口的 `SetAppDomainManager` 函数，传入 GAC 安装的程序集的标识和派生自 `AppDomainManager` 的类的名称。

现在，让我们来谈谈派生自 `AppDomainManager` 的类可以做什么。派生自 `AppDomainManager` 的类的目的是允许主机即使在尝试创建新的 `AppDomain` 时保持控制，该 `AppDomain` 中派生自 `AppDomainManager` 的对象也可以修改安全和配置设置。它还可以决定失败 `AppDomain` 的创建，或者决定返回现有 `AppDomain` 的引用。当创建新的 `AppDomain` 时，CLR 会在 `AppDomain` 中创建一个新的派生自 `AppDomainManager` 的对象。该对象还可以修改配置设置、执行上下文在线程之间的流动方式，以及授予程序集的权限。

> 5 使用环境变量和注册表设置来配置 `AppDomainManager` 也是可能的，但这些机制比文中提到的方法更繁琐，在某些测试场景下应避免。

## 编写健壮的主机应用程序

主机可以告诉 CLR 在托管代码发生故障时采取什么操作。以下是一些示例（按严重程度从低到高列出）：

- 如果某个线程执行并返回响应耗时过长，CLR 可以中止该线程。（我将在下一节中讨论这一点。）
- CLR 可以卸载一个 `AppDomain`。这将中止该 `AppDomain` 中的所有线程，并导致出现问题的代码被卸载。
- CLR 可以被禁用。这会停止进程中继续执行任何托管代码，但仍允许非托管代码运行。
- CLR 可以退出 Windows 进程。这将中止所有线程并卸载所有 `AppDomain` 以进行清理操作，然后终止进程。

CLR 可以以优雅或粗暴的方式中止线程或 `AppDomain`。优雅中止意味着清理代码执行。也就是说，`finally` 块中的代码会运行，对象会执行其 `Finalize` 方法。粗暴中止意味着清理代码不执行。也就是说，`finally` 块代码不运行，对象可能不会执行其 `Finalize` 方法。优雅中止无法中止位于 `catch` 或 `finally` 块中的线程。然而，粗暴中止会中止位于 `catch` 或 `finally` 块中的线程。不幸的是，非托管或在约束执行区域 `CER` 中的线程完全无法被中止。

主机可以设置一个称为**升级策略 `escalation policy`** 的策略，它告诉 CLR 如何处理托管代码故障。例如，`SQL Server` 告诉 CLR 在 CLR 执行代码时抛出未处理异常时该做什么。当线程遇到未处理的异常时，CLR 首先尝试将异常升级为优雅线程中止。如果线程在指定的时间内没有中止，CLR 尝试将优雅线程中止升级为线程中止。
