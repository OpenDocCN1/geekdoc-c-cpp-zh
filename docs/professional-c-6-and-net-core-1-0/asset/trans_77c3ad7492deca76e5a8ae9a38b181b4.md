

System.Net.Http

MyApplicatonEvents

## 命名空间

System

System.Collections.Generic

System.Diagnostics.Tracing

System.Net.Http

System.Threading.Tasks

static System.Console

`ParallelRequestSample` 方法调用 `RequestStart` 和 `RequestStop` 方法来启动和停止活动。在这两个调用之间，使用 `Parallel.For` 创建了一个并行循环。`Parallel` 类使用多个任务并发运行，通过调用第三个参数的委托来实现。该参数被实现为 lambda 表达式，用于调用 `ProcessTaskAsync` 方法（代码文件 ClientApp/Program.cs）：

```
private static void ParallelRequestSample()
{
    SampleEventSource.Log.RequestStart();
    Parallel.For(0, 20, x =>
    {
        ProcessTaskAsync(x).Wait();
    });
    SampleEventSource.Log.RequestStop();
    WriteLine("Activity complete");
}
```

> 注意 `Parallel` 类在第 21 章“任务和并行编程”中有详细说明。

`ProcessTaskAsync` 方法使用 `ProcessingStart` 和 `ProcessingStop` 写入跟踪。在这里，一个活动在另一个活动内部启动。正如你从分析日志的输出中可以看到的那样，活动可以是分层的（代码文件 ClientApp/Program.cs）：

```
private static async Task ProcessTaskAsync(int x)
{
    SampleEventSource.Log.ProcessingStart(x);
    var r = new Random();
    await Task.Delay(r.Next(500));

    using (var client = new HttpClient())
    {
        var response = await client.GetAsync("http://www.bing.com");
    }
    SampleEventSource.Log.ProcessingStop(x);
}
```

之前，你已经使用 PerfView 工具打开了 ETL 日志文件。PerfView 也可以分析正在运行的应用程序。你可以使用以下选项运行 PerfView：

```
PerfView /onlyproviders=*Wrox-SampleEventSource collect
```

选项 `collect` 启动数据收集。使用限定符 `/onlyproviders` 关闭内核和 CLR 提供程序，只记录所列提供程序的消息。使用限定符 -h 查看 PerfView 的可能选项和限定符。当你以这种方式启动 PerfView 时，数据收集会立即开始并持续到你单击停止收集按钮为止（见图 20.2）。

![](img/3d365b72b289213a91ade7eb366b8f35_746_0.png)

## 图 20.2

当你在开始跟踪收集后运行应用程序，然后在之后停止收集时，你可以看到使用事件类型 `Wrox-SampleEventSource/ProcessingStart/Start` 生成的活动 ID。ID 允许层次结构，例如 //1/2，其中有一个父活动和一个子活动。对于每次循环迭代，你都会看到不同的活动 ID（见图 20.3）。使用事件类型 `Wrox-SampleEventSource/ProcessingStop/Stop`，你可以看到与同一活动相关的相同活动 ID。

![](img/3d365b72b289213a91ade7eb366b8f35_746_1.png)

## 图 20.3

使用 PerfView，你可以在左侧选择多个事件类型，并添加过滤器——例如 //1/4——以便查看属于此活动的所有事件（见图 20.4）。在这里你可以看到，活动 ID 可以跨多个线程。同一活动的开始和停止事件使用不同的线程。

![](img/3d365b72b289213a91ade7eb366b8f35_747_0.png)

## 图 20.4

## 创建自定义侦听器

在你编写跟踪消息时，你已经看到了如何使用 logman、tracert 和 PerfView 等工具读取它们。你也可以创建一个自定义的进程内事件侦听器来将事件写入你想要的位置。

你可以通过创建派生自基类 `EventListener` 的类来创建自定义事件侦听器。你需要做的就是重写 `OnEventWritten` 方法。通过此方法，跟踪消息会传递给类型为 `EventWrittenEventArgs` 的参数。示例实现发送有关事件的信息，包括有效负载，即传递给 `EventSource` 的 `WriteEvent` 方法的附加数据（代码文件 ClientApp/MyEventListener.cs）：

```
```csharp
public class MyEventListener : EventListener
{
    protected override void OnEventSourceCreated(EventSource eventSource)
    {
        WriteLine($"created {{eventSource.Name}} {{eventSource.Guid}}");
    }

    protected override void OnEventWritten(EventWrittenEventArgs eventData)
    {
        WriteLine($"event id: {{eventData.EventId}} source:
        {{eventData.EventSource.Name}}");
        foreach (var payload in eventData.Payload)
        {
            WriteLine($"\t{payload}");
        }
    }
}
```
```

侦听器在 Program 类的 Main 方法中被激活。你可以通过调用 `EventSource` 类的静态方法 `GetSources` 来访问事件源（代码文件 ClientApp/Program.cs）：

```
```csharp
IEnumerable<EventSource> eventSources = 
EventSource.GetSources ();
InitListener(eventSources);
```
```

`InitListener` 方法调用自定义侦听器的 `EnableEvents` 方法并传递每个事件源。示例代码注册设置 `EventLevel.LogAlways` 以监听每个写入的日志消息。你也可以指定只写入信息消息——这也包括错误——或只写入错误。

```
private static void InitListener(IEnumerable<EventSource>
sources)
{
    listener = new MyEventListener();
    foreach (var source in sources)
    {
        listener.EnableEvents(source, EventLevel.LogAlways);
    }
}
```

当你运行应用程序时，你会看到 `FrameworkEventSource` 和 `Wrox-SampleEventSource` 的事件写入控制台。使用这样的自定义事件侦听器，你可以轻松地将事件写入 Application Insights，这是一种云端遥测服务，将在下一节中进行说明。

## 使用 Application Insights

Application Insights 是 Microsoft Azure 的一项技术，允许监控应用程序的使用情况和性能，无论它们在哪里使用。你可以获得有关用户在使用你的应用程序时遇到问题的报告——例如，你可以了解异常情况——你还可以了解用户从你的应用程序中使用的功能。例如，假设你向应用添加了新功能。用户是否找到了激活该功能的按钮？

当你使用 Application Insights 时，很容易识别用户在使用应用程序时遇到的问题。微软之所以让将 Application Insights 与各种应用程序（包括 Web 和 Windows 应用）集成变得容易是有充分理由的。

> **注意** *以下是用户在使用微软自己的产品时遇到困难的一些功能示例。Xbox 是第一个提供带大磁贴的用户界面的设备。搜索功能直接位于磁贴下方。虽然该按钮直接在用户面前可用，但用户没有看到它。微软将搜索功能移入磁贴中，现在用户能够找到它。另一个例子是 Windows Phone 上的物理搜索按钮。该按钮本意是用于在应用内搜索。用户抱怨无法在电子邮件中搜索选项，因为他们没有想到按此物理按钮来搜索电子邮件。微软更改了功能。现在物理搜索按钮仅用于搜索网络内容，而邮件应用有自己的搜索按钮。Windows 8 也存在类似的搜索问题；用户没有使用魅力栏中的搜索功能在应用内搜索。Windows 8.1 更改了指南，使用魅力栏进行搜索，现在应用包含自己的搜索框；在 Windows 10 中还有自动建议框。看起来有些共同点吗？*

## 创建通用 Windows 应用

用于使用 Application Insights 的示例应用之一是一个通用 Windows 平台应用，具有两个页面——`MainPage` 和 `SecondPage`——以及几个按钮和文本框控件，用于模拟操作、抛出异常以及在页面之间导航。用户界面在以下代码片段中定义（代码文件 `WinAppInsights/MainPage.xaml`）：

```
```xml
<StackPanel Orientation="Vertical">
    <Button Content="Navigate to SecondPage" Click="OnNavigateToSecondPage" />
    <TextBox x:Name="SampleDataText" Header="Sample Data" />
    <Button Content="Action" Click="OnAction" />
    <Button Content="Create Error" Click="OnError" />
</StackPanel>
```
```

单击“Navigate to SecondPage”按钮会调用 `OnNavigateToSecondPage` 事件处理程序方法并导航到第二个页面（代码文件 `WinAppInsights/MainPage.xaml.cs`）：

```
```csharp
private void OnNavigateToSecondPage(object sender,
    RoutedEventArgs e)
{
    this.Frame.Navigate(typeof(SecondPage));
}
```
```

使用 `OnAction` 方法，会显示一个对话框，显示用户输入的数据：

```
```csharp
private async void OnAction(object sender, RoutedEventArgs e)
{
    var dialog = new ContentDialog
    {
        Title = "Sample",
```
