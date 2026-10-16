
属性，并且元素选择器引用了 Racer 属性：

```
var racers = (from r in Formula1.GetChampions()
    from c in r.Cars
    select new
    {
        Car = c,
        Racer = r
    }).ToLookup(cr => cr.Car, cr => cr.Racer);
```

```
if (racers.Contains("Williams"))
{
    foreach (var williamsRacer in racers["Williams"])
    {
        WriteLine(williamsRacer);
    }
}
```

使用 Lookup 类的索引器访问所有“Williams”冠军的结果如下：

```
Alan Jones
Keke Rosberg
Nigel Mansell
Alain Prost
Damon Hill
Jacques Villeneuve
```

如果你需要对非类型化集合（如 ArrayList）使用 LINQ 查询，可以使用 `Cast` 方法。在下面的示例中，一个基于 Object 类型的 ArrayList 集合填充了 Racer 对象。要定义强类型查询，可以使用 `Cast` 方法：

```
var list = new System.Collections.ArrayList(Formula1.GetChampions()
    as System.Collections.ICollection);

var query = from r in list.Cast<Racer>()
    where r.Country == "USA"
    orderby r.Wins descending
    select r;
foreach (var racer in query)
{
    WriteLine($"{racer:A}", racer);
}
```

结果包括唯一的美国一级方程式冠军：

```
Mario Andretti, country: USA, starts: 128, wins: 12
Phil Hill, country: USA, starts: 48, wins: 3
```

## 生成运算符

生成运算符 `Range`、`Empty` 和 `Repeat` 不是扩展方法，而是返回序列的普通静态方法。在使用 LINQ to Objects 时，这些方法可通过 `Enumerable` 类使用。

你是否曾经需要填充一系列数字？没有什么比使用 `Range` 方法更简单了。该方法接收第一个参数作为起始值，第二个参数作为项数：

```
var values = Enumerable.Range(1, 20);
foreach (var item in values)
{
    Write($"{item} ", item);
}
WriteLine();
```

> **注意** `Range` 方法不会返回按定义填充了值的集合。与其他方法类似，该方法执行延迟查询执行。它返回一个 `RangeEnumerator`，该枚举器只对递增的值执行 yield return。

当然，结果现在看起来是这样的：

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
```

你可以将结果与其他扩展方法结合使用以获得不同结果——例如，使用 `Select` 扩展方法：

```
var values = Enumerable.Range(1, 20).Select(n => n * 3);
```

`Empty` 方法返回一个不返回值的迭代器。这可用于需要集合的参数，你可以将空集合传递给它。

`Repeat` 方法返回一个迭代器，该迭代器会重复返回同一个值指定次数。

## 并行 LINQ

`System.Linq` 命名空间中的 `ParallelEnumerable` 类将查询的工作分解到多个同时运行的线程上。虽然 `Enumerable` 类定义了 `IEnumerable<T>` 接口的扩展方法，但 `ParallelEnumerable` 类的大多数扩展方法是 `ParallelQuery<TSource>` 类的扩展。一个重要的例外是 `AsParallel` 方法，它扩展了 `IEnumerable<TSource>` 并返回 `ParallelQuery<TSource>`，因此普通集合类可以以并行方式查询。

### 并行查询

为了演示并行 LINQ（PLINQ），需要一个大集合。使用小集合时，当集合适合 CPU 缓存时你不会看到任何效果。在下面的代码中，一个大的 int 集合被随机值填充（代码文件 `ParallelLinqSample/Program.cs`）：

```
static IEnumerable<int> SampleData()
{
    const int arraySize = 50000000;
    var r = new Random();
    return Enumerable.Range(0, arraySize).Select(x =>
        r.Next(140)).ToList();
}
```

现在你可以使用 LINQ 查询来过滤数据、进行一些计算，并获取过滤后数据的平均值。该查询使用 `where` 子句定义过滤器，只汇总值小于 20 的项，然后调用聚合函数 `sum`。与目前所见 LINQ 查询的唯一区别是调用了 `AsParallel` 方法：

```
var res = (from x in data.AsParallel()
    where Math.Log(x) < 4
    select x).Average();
```

与已展示的 LINQ 查询一样，编译器会将语法转换为调用 `AsParallel`、`Where`、`Select` 和 `Average` 方法。`AsParallel` 在 `ParallelEnumerable` 类中定义，用于扩展 `IEnumerable<T>` 接口，因此可以简单地使用数组调用。`AsParallel` 返回 `ParallelQuery<TSource>`。由于返回类型的原因，编译器选择的 `Where` 方法是 `ParallelEnumerable.Where` 而不是 `Enumerable.Where`。在下面的代码中，`Select` 和 `Average` 方法也来自 `ParallelEnumerable`。与 `Enumerable` 类的实现相比，`ParallelEnumerable` 类会将查询分区，以便多个线程可以同时处理查询。集合可以被拆分成多个部分，不同的线程分别处理每部分以过滤剩余项。分区工作完成后，必须进行合并以获得所有部分的汇总结果：

```
var res = data.AsParallel().Where(x => Math.Log(x) < 4).
    Select(x => x).Average();
```

运行此代码时，你还可以打开任务管理器确认系统所有 CPU 都在忙碌。如果移除 `AsParallel` 方法，则可能无法使用多个 CPU。当然，如果你的系统没有多个 CPU，则不要期望并行版本会有所改善。

### 分区器

`AsParallel` 方法不仅扩展了 `IEnumerable<T>` 接口，还扩展了 `Partitioner` 类。这样你可以影响要创建的分区。

`Partitioner` 类定义在 `System.Collections.Concurrent` 命名空间中，并有不同的变体。`Create` 方法接受数组或实现 `IList<T>` 的对象。根据这些，以及参数 `loadBalance`（布尔类型，在该方法的一些重载中可用），会返回不同类型的分区器。对于数组，使用 `DynamicPartitionerForArray<TSource>` 和 `StaticPartitionerForArray<TSource>` 类，两者都派生自抽象基类 `OrderablePartitioner<TSource>`。

在下面的示例中，“并行查询”部分的代码被修改为手动创建分区器，而不是依赖默认分区器：

```
var result = (from x in Partitioner.Create(data,
    true).AsParallel()
    where Math.Log(x) < 4
    select x).Average();
```

你还可以通过调用 `WithExecutionMode` 和 `WithDegreeOfParallelism` 方法来影响并行度。使用 `WithExecutionMode` 你可以传入 `ParallelExecutionMode` 的值，该值可以是 `Default` 或 `ForceParallelism`。默认情况下，并行 LINQ 会避免高开销的并行化。使用 `WithDegreeOfParallelism` 方法，你可以传入一个整数值来指定应并行运行的最大任务数。如果查询不应使用所有 CPU 核心，这很有用。

> **注意** 你可以在第 21 章“任务与并行编程”和第 22 章“任务同步”中了解更多关于任务和线程的内容。

### 取消

.NET 提供了一种取消长时间运行任务的标准方式，并行 LINQ 也是如此。

要取消长时间运行的查询，你可以向查询添加 `WithCancellation` 方法，并将 `CancellationToken` 传递给参数。`CancellationToken` 由 `CancellationTokenSource` 创建。查询在单独线程中运行，在该线程中捕获 `OperationCanceledException` 类型的异常。如果查询被取消，则会触发此异常。在主线程中，可以通过调用 `CancellationTokenSource` 的 `Cancel` 方法来取消任务：

```
var cts = new CancellationTokenSource();

Task.Run(() =>
{
    try
    {
        var res = (from x in data.AsParallel().WithCancellation(cts.Token)
            where Math.Log(x) < 4
            select x).Average();
        WriteLine($"query finished, sum: {res}");
    }
    catch (OperationCanceledException ex)
    {
        WriteLine(ex.Message);
    }
});
```

