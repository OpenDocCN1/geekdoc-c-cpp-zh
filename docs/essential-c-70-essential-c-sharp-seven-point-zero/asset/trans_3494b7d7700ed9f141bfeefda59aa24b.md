

### 表 19.1：可用的 TaskContinuationOptions 枚举列表

| 枚举 | 描述 |
| --- | --- |
| `PreferFairness` | 如果两个任务都是异步启动的，且一个在另一个之前启动，那么先启动的任务并不保证会先执行。此标志请求任务调度器尝试提高先启动的任务最先执行的可能性——当所描述的两个任务是由不同的线程池线程创建时，这一点尤其相关。 |
| `LongRunning` | 这告知任务调度器，该任务很可能是 I/O 受限的高延迟任务。调度器随后可以允许处理其他排队的工作，而不是因为长时间运行的任务导致饥饿。此选项应谨慎使用。 |
| `AttachedToParent` | 这指定任务应尝试附加到任务层次结构中的父任务。 |
| `DenyChildAttach` (.NET 4.5) | 如果尝试创建子任务，这将抛出异常。如果延续体中的代码试图使用 `AttachedToParent`，它将表现得好像没有父任务一样。 |
| `NotOnRanToCompletion`* | 这指定如果其先行任务已运行至完成，则不应调度该延续任务。此选项对多任务延续无效。 |
| `NotOnFaulted`* | 这指定如果其先行任务抛出了未处理的异常，则不应调度该延续任务。此选项对多任务延续无效。 |
| `OnlyOnCanceled`* | 这指定仅当其先行任务被取消时才应调度该延续任务。此选项对多任务延续无效。 |
| `NotOnCanceled`* | 这指定如果其先行任务被取消，则不应调度该延续任务。此选项对多任务延续无效。 |
| `OnlyOnFaulted`* | 这指定仅当其先行任务抛出了未处理的异常时才应调度该延续任务。此选项对多任务延续无效。 |
| `OnlyOnRanToCompletion`* | 这指定仅当其先行任务已运行至完成时才应调度该延续任务。此选项对多任务延续无效。 |
| `ExecuteSynchronously` | 这指定延续任务应同步执行。指定此选项时，调度的延续体将尝试在使先行任务进入最终状态的那个线程上执行工作。如果在创建延续体时先行任务已经完成，则延续体将在创建该延续体的线程上运行。 |
| `HideScheduler` (.NET 4.5) | 这防止环境调度器被创建的任务视为当前调度器。这意味着在创建的任务中执行的操作，如 `Run/StartNew` 和 `ContinueWith`，将看到 `TaskScheduler.Default` (null) 作为当前调度器。当延续体应在特定调度器上运行，但延续体调用的额外代码不应在同一调度器上安排工作时，这很有用。 |
| `LazyCancellation` (.NET 4.5) | 这导致延续体延迟监视提供的取消令牌，直到先行任务完成后才检测取消请求。考虑任务 t1、t2 和 t3，其中后者是前者的延续体。如果在 t1 完成之前 t2 被取消，t3 有可能在 t1 完成之前开始。设置 LazyCancellation 可以避免这种情况。 |
| `RunContinuationsAsynchronously` (.NET 4.6) | 当任务以 RunContinuationsAsynchronously 选项创建时，这告知任务应强制其延续体异步运行。即使该任务本身是一个延续体，此选项也不影响该任务本身的运行方式，仅影响其延续体的运行方式。延续任务可以同时使用 TaskContinuationOptions.ExecuteSynchronously 和 TaskContinuationOptions.RunContinuationsAsynchronously 创建。前者使得延续体在其先行任务完成时同步执行，并使该延续体的延续体在该延续体完成时异步运行。 |

在表 19.1 中，用星号 (*) 标记的项目指示在何种条件下会执行延续任务；因此，它们对于创建像先行任务行为的事件处理程序一样的延续体特别有用。列表 19.6 演示了如何为先行任务提供多个有条件执行的延续体，这取决于先行任务是如何完成的。

### 列表 19.6：使用 ContinueWith() 注册任务行为通知

```csharp
using System;
using System.Threading.Tasks;
using System.Diagnostics;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;

public class Program
{
    public static void Main()
    {
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task<string> task =
            Task.Run<string>(
                () => PiCalculator.Calculate(10));

        Task faultedTask = task.ContinueWith(
            (antecedentTask) =>
            {
                Trace.Assert(antecedentTask.IsFaulted);
                Console.WriteLine(
                    "Task State: Faulted");
            },
            TaskContinuationOptions.OnlyOnFaulted);

        Task canceledTask = task.ContinueWith(
            (antecedentTask) =>
            {
                Trace.Assert(antecedentTask.IsCanceled);
                Console.WriteLine(
                    "Task State: Canceled");
            },
            TaskContinuationOptions.OnlyOnCanceled);

        Task completedTask = task.ContinueWith(
            (antecedentTask) =>
            {
                Trace.Assert(antecedentTask.IsCompleted);
                Console.WriteLine(
                    "Task State: Completed");
            }, TaskContinuationOptions.
            OnlyOnRanToCompletion);

        completedTask.Wait();
    }
}
```

在此列表中，我们为先行任务的有效*监听器*注册了*事件*，以便当任务正常或异常完成时，特定的“监听”任务将开始执行。这是一个强大的功能，特别是如果原始任务是一个即发即忘任务——即，我们启动它，将其连接到延续任务，然后不再引用它。

在列表 19.6 中，注意最后的 Wait() 调用是在 completedTask 上，而不是在 task——即使用 Task.Run() 创建的原始先行任务——上。尽管每个委托的 antecedentTask 都是对先行任务 (task) 的引用，但从委托监听器外部，我们可以有效地丢弃对原始任务的引用。然后，我们可以完全依赖于那些异步开始执行的延续任务，而不需要任何后续代码来检查原始任务的状态。
在这种情况下，我们调用 `completedTask.Wait()`，以便主线程在完成的输出出现之前不退出程序（参见输出 19.3）。

### 输出 19.3

```
Task State: Completed.
```

在这种情况下，调用 `completedTask.Wait()` 有些牵强，因为我们要知道原始任务将成功完成。然而，在 `canceledTask` 或 `faultedTask` 上调用 `Wait()` 将导致异常。这些延续任务仅在先行任务被取消或抛出异常时才会运行；鉴于这些情况不会在本程序中发生，这些任务将永远不会被调度运行，等待它们完成将抛出异常。列表 19.3 中的延续选项恰好是互斥的，因此当先行任务运行至完成并与 `completedTask` 关联的任务执行时，任务调度器会自动取消与 `canceledTask` 和 `faultedTask` 关联的任务。被取消的任务以其状态设置为 `Canceled` 结束。因此，在这两个任务中的任何一个上调用 `Wait()`（或任何会导致当前线程等待任务完成的调用）将抛出异常，指示它们已被取消。

一种不那么牵强的方法可能是调用 `Task.WaitAny(completedTask, canceledTask, faultedTask)`，这将抛出一个需要处理的 `AggregateException`。

### 使用 AggregateException 对任务进行未处理异常处理

在同步调用方法时，我们可以将其包裹在带有 catch 子句的 try 块中，以向编译器指明当发生异常时我们希望执行哪些代码。然而，这对异步调用不起作用。我们不能简单地用一个 try 块包裹 `Start()` 调用来捕获异常，因为控制权立即从调用返回，随后离开 try 块，可能远远早于异常发生的时候

