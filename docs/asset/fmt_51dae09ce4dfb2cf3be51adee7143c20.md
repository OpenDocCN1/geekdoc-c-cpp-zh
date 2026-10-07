
此外，任何方法都是长时间运行的，多线程编程——也就是说，异步地调用长时间运行的方法。遗憾的是，C# 5.0 之前的多线程编程需要使用一个相对低级的 `System.Thread` 类，该类几乎没有模式可以避免这些这些复杂性。

然而，随着开发者编写更多的多线程代码，出现了一组常见的场景和编程模式……

# 第19章：引入多线程

通过调用 `Task.Start()` 触发的返回已正在运行（热的）任务的 API 内部细节。

请注意，在调用 `Run()` 之后，热任务的确切状态是不定的。其行为由操作系统、其负载以及伴随的任务库共同决定的。这种组合决定了 `Run()` 是选择立即执行工作线程，还是推迟到有可用资源为止。事实上，当调用线程再次获得执行轮机时，该热任务可能已经完成。对 `Wait()` 的调用会强制主线程等待，直到分配给任务的所有工作执行完毕。

在这种场景下，我们有一个任务，但也有可能许多任务在异步运行。在继续执行当前线程之前，等待所有任务完成或等待其中任何一个任务完成是十分常见的常常做法。`Task.WaitAll()` 和 `Task.WaitAny()` 方法分别就是实现了这些操作。

到目前为止，我们已经看到了任务如何接收一个 `Action` 并异步运行它。但如果在任务中执行的工作返回了结果呢？我们可以使用 `Task<T>` 类型来异步运行 `Func<T>`。当同步执行委托时，我们知道在结果可用之前控制权不会返回。当异步执行 `Task<T>` 时，我们可以从一个线程对其进行轮询以检查它是否完成，并在完成后获取结果。列表 19.2 展示了如何在简单的计算器中这样操作。请注意，此示例使用了 `PiCalculator.Calculate()` 方法，我们将在第 21 章的“并行执行循环迭代”节中深入探讨。

## 列表 19.2：轮询 Task<T>

```sharp
using System;
using System.Threading.Tasks;

public class Program
{
```

- 使用此技术时要格外谨慎。当像我们这里这样从委托创建任务时，任务将会在调度到线程池的工作线程上运行。结果是，当前线程将一直循环，直到工作线程上的工作完成。这种技术虽然可行，但它可能会不必要地消耗 CPU 资源。轮询技术上，如果你不是将任务调度在工作线程上运行，而是将其调度在未来在当前线程上执行，那么这种技术就是危险且错误的。由于当前线程在循环中进行轮询，它将永远循环下去，因为在当前线程退出循环之前，任务将不会完成。

### 异步任务

```csharp
public static void Main()
{
    // 在 .NET 4.5 之前的 TPL 
    // 使用 Task.StartNew<string>()
    Task<string> task =
        Task.Run(
            () => PiCalculator.Calculate(100));

    foreach (
    {
        foreach (char busySymbol in Utility.BusySymbols())
        {
            if (task.IsCompleted)
            {
                Console.Write('\b');
                break;
            }
            Console.Write(busySymbol);
        }
    })

    Console.WriteLine();

    Console.WriteLine(task.Result);
    System.Diagnostics.Trace.Assert(
        task.IsCompleted);
}

public class PiCalculator
{
    public static string Calculate(int digits = 100)
    {
        // ...
    }
}

public class Utility
{
    public static IEnumerable<char> BusySymbols()
    {
        string busySymbols = "@-\|\\|/";
        int next = 0;
        while (true)
        {
            yield return busySymbols[next];
            next = (next + 1) % busySymbols.Length;
            yield return '\b';
        }
    }
}
```

此列表显示任务的数据类型为 `Task<string>`。泛型类型包含一个 `Result` 属性，通过该属性可以获取 `Task<string>` 执行的 `Func<string>` 返回的值。

请注意，列表 19.2 中，除了 `IsCompleted` 属性外，还有其他值得注意的属性： 任务的状态可以通过 `TaskStatus` 枚举获取，可能的值包括 `Created`、`WaitingForActivation`、`WaitingToRun`、`WaitingForChildren`、`RanToCompletion`、`Canceled` 和 `Faulted`。当任务完成时（无论是正常完成还是故障），`IsCompleted` 属性会被设置为 true。任务可以通过 `Id` 属性进行唯一标识。静态 `Task.CurrentId` 提供了当前执行任务的标识符。这些属性在调试时非常有用。- 当任务在另一个线程上运行期间，状态可能会发生变化。只有 `RanToCompletion`、`Canceled` 和 `Faulted` 被视为最终状态。- 你可以使用 `AsyncState` 与任务关联额外数据。例如，想象一个通过各种任务计算的 `List<T>`。通过这种方式，当任务完成时，代码可以索引 `AsyncState`。- 使用任务修改集合时要小心。任务可能在工作线程上运行，集合可能不是线程安全的。

## 任务延续

我们多次讨论了程序的控制流，但没有说明控制流的本质：控制流决定了接下来会发生什么。当你有一个简单的控制流如 `Console.WriteLine(x.ToString());` 时，控制流告诉你 `ToString` 完成了，下一步是调用 `WriteLine`。这种“接下来发生什么”的概念被称为延续（Continuation）；控制流中的每个点都有延续。在示例中，`ToString` 的延续是 `WriteLine`（而 `WriteLine` 的延续则是后续的代码）。延续的概念在 C# 编程中如此基础，以至于大多数程序员甚至不会考虑它；它是我们呼吸的空气。C# 编程的行为就是不断构建延续，直到整个程序的控制流完成。

请注意，在普通的 C# 程序中，给定代码段的延续将在代码完成后立即执行。当 `ToString()` 返回时，当前线程的控制点会立即同步调用 `WriteLine`。注意，给定代码段实际上有两个可能的延续：正常延续以及当当前代码抛出异常时执行的异常延续。

异步方法调用（如启动任务）为控制流增加了一个额外的维度。在异步任务调用时，控制流会立即跳转到 `Task.Start()` 之后的语句，同时它开始在任务委托体内部执行。换句话说，当涉及到异步时，接下来会发生什么是多维度的。与异常不同，延续只是另一条路径，延续是一个额外的、行的路径。

异步任务还允许通过描述异步延续将小任务组合成大任务。实现这一点有多种技术，最显式的是 `ContinueWith()` 方法（见列表 19.3 及其对应的输出 输出 19.1）。

## 列表 19.3：调用 Task.ContinueWith()

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Starting...");
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task taskA =
        Task.Run(() =>
        {
            Console.WriteLine("Starting...");
        }).ContinueWith(antecedent =>
        {
            Console.WriteLine("Continuing A...");
        });
        Task taskB = taskA.ContinueWith(antecedent =>
        {
            Console.WriteLine("Continuing B...");
        });
        Task taskC = taskA.ContinueWith(antecedent =>
        {
            Console.WriteLine("Continuing C...");
        });
        Task.WaitAll(taskB, taskC);
        Console.WriteLine("Finished!");
    }
}
```

## 输出 19.1

```
Before
Starting...
 A...
Continuing C...
Continuing B...
Finished!
```

`ContinueWith()` 方法允许将两个任务“链”在一起，当先前的任务——即前驱任务（antecedent task）完成时，第二个任务——延续任务（continuation task）会自动异步启动。…… `Console.WriteLine("Starting...")` 是前驱任务体，而 `Console.WriteLine("Continuing A...")` 是它的延续任务体。延续任务接受一个 `Task` 作为参数（前驱），允许延续任务的代码访问前驱任务的完成状态。当前驱任务完成时，延续任务会自动启动，异步执行第二个委托程序，并将刚刚完成的前驱任务作为参数传递给委托程序。此外，由于 `ContinueWith()` 方法也返回一个 `Task`，该 `Task` 可以用作另一个任务的前驱任务，以此此类推，形成一个长度可以任意延伸的任务延续链。

如果你对同一个前驱任务调用了两次 `ContinueWith()`（如列表 19.3 所示，`taskB` 和 `taskC` 代表 `taskA` 的延续任务），则前驱任务（`taskA`）有两个延续任务，当前驱任务完成时，两个延续任务都将异步执行。注意，从单个前驱任务开始的任务执行顺序在编译时是不确定的。输出 19.1 恰好显示 `taskC` 在 `taskB` 之前执行，但在程序的第二次执行中，顺序可能会反过来。然而，`taskA` 始终会在 `taskB` 和 `taskC` 之前执行，因为后者是 `taskA` 的延续任务，因此无法在 `taskA` 完成之前启动。同样，`Console.WriteLine("Starting...")` 委托程序始终会在 `taskA`（`Console.WriteLine("Continuing...")`）完成之前执行，因为后者是前者的延续。此外，`Finished!` 总是最后出现，这是因为调用了 `Task.WaitAll(taskB, taskC)`，该调用会阻塞控制流，直到 `taskB` 和 `taskC` 都完成才会继续。

`ContinueWith()` 有许多不同的重载，其中某些重载接受一个 `TaskContinuationOptions` 值来微调延续链的行为。这些值是标志位（flags），因此可以使用逻辑或运算符 (`|`) 将它们组合。表 19.1 简要描述了一些可能的标志位值；更多详情请参阅在线文档。

### 表 19.1: 可用的 TaskContinuationOptions 枚举列表

| 枚举 | 描述 |
|---|---|
| None | 这是默认行为。当前驱任务完成时，无论其任务状态如何，都会执行延续任务。 |

7. Microsoft .NET Docs, https://docs.microsoft.com/dotnet/api/system.threading.taskcontinuationoptions.

### 表 19.1: 可用的 TaskContinuationOptions 枚举列表（续）

| 枚举 | 描述 |
|---|---|
| PreferFairness | 如果两个任务都是被异步启动的，且一个在另一个之前，则不能保证先启动的那个实际上会先运行。此标志请求任务调度器尝试增加第一个启动的任务成为第一个执行任务的概率——当您描述的两个任务从不同的线程池中创建时，这一点尤为相关。 |
| LongRunning | 这告诉任务调度器该任务可能是一个 I/O 高延迟任务。调度器随后可以允许处理队列中的其他工作，而不是因为长时间运行的任务而导致饥饿。此选项应谨慎使用。 |
| AttachedToParent | 这指定任务应尝试附加到任务层次结构中的父任务。 |
| DenyChildAttach (.NET 4.5) | 如果尝试创建子任务，将抛出异常。如果延续任务中的代码尝试使用 `AttachedToParent`，其行为将像没有父任务一样。 |
| NotOnRanToCompletion* | 这指定如果前驱任务运行完成，则不应调度延续任务。此选项对于多任务延续无效。 |
| NotOnFaulted* | 这指定如果前驱任务抛出了未处理的异常，则不应调度延续任务。此选项对于多任务延续无效。 |
| OnlyOnCanceled* | 这指定只有在在前驱任务被取消时，才调度延续任务。此选项对于多任务延续无效。 |

### 异步任务

### 表 19.1: 可用的 TaskContinuationOptions 枚举列表（续）

| 枚举 | 描述 |
|---|---|
| NotOnCancelled* | 这指定如果前驱任务被取消，则不应调度延续任务。此选项对于多任务延续无效。 |
| OnlyOnFaulted* | 这指定只有在在前驱任务抛出未处理的异常时，才调度延续任务。此选项对于多任务延续无效。 |
| OnlyOnRanToCompletion* | 这指定只有在在前驱任务运行完成时，才调度延续任务。此选项对于多任务延续无效。 |
| ExecuteSynchronously | 这指定延续任务应同步执行。指定此选项后，调度将尝试在导致前驱任务转换到其最终状态的同一线程上执行工作。如果在延续任务运行时前驱已经完成，则将在创建延续任务的线程上执行。 |
| HideScheduler (.NET 4.5) | 这防止环境调度器被视为当前调度器。这意味着在所创建的任务中执行的 `Run/StartNew` 和 `ContinueWith` 操作会将 `TaskScheduler.Default` (null) 作为当前调度器。当延续应在特定调度器上运行，但延续调用了不应在该调度器上调度工作的代码时，这非常有用。 |

### 表 19.1: 可用的 TaskContinuationOptions 枚举（续）

| 枚举 | 描述 |
|---|---|
| LazyCancellation (.NET 4.5) | 这导致延续在前驱任务完成之前延迟监控取消令牌。考虑任务 t1、t2 和 t3，后者是前者的延续。如果 t2 在 t1 完成之前被取消，则 t3 可能在 t1 完成之前启动。LazyCancellation 避免了这种情况。 |
| RunContinuationsAsynchronously (.NET 4.6) | 当使用 `RunContinuationsAsynchronously` 选项创建任务时，它告诉任务应强制其延续异步运行。即使任务本身是延续，此选项也不会影响该任务的运行方式——只影响从它发出的延续。可以同时使用 `TaskContinuationOptions.ExecuteSynchronously` 和 `TaskContinuationOptions.RunContinuationsAsynchronously` 创建延续。前者在前驱完成时同步执行延续，并在延续完成后异步执行该延续的延续。 |

在任务 19.1 中，带有星号 (*) 的项目指定了延续任务执行的条件；它们对于创建像前驱任务行为的事件处理程序的延续任务特别有用。列表 19.4 展示了如何为前驱任务分配多个根据前驱任务完成情况有条件执行的延续任务。

## LISTING 19.4: 使用 ContinueWith() 注册任务行为通知

```csharp
using System;
using System.Threading.Tasks;
using System.Diagnostics;
using AddisonWesley.Michaelis.EssentialCSharp.Shared
```

## 异步任务
