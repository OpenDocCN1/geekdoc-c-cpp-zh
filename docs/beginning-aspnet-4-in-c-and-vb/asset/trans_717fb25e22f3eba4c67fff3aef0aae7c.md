
接下来，你必须使用资源编译器 rc.exe。命令 rc EventLogDemoMessages.rc 会创建资源文件 EventLogDemoMessages.RES：

```
rc EventLogDemoMessages.rc
```

使用链接器，你可以将二进制消息文件 EventLogDemoMessages.RES 绑定到一个原生 DLL：

```
link /DLL /SUBSYSTEM:WINDOWS /NOENTRY /MACHINE:x86 EventLogDemoMessages.RES
```

现在，你可以根据以下代码所示注册一个事件源来定义资源文件。首先，会检查名为 EventLogDemoApp 的事件源是否存在。如果事件日志必须创建（因为不存在），下一个检查会验证资源文件是否可用。MSDN 文档中的一些示例演示了将消息文件写入 <windows>\system32 目录，但你不应该这样做。将消息 DLL 复制到程序特定的目录，该目录可通过 SpecialFolder 枚举值 ProgramFiles 获取。如果需要在多个应用程序之间共享消息文件，可以将其放入 Environment.SpecialFolder.CommonProgramFiles。

如果文件存在，则会实例化一个类型为 EventSourceCreationData 的新对象。源的名称和日志的名称被定义。你使用 CategoryResourceFile、MessageResourceFile 和 ParameterResourceFile 属性来定义对资源文件的引用。事件源创建后，你可以在注册表中通过事件源找到有关资源文件的信息。CreateEventSource 方法注册新的事件源和日志文件。最后，EventLog 类中的 RegisterDisplayName() 方法指定日志在事件查看器中显示的名称。ID 5001 取自消息文件。

![](img/d7d2ffa0a76feaab821930e95daace93_543_0.png)

```
string logName = "ProCSharpLog";
string sourceName = "EventLogDemoApp";
string resourceFile = Environment.GetFolderPath(
    Environment.SpecialFolder.ProgramFiles) +
    @"\\procsharp\\EventLogDemoMessages.dll";

if (!EventLog.SourceExists(sourceName))
{
    if (!File.Exists(resourceFile))
    {
        Console.WriteLine("Message resource file does not exist");
        return;
    }

    var eventSource = new EventSourceCreationData(sourceName, logName);

    eventSource.CategoryResourceFile = resourceFile;
    eventSource.CategoryCount = 4;
    eventSource.MessageResourceFile = resourceFile;
    eventSource.ParameterResourceFile = resourceFile;

    EventLog.CreateEventSource(eventSource);
}
else
{
    logName = EventLog.LogNameFromSourceName(sourceName, ".");
}
```

```csharp
var evLog = new EventLog(logName, "*", sourceName);
evLog.RegisterDisplayName(resourceFile, 5001);
```

现在，你可以使用 WriteEvent() 方法代替 WriteEntry() 来写入事件日志条目。WriteEvent() 需要一个类型为 EventInstance 的对象作为参数。通过 EventInstance，你可以分配消息 ID、类别以及类型为 EventLogEntryType 的严重性。除了 EventInstance 参数外，WriteEvent() 还接受用于具有参数的消息的参数以及以字节数组形式表示的二进制数据。

```csharp
using (var log = new EventLog(logName, "*", sourceName))
{
    var info1 = new EventInstance(1000, 4,
        EventLogEntryType.Information);
    log.WriteEvent(info1);
    var info2 = new EventInstance(1001, 4,
        EventLogEntryType.Error);
    log.WriteEvent(info2, "avalon");
    var info3 = new EventInstance(1002, 3,
        EventLogEntryType.Error);
    byte[] additionalInfo = { 1, 2, 3 };
    log.WriteEvent(info3, additionalInfo);
}
```

> 对于消息标识符，定义一个包含 const 值 的类以在应用程序中为标识符提供更有意义的名称是很有用的。

你可以使用事件查看器读取事件日志条目。

## 性能监视

性能监视可用于获取有关应用程序正常行为的信息。性能监视是一个很棒的工具，有助于你了解系统的负载并观察变化和趋势，尤其是在服务器上运行的应用程序中。

Microsoft Windows 具有许多性能对象，例如 System、Memory、Objects、Process、Processor、Thread、Cache 等。每个对象都有许多可监视的计数。例如，对于 Process 对象，可以监视所有进程或特定进程实例的用户时间、句柄计数、页面错误、线程计数等。某些应用程序，例如 SQL Server，也会添加特定于应用程序的对象。

## 性能监视类

System.Diagnostics 命名空间提供了以下用于性能监视的类：

- PerformanceCounter 可用于监视计数和写入计数。也可以使用此类创建新的性能类别。
- PerformanceCounterCategory 使你能够遍历所有现有类别并创建新类别。你可以以编程方式获取类别中的所有计数器。
- PerformanceCounterInstaller 用于性能计数器的安装。其用法与之前讨论的 EventLogInstaller 类似。

## 性能计数器生成器

示例应用程序 PerformanceCounterDemo 是一个简单的 Windows 应用程序，仅有两个按钮来演示写入性能计数。通过一个按钮的处理程序注册性能计数器类别；通过另一个按钮的处理程序写入性能计数器值。与示例应用程序类似，你可以将性能计数器添加到 Windows 服务（参见第 25 章“Windows 服务”）、网络应用程序（参见第 24 章“Networking”）或任何你希望接收实时计数的其他应用程序。

使用 Visual Studio，你可以通过在服务器资源管理器中选择性能计数器并在上下文菜单中选择菜单项 Create New Category 来创建新的性能计数器类别。这将启动性能计数器生成器（参见图 19-7）。

![](img/d7d2ffa0a76feaab821930e95daace93_545_0.png)

FIGURE 19-7

> 要使用 Visual Studio 创建性能计数器类别，Visual Studio 必须以提升的模式启动。

将性能计数器类别的名称设置为 Wrox Performance Counters。下表显示了报价服务的全部性能计数器。

| 名称 | 描述 | 类型 |
|---|---|---|
| 按钮点击次数 | 按钮点击总数 | NumberOfItems32 |
| 每秒按钮点击次数 | 一秒内的按钮点击次数 | RateOfCountsPerSecond32 |
| 鼠标移动事件次数 | 鼠标移动事件总数 | NumberOfItems32 |
| 每秒鼠标移动事件次数 | 一秒内的鼠标移动事件次数 | RateOfCountsPerSecond32 |

性能计数器生成器将配置写入性能数据库。这也可以通过使用 System.Diagnostics 命名空间中 PerformanceCounterCategory 类的 Create() 方法动态完成。稍后可以使用 Visual Studio 添加其他系统的安装程序。

以下代码片段显示了如何以编程方式添加性能类别。使用 Visual Studio 的工具，你只能创建一个全局性能类别，该类别对运行应用程序的不同进程没有不同的值。以编程方式创建性能类别允许你监视来自不同应用程序的性能计数，这也是在此处所做的。

首先，定义了类别名称的 const，以及包含性能计数名称的 SortedList<TKey, TValue>：

```
private const string performanceCounterCategoryName = "Wrox Performance Counters";
private SortedList<string, Tuple<string, string>> perfCountNames;
```

code snippet PerformanceCounterDemo/MainWindow.xaml.cs

```csharp
var counters =
    new CounterCreationDataCollection(counterCreationData);

var category = PerformanceCounterCategory.Create(
    performanceCounterCategoryName,
    "Sample Counters for Professional C#",
    PerformanceCounterCategoryType.MultiInstance,
    counters);

MessageBox.Show(String.Format(
    "category {0} successfully created",
    category.CategoryName));
}
```

code snippet PerformanceCounterDemo/MainWindow.xaml.cs

## 添加 PerformanceCounter 组件

对于 Windows Forms 或 Windows Service 应用程序，你可以从工具箱或服务器资源管理器通过拖放将 PerformanceCounter 组件添加到设计器表面。

对于 WPF 应用程序则不可能。然而，手动定义性能计数器是一项大量工作，如 InitializePerformanceCounts() 方法所示。在这里，所有性能计数的 CategoryName 从 const string performanceCounterCategoryName 设置；CounterName 从排序列表设置。由于应用程序写入性能计数，因此必须将 ReadOnly 属性设置为 false。当编写仅读取性能计数用于显示目的的应用程序时，可以使用 ReadOnly 属性的默认值，即 true。PerformanceCounter 对象的 InstanceName 设置为应用程序名称。如果计数器配置为全局计数，则可能不设置 InstanceName。

```csharp
private PerformanceCounter performanceCounterButtonClicks;
private PerformanceCounter performanceCounterButtonClicksPerSec;
private PerformanceCounter performanceCounterMouseMoveEvents;
private PerformanceCounter performanceCounterMouseMoveEventsPerSec;

private void InitializePerformanceCounts()
{
    performanceCounterButtonClicks = new PerformanceCounter
    {
        CategoryName = performanceCounterCategoryName,
        CounterName = perfCountNames["clickCount"].Item1,
        ReadOnly = false,
        MachineName = "*",
        InstanceLifetime = PerformanceCounterInstanceLifetime.Process,
        InstanceName = this.instanceName
    };
    performanceCounterButtonClicksPerSec = new PerformanceCounter
    {
        CategoryName = performanceCounterCategoryName,
        CounterName = perfCountNames["clickSec"].Item1,
        ReadOnly = false,
        MachineName = "*",
        InstanceLifetime = PerformanceCounterInstanceLifetime.Process,
        InstanceName = this.instanceName
    };
    performanceCounterMouseMoveEvents = new PerformanceCounter
    {
        CategoryName = performanceCounterCategoryName,
        CounterName = perfCountNames["mouseCount"].Item1,
```
