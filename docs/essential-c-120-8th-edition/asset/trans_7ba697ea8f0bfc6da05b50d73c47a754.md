

TPL 还提供了一个类似于 `foreach` 语句的并行版本，如列表 21.3 所示。

# 列表 21.3：foreach 循环的并行执行

```c
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

public class Program
{
    //
    public static void EncryptFiles(
        string directoryPath, string searchPattern
    )
    {
        IEnumerable<string> files = Directory.EnumerateFiles(
            directoryPath, searchPattern,
            SearchOption.AllDirectories);

        Parallel.ForEach(files, fileName =>
        {
            Encrypt(fileName);
        });
    }
    //
}
```

在此示例中，我们调用了一个加密 `files` 集合中每个文件的方法。它是并行执行的，执行的线程数量取决于 TPL 认为最高效率的数量。

# 高级主题

# TPL 如何调优自身的性能

TPL 的默认调度器目标是线程池，这产生了多种启发式策略，以确保在任何时刻都有正确数量的线程在执行。它使用的两种启发式策略是爬山算法（hill climbing）和工作窃取（work stealing）。

爬山算法涉及创建线程来运行任务，然后监控这些任务的性能，以实验性地确定增加更多线程开始导致性能下降的界点。一旦达到该点，线程数量就可以减少到产生最佳性能的数量。

TPL 不会将等待执行的顶层任务与任何特定线程关联。然而，如果运行在线程上的任务本身创建了另一个任务，则该新创建的任务将自动与该线程关联。当新的子任务最终被调度执行时，它通常会在创建它的任务所同一个线程上运行。工作窃取算法会识别出待处理工作异常多或异常少的线程；关联任务过少的线程有时会“窃取”那些有太多任务等待运行的线程中尚未执行的任务。

这些算法的关键特征是它们能够让 TPL 动态调优自身的性能，以缓解过度调度和调度不足的问题，并在可用处理器之间平衡工作。

TPL 通常在调优性能方面做得良好，但通过提供最佳行动方案的提示，可以帮助它做得更好。指定在第 19 章“长时间运行的任务”节中描述的 TPL `TaskCreationOptions.LongRunning` 选项就是此类提示的一个示例。你还可以显式地告诉任务调度器你认为多少线程最适合处理并行循环；参见本章后部分的“高级主题：并行循环选项”获取更多细节。

# 初学者主题

# 使用 AggregateException 处理并行循环异常

TPL 在 `AggregateException` 中捕获并保存与任务相关的异常，因为给定的任务可能会从其子任务中获取多个异常。并行执行循环也是如此：每次迭代都可能产生异常，因此需要将这些异常收集到一个聚合异常中。考虑列表 21.4 中的示例及其在输出 21.2 中的结果。

# 列表 21.4：并行迭代的未处理异常处理

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

public static class Program
{
    static void EncryptFiles(
        string directoryPath, string searchPattern)
    {
        IEnumerable<string> files = Directory.EnumerateFiles(
            directoryPath, searchPattern,
            SearchOption.AllDirectories);

        try
        {
            Parallel.ForEach(files, fileName =>
            {
                Encrypt(fileName);
            });
        }
        catch (AggregateException exception)
        {
            Console.WriteLine(
                "ERROR: {0}",
                exception.GetType().Name);
            foreach(Exception item in exception.InnerExceptions)
            {
                Console.WriteLine("{0} - {1}",
                    item.GetType().Name, item.Message);
            }
        }
        // ...
    }
}
```

# 输出 21.2

```
ERROR: AggregateException:
UnauthorizedAccessException - Attempted to perform an unauthorized operation.
UnauthorizedAccessException - Attempted to perform an unauthorized operation.
UnauthorizedAccessException - Attempted to perform an unauthorized operation.
```

输出 21.2 显示在执行 `Parallel.ForEach<T>(...)` 循环时发生了三个异常。然而，代码只显示了一个类型为 `System.AggregateException` 的 catch 块。`UnauthorizedAccessExceptions` 是从 `AggregateException` 的 `InnerExceptions` 属性获取的。对于 `Parallel.ForEach<T>()` 循环，每次迭代都可能抛出异常，因此方法抛出的 `System.AggregateException` 将在其 `InnerExceptions` 属性中包含这些每一个异常。

# 取消并行循环

与任务不同，任务如果需要阻塞直到完成则需要显式调用，而并行循环并行执行迭代，但在整个并行循环完成之前它不会返回。因此，取消并行循环通常涉及从执行并行循环的线程之外线程调用取消请求。在列表 21.5 中，我们使用 `Task.Run()` 调用了 `Parallel.ForEach<T>()`。通过这种方式，查询不仅并行执行，而且是异步执行，允许代码提示用户“按任意键退出”。

列表 21.5：取消并行循环

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    // ...
    static void EncryptFiles(
        string directoryPath, string searchPattern
    )
    {
        string stars = "*".PadRight(Console.WindowWidth - 1);
        IEnumerable<string> files = Directory.GetFiles(
            directoryPath, searchPattern,
            SearchOption.AllDirectories);

        CancellationToken cts = new CancellationToken();
        ParallelOptions parallelOptions = new ParallelOptions()
        {
            CancellationToken = cts.Token
        };
        cts.Token.Register(() => Console.WriteLine("Canceling..."));

        Console.WriteLine("Press ENTER to exit.");
        // 等待用户输入
        Console.ReadLine();

        // 取消查询
        cts.Cancel();
        Console.Write(stars);
    }
}
```

等等，并行循环使用了与任务相同的取消令牌模式。注意，如果你取消并行循环操作，任何尚未启动的迭代都将被防止启动。正在执行的迭代将运行到终止点。此外，即使在所有迭代完成后调用 `Cancel()`，仍然会导致注册的事件（通过 `cts.Token.Register()`）执行。`ForEach()` 方法确认循环已取消的唯一方法是通过 `OperationCanceledException`。鉴于此示例中的取消是预期的，该异常被捕获并忽略，允许应用程序显示“Canceling...”，随后是一行星号。

# 第 21 章：并行迭代

# 高级主题

并行循环选项
尽管通常是必要的，但可以通过 `Parallel.For()` 和 `Parallel.ForEach<T>()` 循环重载上的 `ParallelOptions` 参数来控制最大并行度（即同时调度运行的线程数量）。在某些特定情况下，开发者可能更了解特定的算法或情况，从而更改最大并行度是有意义的。这些情况包括：

- 你希望禁用并行以便以便更于调试或分析的场景。将最大并行度设置为 1 可以确保循环迭代不会并发运行。
- 你预先知道并行度将受外部因素限制的场景。例如，如果你的并行操作涉及多个 USB 端口，那么创建比可用端口更多的线程可能没有意义。
- 具有长时间运行循环迭代的场景（例如几分钟或几小时）。线程池无法区分长时间运行的迭代和阻塞操作，因此可能会引入许多新线程，所有这些线程将

