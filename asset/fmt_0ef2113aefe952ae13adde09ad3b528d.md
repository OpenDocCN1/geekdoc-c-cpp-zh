

`Empty` 方法返回一个不返回值的迭代器。这可用于需要集合的参数，你可以将空集合传递给它。

`Repeat` 方法返回一个迭代器，该迭代器会重复返回同一个值指定次数。

### 并行 LINQ

`System.Linq` 命名空间中的 `ParallelEnumerable` 类将查询的工作分解到多个同时运行的线程上。虽然 `Enumerable` 类定义了 `IEnumerable<T>` 接口的扩展方法，但 `ParallelEnumerable` 类的大多数扩展方法是 `ParallelQuery<TSource>` 类的扩展。一个重要的例外是 `AsParallel` 方法，它扩展了 `IEnumerable<TSource>` 并返回 `ParallelQuery<TSource>`，因此普通集合类可以以并行方式查询。

#### 并行查询

为了演示并行 LINQ（PLINQ），需要一个大集合。使用小集合时，当集合适合 CPU 缓存时你不会看到任何效果。在下面的代码中，一个大的 int 集合被随机值填充（代码文件 `ParallelLinqSample/Program.cs`）：

```csharp
static IEnumerable<int> SampleData()
{
    const int arraySize = 50000000;
    var r = new Random();
    return Enumerable.Range(0, arraySize).Select(x =>
        r.Next(140)).ToList();
}
```

现在你可以使用 LINQ 查询来过滤数据、进行一些计算，并获取过滤后数据的平均值。该查询使用 `where` 子句定义过滤器，只汇总值小于 20 的项，然后调用聚合函数 `sum`。与目前所见 LINQ 查询的唯一区别是调用了 `AsParallel` 方法：

```csharp
var res = (from x in data.AsParallel()
    where Math.Log(x) < 4
    select x).Average();
```

与已展示的 LINQ 查询一样，编译器会将语法转换为调用 `AsParallel`、`Where`、`Select` 和 `Average` 方法。`AsParallel` 在 `ParallelEnumerable` 类中定义，用于扩展 `IEnumerable<T>` 接口，因此可以简单地使用数组调用。`AsParallel` 返回 `ParallelQuery<TSource>`。由于返回类型的原因，编译器选择的 `Where` 方法是 `ParallelEnumerable.Where` 而不是 `Enumerable.Where`。在下面的代码中，`Select` 和 `Average` 方法也来自 `ParallelEnumerable`。与 `Enumerable` 类的实现相比，`ParallelEnumerable` 类会将查询分区，以便多个线程可以同时处理查询。集合可以被拆分成多个部分，不同的线程分别处理每部分以过滤剩余项。分区工作完成后，必须进行合并以获得所有部分的汇总结果：

```csharp
var res = data.AsParallel().Where(x => Math.Log(x) < 4).
    Select(x => x).Average();
```

运行此代码时，你还可以打开任务管理器确认系统所有 CPU 都在忙碌。如果移除 `AsParallel` 方法，则可能无法使用多个 CPU。当然，如果你的系统没有多个 CPU，则不要期望并行版本会有所改善。

#### 分区器

`AsParallel` 方法不仅扩展了 `IEnumerable<T>` 接口，还扩展了 `Partitioner` 类。这样你可以影响要创建的分区。

`Partitioner` 类定义在 `System.Collections.Concurrent` 命名空间中，并有不同的变体。`Create` 方法接受数组或实现 `IList<T>` 的对象。根据这些，以及参数 `loadBalance`（布尔类型，在该方法的一些重载中可用），会返回不同类型的分区器。对于数组，使用 `DynamicPartitionerForArray<TSource>` 和 `StaticPartitionerForArray<TSource>` 类，两者都派生自抽象基类 `OrderablePartitioner<TSource>`。

在下面的示例中，“并行查询”部分的代码被修改为手动创建分区器，而不是依赖默认分区器：

```csharp
var result = (from x in Partitioner.Create(data,
    true).AsParallel()
    where Math.Log(x) < 4
    select x).Average();
```

你还可以通过调用 `WithExecutionMode` 和 `WithDegreeOfParallelism` 方法来影响并行度。使用 `WithExecutionMode` 你可以传入 `ParallelExecutionMode` 的值，该值可以是 `Default` 或 `ForceParallelism`。默认情况下，并行 LINQ 会避免高开销的并行化。使用 `WithDegreeOfParallelism` 方法，你可以传入一个整数值来指定应并行运行的最大任务数。如果查询不应使用所有 CPU 核心，这很有用。

> 注意 你可以在第 21 章“任务与并行编程”和第 22 章“任务同步”中了解更多关于任务和线程的内容。

### 取消

.NET 提供了一种取消长时间运行任务的标准方式，并行 LINQ 也是如此。

要取消长时间运行的查询，你可以向查询添加 `WithCancellation` 方法，并将 `CancellationToken` 传递给参数。`CancellationToken` 由 `CancellationTokenSource` 创建。查询在单独线程中运行，在该线程中捕获 `OperationCanceledException` 类型的异常。如果查询被取消，则会触发此异常。在主线程中，可以通过调用 `CancellationTokenSource` 的 `Cancel` 方法来取消任务：

```csharp
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

```csharp
WriteLine("query started");
Write("cancel?");
string input = ReadLine();
if (input.ToLower().Equals("y"))
{
    // cancel!
    cts.Cancel();
}
```

> 注意：你可以在第21章了解更多关于取消和 `CancellationToken` 的详细信息。

### 表达式树

对于 LINQ to Objects，扩展方法需要一个委托类型作为参数；这样，lambda 表达式可以赋给该参数。lambda 表达式也可以赋给类型为 `Expression<T>` 的参数。C# 编译器根据类型的不同，为 lambda 表达式定义不同的行为。如果类型是 `Expression<T>`，编译器将从 lambda 表达式创建表达式树并将其存储在程序集中。表达式树可以在运行时进行分析，并针对数据源优化查询。

让我们转向之前使用过的查询表达式（代码文件 `ExpressionTreeSample/Program.cs`）：

```csharp
var brazilRacers = from r in racers
    where r.Country == "Brazil"
    orderby r.Wins
    select r;
```

前面的查询表达式使用了扩展方法 `Where`、`OrderBy` 和 `Select`。`Enumerable` 类定义了 `Where` 扩展方法，其委托类型 `Func<T, bool>` 作为谓词参数：

```csharp
public static IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source, Func<TSource, bool> predicate);
```

这样，lambda 表达式被赋给谓词。这里，lambda 表达式类似于匿名方法，如前所述：

```csharp
Func<Racer, bool> predicate = r => r.Country == "Brazil";
```

`Enumerable` 类不是定义 `Where` 扩展方法的唯一类。`Where` 扩展方法也由 `Queryable` 类定义。该类有 `Where` 扩展方法的不同定义：

```csharp
public static IQueryable<TSource> Where<TSource>(
    this IQueryable<TSource> source,
    Expression<Func<TSource, bool>> predicate);
```

这里，lambda 表达式被赋给类型 `Expression<T>`，其行为有所不同：

```csharp
Expression<Func<Racer, bool>> predicate = r => r.Country == "Brazil";
```

编译器不是使用委托，而是向程序集发出表达式树。表达式树可以在运行时读取。表达式树由派生自抽象基类 `Expression` 的类构建。`Expression` 类与 `Expression<T>` 不同。一些继承自 `Expression` 的表达式类包括 `BinaryExpression`、`ConstantExpression`、`InvocationExpression`、`LambdaExpression`、`NewExpression`、`NewArrayExpression`、`TernaryExpression`、`UnaryExpression` 等。编译器根据 lambda 表达式创建表达式树。

例如，lambda 表达式 `r.Country == "Brazil"` 利用 `ParameterExpression`、`MemberExpression`、`ConstantExpression` 和 `MethodCallExpression` 来创建树并将树存储在程序集中。然后，此树在运行时用于为底层数据源创建优化的查询。

实现 `DisplayTree` 方法是为了在控制台上以图形方式显示表达式树。在下面的示例中，可以传递一个 `Expression` 对象，根据表达式类型，将有关该表达式的一些信息写入控制台。根据表达式的不同类型，递归调用 `DisplayTree`：

> 注意：此方法并不处理所有表达式类型，只处理以下示例表达式所使用的类型。

```csharp
private static void DisplayTree(int indent, string message, Expression expression)
{
    string output = $"{string.Empty.PadLeft(indent, '>')}{message}" +
        $"! NodeType: {expression.NodeType}; Expr: {expression}";
    indent++;
    switch (expression.NodeType)
    {
        case ExpressionType.Lambda:
            Console.WriteLine(output);
            LambdaExpression lambdaExpr = (LambdaExpression)expression;
            foreach (var parameter in lambdaExpr.Parameters)
            {
                DisplayTree(indent, "Parameter", parameter);
            }
            DisplayTree(indent, "Body", lambdaExpr.Body);
            break;
        case ExpressionType.Constant:
            ConstantExpression constExpr = (ConstantExpression)expression;
            WriteLine($"{output} Const Value: {constExpr.Value}");
            break;
        case ExpressionType.Parameter:
            ParameterExpression paramExpr = (ParameterExpression)expression;
            WriteLine($" {output} Param Type: {paramExpr.Type.Name} ");
            break;
        case ExpressionType.Equal:
        case ExpressionType.AndAlso:
        case ExpressionType.GreaterThan:
            BinaryExpression binExpr = (BinaryExpression)expression;
            if (binExpr.Method != null)
            {
                WriteLine($" {output} Method: {binExpr.Method.Name} ");
            }
            else
            {
                WriteLine(output);
            }
            DisplayTree(indent, "Left", binExpr.Left);
            DisplayTree(indent, "Right", binExpr.Right);
            break;
        case ExpressionType.MemberAccess:
            MemberExpression memberExpr = (MemberExpression)expression;
            WriteLine($" {output} Member Name: {memberExpr.Member.Name}, " +
                $"Type: {memberExpr.Type.Name}");
            DisplayTree(indent, "Member Expr", memberExpr.Expression);
            break;
        default:
            WriteLine();
            WriteLine($" {expression.NodeType} {expression.Type.Name} ");
            break;
    }
}
```

用于展示树的表达式已经周知。它是一个带有 `Racer` 参数的 lambda 表达式，表达式的主体仅选择来自巴西且获胜次数超过六次的赛车手：

```csharp
Expression<Func<Racer, bool>> expression =
    r => r.Country == "Brazil" && r.Wins > 6;
DisplayTree(0, "Lambda", expression);
```

查看树结果，你可以从输出中看到，lambda 表达式由 `Parameter` 和 `AndAlso` 节点类型组成。`AndAlso` 节点类型左侧是 `Equal` 节点类型，右侧是 `GreaterThan` 节点类型。`AndAlso` 节点类型左侧的 `Equal` 节点类型左侧是 `MemberAccess` 节点类型，右侧是 `Constant` 节点类型，依此类推：

```text
Lambda! NodeType: Lambda; Expr: r => ((r.Country == "Brazil") AndAlso (r.Wins > 6))
> Parameter! NodeType: Parameter; Expr: r Param Type: Racer
> Body! NodeType: AndAlso; Expr: ((r.Country == "Brazil") AndAlso (r.Wins > 6))
>> Left! NodeType: Equal; Expr: (r.Country == "Brazil") Method: op_Equality
