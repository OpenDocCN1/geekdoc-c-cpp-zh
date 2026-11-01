
任务需要很长时间，因此调度器更可能使用新线程。如果任务应附加到父任务，并且如果父任务被取消，子任务也应该被取消，则设置 AttachToParent 选项。PreferFairness 值表示调度器应优先处理已经等待的任务。这是非默认情况，如果任务是在另一个任务内创建的。如果任务使用子任务创建额外工作，子任务优先于其他任务。它们不会在线程池队列中等待最后才执行。如果这些任务应与其他所有任务以公平的方式处理，请将选项设置为 PreferFairness。

```
Task t4 = new Task(TaskMethod, TaskCreationOptions.PreferFairness);
t4.Start();
```

## 延续任务

通过任务，您可以指定在一个任务完成后，另一个特定任务应开始运行，例如，一个新任务使用前一个任务的结果，或者如果前一个任务失败则执行一些清理工作。

任务处理程序要么没有参数，要么有一个对象参数，而延续处理程序有一个类型为 Task 的参数。在这里，您可以访问有关原始任务的信息。

```
static void DoOnFirst()
{
    Console.WriteLine("doing some task {0}", Task.CurrentId);
    Thread.Sleep(3000);
}

static void DoOnSecond(Task t)
{
    Console.WriteLine("task {0} finished", t.Id);
    Console.WriteLine("this task id {0}", Task.CurrentId);
    Console.WriteLine("do some cleanup");
    Thread.Sleep(3000);
}
```

代码片段 TaskSamples/Program.cs

延续任务是通过在任务上调用 ContinueWith 方法来定义的。您也可以为此使用 TaskFactory。t1.ContinueWith(DoOnSecond) 意味着一旦任务 t1 完成，就应该启动一个调用 DoOnSecond() 方法的新任务。当一个任务完成时，您可以启动多个任务，并且一个延续任务也可以有另一个延续任务，如本示例所示。

```
Task t1 = new Task(DoOnFirst);
Task t2 = t1.ContinueWith(DoOnSecond);
Task t3 = t1.ContinueWith(DoOnSecond);
Task t4 = t2.ContinueWith(DoOnSecond);
```

无论前一个任务如何完成，只要前一个任务完成，延续任务总是会启动。使用 TaskContinuationOptions 的值，您可以定义延续任务仅在原始任务成功（或失败）时才启动。一些可能的值包括 OnlyOnFaulted、NotOnFaulted、OnlyOnCanceled、NotOnCanceled 和 OnlyOnRanToCompletion。

```
Task t5 = t1.ContinueWith(DoOnError,
    TaskContinuationOptions.OnlyOnFaulted);
```

## 任务层次结构

通过任务延续，一个任务在另一个之后启动。任务也可以形成层次结构。当任务本身启动一个新任务时，就开始了父子层次结构。

```
8, task: 3, thread: 4
9, task: 3, thread: 4
True
```

您也可以提前中断 Parallel.For()。For() 方法的一个重载接受第三个参数 Action<int, ParallelLoopState>。通过定义具有这些参数的方法，您可以通过调用 ParallelLoopState 的 Break() 或 Stop() 方法来影响循环的结果。

请记住，迭代的顺序是未定义的。

```csharp
ParallelLoopResult result =
    Parallel.For(10, 40, (int i, ParallelLoopState pls) =>
    {
        Console.WriteLine("{0}: task {1}", i, Task.CurrentId);
        Thread.Sleep(10);
        if (i > 15)
            pls.Break();
    });
Console.WriteLine(result.IsCompleted);
Console.WriteLine("lowest break iteration: {0}",
    result.LowestBreakIteration);
```

应用程序的这次中断运行演示了迭代在大于 15 的值处中断，但其他任务可以同时运行，并且具有其他值的任务也可以运行。借助 LowestBreakIteration 属性，您可以决定忽略其他任务的结果。

```
10 task 1
25 task 2
11 task 1
13 task 3
12 task 1
14 task 3
16 task 1
15 task 3
False
lowest break iteration: 16
```

Parallel.For() 可能使用多个线程来执行循环。如果需要为每个线程执行初始化，可以使用 Parallel.For<TLocal>() 方法。For 方法的泛型版本除了 from 和 to 值之外，还接受三个委托参数。第一个参数的类型是 Func<TLocal>。因为这里的示例使用字符串作为 TLocal，所以该方法需要定义为 Func<string>，即返回字符串的方法。此方法仅为用于执行迭代的每个线程调用一次。

第二个委托参数定义了主体的委托。在示例中，参数的类型是 Func<int, ParallelLoopState, string, string>。第一个参数是循环迭代；第二个参数 ParallelLoopState 允许停止循环，如您之前所见。通过第三个参数，主体方法接收 init 方法返回的值。主体方法还需要返回一个与泛型 For 参数定义的类型相同的值。

For() 方法的最后一个参数指定一个委托 Action<TLocal>；在示例中，接收到一个字符串。此方法同样仅为每个线程调用一次；这是一个线程退出方法。

```csharp
Parallel.For<string>(0, 20,
    () =>
    {
        // invoked once for each thread
        Console.WriteLine("init thread {0} managed {1}", Task.CurrentId, Thread.CurrentThread.ManagedThreadId);
        return Thread.CurrentThread.ManagedThreadId;
    },
    (i, pls, str1) =>
```

通过创建 CancellationTokenSource 来进行取消。CancellationTokenSource 实现了 ICancellableOperation 接口，因此可以与 CancellationToken 注册，并允许通过 Cancel() 方法进行取消。要取消并行循环，会创建一个新任务，在 500 毫秒后调用 CancellationTokenSource 的 Cancel() 方法。

在 For() 循环的实现中，Parallel 类会验证 CancellationToken 的结果并取消操作。取消时，For() 方法抛出 OperationCanceledException 类型的异常，在示例中被捕获。使用 CancellationToken，可以注册在取消完成时获得通知。这通过调用 Register() 方法并传递一个在取消时调用的委托来实现。

```
var cts = new CancellationTokenSource();
cts.Token.Register(() =>
    Console.WriteLine("*** token canceled"));
// start a task that sends a cancel after 500 ms
new Task(() =>
{
    Thread.Sleep(500);
    cts.Cancel(false);
}).Start();

try
{
    ParallelLoopResult result =
        Parallel.For(0, 100,
            new ParallelOptions()
            {
                CancellationToken = cts.Token,
            },
            x =>
            {
                Console.WriteLine("loop {0} started", x);
                int sum = 0;
                for (int i = 0; i < 100; i++)
                {
                    Thread.Sleep(2);
                    sum += i;
                }
                Console.WriteLine("loop {0} finished", x);
            });
}
catch (OperationCanceledException ex)
{
    Console.WriteLine(ex.Message);
}
```

代码片段 CancellationSamples/Program.cs

运行该应用程序时，您将获得类似以下的输出。迭代 0、1、25、26、50、51、75 和 76 都已启动。这是在具有四核 CPU 的系统上进行的。由于取消，所有其他迭代在开始之前就被取消了。已启动的迭代允许完成，因为取消始终以协作方式进行，以避免在迭代中途取消时造成资源泄漏的风险。

```
loop 0 started
loop 50 started
loop 25 started
loop 75 started
loop 50 finished
```

