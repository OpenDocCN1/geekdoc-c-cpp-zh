

## 代码示例：忙碌指示器

```csharp
foreach(
    char busySymbol in Utility.BusySymbols())
{
    if(task.IsCompleted)
    {
        Console.Write('\b');
        break;
    }
    Console.Write(busySymbol);
}
Console.WriteLine();
Console.WriteLine(task.Result);
System.Diagnostics.Trace.Assert(
    task.IsCompleted);
```

```csharp
public class PiCalculator
{
    public static string Calculate(int digits = 100)
    {
        // ...
    }
}
```

```csharp
public class Utility
{
    public static IEnumerable<char> BusySymbols()
    {
        string busySymbols = @"-~\/|";
        int next = 0;
        while(true)
        {
            yield return busySymbols[next];
            next = (next + 1) % busySymbols.Length;
            yield return '\b';
        }
    }
}
```

此列表表明该任务的数据类型为 `Task<string>`。泛型类型包含一个 `Result` 属性，用于检索由 `Task<string>` 执行的 `Func<string>` 返回的值。

注意，列表 19.4 并未调用 `Wait()`。相反，从 `Result` 属性读取值会自动导致当前线程阻塞，直到结果可用为止（如果结果尚未可用）；在这种情况下，我们知道在获取结果时任务已经完成。

除了 `Task<T>` 上的 `IsCompleted` 和 `Result` 属性外，还有几个值得注意的属性：

- 当任务完成时，无论是正常完成还是发生故障（即因抛出异常而结束），`IsCompleted` 属性都会被设置为 `true`。通过读取返回 `TaskStatus` 类型值的 `Status` 属性，可以获得有关任务状态的更详细信息。可能的值包括 `Created`、`WaitingForActivation`、`WaitingToRun`、`Running`、`WaitingForChildrenToComplete`、`RanToCompletion`、`Canceled` 和 `Faulted`。每当 `Status` 为 `RanToCompletion`、`Canceled` 或 `Faulted` 时，`IsCompleted` 均为 `true`。当然，如果任务在另一个线程上运行，并且你读取的状态为运行中，该状态可能会随时变为已完成状态，包括在读取属性值之后立即发生。许多其他状态也是如此——甚至 `Created` 状态也可能因另一个线程启动任务而改变。只有 `RanToCompletion`、`Canceled` 和 `Faulted` 可以被视为不再发生状态转换的最终状态。

- 可以通过 `Id` 属性的值唯一标识一个任务。静态 `Task.CurrentId` 属性提供当前正在执行的 `Task` 的标识符（即执行 `Task.CurrentId` 调用所在的线程对应的任务）。这些属性在调试时特别有用。

- 你可以使用 `AsyncState` 将与任务关联的附加数据。例如，假设有一个 `List<T>`，其值将由各种任务计算得出。每个任务都可以在 `AsyncState` 属性中包含该值在列表中的索引。这样，当任务完成时，代码可以使用 `AsyncState`（先将其强制转换为 `int`）来索引该列表。¹

我们稍后会在本章中“取消任务”部分讨论其他有用的属性。

> 5. 使用任务异步修改集合时要小心。任务可能在工作者线程上运行，而集合可能不是线程安全的。更安全的做法是在任务完成后，从主线程填充集合。

## 任务延续

我们多次讨论过程序的控制流，却从未提及控制流最基本的本质：控制流决定了接下来会发生什么。当你拥有一个简单的控制流，如 `Console.WriteLine(x.ToString());` 时，控制流告诉你，当 `ToString` 正常完成后，接下来发生的事情是调用 `WriteLine`，并将返回值作为参数传入。“接下来发生什么”的概念被称为**延续**；控制流中的每个点都有一个延续。在我们的示例中，`ToString` 的延续是 `WriteLine`（而 `WriteLine` 的延续是下一条语句中运行的任何代码）。延续的概念对于 C# 编程来说非常基础，以至于大多数程序员甚至不会去思考它；它是他们呼吸的看不见空气的一部分。C# 编程的过程就是构建一个又一个延续，直到整个程序的控制流完成。

注意，在普通的 C# 程序中，给定代码的延续会在该代码完成后*立即*执行。当 `ToString()` 返回时，当前线程的控制点会立即同步调用 `WriteLine`。还要注意，给定代码实际上有两个可能的延续：*正常*延续和如果当前代码抛出异常时将执行的*异常*延续。

异步方法调用，如启动一个 `Task`，为控制流增加了另一个维度。在异步 `Task` 调用中，控制流立即仅指向 `Task.Start()` 之后的语句，与此同时，它开始在 `Task` 委托的主体内执行。换句话说，涉及异步性时，接下来发生什么是多维的。与异常不同（其延续只是另一条路径），异步性的延续是一条额外的并行路径。

异步任务还允许通过描述异步延续将较小的任务组合成较大的任务。与常规控制流类似，任务可以有不同的延续来处理错误情况，并且可以通过操作其延续将任务合并在一起。有几种技术可以做到这一点，其中最明确的是 `ContinueWith()` 方法（参见列表 19.5 及其对应输出，输出 19.2）。

### 列表 19.5：调用 Task.ContinueWith()

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Before");
        // 在 .NET 4.5 之前的 TPL 中，
        // 使用 Task.Factory.StartNew<string>()
        Task taskA =
            Task.Run(() =>
                Console.WriteLine("Starting..."))
                .ContinueWith(antecedent =>
                    Console.WriteLine("Continuing A..."));
        Task taskB = taskA.ContinueWith(antecedent =>
            Console.WriteLine("Continuing B..."));
        Task taskC = taskA.ContinueWith(antecedent =>
            Console.WriteLine("Continuing C..."));
        Task.WaitAll(taskB, taskC);
        Console.WriteLine("Finished!");
    }
}
```

### 输出 19.2

![](img/ef6a8a417630b222bfb3f3b949facff0_833_0.png)

`ContinueWith()` 方法允许将两个任务“链接”在一起，使得当前序任务——即**前置任务**——完成时，第二个任务——即**延续任务**——会自动异步启动。例如，在列表 19.5 中，`Console.WriteLine("Starting...")` 是前置任务主体，而 `Console.WriteLine("Continuing A...")` 是其延续任务主体。延续任务以一个 `Task` 作为其参数（前置任务），从而允许延续任务的代码访问前置任务的完成状态。当前置任务完成时，延续任务自动启动，异步执行第二个委托，并将刚刚完成的前置任务作为参数传递给该委托。此外，由于 `ContinueWith()` 方法也返回一个 Task，该 Task 可以用作另一个 Task 的前置任务，依此类推，形成一个可以任意长度的任务延续链。

如果你对同一个前置任务调用两次 `ContinueWith()`（如列表 19.5 所示，`taskB` 和 `taskC` 代表 `taskA` 的延续任务），那么前置任务（`taskA`）将有两个延续任务，当前置任务完成时，这两个延续任务都会异步执行。请注意，来自单个前置任务的延续任务的执行顺序在编译时是不确定的。输出 19.2 恰好显示 `taskC` 在 `taskB` 之前执行，但在程序的第二次运行中，顺序可能会反转。然而，`taskA` 总是会先于 `taskB` 和 `taskC` 执行，因为后者是 `taskA` 的延续任务，因此在 `taskA` 完成之前不能启动。同样，`Console.WriteLine("Starting...")` 委托总是会先于 `taskA`（`Console.WriteLine("Continuing A...")`）执行完毕，因为后者是前者的延续任务。此外，由于对 `Task.WaitAll(taskB, taskC)` 的调用会阻塞控制流，直到 `taskB` 和 `taskC` 都完成，因此 `Finished!` 总是最后出现。

`ContinueWith()` 有许多不同的重载，其中一些接受 `TaskContinuationOptions` 值来调整延续链的行为。这些值是标志，因此可以使用逻辑或运算符（`|`）进行组合。表 19.1 简要介绍了一些可能的标志值；有关更多细节，请参阅在线 MSDN 文档²。

**表 19.1：可用的 TaskContinuationOptions 枚举列表**

| 枚举 | 描述 |
| :--- | :--- |
| None | 这是默认行为。无论前置任务的状态如何，当前置任务完成时，都会执行延续任务。 |

> ² MSDN .NET Framework 开发人员中心，http://msdn.microsoft.com/en-us/library/system.threading.tasks.taskcontinuationoptions(v=vs.110).aspx

