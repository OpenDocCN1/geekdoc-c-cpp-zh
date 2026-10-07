
```csharp
public class Program
{
    public static void Main()
    {
        // 在 .NET 4.5 之前的 TPL 使用 Task.Factory.StartNew<string>()
        Task<string> task = 
            Task.Run(() => Calculator.Calculate(10));

        Task faultedTask = task.ContinueWith(
            (antecedentTask) => {
                Trace.Assert(antecedentTask.IsFaulted);
                Console.WriteLine(
                    "Task State: 故障（Faulted）");
            },
            ContinuationOptions.OnlyOnFaulted);

        Task canceledTask = task.ContinueWith(
            (antecedentTask) => {
                Trace.Assert(antecedentTask.IsCanceled);
                Console.WriteLine(
                    "Task State: 已取消（Canceled）");
            },
            ContinuationOptions.OnlyOnCancelled);

        Task completedTask = task.ContinueWith(
            (antecedentTask) => {
                Trace.Assert(antecedentTask.IsCompleted);
                Console.WriteLine(
                    "Task State: 已完成（Completed）");
            },
            ContinuationOptions.OnlyOnRanToCompletion);

        completedTask.Wait();
    }
}
```

在此列表中，我们实际上为先置任务的事件注册了监听器，这样当任务正常或异常完成时，特定的“监听”任务将开始执行。这是一项非常强大的能力，特别是当原始任务是一个“触发后遗忘”的任务时——即一个我们启动它、让其连接到延续任务、然后再也不引用的任务。

在列表 19.4 中，注意最后的 `Wait()` 调用是针对 `completedTask` 而不是 `task`——即通过 `Task.Run()` 创建的原始先置任务。虽然每个委托的 `antecedentTask` 都是先置任务（`task`）的引用，但在委托监听器的外部，我们可以有效地丢弃对原始任务的引用。然后，我们可以完全依赖延续任务的异步启动，而无需任何检查原始任务状态的后续。在这种情况下，我们调用 `completedTask.Wait()`，以便主线程不会在完成输出出现之前退出程序（参见输出 19.2）。

# 输出 19.2

`Task State: Completed.`

在这种情况下，调用 `completedTask.Wait()` 有些棘手，因为我们知道原始任务将成功完成。然而，在 `canceledTask` 或 `faultedTask` 上调用 `Wait()` 将导致异常。延续任务仅在先置任务被取消或抛出异常时才会运行；鉴于此程序中不会发生这种情况，这些任务永远不会被调度运行，等待它们完成将抛出异常。列表 19.1 中的延续任务恰好是互斥的，因此当先置任务运行完成，任务调度器会自动取消与 `canceledTask` 和 `faultedTask` 关联的任务。被取消的任务以状态设置为 `Canceled` 结束。因此，在这些任务上的任一调用 `Wait()`（或任何会导致当前线程等待任务完成的调用）都会抛出异常，指示它们已取消。一种不那么刻意的方法可能是调用 `Task.WaitAny(completedTask, canceledTask, faultedTask)`，它将抛出一个需要处理的 `AggregateException`。

# 使用 AggregateException 处理任务上的未处理异常

当同步调用一个方法时，我们可以将其封装在带有 `catch` 句的 `try` 块中，以识别我们希望在异常发生时执行的编译器。然而，这对于异步调用是不起作用。我们不能简单地在 `Start()` 调用周围封装一个块来捕获异常，因为控制会立即从调用返回，然后离开该块，可能在工作线程发生异常很久之前就离开了。

一种解决方案是将任务委托的主体封装在 `try/catch` 块中。在工作线程上抛出并随后捕获的异常因此不会产生问题，因为 `try` 块会在工作线程上正常工作。然而，对于未处理异常——那些工作线程未捕获的异常——情况并非如此。

通常（从 CLR 2.0 版本开始），任何线程上的未处理异常都被视为致命的，触发操作系统的报告对话框并导致应用程序异常终止。所有线程上的所有异常必须被捕获；如果没有捕获，应用程序将不允许继续运行。（有关处理未处理异常的某些高级技术，请参见即将推出的“高级主题：处理线程上的未处理异常”。）幸运的是，对于异步运行任务中的未处理异常并非如此。在这种情况下，任务调度器会在委托周围插入一个全捕异常处理器，这样如果任务抛出了其他未处理的异常，全捕处理器将捕获它并在任务中记录异常详情，从而避免触发 CLR 自动终止进程。

正如我们在列表 19.4 中看到的，处理故障任务的一种技术是显式创建一个延续任务，该任务作为该任务的故障处理器；当任务调度器检测到先置任务出现未处理异常时，会自动调度该延续任务。如果没有此类处理器，并且在故障任务上执行 `Wait()`（或尝试获取 `Result`），则将抛出 `AggregateException`（参见列表 19.5 和输出 19.3）。

# 列表 19.5：处理任务的未处理异常

```csharp
using System;
using System.Threading.Tasks;
public class Program
{
```

- 在 CLR 的 1.0 版本中，工作线程上的未处理异常会终止线程但不会终止应用程序。结果是，工作线程死亡但应用程序可以继续运行。这对于用户来说是一个困惑的情况，尽管在工作线程上抛出的未处理异常类型是 `InvalidException`，在主线程上捕获的异常类型是 `AggregateException`。

- 在 CLR 的 2.0 版本中，工作线程上的未处理异常会终止线程但不会终止应用程序。结果是，工作线程死亡但应用程序可以继续运行。这对于用户来说是一个困惑的情况，尽管在工作线程上抛出的未处理异常类型是 `InvalidException`，在主线程上捕获的异常类型是 `AggregateException`。

```csharp
using System;
using System.Diagnostics;
using System.Threading.Tasks;
public class Program
{
    public static void Main()
    {
        // 在 .NET 4.5 之前的 TPL 使用 Task.Factory.StartNew<string>()
        Task<string> task = Task.Run(() =>
        {
            throw new InvalidException();
        });

        try
        {
            task.Wait();
        }
        catch (AggregateException exception)
        {
            exception.Handle(eachException =>
            {
                Console.WriteLine("ERROR: {eachException.Message}");
                return true;
            });
        }
    }
}
```

# 输出 19.3

`ERROR: Operation is not valid due to the current state.`

聚合异常之所以被称为，是因为它可以包含来自多个任务的异常。此外，由于在编译时未知任务是否会抛出一个或多个异常，框架使用 `AggregateException` 作为收集并报告这些异常的方法。尽管在工作线程上抛出的未处理异常类型是 `InvalidException`，在主线程上捕获的异常类型是 `AggregateException`。

`AggregateException` 包含的异常列表可以通过 `InnerExceptions` 属性获取。你可以遍历此属性以检查每个异常并确定适当的操作。或者，如列表 19.5 所示，可以使用 `AggregateException.Handle()` 方法，指定针对每个异常执行的表达式。然而，需要考虑 `Handle()` 方法的一个特征是它是一个谓词。作为，谓词对于 `Handle()` 成功处理的异常应返回 `true`。如果任何处理调用对异常返回 `false`，`Handle()` 方法将抛出一个新的 `AggregateException`，其中包含相应异常的复合列表。

你可以通过简单查看任务的 `Exception` 属性来观察任务的状态，而不会导致异常在当前线程上重新抛出。列表 19.6 通过等待抛出异常的任务的故障延续任务演示了这种方法。

# 列表 19.6：使用 ContinueWith() 观察任务上的未处理异常

```csharp
using System;
using System.Diagnostics;
using System.Threading.Tasks;
public class Program
{
    bool parentTaskFaulted = false;
    Task task = new Task(() =>
    {
        throw new InvalidOperationException();
    });
    Task continuationTask = task.ContinueWith(
        (antecedentTask) =>
        {
            parentTaskFaulted = antecedentTask.IsFaulted;
        }, TaskContinuationOptions.OnlyFaulted());
    task.Start();
    continuationTask.Wait();
    Trace.Assert(parentTaskFaulted);
    Trace.Assert(!task.IsFaulted);
}
```

# 第 19 章：引入多线程

```csharp
{
    Console.WriteLine(
    $"ERROR: {exception.Message}");
    return true;
}
```

请注意，为了从原始任务中检索未处理的异常，我们使用了 `Exception` 属性（并使用空值宽容忽略运算符 `?` 进行解引用，因为我们知道该值不会为空）。输出结果与输出 19.3 相同。

如果在任务内部发生的异常完全没有被观察到——即：(1) 异常没有在任务内部被捕获；(2) 从未通过 `Wait()`、`Result` 或访问 `Exception` 属性等方式观察到任务的完成情况；且故障的 `ContinuedWith()` 延续任务也未被观察——那么该异常可能完全未被处理，从而导致整个进程范围内的未处理异常。在 .NET 4.0 中，失败的任务将由终结器线程（finalizer thread）重新抛出，并可能导致进程崩溃。相比之下，在 .NET 2.5 中，崩溃行为已被抑制（尽管如果需要，可以为 CLR 配置崩溃行为）。

在任何情况下，你都可以通过 `TaskScheduler.UnobservedTaskException` 事件注册未处理的任务异常。

## 进阶主题

### 处理线程上的未处理异常

正如我们早些讨论的那样，默认情况下，任何线程上的未处理异常都会导致应用程序关闭。未处理的异常是一个致命的、意料之外的错误，异常的发生可能是因为某个关键数据结构已损坏。由于你无法确定程序可能在做什么，最安全的做法是立即关闭整个程序。

理想情况下，没有任何程序应该在任何线程上抛出出未处理的异常；对于确实存在 Bug 的程序，最佳行动是在软件交付给客户之前找到并修复它。然而，当发生未处理异常时，与其尽快关闭应用程序，不如保存任何正在运行的数据和/或记录异常以便错误报告和未来的调试，这通常更好。这需要一种注册未处理异常通知的机制。

在 Microsoft .NET Framework 和 .NET Core 2.0（或更高版本）中，每个 `AppDomain` 都提供这种机制。若要观察发生在 `AppDomain` 中的未处理异常，你必须为 `UnhandledException` 事件添加一个处理程序。对于应用程序域内的所有未处理异常（无论是主线程还是工作线程），`UnhandledException` 事件都会触发。该机制的目的是通知；它并不允许应用程序从未处理的异常中恢复并继续执行。处理程序运行后，应用程序将显示操作系统的错误报告对话，然后退出。（对于控制台应用程序，异常详情也将显示在控制台上。）

在代码列表 19.7 中，我们展示了如何创建一个抛出异常的第二个线程，该异常将由应用程序域的未处理异常处理程序处理。出于演示之目的，为了确保线程问题不发生，我们使用 `Thread.Sleep` 插入了一些人工延迟。输出 19.4 显示了结果。

## 代码列表 19.7：注册未处理异常

```csharp
using System;
using System.Diagnostics;
using System.Threading;

public static class Program
{
    public static Stopwatch _Clock = new Stopwatch();
    public static void Main()
    {
        try
        {
            _Clock.Start();
            // 注册一个回调来接收
            // 任何未处理异常的通知 +=
            AppDomain.CurrentDomain.UnhandledException += (s, e) =>
            {
                Message("Event handler starting");
                Delay(4000);
            };

            Thread thread = new Thread(() =>
            {
                Message("Throwing exception.");
                throw new Exception();
            });
            thread.Start();

            Delay(2000);
        }
        finally
        {
            Message("Finally block running.");
        }

        static void Delay(int i)
        {
            Message($"Sleeping for {i} ms");
            Thread.Sleep(i);
            Message("Awake");
        }

        static void Message(string text)
        {
            Console.WriteLine("{0}:{1:0000}:{2}",
            Thread.CurrentThread.ManagedThreadId,
            _Clock.ElapsedMilliseconds, text);
        }
    }
}
```

# 输出 19.4

`3:00:47:Throwing exception.`

`3:00:52:Event handler starting.`

`3:00:55:Sleeping for 400 ms`

`1:00:58:Sleeping for 2000 ms`

`1:20:59:Finally block running.`

`3:20:60:Awake`

`Unhandled Exception: System.Exception: Exception of type 'System.Exception' was thrown.`

正如你在输出 19.4 中看到的，新线程被分配为 ID 3，主线程被分配为 ID 1。操作系统调度线程 3 运行一段时间；它抛出一个未处理异常，触发了处理程序，并进入睡眠。不久后，操作系统意识到可以调度线程 1，但它的代码立即让自己进入睡眠。线程 1 先醒来并运行 finally 块， 2 秒后线程 3 醒来，未处理异常导致进程崩溃。

## 取消任务
