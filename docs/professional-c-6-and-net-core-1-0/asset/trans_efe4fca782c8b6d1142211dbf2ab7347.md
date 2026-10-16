

在内部，访问队列元素的方法有 `Enqueue`、`TryDequeue` 和 `TryPeek`。这些方法的命名与你已经熟悉的 `Queue<T>` 的方法非常相似，区别在于 `Try` 前缀表示方法调用可能会失败。

由于该类实现了 `IProducerConsumerCollection<T>` 接口，`TryAdd` 和 `TryTake` 方法只是调用了 `Enqueue` 和 `TryDequeue`。

-   `ConcurrentStack<T>`——与 `ConcurrentQueue<T>` 非常相似，但具有其他项访问方法，该类定义了 `Push`、`PushRange`、`TryPeek`、`TryPop` 和 `TryPopRange` 方法。在内部，此类使用其项的链表。
-   `ConcurrentBag<T>`——该类不定义添加或取出项的任何顺序。它使用一种将线程映射到内部使用的数组的概念，从而尝试减少锁。访问元素的方法有 `Add`、`TryPeek` 和 `TryTake`。
-   `ConcurrentDictionary<TKey, TValue>`——这是一个线程安全的键值对集合。`TryAdd`、`TryGetValue`、`TryRemove` 和 `TryUpdate` 是以非阻塞方式访问成员的方法。由于项基于键和值，`ConcurrentDictionary<TKey, TValue>` 不实现 `IProducerConsumerCollection<T>`。
-   `BlockingCollection<T>`——一个会阻塞并等待直到可以添加或取出项来完成任务的集合，`BlockingCollection<T>` 提供了使用 `Add` 和 `Take` 方法添加和移除项的接口。这些方法会阻塞线程并等待直到任务变为可能。`Add` 方法有一个重载，你还可以传入一个 `CancellationToken`。此令牌可以取消阻塞调用。如果你不希望线程无限期等待，并且你也不希望从外部取消调用，还提供了 `TryAdd` 和 `TryTake` 方法，你还可以指定超时值，以表示你希望阻塞线程并在调用失败前等待的最长时间。

`ConcurrentXXX` 集合类是线程安全的，如果某个操作在当前线程状态下无法执行，则返回 `false`。你必须在继续之前检查添加或取出项是否成功。你不能指望集合总能完成任务。

`BlockingCollection<T>` 是任何实现 `IProducerConsumerCollection<T>` 接口的类的装饰器，并且默认使用 `ConcurrentQueue<T>`。通过构造函数，你还可以传入任何其他实现 `IProducerConsumerCollection<T>` 的类，例如 `ConcurrentBag<T>` 和 `ConcurrentStack<T>`。

## 创建管道

这些并发集合类的一个很好的用途是管道。一个任务向集合类写入一些内容，而另一个任务可以同时从集合中读取。

以下示例应用程序演示了将 `BlockingCollection<T>` 类与多个任务一起使用以形成管道。第一个管道如图 12.1 所示。第一阶段的线程任务读取文件名并将它们添加到队列中。在此任务运行时，阶段 2 的任务已经可以开始从队列中读取文件名并加载其内容。结果被写入另一个队列。阶段 3 可以同时启动，从第二个队列读取内容并处理它。在这里，结果被写入字典。

![](img/3d365b72b289213a91ade7eb366b8f35_451_0.png)

### 图 12.1

在此场景中，下一阶段只能在阶段 3 完成并且内容最终处理完毕且结果完整存入字典后才能开始。后续步骤如图 12.2 所示。阶段 4 从字典中读取，转换数据，并将其写入队列。阶段 5 向项添加颜色信息，并将它们放入另一个队列。最后阶段显示信息。阶段 4 到 6 也可以并发运行。

![](img/3d365b72b289213a91ade7eb366b8f35_452_0.png)

### 图 12.2

Info 类表示由管道维护的项（代码文件 PipelineSample/Info.cs）：

```
public class Info
{
    public string Word { get; set; }
    public int Count { get; set; }
    public string Color { get; set; }
    public override string ToString() => $"{Count} times: {Word}";
}
```

PipelineSample 使用以下依赖项和命名空间：

### 依赖项

NETStandard.Library

### 命名空间

-   System.Collections.Generic
-   System.Collections.Concurrent
-   System.IO
-   System.Linq
-   System.Threading.Tasks
-   static System.Console

查看此示例应用程序的代码，完整管道在方法 `StartPipeline` 中管理。在这里，集合被实例化并传递给管道的各个阶段。第一阶段使用 `ReadFilenamesAsync` 处理，第二阶段和第三阶段 `LoadContentAsync` 和 `ProcessContentAsync` 同时运行。然而，第四阶段只能在第一到第三阶段完成后才能开始（代码文件 PipelineSample/Program.cs）：

```
public static async Task StartPipelineAsync()
{
    var fileNames = new BlockingCollection<string>();
    var lines = new BlockingCollection<string>();
    var words = new ConcurrentDictionary<string, int>();
    var items = new BlockingCollection<Info>();
    var coloredItems = new BlockingCollection<Info>();
    Task t1 = PipelineStages.ReadFilenamesAsync("@../../..", fileNames);
    ColoredConsole.WriteLine("started stage 1");
    ConsoleHelper.WriteLine("started stage 2");
    Task t2 = PipelineStages.LoadContentAsync(fileNames, lines);
    Task t3 = PipelineStages.ProcessContentAsync(lines, words);
    await Task.WhenAll(t1, t2, t3);
    ConsoleHelper.WriteLine("stages 1, 2, 3 completed");
    Task t4 = PipelineStages.TransferContentAsync(words, items);
    Task t5 = PipelineStages.AddColorAsync(items, coloredItems);
    Task t6 = PipelineStages.ShowContentAsync(coloredItems);
    ColoredConsole.WriteLine("stages 4, 5, 6 started");
    await Task.WhenAll(t4, t5, t6);
    ColoredConsole.WriteLine("all stages finished");
}
```

> 注意 此示例应用程序使用了任务以及 async 和 await 关键字，这些将在第 15 章详细解释。你可以在第 21 章阅读更多关于线程、任务和同步的内容。文件 I/O 在第 23 章“文件和流”中讨论。

该示例使用 `ColoredConsole` 类向控制台写入信息。该类提供了一种更改控制台输出颜色的简便方法，并使用同步来避免返回颜色错误的输出（代码文件 PipelineSample/ColoredConsole.cs）：

```
public static class ColoredConsole
{
    private static object syncOutput = new object();
    public static void WriteLine(string message)
    {
        lock (syncOutput)
        {
            Console.WriteLine(message);
        }
    }
    public static void WriteLine(string message, string color)
    {
        lock (syncOutput)
        {
            Console.ForegroundColor = (ConsoleColor)Enum.Parse(
                typeof(ConsoleColor), color);
            Console.WriteLine(message);
            Console.ResetColor();
        }
    }
}
```

## 使用 BlockingCollection

让我们进入管道的第一阶段。`ReadFilenamesAsync` 接收一个 `BlockingCollection<T>`，它可以将其输出写入其中。此方法的实现使用枚举器来迭代指定目录及其子目录中的 C# 文件。文件名通过 `Add` 方法添加到 `BlockingCollection<T>`。添加文件名完成后，调用 `CompleteAdding` 方法以通知所有读取者，它们不应再等待集合中的任何其他项（代码文件 PipelineSample/PipelineStages.cs）：

```
public static class PipelineStages
{
    public static Task ReadFilenamesAsync(string path,
        BlockingCollection<string> output)
    {
        return Task.Factory.StartNew(() =>
        {
            foreach (string filename in
                Directory.EnumerateFiles(path, "*.cs",
                    SearchOption.AllDirectories))
            {
                output.Add(filename);
                ColoredConsole.WriteLine($"stage 1: added {filename}");
            }
            output.CompleteAdding();
        }, TaskCreationOptions.LongRunning);
    }
    // . . .
```

> 注意 如果有一个读取者从 `BlockingCollection<T>` 中读取，同时写入者添加项，那么调用 `CompleteAdding` 方法非常重要。否则，读取者会在 `foreach` 循环中等待更多项的到达。

下一阶段是读取文件并将其内容添加到另一个集合，这是由 `LoadContentAsync` 方法完成的。该方法使用通过输入集合传递的文件名，打开文件，并将文件的所有行添加到输出集合。在 `foreach` 循环中，调用 `GetConsumingEnumerable` 并传入输入阻塞集合以迭代项。也可以直接使用输入变量而不调用 `GetConsumingEnumerable`，但这只会迭代集合的当前状态，而不会迭代之后添加的项。

```
public static async Task
LoadContentAsync(BlockingCollection<string> input,
    BlockingCollection<string> output)
```

