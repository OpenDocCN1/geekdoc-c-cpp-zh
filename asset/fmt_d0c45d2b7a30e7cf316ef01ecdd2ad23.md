
```csharp
t => cts.Cancel(), TaskContinuationOptions.OnlyFaulted);
```
```
// 当所有子任务完成后，从非故障/取消的任务中获取返回的最大值。
```

// 然后将最大值传递给另一个任务显示最大结果

```csharp
tf.ContinueWithAll(
    childTasks,
    completedTasks => completedTasks.Where(t => t.IsCompleted && !t.IsCanceled).Max(t => t.Result),
    CancellationToken.None)
    .ContinueWith(t => Console.WriteLine("The maximum is: " + t.Result),
    TaskContinuationOptions.OnlyFaulted));
});
```

```
// 当子任务完成后，也显示任何未处理的异常
parent.ContinueWith(p => {
    // 我将所有这些文本放在 StringBuilder 中并调用一次 Console.WriteLine
    // 因为此任务可能与上面的任务并发执行，我不希望
    // 任务的输出交织在一起
    StringBuilder sb = new StringBuilder();
    sb.Append("The exception(s) occurred: " + Environment.NewLine);
    foreach (var e in p.Exception.Flatten().InnerExceptions)
        sb.Append(" " + e.GetType().ToString());
    Console.WriteLine(sb.ToString());
}, TaskContinuationOptions.OnlyFaulted);
```

```
// 启动父任务以便它可以启动子任务
parent.Start();
```

# 第 26 章 计算密集型异步操作 737

通过这段代码，我正在创建一个 `TaskFactory<Int32>` 对象，我将用它创建三个 `Task` 对象。我希望四点：每个 `Task` 对象共享相同的 `CancellationSource`，所有三个都被视为其父任务的子任务，所有由 `TaskFactory` 创建的任务都同步执行，并且由 `TaskFactory` 创建的所有 `Task` 对象都使用默认调度器。

## 任务调度器

基础设施非常灵活，`TaskScheduler` 对象将在本章进行更详细的讨论。

同步调度器通常用于 Windows Forms、Windows Foundation (WPF) 和 Silverlight 应用程序。此任务将所有任务调度到 GUI 线程上，以便更新按钮、菜单项等 UI 组件。同步上下文完全不使用线程池。你可以通过查询 `TaskScheduler` 的静态方法获取同步上下文的引用。

这是一个演示任务调度器的简单 Forms 应用程序：

```csharp
sealed class MyForm : Form {
public MyForm() {
    Text = "Synchronization Context Demo";
    Visible = true; Height = 400; Width = 100;
}
}
```

```csharp
// 获取同步上下文调度器
private readonly TaskScheduler m_syncContextScheduler =
TaskScheduler.FromSynchronizationContext();
```

```csharp
private CancellationTokenSource m_cts;
```

```csharp
protected override void OnClick(EventArgs e) {
    if (m_cts != null) { // 操作正在进行中，取消它
    m_cts.Cancel();
    m_cts = null;
} else {
    Text = "Operation running";
    m_cts = new CancellationTokenSource();
}
}
```

```csharp
// 此任务使用默认任务调度器并在线程池上执行
var t = new Task<int32>(() => Sum(m_cts.Token, 20000), m_cts.Token);
t.Start();
```

```csharp
// 这些任务使用同步上下文调度器并在 GUI 线程上执行
t.ContinueWith(task => Text = "Result: " + task.Result,
CancellationToken.None, TaskContinuationOptions.OnlyOnRanToCompletion,
m_syncContextTaskScheduler);
```

```csharp
t.ContinueWith(task => Text = "Operation canceled",
CancellationToken.None, TaskContinuationOptions.OnlyOnRanCanceled,
m_syncContextTaskScheduler);
```

```csharp
t.ContinueWith(task => Text = "Operation faulted",
CancellationToken.None, TaskContinuationOptions.OnlyOnFailed,
m_syncContextTaskScheduler);
```

```csharp
base.OnClick(e);
}
```

当你点击此表单的客户区域时，一个计算密集型任务将在线程池线程上开始执行。这是好事，因为在此期间 GUI 不会被阻塞，并且可以响应其他 UI 操作。然而，由线程池执行的代码不应尝试更新 UI 组件，否则将抛出 `InvalidOperationException`。

# 第 26 章 计算密集型异步操作 739

当计算密集型任务完成后，三个 `continue-with` 任务之一将执行。这些任务都是针对对应 GUI 线程的同步上下文任务调度器发布的，该任务调度器将任务队列到 GUI 线程，允许这些任务执行的代码能够成功更新 UI 组件。所有这些任务都通过继承的 `Text` 属性更新表单标题。

由于计算密集型工作（`Sum`）在线程池上运行，用户可以与 UI 交互以取消操作。在我简单的代码示例中，我将允许你在操作运行时点击表单的客户区域来取消操作。

当然，如果你有特殊的任务调度需求，可以定义派生自 `TaskScheduler` 的自定义类。微软提供了一系列任务的示例代码，并在 `Parallel Extensions` 附加包中包含了许多任务调度器的源代码，你可以从这里处下载：`http://code.msdn.microsoft.com/ParExtSamples`。以下是该包中包含的一些任务调度器：

- `IOScheduler`：此任务调度器将任务队列到线程池的 I/O 线程而不是工作线程。
- `LimitedConcurrencyLevelTaskScheduler`：此调度器允许最多有 n（一个构造函数参数）个任务同时执行。
- `OrderedTaskScheduler`：此任务调度器一次允许执行一个任务。该类派生自 `LimitedConcurrencyLevelTaskScheduler` 并将 n 的值推入为 1。
- `PrioritizingTaskScheduler`：此任务调度器将任务队列到 CLR 线程池。发生后，你可以调用 `Prioritize` 来指示某个 `Task` 应该在所有普通任务之前处理（如果尚未被处理）。你可以调用 `Deprioritize` 让 `Task` 在所有普通任务之后处理。
- `ThreadPerTaskScheduler`：此任务调度器为每个任务创建并启动一个独立的线程；它完全不使用线程池。

## Parallel 的静态方法、ForEach 和 Invoke 方法

有一些常见的编程场景可能会从任务带来的性能提升中获益。为了简化编程，静态的 `System.Threading.Tasks.Parallel` 在内建使用 `Task` 对象的同时，封装了这些常见场景。例如，处理集合中所有项的实例如下：

```csharp
// 一个线程按顺序执行所有工作
for (Int32 i = 0; i < 1000; i++) DoWork(i);
```

你可以通过使用 `Parallel` 类的 `For` 方法获取多个线程池来协助执行此工作：

```csharp
// 线程池的线程并行处理工作
Parallel.For(0, 1000, i => DoWork(i));
```

同样，如果你有一个集合，与其这样做：

```csharp
// 一个线程按顺序执行所有这些工作
foreach(var item in collection) DoWork(item);
```

你可以这样做：

```csharp
// 线程池的线程并行处理工作
Parallel.ForEach(collection, item => DoWork(item));
```

如果你在代码中使用 **For** 或 **ForEach**，则建议使用 **For**，因为它的执行速度更快。

最后，如果你有几个方法需要执行，你可以像这样按顺序执行所有它们：

```csharp
// 一个线程按顺序执行所有方法
Method1();
Method2();
Method3();
```

或者你也可以这样并行地执行它们，如下所示：

```csharp
// 线程池的线程并行执行方法
Parallel.Invoke(
  () => Method1()
)
```

`Parallel` 的所有方法都让调用线程参与工作的处理，这在资源利用方面是有益的，我们不希望调用线程在等待线程池完成所有工作时挂挂起。然而，如果调用线程在线程池完成部分工作之前结束了自己的工作，那么调用线程将挂挂起直到所有工作完成。

## 第 26 章 计算密集型异步操作 743

```csharp
public Boolean IsExceptional { get; }
public Boolean ShouldExitIteration { get; }
```

每个参与工作的任务都拥有自己的自己的 `ParallelState` 对象，并可以使用该对象与参与工作的其他任务进行交互。`Stop` 方法调用循环停止处理任何工作，后续对 `IsStopped` 属性的查询将返回 `true`。`Break` 方法告诉循环停止处理当前项目之后的任何项目。例如，假设 `ForEach` 要处理 100 个项目，在处理第五个项目时调用了 `Break`，循环将确保在 `ForEach` 之前处理了前五个项目。但注意，`LowestBreakIteration` 在调用 `Break` 方法时返回最低的项目编号。如果从未调用过 `Break`，则 `LowestBreakIteration` 返回 `null`。

如果任何项目的处理导致了未处理的异常，`Exception` 属性将返回 `true`。如果某个项目的处理需要很长时间，你的代码可以查询 `ExitIteration` 属性来查看是否提前退出。如果调用了 `Stop`、`Break`、`CancellationSource`（由 `ParallelOptions.CancellationToken` 属性引用）被取消，或者项目的处理导致了意外异常，该属性将返回 `true`。

`Parallel.For` 和 `ForEach` 方法都返回 `ParallelLoopResult` 实例，结构如下：

```csharp
struct ParallelLoopResult {
  // 如果操作提前结束，返回 false
  public bool IsCompleted { get; }
  public Int64 LowestBreakIteration { get; }
}
```

你可以检查这些属性来确定循环的结果。如果 `IsCompleted` 返回 `true`，则循环运行完成，所有项目都已处理。如果 `IsCompleted` 为 `false` 且 `LowestBreakIteration` 为 `null`，则某个参与线程调用了 `Stop` 方法。如果 `IsCompleted` 为 `false` 且 `LowestBreakIteration` 不为 `null`，则某个参与线程调用了 `Break` 方法，`LowestBreakIteration` 返回的 `Int64` 值表示保证已处理的项目索引。

## 并行语言集成查询

Microsoft 的语言集成查询 (LINQ) 功能为对数据集合执行查询提供了方便的语法。使用 LINQ，你可以轻松地过滤项目、排序项目、返回投影的项目集等。当你使用 `LINQ to Objects` 时，只有一个线程按顺序处理你数据集合中的所有项目；我们称之为顺序的。

## 744 第五部分 多线程

你可以通过使用并行 LINQ (Parallel LINQ) 潜在地提高这种处理的性能，它可以将你的顺序查询转换为并行查询，内部使用任务（由默认调度器排队）将集合项目的处理分布在多个 CPU 上，从而实现多个项目的并发处理。如果你有项目需要处理，或者每个项目的处理是耗时的计算密集型操作，你从 LINQ 中受益最多。

静态 `System.Linq.ParallelEnumerable` 类（定义在 `System.Core.dll` 中）实现了所有的并行 LINQ 功能，你必须在源代码中通过指令使用 `System.Linq` 命名空间。特别是，此类暴露了标准 LINQ 操作符的版本，如 `Where`、`Select`、`SelectMany`、`GroupBy`、`Join`、`Order-By`、`Skip` 和 `Take`。这些都是扩展 `System.Linq.ParallelQuery<T>` 类型的扩展方法。要让你的 LINQ 对象调用这些方法的并行版本，你必须使用 `AsParallel` 扩展方法将你的顺序查询（基于 `Enumerable` 或 `Enumerable<T>`）转换为并行查询（基于 `ParallelQuery` 或 `ParallelQuery<T>`），它看起来如下：

```csharp
public static ParallelQuery<TSource> TSourceAsParallel<TSource>(this IEnumerable<TSource> source)
public static ParallelQuery AsParallel(this IEnumerableource source)
```

这里是将顺序查询转换为并行查询的示例，用于返回程序集内所有过时的方法：

```csharp
private static void ObsoleteMethods(Assembly assembly) {
    var query =
        from type in assembly.GetExportedTypes().AsParallel()
        from method in type.GetMethods(BindingFlags.Public | 
            BindingFlags.Instance | BindingFlags.Static)
        let obsoleteAttr = typeof(ObsoleteAttribute)
        where obsoleteAttr.IsDefined(method, obsoleteAttr)
        orderby type.FullName
        select method.FullName
        let obsoleteAttrObj = (ObsoleteAttribute)
            Attribute.GetCustomAttribute(method, obsoleteAttr)
        select String.Format("Type={0}\nMethod={1}\nMessage={2}\n",
            type.FullName, method.ToString(), obsoleteAttrObj.Message);
    // 显示结果
    foreach (var result in query) Console.WriteLine(result);
}
```

> `ParallelQuery<T>` 类派自 `ParallelQuery` 类。

## 第 26 章 计算密集型异步操作 745

虽然不常见，但在查询内部你可以通过调用 `ParallelEnumerable.AsSequential` 方法从并行操作切换为顺序操作：

```csharp
public static IEnumerable<TSource> AsSequential<TSource>(this ParallelQuery<TSource> source)
```
