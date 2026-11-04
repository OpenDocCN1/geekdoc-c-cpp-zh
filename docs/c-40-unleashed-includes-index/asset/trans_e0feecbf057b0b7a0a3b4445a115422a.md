

## “无需关心”参数

一些函数式语言提供一种“无需关心”标识符，可用于声明函数的某个参数不会被使用。通常使用下划线字符。由于下划线在 C# 中是有效标识符，你也可以采用同样的技巧：

```csharp
source.Aggregate(0, (n, _) => n + 1)
```

不过请注意，下划线只是一个与其他标识符一样的标识符，因此受适用于标识符、其声明及外围作用域的所有规则约束。如果函数有多个参数可以被忽略，你无法用下划线在所有这些参数上表达“无需关心”的特性。在函数式语言中，这种“通配符”语法实际上是一种允许此类用法的特殊标识符，但在 C# 中，它只是一个与其他标识符一样的标识符。

还有一些重载可用于计算序列中与特定谓词匹配的元素数量：

```csharp
int Count<T>(this IEnumerable<T> source, Func<T, bool> predicate);
long LongCount<T>(this IEnumerable<T> source, Func<T, bool> predicate);
```

使用这些重载，只不过等同于将 Where 运算符与 Count 或 LongCount 的简单形式（不带谓词）结合使用。

## Sum 与 Average

Sum 与 Average 密切相关，计算的就是你所期望的结果。这些聚合操作有大量重载，适用于所有数值基元类型及其可空变体。我们先来看 Sum，展示各种数值类型可用的两个重载：

```csharp
static int Sum(this IEnumerable<int> source);
static int Sum<TSource>(this IEnumerable<TSource> source,
    Func<TSource, int> selector);
```

第一个重载直接作用于数值序列，而后者先执行投影。第二种形式也可以写成先调用 Select，再调用第一种形式的 Sum。

当结果超出该数值类型的精度时，会生成 OverflowException。如果不想这样，你始终可以使用通用的 Aggregate 运算符手动计算总和，并可能返回更精确的类型。下面是一个将 32 位整数值求和为 64 位整数、且不使用 checked 关键字的示例：

```csharp
source.Aggregate(0L, (long sum, int item) => sum + item)
```

可空变体会隐式将 null 值合并为被求和数值类型的默认值。这对应于 Sum 等聚合运算符的典型数据库语义：

```csharp
static int? Sum(this IEnumerable<int> source);
static int? Sum<TSource>(this IEnumerable<TSource> source,
                         Func<TSource, int?> selector);
// Sample use:
new int?[] { 1, null, 2 }.Sum() == 3
```

如果不需要这种 null 合并，你始终可以使用 Aggregate 来获得不同的行为。例如：

```csharp
new int?[] { 1, null, 2 }.Aggregate((int?)0, (sum, n) => sum + n) == null
```

或者，如果你希望在遇到 null 值时抛出异常，只需在聚合期间对可空元素调用 Value 属性：

```csharp
new int?[] { 1, null, 2 }.Aggregate((int?)0, (sum, n) => sum + n.Value)
```

这清楚地说明了通用聚合运算符的强大之处：当某些专用聚合运算符无法提供所需结果时，它可以充当一个“安全阀”。

基于到目前为止对各种聚合运算符的介绍，Average 也应该很容易理解。需要指出的是，Average 运算符并不等同于对同一序列调用 Sum() 再除以 Count()。这个不变式不成立有几个原因：

- Sum 的 null 合并行为会将 null 值视为零。Count 会把 null 值当作正常元素计数，因此 null 元素会被计入除法的分母。而对可空序列求 Average 时，计数只使用非 null 值。
- 分别使用 Sum 和 Count 会导致对源序列进行两次迭代。由于序列采用延迟求值，两次迭代可能产生与单次迭代不同的结果（例如，由于全局状态或外部状态发生变化）。此外，如果输入序列是暴露副作用的迭代器，这些副作用会被重复执行。

关于可用的 Average 重载，最后要说明一点：对整数值求平均时，结果类型属于浮点域。例如：

```csharp
static double Average(this IEnumerable<int> source);
```

如何通过手动应用 Aggregate 来实现不同的效果？基于前面反对使用 Count 和 Sum 的建议，我们应当考虑另一种同时完成求和与元素计数的方式。一种做法是将累加值设为一个匿名类型实例，该实例分别具有用于总和与计数的两个属性：

```csharp
new[] { 1, 2, 3 }.Aggregate(
    new { Count = 0, Sum = 0 },
    (acc, n) => new { Count = acc.Count + 1, Sum = acc.Sum + n },
    acc => acc.Sum / acc.Count /* integral division */
)
```

前面的示例说明了 C# 语言借助匿名类型和 lambda 表达式引入的表达能力。请注意，在同一个外围方法内，多次使用具有相同属性名称和类型的匿名类型会得到兼容的类型。特别是，我们对累加函数的种子和结果使用了同一个匿名类型。

## 结构化类型

匿名类型是该语言中一种非常弱的结构化类型形式。只要它们在属性名称及其类型方面形状相同，它们就是兼容的（在外围方法的范围内）。

在前面的示例中，Aggregate 上的类型推断必须得出结论：种子类型与累加函数的返回类型彼此兼容：

```
new[] { 1, 2, 3 }.Aggregate<int, <>__Anon`2, int>(...)
```

在真正的结构化类型系统（如 Microsoft 的 M 建模语言等语言中所见）中，值之间兼容性的灵活度会更大；例如，可以声明 { X = 1, Y = 2 } 和 { X = 1, Y = 2, Z = 3 } 参与子类型关系（即声明二维点和三维点之间存在某种兼容性）。

## Min 与 Max

最小值和最大值聚合也很容易理解。Min 和 Max 有一系列重载，提供在序列上计算数值最小值和最大值的功能。例如

```
new[] { 1, 3, 2 }.Max() == 3
```

还存在针对可空值的重载，它们在计算最小值或最大值时会忽略 null 值。除此之外，还有接受额外选择器函数的重载：

```
static T Min<T, R>(this IEnumerable<T> source, Func<T, R> selector);
```

对于这类重载，使用类型 R 上的默认比较器执行比较。遗憾的是，没有接受 IComparer<R> 的重载可用。这个非数值运算符也可以在没有选择器函数的情况下使用：

```
static T Min<T>(this IEnumerable<T> source);
```

下面是上述运算符的兄弟运算符 Max 的一个示例用法：

```
new[] { "Bart", "Lisa", "John" }.Max() == "Lisa"
```

## MinBy、MaxBy？

聚合运算符中一个相对经常被要求的功能是 MinBy 和 MaxBy 运算符，它们允许通过指定键提取器函数来选择最小或最大元素（例如，选择年龄最小的人）：

```
people.MinBy(person => person.Age).Name
```

在面对泛型比较器之类的情况时，创建这样的运算符有点棘手。尽管这是一个很好的练习，但 .NET 的响应式扩展很可能会将此类运算符作为 System.Interactive 程序集的一部分提供。有关更多信息，请在 MSDN 上搜索“DevLabs Reactive Extensions”。

## 组合更佳：GroupBy 与聚合

聚合运算符最常见的用途之一是与分组操作结合使用。按某个共同属性对元素分组后，人们希望分别计算每个组内所有元素的统计信息。示例如下：

```
var procStats = from process in Process.GetProcesses()
    group process by process.ProcessName into g
    select new { Process = g.Key,
        Count = g.Count(),
        Memory = g.Sum(p => p.WorkingSet64) } into stat
where stat.Memory > 100 * 1024 * 1024
orderby stat.Memory descending
select stat;
```

打印这些统计信息将显示使用同一可执行文件的进程组，按内存消耗降序排列，并且仅限于总消耗达到 100MB 或以上的组。请注意，在这种场景下，使用带选择器函数的 Sum 重载非常有用。

## Visual Basic 中的聚合

与 C# 相比，Visual Basic 语言为标准查询运算符提供了稍多一点的查询表达式支持。Visual Basic 在查询操作方面额外提供内置关键字的一个领域就是聚合：

```
From p In Process.GetProcesses()
Group p By p.ProcessName Into Memory = Sum(p.WorkingSet64), Count = Count()
Where Memory > 100 * 1024 * 1024
```

