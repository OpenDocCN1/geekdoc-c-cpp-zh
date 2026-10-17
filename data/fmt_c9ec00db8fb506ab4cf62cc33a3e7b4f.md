

现在，在代码中，可以使用 `WebTest` 的 `Context` 属性访问数据源，该属性返回 `WebTestContext` 以通过索引访问所需的数据源：

#### 新建测试数据源向导

#### 选择数据源类型

数据源名称：`DataSource1`

数据源类型：
- 数据库
- CSV 文件
- XML 文件

请选择将作为此数据源基础的数据类型。

< 上一步 下一步 > 完成 取消

#### 图 19.16

#### Web 负载测试

使用 Web 负载测试，您可以模拟对 Web 应用程序的高负载。 对于非常高的负载，一个测试服务器是不够的；您可以使用测试服务器列表。 使用 `Visual Studio 2015`，您可以直接使用 `Microsoft Azure` 的基础设施并选择基于云的负载测试，如图 19.17 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_728_0.png)

#### 图 19.17

您可以通过向 `WebAndLoadTestProject` 项目添加新项 `Web Load Test` 来创建负载测试。 这将启动一个向导，您可以在其中执行以下操作：

- 定义恒定负载或随时间增加的负载（参见图 19.18）
- 建立基于测试次数或虚拟用户数量的测试混合模型
- 将测试添加到负载中并定义哪个测试应运行的百分比与其他测试相比
- 指定网络混合以模拟快速和慢速网络（如果服务器被快速网络的客户端占用，慢速网络用户的结果会怎样？）
- 确定浏览器混合以使用 `Internet Explorer`、`Chrome`、`Firefox` 和其他浏览器进行测试
- 建立运行设置以运行测试所需的时间

![](img/3d365b72b289213a91ade7eb366b8f35_729_0.png)

#### 图 19.18

### 摘要

在本章中，您已了解有关测试应用程序的最重要方面：创建单元测试、编码的 UI 测试和 Web 测试。

`Visual Studio` 提供了一个 `Test Explorer` 来运行单元测试，无论它们是使用 `MSTest` 还是 `xUnit` 创建的。 `xUnit` 的优势在于支持 `.NET Core`。 本章还向您展示了三 `A` 的实际应用：`Arrange`、`Act` 和 `Assert`。

通过编码的 UI 测试，您已了解如何创建录制并调整录制以按需修改 UI 测试代码。

对于 Web 应用程序，您已了解如何创建 Web 测试以向服务器发送请求。 您还了解了如何更改请求。

尽管测试有助于在应用程序部署前修复问题，但第 20 章“诊断和 Application Insights”可帮助您修复正在运行的应用程序。

### 20 诊断和 Application Insights

#### 本章内容

- 使用 `EventSource` 进行简单跟踪
- 使用 `EventSource` 进行高级跟踪
- 创建自定义跟踪侦听器
- 使用 `Application Insights`

#### 本章 Wrox.com 代码下载

本章的 `wrox.com` 代码下载可在 `www.wrox.com/go/professionalcsharp6` 的 `Download Code` 选项卡上找到。 本章的代码分为以下主要示例：

- `SimpleEventSourceSample`
- `EventSourceSampleInheritance`
- `EventSourceSampleAnnotations`
- `ClientApp/MyApplicationEvents`
- `WinAppInsights`

#### 诊断概述

随着应用程序的发布周期变得越来越快，了解应用程序在生产环境中运行时如何表现变得越来越重要。 发生了哪些异常？ 了解使用哪些功能也很重要。 用户是否找到了应用程序的新功能？ 他们在页面中停留了多长时间？ 要回答这些问题，您需要有关应用程序的实时信息。

本章解释了如何获取有关正在运行的应用程序的实时信息，以便在生产期间识别可能出现的问题或监控资源使用情况以确保可以容纳更高的用户负载。 这就是命名空间 `System.Diagnostics.Tracing` 发挥作用的地方。 该命名空间提供用于使用 Windows 事件跟踪（ETW）进行跟踪的类。

当然，处理应用程序中的错误的一种方法是抛出异常。 然而，应用程序可能不会因异常而失败，但仍然表现不正常。 应用程序可能在大多数系统上运行良好，但在少数系统上出现问题。 在实时系统中，您可以通过启动跟踪收集器来更改日志并获取有关应用程序内部发生情况的详细实时信息。 您可以使用 `ETW` 来完成此操作。

如果应用程序出现问题，系统管理员需要被告知。 事件查看器是一个常用的工具，不仅系统管理员应该了解，软件开发人员也应该了解。 使用事件查看器，您可以交互式监控应用程序的问题，并可以添加订阅以获取有关发生的特定事件的通知。 `ETW` 使您能够编写有关应用程序的信息。

`Application Insights` 是 `Microsoft Azure` 云服务，使您能够监控云中的应用程序。 只需几行代码，您就可以获得有关应用程序或服务使用情况的详细信息。

本章解释了这些功能并演示了如何将它们用于您的应用程序。

> **注意** `System.Diagnostics` 命名空间还提供其他用于跟踪的类，例如 `Trace` 和 `TraceSource`。 这些类已在 `.NET` 的早期版本中使用。 本章仅涉及跟踪的最新的技术：`EventSource`。 您可以在 `Professional C# 5.0 and .NET 4.5.1` 中阅读有关旧跟踪类型的信息。

#### 使用 EventSource 进行跟踪

跟踪使您能够看到有关正在运行的应用程序的信息性消息。 要获取有关正在运行的应用程序的信息，您可以启动调试器中的应用程序。 在调试期间，您可以逐步遍历应用程序并在特定行和达到特定条件时设置断点。 调试的问题在于，带有发布代码的程序的行为可能与带有调试代码的程序不同。 例如，当程序在断点处停止时，应用程序的其他线程也会被挂起。 此外，使用发布版本，编译器生成的输出会被优化，因此可能会出现不同的效果。 使用优化的发布代码，垃圾回收比调试代码更积极。 方法内的调用顺序可能会改变，并且某些方法可能会被完全删除并就地调用。 也有必要从程序的发布版本中获取运行时信息。 跟踪消息在调试和发布代码中都会写入。

下面描述了一个跟踪如何提供帮助的场景。 部署后，应用程序在一个系统上运行没有问题，而在另一个系统上出现间歇性问题。 当您启用详细跟踪时，出现问题的系统会为您提供有关应用程序内部发生情况的详细信息。 运行正常的系统仅将跟踪配置为将错误消息重定向到 Windows 事件日志系统。 关键错误会被系统管理员看到。 跟踪的开销非常小，因为您仅在需要时才配置跟踪级别。

`Tracing` 在 `.NET` 中有着相当悠久的历史。在 `.NET` 的第一个版本中仅提供简单的 `tracing` 功能以及 `Trace` 类之后，`.NET 2.0` 对 `tracing` 进行了巨大改进并引入了 `TraceSource` 类。`TraceSource` 背后的架构在分离源、侦听器以及基于 `trace` 级别列表来打开和关闭 `tracing` 的开关方面非常灵活。

从 `.NET 4.5` 开始，又引入了新的 `tracing` 类，并在 `.NET 4.6` 中得到增强：`EventSource` 类。该类定义在 `NuGet` 包 `System.Diagnostics` 中的 `System.Diagnostics.Tracing` 命名空间里。

新的 `tracing` 架构基于 `Event Tracing for Windows (ETW)`，`ETW` 是在 `Windows Vista` 中引入的。它允许快速的系统范围消息传递，也被 Windows 事件日志和性能监视设施所使用。

让我们深入了解 `ETW tracing` 和 `EventSource` 类的概念。

- 一个 `ETW provider` 是触发 `ETW` 事件的库。本章创建的应用程序就是 `ETW provider`。
- 一个 `ETW manifest` 描述了可以从 `ETW provider` 触发的事件。使用预定义 `manifest` 的优点是，系统管理员在应用程序安装后就已经知道应用程序可以触发哪些事件。这样管理员就可以提前配置对特定事件的监听。`EventSource` 的新版本同时允许自描述事件和由 `manifest` 描述的事件。
- `ETW keywords` 可用于为事件创建类别。它们被定义为位标志。
- `ETW tasks` 是对事件进行分组的另一种方式。可以创建任务来根据程序的不同场景定义事件。任务通常与 `opcodes` 一起使用。
- `ETW opcodes` 在任务内标识操作。任务和 `opcodes` 均使用整数值定义。
- 一个 `event source` 是触发事件的类。你可以直接使用 `EventSource` 类，也可以创建一个派生自基类 `EventSource` 的类。
- 一个 `event method` 是 `event source` 中触发事件的方法。派生自 `EventSource` 类后，每个 `void` 方法如果未用 `NonEvent` 属性标注即为 `event method`。`Event methods` 可以用 `Event` 属性标注。
- `event level` 定义了事件的严重性或详细程度。这可用于区分 `critical`、`error`、`warning`、`informational` 和 `verbose` 事件。
- `ETW channels` 是事件的接收端。事件可以写入通道和日志文件。`Admin`、`Operational`、`Analytic` 和 `Debug` 是预定义的通道。

使用 `EventSource` 类，你将看到 `ETW` 概念的实际应用。

### Examining a Simple Use of EventSource

使用 `EventSource` 类的示例代码使用了以下依赖项和命名空间：

#### Dependencies

`NETStandard.Library`

`System.Net.Http`

#### Namespaces

`System`

`System.Collections.Generic`

`System.Diagnostics.Tracing`

`System.IO`

`System.Net.Http`

`System.Threading.Tasks`

`static System.Console`

随着 `.NET 4.6` 的发布——以及 `.NET Core 1.0`——`EventSource` 类被扩展并简化，允许在无需派生类的情况下实例化并使用它。这使得在小型场景中使用它变得更简单。

使用 `EventSource` 的第一个示例展示了一个简单案例。`EventSource` 作为 `Program` 类的静态成员实例化，使用 `Console Application (Package)` 项目。通过构造函数指定了事件源的名称（代码文件 `SimpleEventSourceSample/Program.cs`）：

```csharp
private static EventSource sampleEventSource =
    new EventSource("Wrox-EventSourceSample1");
```

通过 `Program` 类的 `Main` 方法，使用 `Guid` 属性获取事件源的唯一标识符。该标识符是基于事件源名称创建的。之后，写入第一个事件以调用 `EventSource` 的 `Write` 方法。所需参数是需要传递的事件名称。其他参数可通过对象的重载提供。传递的第二个参数是一个匿名对象，定义了 `Info` 属性。这可用于向事件日志传递有关事件的任何信息：

```csharp
static void Main()
{
    WriteLine($"Log Guid: {sampleEventSource.Guid}");
    WriteLine($"Name: {sampleEventSource.Name}");
    sampleEventSource.Write("Startup", new { Info = "started app" });
    NetworkRequestSample().Wait();
    ReadLine();
    sampleEventSource?.Dispose();
}
```

> **NOTE** *除了向 `Write` 方法传递包含自定义数据的匿名对象外，你还可以创建一个派生自基类 `EventSource` 的类并用 `EventData` 属性标记它。本章后面会展示该属性。*

从 `Main` 方法调用的 `NetworkRequestSample` 方法进行网络请求并写入 `trace` 日志，将请求的 `URL` 传递给 `trace` 信息。网络调用完成后再次写入 `trace` 信息。异常处理代码展示了写入 `trace` 信息的另一个方法重载。不同的重载允许传递在下一节中展示的特定信息。以下代码片段展示了 `EventSourceOptions` 设置 `trace` 级别。通过写入错误信息设置了 `Error` 事件级别。该级别可用于过滤特定 `trace` 信息。通过过滤，你可以决定只读取错误信息——例如，错误级别的信息以及比错误级别更关键的信息。在另一次 `tracing` 会话中，你可以决定使用 `verbose` 级别读取所有 `trace` 信息。`EventLevel` 枚举定义了 `LogAlways`、`Critical`、`Error`、`Warning`、`Informational` 和 `Verbose` 值：

```csharp
private static async Task NetworkRequestSample()
{
    try
    {
        using (var client = new HttpClient())
        {
            string url = "http://www.cninnovation.com";
            sampleEventSource.Write("Network", new { Info = $"requesting {url}" });
            string result = await client.GetStringAsync(url);
            sampleEventSource.Write("Network", new { Info = $"completed call to {url}, result string length: {result.Length}" });
        }
        WriteLine("Complete..................");
    }
    catch (Exception ex)
    {
        sampleEventSource.Write("Network Error", new EventSourceOptions { Level = EventLevel.Error }, new { Message = ex.Message, Result = ex.HResult });
        WriteLine(ex.Message);
    }
}
```

在运行应用程序之前，你需要进行一些配置并使用读取 `traces` 的工具。下一节将解释如何操作。

> **NOTE** *简单的 `EventSource` 用法仅在 `.NET 4.6`、`.NET Core 1.0` 及更高版本中可用。使用早期 `.NET` 版本创建的程序需要创建派生自 `EventSource` 的类，如下一节所示。或者，要使用更简单的选项，可以使用适用于旧版 `.NET` 的 `NuGet` 包 `Microsoft.Diagnostics.Tracing.EventSource`。*

### Understanding Tools for Tracing

用于分析 `trace` 信息，有多种工具可用。`logman` 是 `Windows` 的一部分工具。可使用 `logman` 创建和管理事件 `trace` 会话，并将 `ETW traces` 写入二进制日志文件。`tracerpt` 也随 `Windows` 提供。该工具可将 `logman` 写入的二进制信息转换为 `CSV`、`XML` 或 `EVTX` 文件格式。`PerfView` 是一款提供 `ETW traces` 图形信息的工具。

#### Logman

让我们开始使用 `logman` 从之前创建的应用程序创建 `trace` 会话。你需要先启动应用程序以复制为应用程序创建的 `GUID`。你需要此 `GUID` 来使用 `logman` 启动日志会话。`start` 选项启动新的会话以记录日志。`-p` 选项定义提供程序的名称；此处使用 `GUID` 来标识提供程序。`-o` 选项定义输出文件，`-ets` 选项将命令直接发送到事件跟踪系统而不进行调度。确保在有写入权限的目录中启动 `logman`；否则它将无法写入输出文件 `mytrace.etl`：

```bash
logman start mysession -p {3b0e7fa6-0346-5781-db55-49d84d7103de} -o mytrace.etl -ets
```

运行应用程序后，你可以使用 `stop` 命令停止 `trace` 会话：

```bash
logman stop mysession -ets
```

