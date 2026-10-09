
## **列表 19.30：取消并行循环**

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
        string directoryPath, string searchPattern)
    {

        string stars =
            "*".PadRight(Console.WindowWidth-1, '*');

        IEnumerable<string> files = Directory.GetFiles(
            directoryPath, searchPattern,
            SearchOption.AllDirectories);

        CancellationTokenSource cts =
            new CancellationTokenSource();
        ParallelOptions parallelOptions =
            new ParallelOptions
                { CancellationToken = cts.Token };
        cts.Token.Register(
            () => Console.WriteLine("Canceling..."));

        Console.WriteLine("Press ENTER to exit.");

        Task task = Task.Run(() =>
        {
            try
            {
                Parallel.ForEach(
                    files, parallelOptions,
                    (fileName, loopState) =>
                    {
                        Encrypt(fileName);
                    });
            }
            catch(OperationCanceledException){}
        });

        // Wait for the user's input
        Console.Read();

        // Cancel the query
        cts.Cancel();
        Console.Write(stars);
        task.Wait();
    }
}
```

![](img/ef6a8a417630b222bfb3f3b949facff0_889_0.png)

并行循环使用了与任务相同的取消令牌模式。从 *CancellationTokenSource* 获取的令牌通过调用 *ForEach()* 方法的某个重载与并行循环相关联，该方法具有类型为 *ParallelOptions* 的参数。此对象包含取消令牌。

请注意，如果您取消并行循环操作，任何尚未开始的迭代都会通过检查 *IsCancellationRequested* 属性而被阻止开始。正在执行迭代将继续运行到各自的终止点。此外，即使在所有迭代都完成后调用 *Cancel()*，仍会导致注册的取消事件（通过 *cts.Token.Register()*）执行。

*ForEach()* 方法承认循环已被取消的唯一手段是通过 *OperationCanceledException*。鉴于在此示例中取消是预期的，该异常会被捕获并忽略，从而允许应用程序在退出前显示“Canceling...”后跟一行星号。

### **高级主题：并行循环选项**

虽然通常不需要，但可以通过 *Parallel.For()* 和 *Parallel.ForEach<T>()* 循环的重载中的 *ParallelOptions* 参数来控制最大并行度（即计划同时运行的线程数）。在某些特定情况下，开发人员可能对特定算法或情况有更多了解，使得改变最大并行度是有意义的。这些情况包括以下情形：

- 希望禁用并行性以简化调试或分析的场景。将最大并行度设置为 1 可确保循环迭代不会并发运行。
- 提前知道并行度将受外部因素（如硬件约束）限制的场景。例如，如果您的并行操作涉及使用多个 USB 端口，那么创建比可用端口更多的线程可能没有意义。
- 具有非常长的循环迭代时间（例如，几分钟或几小时）的场景。线程池无法区分长时间运行的迭代和阻塞操作，因此最终可能会引入许多新线程，所有线程都会被 `for` 循环消耗。这可能导致线程随时间逐渐增长，结果进程中拥有大量的线程。
- 等等。

要控制最大并行度，请使用 ParallelOptions 对象上的 MaxDegreeOfParallelism 属性。

您还可以使用 `ParallelOptions` 对象的 `TaskScheduler` 属性来指定用于安排与每个迭代相关的任务的自定义任务调度器。例如，您可能有一个异步事件处理器，响应用户单击“Next”按钮。如果用户多次单击该按钮，您可能希望使用一个自定义任务调度器，该调度器优先考虑最近创建的任务，而不是优先考虑等待时间最长的任务。任务调度器提供了一种指定任务之间如何执行的方式。

`ParallelOptions` 对象还有一个 Cancellation Token 属性，提供了一种向循环通信不再开始更多迭代的机制。此外，迭代的主体可以监视取消令牌，以确定是否应该提前退出迭代。

### **高级主题：终止并行循环**

与标准 `for` 循环一样，`Parallel.For()` 循环支持“break”概念以退出循环并取消任何进一步的迭代。然而，在并行 `for` 执行上下文中，break 表示在发生 break 的迭代之后的任何新迭代都不应开始。不过，当前正在执行的所有迭代都将继续运行到完成。

要终止并行循环，您可以提供一个取消令牌并在另一个线程上取消它，如前面的高级主题中所述。

您还可以使用 `Parallel.For()` 方法的一个重载，其主体委托接受两个参数：索引和一个 `ParallelLoopState` 对象。希望终止循环的迭代可以调用传递给委托的循环状态对象上的 `Break()` 或 `Stop()` 方法。`Break()` 方法表示不需要再执行索引值高于当前值的迭代；`Stop()` 方法表示完全不需要再执行任何迭代。

例如，假设您有一个执行十次并行迭代的 `Parallel.For()` 循环。其中一些迭代可能比其他迭代运行得更快，且任务调度器不保证它们会以任何特定顺序运行。假设第一次迭代已完成；迭代 3、5、7 和 9 正在“进行中”，调度到四个不同的线程；并且迭代 5 和 7 都调用了 `Break()`。在这种情况下，迭代 6 和 8 永远不会开始，但迭代 2 和 4 仍会被调度运行。迭代 3 和 9 将运行到完成，因为它们在发生 break 时已经开始。

`Parallel.For()` 和 `Parallel.ForEach<T>()` 方法返回指向 `ParallelLoopResult` 对象的引用，其中包含有关循环期间发生情况的有用信息。此结果对象具有以下属性：

- `IsCompleted` 返回一个布尔值，指示是否已启动所有迭代。
- `LowestBreakIteration` 标识执行了 break 的最低迭代。该值类型为 `long?`，其中 `null` 值表示未遇到 break 语句。

回到十次迭代的例子中，`IsCompleted` 属性将返回 `false`，而 `LowestBreakIteration` 将返回值为 5。

## **并行运行 LINQ 查询**

正如可以使用 `Parallel.For()` 并行执行循环一样，也可以使用并行 LINQ API（简称为 PLINQ）并行执行 LINQ 查询。列表 19.31 中展示了一个简单的非并行 LINQ 表达式示例；在列表 19.32 中，我们修改它以并行运行。

### **列表 19.31：LINQ Select()**

```csharp
using System.Collections.Generic;
using System.Linq;

class Cryptographer
{
    // ...
    public List<string>
        Encrypt(IEnumerable<string> data)
    {
        return data.Select(
            item => Encrypt(item)).ToList();
    }
    // ...
}
```

在列表 19.31 中，LINQ 查询使用 Select() 标准查询操作符加密字符串序列中的每个字符串，并将结果序列转换为列表。这似乎是一个令人尴尬的并行操作；每个加密可能是一个高延迟的处理器密集型操作，可以分派给另一 CPU 上的工作线程。

列表 19.32 展示了如何修改列表 19.31，使得加密字符串的代码并行执行。

### **列表 19.32：并行 LINQ Select()**

```csharp
using System.Linq;

class Cryptographer
{
    // ...
    public List<string> Encrypt (IEnumerable<string> data)
    {
        return data.AsParallel().Select(
            item => Encrypt(item)).ToList();
    }
    // ...
}
```

正如列表 19.32 所示，启用并行支持的更改极小！它仅使用了一个标准查询操作符 AsParallel()，它可以在静态类 System.Linq.ParallelEnumerable 中找到。这个简单的扩展方法告知运行时可以并行执行查询。其结果是，在具有多个可用 CPU 的机器上，执行查询所需的总时间可以显著缩短。

