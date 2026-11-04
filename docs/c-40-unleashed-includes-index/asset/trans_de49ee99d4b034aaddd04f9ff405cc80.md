

要理解其工作原理，不妨深入幕后一探究竟。在查询执行期间，会创建表示包含姓名和年龄的复合键的匿名类型的实例。为了进行分组，必须维护一种数据结构，将键值映射到共享该键的所有对象。

你会想起在讨论泛型时介绍过的一个合适的集合类型，即 `Dictionary<TKey, TValue>`。在这里，键的类型参数将成为匿名类型，而值将是共享该键的对象的某种集合。为此，我们应该能够检查键是否相等，并且为了使内部字典存储性能良好，一个好的哈希码也是可取的。那么，对于用于复合键的匿名类型，这是如何实现的呢？

简单来说，匿名类型是由编译器根据你指定的结构生成的类，它们重写了定义在 `System.Object` 上的 `Equals`、`GetHashCode` 和 `ToString` 方法。在输出中，我们已经看到了 `ToString` 方法的样子，因为它会输出属性的名称-值对：

```
// 打印 { First = Bart, Age = 26 }
Console.WriteLine(new { First = "Bart", Age = 26 });
```

图 19.27 通过 ILDASM 显示了这些被重写方法的存在。建议你使用更合适的工具（如 .NET Reflector）检查这些方法的实现，以了解相等性检查和哈希码计算是如何完成的。简而言之，`Equals` 使用底层数据的默认相等比较器（本例中为 `Age` 整数和 `First` 字符串），而 `GetHashCode` 计算并组合底层数据字段的哈希码，并混入一些（看似神奇的）常量数字，以确保良好的哈希码特性。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_976_0.png)

图 19.27 对 `Equals`、`GetHashCode` 和 `ToString` 的重写。

为结束本示例的讨论，请注意对局部变量过度使用类型推断的情况。使用复合键会产生匿名类型，顾名思义，这种类型无法通过名称引用。在这种情况下，必须使用隐式类型局部变量，既要引用结果，也要遍历分组：

```csharp
var personnel = new[] {
    new { ID = 1, First = "Bart", Age = 26 },
    ...
};
```

```csharp
var byNameAndAge = from employee in personnel
                   group employee by new { employee.First,
                                           employee.Age };
```

此外，我们使用了一个包含匿名类型的隐式类型数组作为数据源，这仅仅是为了说明。更常见的情况是，你会有针对人员表中员工对象的命名类型。然而，在本示例中到处使用匿名类型，这让你处于一个独特的位置来测试对分组行为与类型关系的理解。像往常一样，编辑器将引导我们完成这个探索性练习。

首先，让我们看一下为 `personnel` 数组推断出的类型，如图 19.28 所示。由于元素是同一个匿名类型的实例，推断出的类型是该匿名类型的数组。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_977_0.png)

图 19.28 一个包含匿名类型元素的隐式类型数组。

鉴于数组元素属于这个匿名类型，我们已经可以推断出 `GroupBy` 结果对象的部分类型：

```csharp
public static IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(
    this IEnumerable<TSource> source, Func<TSource, TKey> keySelector);
```

这里，`TSource` 应该是用于源元素的匿名类型（即图 19.28 所示的类型）。键选择器函数接收这些对象，并将其映射到我们用另一个匿名类型指定的复合键对象上。这使我们能够推断出 `TKey` 泛型类型参数。最后，由此我们可以推断出 `GroupBy` 运算符或 LINQ 查询表达式转换后的结果的类型。图 19.29 显示了最终类型。

```
var byNameAndAge = from employee in personnel
System.Collections.Generic.IEnumerable<out T>
公开枚举器，该枚举器支持对指定类型集合进行简单迭代。
如果 IsGrouping 'a','b'
匿名类型：
'a' 是 new { string First, int Age }
'b' 是 new { int ID, string First, int Age }
```

图 19.29 使用复合键的 `GroupBy` 操作的结果类型。

在这里，'a' 表示分组的键类型，包含 `First` 和 `Age` 属性，而 'b' 与我们的源集合元素所使用的类型完全相同。

## 查询模式

我们目前所见的 `group by` 子句可以根据其在幕后发生的转换进行总结。像往常一样，LINQ 查询表达式语法会转换为底层的方法调用，`group by` 也不例外。图 19.30 展示了如何实现 `group by` 的转换。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_978_0.png)

图 19.30 `group by` 子句的查询模式转换。

## 更复杂的分组子句

紧跟在 `group` 之后、`by` 关键字之前指定的标识符不必与某个范围变量相同。例如，你可以这样写：

```
from product in products
group product.Price by product.Category
```

这将产生以类别为键、每组包含价格的分组结果。此形式的转换使用了另一个 `GroupBy` 重载，该重载额外接收一个用于“元素选择器”的 lambda 表达式。

## 使用 join 子句进行联接

数据往往是更大的整体图景中的一部分，其中包含许多相互关联的数据源，就像关系数据库中那样。在这样的环境中，查询通常会通过某个条件联接多个数据源，从而同时针对多个数据源进行。在关系数据库技术中，这通常是通过为数据记录赋予唯一标识符（称为主键）来实现的。为了引用另一个表中的数据记录，会将某列指定为外键，引用相关表的主键。

图 19.31 在 LINQ to SQL 的上下文中展示了这种关系，有时也称为关联。在这个特定案例中，一个类别可以关联多个产品，因此基数为一对多。要从 `Product` 转到其 `Category`，`Parent` 属性被设置为 `Category`。在相反方向，你可以通过名为 `Products` 的 `Child` 属性获取给定类别中的产品。在“属性”窗口的底部，显示了底层关系：

```
Category.CategoryID -> Product.CategoryID
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_979_0.png)

图 19.31 LINQ to SQL 中两个表之间的关系。

在左侧，我们看到用 ID 唯一标识类别的主键，在右侧，它被引用为 `Product` 表中的外键。

因为我们目前专注于 LINQ to Objects 来解释查询运算符和查询表达式语法中的各种子句，所以我们暂且将 LINQ to SQL 排除在外，而是用内存中的数据来创建一个示例。

基类库（BCL）充满了有趣的数据源，返回泛型或非泛型 `IEnumerable` 对象的成员都可用于查询。其中一处是 `System.Diagnostics` 中的 `Process` 类：

```
Process[] processes = Process.GetProcesses();
```

使用此方法，我们可以获取机器上当前运行的所有进程的信息。例如，使用我们已经了解的查询子句，我们可以检索按内存占用降序排列的前几个进程：

```
const int MB = 1024 * 1024;
var heavyMemoryUsers = (from p in Process.GetProcesses()
                         where p.WorkingSet64 > 100 * MB
                         orderby p.WorkingSet64 descending
                         select new { Name = p.ProcessName,
                                      Memory = p.WorkingSet64 / MB }
                        ).Take(10);

foreach (var p in heavyMemoryUsers)
    Console.WriteLine(p);
```

调用 `Take(10)` 只是检索查询结果的前 10 个对象。你将在第 20 章看到这个标准查询运算符及类似的运算符。在我的机器上，上述查询打印了以下内容：

```
{ Name = devenv, Memory = 552 }
{ Name = devenv, Memory = 326 }
{ Name = iexplore, Memory = 279 }
{ Name = devenv, Memory = 230 }
{ Name = devenv, Memory = 229 }
{ Name = dwm, Memory = 199 }
{ Name = iexplore, Memory = 193 }
{ Name = sqlservr, Memory = 190 }
{ Name = svchost, Memory = 173 }
{ Name = WINWORD, Memory = 169 }
```

虽然这很好，但如果能为进程提供友好的名称就更好了。为了实现这一点，我们可以创建一个独立的集合，将进程名映射到描述信息：

```
var processDescriptions = new [] {
    new { Name = "devenv", Description = "Microsoft Visual Studio" },
    new { Name = "dwm", Description = "Desktop Window Manager" },
    new { Name = "iexplore", Description = "Windows Internet Explorer" },
    new { Name = "sqlservr", Description = "Microsoft SQL Server" },
    new { Name = "svchost", Description = "Service Host" },
    new { Name = "WINWORD", Description = "Microsoft Office Word" }
};
```

现在，包含 `Process` 对象的集合和描述信息集合有了共同之处：进程名。接下来要做的是，基于它们共有的某个键的相等性来联接这两个数据源。这如图 19.32 所示。

