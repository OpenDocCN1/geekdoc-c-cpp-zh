
```csharp
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

在列表 19.31 中，LINQ 查询使用 `Select()` 标准查询操作符加密字符串序列中的每个字符串，并将结果序列转换为列表。这似乎是一个令人尴尬的并行操作；每个加密可能是一个高延迟的处理器密集型操作，可以分派给另一 CPU 上的工作线程。

列表 19.32 展示了如何修改列表 19.31，使得加密字符串的代码并行执行。

### 列表 19.32：并行 LINQ Select()

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

正如列表 19.32 所示，启用并行支持的更改极小！它仅使用了一个标准查询操作符 `AsParallel()`，它可以在静态类 `System.Linq.ParallelEnumerable` 中找到。这个简单的扩展方法告知运行时可以并行执行查询。其结果是，在具有多个可用 CPU 的机器上，执行查询所需的总时间可以显著缩短。

`System.Linq.ParallelEnumerable` 是 Microsoft .NET Framework 4.0 中引入的用于启用 PLINQ 的引擎，它包含了 `System.Linq.Enumerable` 上可用的查询操作符的超集。因此，它为所有常见的查询操作符提供了 API，从而实现了潜在的性能提升，包括用于排序、过滤、`Where()`、投影、`Select()`、联接、分组和聚合的操作。清单 19.33 展示了如何执行并行排序。

## 清单 19.33：使用标准查询操作符的并行 LINQ

```csharp
// ...
OrderedParallelQuery<string> parallelGroups =
data.AsParallel().OrderBy(item => item);
// Show the total count of items still
// matches the original count
System.Diagnostics.Assert(
data.Count == parallelGroups.Sum(
item => item.Count()));
// ...
```

正如清单 19.33 所示，调用并行版本仅需调用 `AsParallel()` 扩展方法。请注意，由并行标准查询操作符返回的结果类型是 `ParallelQuery<T>` 或 `OrderedParallelQuery<T>`；这两者都通知编译器应继续使用可用的标准查询操作的并行版本。

鉴于查询表达式仅仅是清单 19.30 和 19.31 中使用的查询方法调用形式的语法糖，你可以同样轻松地使用表达式形式与 `AsParallel()` 配合使用。清单 19.34 展示了使用查询表达式语法并行执行分组操作的示例。

## 清单 19.34：使用查询表达式的并行 LINQ

```csharp
// ...
ParallelQuery<IGrouping<char, string>> parallelGroups;
parallelGroups =
from text in data.AsParallel()
orderby text
group text by text[0];
// Show the total count of items still
// matches the original count
System.Diagnostics.Trace.Assert(
   data.Count == parallelGroups.Sum(
      item => item.Count()));
// ...
```

如前例所示，将查询或迭代循环转换为并行执行非常简单。但是，有一个重要的注意事项：如我们将在第 20 章中深入讨论的那样，你必须小心，避免允许多个线程同时不恰当地访问和修改相同的内存。这样做会导致竞争条件。

如本章前面所述，`Parallel.For()` 和 `Parallel.ForEach<T>` 方法将收集在并行迭代期间抛出的任何异常，然后抛出一个包含所有原始异常的聚合异常。PLINQ 操作也不例外。也就是说，它们也具有返回多个异常的潜在可能，原因完全相同：当查询逻辑在每个元素上并行运行时，在每个元素上执行的代码可以独立抛出异常。不出所料，PLINQ 以与并行循环和 TPL 完全相同的方式处理这种情况：并行查询期间抛出的异常可以通过 `AggregateException` 的 `InnerExceptions` 属性访问。因此，使用异常类型 `System.AggregateException` 的 try/catch 块包装 PLINQ 查询，将成功处理每次迭代中未被处理的任何异常。

## 取消 PLINQ 查询

如预期那样，取消请求模式也可用于 PLINQ 查询。清单 19.35（配合输出 19.11）提供了一个示例。与并行循环类似，被取消的 PLINQ 查询将抛出 `System.OperationCanceledException`。同样，执行 PLINQ 查询是调用线程上的同步操作。因此，一种常见技术是将并行查询包装在一个运行于另一线程的任务中，以便当前线程在必要时取消它——这与清单 19.30 中使用的解决方案相同。

## 清单 19.35：取消 PLINQ 查询

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading;
using System.Threading.Tasks;
public class Program
{
    public static List<string> ParallelEncrypt(
        List<string> data,
        CancellationToken cancellationToken)
    {
        return data.AsParallel().WithCancellation(
        cancellationToken).Select(
        (item) => Encrypt(item)).ToList();
    }
    public static void Main()
    {
        ConsoleColor originalColor = Console.ForegroundColor;
        List<string> data = Utility.GetData(1000000).ToList();
        CancellationTokenSource cts =
            new CancellationTokenSource();
        Console.WriteLine("Push ENTER to Exit.");
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task task = Task.Run(() =>
        {
            data = ParallelEncrypt(data, cts.Token);
        }, cts.Token);
        // Wait for the user's input
        Console.Read();
        if (!task.IsCompleted)
        {
            cts.Cancel();
            try { task.Wait(); }
            catch (AggregateException exception)
            {
                Console.ForegroundColor = ConsoleColor.Red;
                TaskCanceledException taskCanceledException =
                    (TaskCanceledException)exception.Flatten()
                        .InnerExceptions
                        .FirstOrDefault(
                            innerException =>
                            innerException.GetType() ==
                            typeof(TaskCanceledException));
                if(taskCanceledException != null){
                    Console.WriteLine($@"Canceled: {
                        taskCanceledException.Message }");
                }
                else
                {
                    /// ...
                }
            }
        }
        else
        {
            task.Wait();
            Console.ForegroundColor = ConsoleColor.Green;
            Console.Write("Completed successfully");
        }
        Console.ForegroundColor = originalColor;
    }
}
```

**输出 19.11**
Canceled: A task was canceled.

与并行循环或任务一样，取消 PLINQ 查询需要一个 `CancellationToken`，它可以从 `CancellationTokenSource` 中获取。然而，PLINQ 没有重载每个查询以支持取消令牌，而是由 `IEnumerable` 的 `AsParallel()` 方法返回的 `ParallelQuery<T>` 对象包含一个 `WithCancellation()` 扩展方法，该方法仅接收一个 `CancellationToken`。结果是，对 `CancellationTokenSource` 对象调用 `Cancel()` 将请求取消并行查询——因为它检查 `CancellationToken` 上的 `IsCancellationRequested` 属性。

如前所述，取消 PLINQ 查询将抛出异常而不是返回完整结果。处理可能被取消的 PLINQ 查询的一种常见技术是将查询包装在 try 块中并捕获 `OperationCanceledException`。第二种常见技术，如清单 19.35 中所示，是将 `CancellationToken` 同时传递给 `ParallelEncrypt()` 和作为 `Run()` 的第二个参数。这将导致 `task.Wait()` 抛出一个 `AggregateException`，其 `InnerException` 属性将被设置为 `TaskCanceledException`。然后可以捕获该聚合异常，就像捕获并行操作中的其他任何异常一样。

## 摘要

在本章中，我们首先考察了多线程程序的基本组成部分：`Thread` 类，它代表程序中的一个独立控制点；以及 `ThreadPool`，它鼓励高效地将线程分配和调度到多个 CPU 上。然而，这些 API 是低层实体，直接操作起来比较困难。从版本 4.0 开始，Microsoft .NET Framework 提供了并行扩展库，其中包含任务并行库（TPL）和并行 LINQ（PLINQ）。两者都提供了新的 API，用于创建和调度由 `Task` 对象表示的工作单元，使用 `Parallel.For()` 和 `Parallel.ForEach()` 并行执行循环，以及使用 `AsParallel()` 自动并行化 LINQ 查询。

我们还讨论了 C# 5.0（及更高版本）如何使使用 `Task` 对象编程复杂工作流变得更容易，通过自动重写你的程序来管理将小任务组合成大任务的延续“接线”。

在本章开始时，我们简要掠过了一些开发者在编写多线程程序时经常面临的棘手问题：原子性问题、死锁以及引入不确定性和不良行为的其他竞争条件。避免这些问题的标准方法是仔细编写使用锁来同步访问共享资源的代码；这是下一章的主题。

# 第20章 线程同步

在第19章中，我们讨论了使用任务并行库（Task Parallel Library, TPL）和并行LINQ（PLINQ）进行多线程编程的细节。然而，我们特意回避了一个主题：线程同步。线程同步旨在防止竞态条件的同时避免死锁。本章的主题就是线程同步。

我们从一个多线程示例开始，该示例对共享数据没有任何线程同步机制，导致出现竞态条件，进而造成数据完整性丢失。这段讨论作为引言，解释了为什么我们需要线程同步。随后，我们将详细介绍实现同步的众多机制和最佳实践。

本书的早期版本中包含了一个关于额外多线程模式的重要章节，以及另一个关于各种计时器回调机制的章节。然而，随着 async/await 模式的引入，除非你在使用早于 C# 5.0/.NET 4.5 的框架进行编程，否则这些方法基本上已被取代。但是，关于 C# 5.0 之前内容的资料仍可在本书网站上找到：https://IntelliTect.com/EssentialCSharp.

本章整体使用 TPL，因此示例无法在早于 Microsoft .NET Framework 4 的框架上编译。不过，除非特别指明是 Microsoft .NET Framework 4 API，否则对 Microsoft .NET Framework 4 的限制仅仅是因为使用了 `System.Threading.Tasks.Task` 类来执行异步操作。如果修改代码以实例化 `System.Threading.Thread` 并使用 `Thread.Join()` 等待线程执行，绝大多数示例都能在较早的框架上编译。

话虽如此，本章中用于启动任务的具体 API 是 .NET 4.5（或更高版本）的 `System.Threading.Tasks.Task.Run()`。正如我们在第19章中讨论的，这种方法优于 `System.Threading.Tasks.Task.Factory.StartNew()`，因为它更简单，且足以应对大多数场景。如果你受限于 .NET 4，可以在不做其他修改的情况下，用 `Task.Factory.StartNew()` 替换 `Task.Run()`。（出于这个原因，当仅使用此方法时，本章不会明确强调此类代码是 .NET 4.5 特有的代码。）

## 为什么要同步？

启动新线程是一个相对简单的编程任务。然而，使多线程编程变得困难的，是识别哪些数据可以被多个线程安全地同时访问。程序必须对这类数据进行同步，以防止同时访问，从而创建“安全性”。请参见列表 20.1。

### 列表 20.1：未同步的状态

```csharp
using System;
using System.Threading.Tasks;
public class Program
{
    const int _Total = int.MaxValue;
    static long _Count = 0;
    public static void Main()
    {
        // 在 .NET 4.0 中请使用 Task.Factory.StartNew
        Task task = Task.Run(() => Decrement());
        // 递增
        for (int i = 0; i < _Total; i++)
        {
            _Count++;
        }
        task.Wait();
        Console.WriteLine("Count = {0}", _Count);
    }
    static void Decrement()
    {
        // 递减
        for (int i = 0; i < _Total; i++)
        {
            _Count--;
        }
    }
}
```
