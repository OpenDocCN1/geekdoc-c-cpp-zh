
接受一个 ParallelOptions 对象，其形式如下：

```csharp
public class ParallelOptions {
    public ParallelOptions();

    // Allows cancellation of the operation
    public CancellationToken CancellationToken { get; set; }   // Default=CancellationToken.None

    // Allow you to specify the maximum number of work items
    // that can be operated on concurrently
    public Int32 MaxDegreeOfParallelism { get; set; }    // Default=-1 (# of available CPUs)

    // Allows you to specify which TaskScheduler to use
    public TaskScheduler TaskScheduler { get; set; }    // Default=TaskScheduler.Default
}
```

此外，For 和 ForEach 方法还有重载，允许你传入三个委托：

- 任务局部初始化委托（localInit）会为参与工作的每个任务调用一次。此委托在要求该任务处理某个工作项之前调用。
- 主体委托（body）会为参与工作的各个线程正在处理的每个项调用一次。
- 任务局部最终委托（localFinally）会为参与工作的每个任务调用一次。此委托在任务处理完将分派给它的所有工作项之后调用。即使主体委托代码发生未处理异常，也会调用它。

以下示例代码通过累加某个目录中所有文件的字节数，演示了这三个委托的用法：

```csharp
private static Int64 DirectoryBytes(String path, String searchPattern,
                                    SearchOption searchOption) {
    var files = Directory.EnumerateFiles(path, searchPattern, searchOption);
    Int64 masterTotal = 0;

    ParallelLoopResult result = Parallel.ForEach<String, Int64>(
        files,

        () => { // localInit: Invoked once per task at start
            // Initialize that this task has seen 0 bytes
            return 0;   // Set taskLocalTotal initial value to 0
        },

        (file, loopState, index, taskLocalTotal) => { // body: Invoked once per work item
            // Get this file's size and add it to this task's running total
            Int64 fileLength = 0;
            FileStream fs = null;
            try {
                fs = File.OpenRead(file);
                fileLength = fs.Length;
            }
```

ParallelOptions 的 CancellationToken 属性）被取消，或者处理某个项导致未处理异常。

Parallel 的 For 和 ForEach 方法都返回一个 ParallelLoopResult 实例，其形式如下：

```csharp
public struct ParallelLoopResult {
    // Returns false if the operation was ended prematurely
    public Boolean IsCompleted { get; }
    public Int64? LowestBreakIteration { get; }
}
```

可以检查这些属性来确定循环的结果。如果 IsCompleted 返回 true，则循环运行到完成，所有项都已处理。如果 IsCompleted 为 false 且 LowestBreakIteration 为 null，则参与工作的某个线程调用了 Stop 方法。如果 IsCompleted 为 false 且 LowestBreakIteration 不为 null，则参与工作的某个线程调用了 Break 方法，并且 LowestBreakIteration 返回的 Int64 值表示保证已处理的最低项的索引。如果抛出异常，则应捕获 AggregateException 以便妥善恢复。

## 并行语言集成查询

Microsoft 的语言集成查询（LINQ）功能提供了一种便捷语法，用于对数据集合执行查询。使用 LINQ，你可以轻松筛选项、排序项、返回投影的项集等。使用 LINQ to Objects 时，只有一个线程按顺序处理数据集合中的所有项；我们称之为顺序查询。你可以通过使用并行 LINQ 来潜在地提高此处理的性能，它可以将你的顺序查询转换为并行查询，并在内部使用任务（排队到默认 TaskScheduler）将集合项的处理分散到多个 CPU 上，从而并发处理多个项。与 Parallel 的方法一样，如果你有许多项要处理，或者每个项的处理是耗时的计算密集型操作，那么从并行 LINQ 中获益最大。

静态的 System.Linq.ParallelEnumerable 类（定义在 System.Core.dll 中）实现了所有并行 LINQ 功能，因此必须通过 C# 的 using 指令将 System.Linq 命名空间导入源代码。特别是，该类公开了所有标准 LINQ 运算符的并行版本，例如 Where、Select、SelectMany、GroupBy、Join、OrderBy、Skip、Take 等。所有这些方法都是扩展方法，用于扩展 `System.Linq.ParallelQuery<T>` 类型。要让 LINQ to Objects 查询调用这些方法的并行版本，必须使用 ParallelEnumerable 的 AsParallel 扩展方法，将顺序查询（基于 `IEnumerable` 或 `IEnumerable<T>`）转换为并行查询（基于 `ParallelQuery` 或 `ParallelQuery<T>`），其形式如下⁴⁰：

```csharp
public static ParallelQuery<TSource> AsParallel<TSource>(this IEnumerable<TSource> source)
public static ParallelQuery AsParallel(this IEnumerable source)
```

以下是一个已转换为并行查询的顺序查询示例。此查询返回程序集中定义的所有过时方法：

```csharp
private static void ObsoleteMethods(Assembly assembly) {
    var query =
        from type in assembly.GetExportedTypes().AsParallel()

        from method in type.GetMethods(BindingFlags.Public |
            BindingFlags.Instance | BindingFlags.Static)

        let obsoleteAttrType = typeof(ObsoleteAttribute)

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

虽然不常见，但在查询中可以通过调用 `ParallelEnumerable` 的 `AsSequential` 方法，从执行并行操作切换回执行顺序操作：

```csharp
public static IEnumerable<TSource> AsSequential<TSource>(this ParallelQuery<TSource> source)
```

此方法基本上将 `ParallelQuery<T>` 转换回 `IEnumerable<T>`，以便在调用 `AsSequential` 之后执行的操作仅由一个线程执行。

通常，LINQ 查询生成的结果数据是通过某个线程执行 `foreach` 语句来计算的（如前所示）。这意味着只有一个线程遍历查询的所有结果。如果希望并行处理查询结果，则应使用 `ParallelEnumerable` 的 `ForAll` 方法处理结果查询：

```csharp
static void ForAll<TSource>(this ParallelQuery<TSource> source, Action<TSource> action)
```

此方法允许多个线程同时处理结果。我可以修改前面的代码以使用此方法，如下所示：

```csharp
// Display the results
query.ForAll(Console.WriteLine);
```

然而，让多个线程同时调用 Console.WriteLine 实际上会损害性能，因为 Console 类在内部同步线程，确保一次只有一个线程能访问控制台窗口。这可以防止多个线程的文本交错，否则输出将难以理解。当你打算对每个结果执行计算时，请使用 ForAll 方法。

由于并行 LINQ 使用多个线程处理项，因此项是并发处理的，结果以无序方式返回。如果需要让并行 LINQ 在项处理时保持其顺序，可以调用 ParallelEnumerable 的 AsOrdered 方法。调用此方法时，线程将分组处理项，然后将各组合并回去并保持顺序；这会损害性能。以下运算符会产生无序操作：Distinct、Except、Intersect、Union、Join、GroupBy、GroupJoin 和 ToLookup。如果希望在这些运算符之一之后再次强制排序，只需调用 AsOrdered 方法。

以下运算符会产生有序操作：OrderBy、OrderByDescending、ThenBy 和 ThenByDescending。如果希望在这些运算符之一之后恢复无序处理以提高性能，只需调用 AsUnordered 方法。

并行 LINQ 还提供了一些额外的 ParallelEnumerable 方法，你可以调用它们来控制查询的处理方式：

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

显然，WithCancellation 方法允许你传入 CancellationToken，以便可以提前停止查询处理。WithDegreeOfParallelism 方法指定允许处理查询的最大线程数；如果并非所有线程都必要，它不会强制创建线程。通常你不会调用此方法，默认情况下查询将使用每个核心一个线程执行。但是，如果你想保留一些核心用于其他工作，可以调用 WithDegreeOfParallelism 并传入一个小于可用核心数的数字。如果查询执行同步 I/O 操作，你也可以传入一个大于核心数的数字，因为线程在这些操作期间会阻塞。这会浪费更多线程，但可以在更短时间内产生最终结果。你可能会考虑在客户端应用程序中这样做，但我强烈建议不要在服务器应用程序中执行同步 I/O 操作。

并行 LINQ 会分析查询，然后决定如何最好地处理它。有时按顺序处理查询会获得更好的性能。在使用以下任何操作时通常如此：
