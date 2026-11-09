
```csharp
where Attribute.IsDefined(method, obsoleteAttrType)

orderby type.FullName

let obsoleteAttrObj = (ObsoleteAttribute)
    Attribute.GetCustomAttribute(method, obsoleteAttrType)

select String.Format("Type={0}\nMethod={1}\nMessage={2}\n",
    type.FullName, method.ToString(), obsoleteAttrObj.Message);

// Display the results
foreach (var result in query) Console.WriteLine(result);
}
```

虽然不常见，但在查询中，你可以通过调用 ParallelEnumerable 的 AsSequential 方法，从执行并行操作切换回执行顺序操作。

```csharp
public static IEnumerable<TSource> AsSequential<TSource>(this ParallelQuery<TSource> source)
```

此方法基本上将 ParallelQuery<T> 转回 IEnumerable<T>，这样在调用 AsSequential 之后执行的操作就只由一个线程执行。

通常，LINQ 查询生成的结果数据是通过让某个线程执行 foreach 语句来计算的（如前面所示）。这意味着只有一个线程遍历查询的所有结果。如果你希望并行处理查询结果，那么应使用 ParallelEnumerable 的 ForAll 方法来处理结果查询。

```csharp
static void ForAll<TSource>(this ParallelQuery<TSource> source, Action<TSource> action)
```

此方法允许多个线程同时处理结果。我可以修改前面的代码，以如下方式使用此方法。

```csharp
// Display the results
query.ForAll(Console.WriteLine);
```

然而，让多个线程同时调用 Console.WriteLine 实际上会损害性能，因为 Console 类在内部同步线程，确保同一时间只有一个线程能访问控制台窗口。这可以防止来自多个线程的文本交错，避免输出难以理解。当你打算对每个结果执行计算时，再使用 ForAll 方法。

因为并行 LINQ 使用多个线程处理项，所以这些项会被并发处理，并且结果以无序方式返回。如果你需要并行 LINQ 在处理项时保留项的顺序，那么可以调用 ParallelEnumerable 的 AsOrdered 方法。调用此方法时，线程将按组处理项，然后将各组合并回去，从而保留顺序；这会损害性能。以下操作符产生无序操作：Distinct、Except、Intersect、Union、Join、GroupBy、GroupJoin 和 ToLookup。如果你想在其中一个操作符之后再次强制排序，只需调用 AsOrdered 方法。

以下操作符产生有序操作：OrderBy、OrderByDescending、ThenBy 和 ThenByDescending。如果你希望在其中一个操作符之后再次回到无序处理以提高性能，只需调用 AsUnordered 方法。

并行 LINQ 还提供了一些额外的 ParallelEnumerable 方法，你可以调用它们来控制查询的处理方式。

```csharp
public static ParallelQuery<TSource> WithCancellation<TSource>(
    this ParallelQuery<TSource> source, CancellationToken cancellationToken)

public static ParallelQuery<TSource> WithDegreeOfParallelism<TSource>(
    this ParallelQuery<TSource> source, Int32 degreeOfParallelism)

public static ParallelQuery<TSource> WithExecutionMode<TSource>(
    this ParallelQuery<TSource> source, ParallelExecutionMode executionMode)

public static ParallelQuery<TSource> WithMergeOptions<TSource>(
    this ParallelQuery<TSource> source, ParallelMergeOptions mergeOptions)
```

显然，WithCancellation 方法允许你传入一个 CancellationToken，以便可以提前停止查询处理。WithDegreeOfParallelism 方法指定允许处理查询的最大线程数；如果并非所有线程都是必需的，它不会强制创建这些线程。通常你不会调用此方法，默认情况下，查询将使用每个核心一个线程来执行。但是，如果你希望保留一些核心用于其他工作，可以调用 WithDegreeOfParallelism，并传入一个小于可用核心数的数字。如果查询执行同步 I/O 操作，因为线程在这些操作期间会阻塞，你也可以传入一个大于核心数的数字。这会浪费更多线程，但可以在更短时间内产生最终结果。你可能考虑在客户端应用程序中这样做，但我强烈建议不要在服务器应用程序中执行同步 I/O 操作。

并行 LINQ 会分析查询，然后决定如何最佳地处理它。有时顺序处理查询会带来更好的性能。在使用以下任一操作时通常如此：Concat、ElementAt(OrDefault)、First(OrDefault)、Last(OrDefault)、Skip(While)、Take(While) 或 Zip。在使用 Select(Many) 或 Where 的重载（这些重载会将位置索引传入选择器或谓词委托）时也是如此。但是，你可以通过调用 WithExecutionMode 并传入 ParallelExecutionMode 标志之一，强制查询以并行方式处理。

```csharp
public enum ParallelExecutionMode {
    Default = 0,        // Let Parallel LINQ decide to best process the query
    ForceParallelism = 1 // Force the query to be processed in parallel
}
```

如前所述，并行 LINQ 使用多个线程处理项，然后必须将结果合并回去。你可以通过调用 WithMergeOptions 并传入 ParallelMergeOptions 标志之一，来控制项的缓冲和合并方式。

```csharp
public enum ParallelMergeOptions {
    Default          = 0,     // Same as AutoBuffered today (could change in the future)
    NotBuffered      = 1,     // Results are processed as ready
    AutoBuffered     = 2,     // Each thread buffers some results before processed
    FullyBuffered    = 3      // Each thread buffers all results before processed
}
```

这些选项基本上让你在速度与内存消耗之间进行一些控制。NotBuffered 节省内存，但处理项较慢。FullyBuffered 消耗更多内存，但运行速度最快。AutoBuffered 是介于 NotBuffered 和 FullyBuffered 之间的折中方案。实际上，对于任何给定查询，要知道该选择哪一个，最好的方法就是全部尝试并比较它们的性能结果，或者直接接受默认值；对于许多查询来说，默认值往往效果很好。有关并行 LINQ 如何跨 CPU 核心进行分区的更多信息，请参阅以下博客文章：

- http://blogs.msdn.com/pfxteam/archive/2009/05/28/9648672.aspx
- http://blogs.msdn.com/pfxteam/archive/2009/06/13/9741072.aspx

## 执行定期的计算密集型操作

System.Threading 命名空间定义了一个 Timer 类，你可以使用它让线程池线程定期调用某个方法。当你构造 Timer 类的实例时，就是在告诉线程池：你希望自己的某个方法在你指定的未来时间被回调。Timer 类提供了几个构造函数，彼此都非常相似。

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Timer(TimerCallback callback, Object state, Int32 dueTime, Int32 period);
    public Timer(TimerCallback callback, Object state, UInt32 dueTime, UInt32 period);
    public Timer(TimerCallback callback, Object state, Int64 dueTime, Int64 period);
    public Timer(TimerCallback callback, Object state, TimeSpan dueTime, TimeSpan period);
}
```

所有四个构造函数构造 Timer 对象的方式完全相同。callback 参数标识你希望由线程池线程回调的方法。当然，你编写的回调方法必须匹配 System.Threading.TimerCallback 委托类型，该类型定义如下。

```csharp
delegate void TimerCallback(Object state);
```

构造函数的 state 参数允许你在每次调用回调方法时向它传递状态数据；如果没有状态数据要传递，可以传入 null。使用 dueTime 参数告诉 CLR 在第一次调用回调方法之前要等待多少毫秒。可以使用有符号或无符号的 32 位值、有符号的 64 位值或 TimeSpan 值来指定毫秒数。如果你希望立即调用回调方法，请为 dueTime 参数指定 0。最后一个参数 period 允许你指定在每次连续调用回调方法之前要等待多长时间（以毫秒为单位）。如果为此参数传入 Timeout.Infinite（-1），线程池线程将只调用回调方法一次。

在内部，线程池只有一个线程用于所有 Timer 对象。这个线程知道下一个 Timer 对象何时到期。当下一个 Timer 对象到期时，该线程会唤醒，并在内部调用 ThreadPool 的 QueueUserWorkItem，将一个条目放入线程池队列，从而导致你的回调方法被调用。如果你的回调方法执行时间较长，计时器可能会再次触发。这可能导致多个线程池线程同时执行你的回调方法。要解决此问题，我建议如下：构造 Timer 时，为 period 参数指定 Timeout.Infinite。这样，计时器将只触发一次。然后，在回调方法中调用 Change 方法，指定新的到期时间，并再次为 period 参数指定 Timeout.Infinite。Change 方法重载如下所示。

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Change(Int32 dueTime, Int32 period);
    public Boolean Change(UInt32 dueTime, UInt32 period);
    public Boolean Change(Int64 dueTime, Int64 period);
    public Boolean Change(TimeSpan dueTime, TimeSpan period);
}
```

Timer 类还提供了一个 Dispose 方法，允许你完全取消计时器，并可选地在计时器的所有挂起回调完成后，向 notifyObject 参数所标识的内核对象发出信号。Dispose 方法重载如下所示。

```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Boolean Dispose();
    public Boolean Dispose(WaitHandle notifyObject);
}
```

> **重要** 当 Timer 对象被垃圾回收时，其终结代码会告诉线程池取消计时器，使其不再触发。因此，在使用 Timer 对象时，请确保有变量使该 Timer 对象保持存活，否则你的回调方法将停止被调用。这一点在第 21 章“托管堆与垃圾回收”的“垃圾回收与调试”一节中进行了讨论和演示。
