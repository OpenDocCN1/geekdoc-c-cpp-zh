

## 表 8-20：使用记录结构体实例比较序列

| 方法 | 时间（毫秒） | 签名 |
|---|---|---|
| 55.7% SequenceEqual | 558 | System.Linq.Enumerable.SequenceEqual(IEnumerable, IEnumerable) |
| 13.7% Equals | 138 | Purchase.Equals(Purchase) |
| 10.2% Equals | 102 | System.Collections.Generic.GenericEqualityComparer`1.Equals(T, T) |
| 3.58% Equals | 36 | Product.Equals(Product) |
| 1.80% Equals | 18 | System.Decimal.Equals(Decimal) |
| 0.60% Equals | 6.0 | System.Int32.Equals(Int32) |
| 0.60% get_Default | 6.0 | System.Collections.Generic.EqualityComparer`1.get_Default() |

虽然 JIT 编译器可能会内联 `EqualityComparer<T>.Default` 属性的部分或全部使用，以及对其 `Equals` 方法的调用，但无法保证它一定能做到。正如我们之前用字段替换属性访问一样，我们可以定义自己的 `Equals` 方法，直接比较值，而无需使用 `EqualityComparer<T>`。但是，我们无法访问编译器为位置记录结构体生成的属性所生成的支撑字段。因此，在清单 8-22 中，我们为 `Purchase` 使用了一个简单的记录结构体，在其中定义了自己的私有字段和一个构造函数来初始化它们。

```
public readonly record struct Purchase
{
    public Purchase(Product item, DateTime ordered, int quantity)
        => (this.item, this.ordered, this.quantity) =
            (item, ordered, quantity);

    --snip--

    public bool Equals(Purchase other)
        => item.Equals(other.item) &&
            ordered.Equals(other.ordered) && quantity == other.quantity;

    private readonly Product item;
    private readonly DateTime ordered;
    private readonly int quantity;
}
```

## 清单 8-22：为 Purchase 结构体构造私有字段

我们还添加了自己实现的 `Equals`，直接比较我们定义的字段。这个自定义的 `Equals` 替换了如果我们没有定义自己的实现时编译器会引入的实现。我们还需要添加属性来暴露字段值，尽管这里没有展示属性，也没有展示以类似方式更改的 `Product` 类型。重新运行代码来比较两个各含 1000 万个 `Purchase` 项的序列，会产生如表 8-21 所示的报告。

对该语言及其惯用用法有一定了解即可。清单 8-23 展示了使用流畅语法创建 `Purchase` 对象列表的示例。

```
private static Purchase MakePurchase(int id)
    => new Purchase(new Product(id, id, "Some Description"),
        DateTime.MinValue, id);

var items = Enumerable.Range(0, count)
    .Select(i => MakePurchase(i))
    .ToList();
```

### 清单 8-23：LINQ 流畅语法

LINQ 还有一种替代查询语法，一些 C# 程序员觉得它更易于使用。清单 8-24 展示了创建清单 8-23 中 `items` 序列的等效查询语法。

```
var query = from i in Enumerable.Range(0, count)
    select MakePurchase(i);

var items = query.ToList();
```

### 清单 8-24：LINQ 查询语法

编译器会为清单 8-23 和 8-24 生成相同的 CIL 代码，因此选择哪种写法主要取决于我们觉得哪种阅读起来更清晰。有一种优化是可能的，但只能应用于流畅版本：避免将 lambda 作为 `Select` 方法的参数。该 lambda 需要捕获 `i` 变量，因此编译器会生成一个闭包对象，这会导致调用 `MakePurchase` 方法时多一层间接寻址。为了避免闭包，我们可以改为将 `MakePurchase` 作为方法组参数传递，如清单 8-25 所示。

```
var items = Enumerable.Range(0, count)
    .Select(MakePurchase)
    .ToList();
```

### 清单 8-25：通过使用方法组优化 LINQ

为了比较每种方法的效率，我们首先对清单 8-23 中使用 lambda 的版本进行性能分析。表 8-22 显示了创建一个包含 1000 万个项的列表的报告。

## 表 8-22：使用带有 Lambda 的 LINQ 创建序列的性能

| 方法 | 时间（毫秒） | 签名 |
|---|---|---|
| 98.1% ToList | 415 | System.Linq.Enumerable .ToList(IEnumerable) |
| 36.0% MakePurchase | 152 | MakePurchase(Int32) |
| 31.3% <Closure> b__3_0 | 132 | <>c.<Closure> b__3_0(Int32) |
| 31.3% MakePurchase | 132 | MakePurchase(Int32) |

标识符名称 `<c` 是编译器为捕获 `i` 变量而生成的闭包对象，这也是编译器引入在我们的代码中属于非法名称的一个例子。该闭包有一个实例方法 `<Closure> b__3_0`，它依次调用我们的 `MakePurchase` 方法。`MakePurchase` 方法在此报告中出现了两次——既在闭包方法内部，也在其外部——这是因为 JIT 编译器内联了对 `<Closure> b__3_0` 方法的一些调用，并直接调用了 `MakePurchase`。

表 8-23 中的报告显示了使用方法组方法创建 1000 万个项时的性能。

## 表 8-23：使用带有方法组的 LINQ 创建序列的性能

| 方法 | 时间（毫秒） | 签名 |
|---|---|---|
| 100% ToList | 430 | System.Linq.Enumerable.ToList(IEnumerable) |
| 71.9% MakePurchase | 309 | MakePurchase(Int32) |

有点反直觉的是，带有闭包对象的版本比使用方法组的版本还要稍微快一点。我们不应对此过度解读，因为这种差异完全在多次运行比较的误差范围内。然而，这确实告诉我们，无论绝对差异如何，使用 lambda 并不会带来显著的性能损失。

表示 lambda 的闭包对象只为整个表达式创建一次，而不是为 `Select` 方法生成的每个元素都创建一次。尽管闭包对象表示每次调用 `MakePurchase` 时多了一层间接寻址，但 JIT 编译器内联了对闭包 `<Closure> b__3_0` 方法的许多调用，并要么直接调用 `MakePurchase`，要么也内联其内容。

我们还可以用其他几种方式创建类似的序列。让我们研究两种常见的方法，看看它们的性能与使用 LINQ 相比如何。

## 迭代器方法

迭代器是 C# 的基础组成部分，也是包括 LINQ 在内的其他更高级功能的基础。事实上，LINQ 在现代 C# 中已经如此无处不在，以至于很容易忘记它基于两个系统接口：`IEnumerable<T>` 接口，它是类型为 `T` 的元素序列的抽象视图；以及 `IEnumerator<T>` 接口，它表示一个可以一次获取 `IEnumerable<T>` 中每个元素的迭代器。基本机制是 `IEnumerable<T>` 接口有一个名为 `GetEnumerator` 的方法，该方法返回一个 `IEnumerator<T>` 的实现。

这两个接口在现代代码中基本上被隐藏了，尽管 `IEnumerable<T>` 仍然很重要，它既是表示序列的类型的协议，也是构成 LINQ 系统大部分内容的扩展方法（如 `Select` 和 `Where`）的宿主。

`IEnumerator<T>` 接口也是 `foreach` 循环的基础，`foreach` 循环是枚举实现 `IEnumerable<T>` 的序列元素的一种方式。在清单 8-26 中，我们编写了自己的简单 `ToList` 方法，以便记录其性能并与 LINQ 等效方法进行比较。我们的 `ToList` 使用 `foreach` 填充 `Purchase` 对象的列表，因此依赖于 `Enumerable.Range` 方法提供的迭代器。

```
public static List<Purchase> ToList(int count)
{
    var items = new List<Purchase>();
    foreach(var i in Enumerable.Range(0, count))
    {
        items.Add(MakePurchase(i));
    }
    return items;
}
```

### 清单 8-26：使用 foreach 填充列表

将我们的 `ToList` 方法与清单 8-23 中的 LINQ 版本进行比较，首先要注意的是，我们需要在循环之前声明目标 `Purchase` 对象列表。`foreach` 循环从 `Enumerable.Range` 获取一个 `IEnumerator<int>`，并且 `foreach` 块的主体为迭代器中的每个元素运行。当我们查看表 8-24 中 `ToList` 方法的分析器报告时，我们可以看到基本机制。

## 表 8-24：对迭代器方法进行性能分析

| 方法 | 时间（毫秒） | 签名 |
|---|---|---|
| 100% ToList | 638 | ToList(Int32) |
| 41.2% AddWithResize | 263 | System.Collections.Generic.List`1.AddWithResize(T) |
| 38.1% MakePurchase | 243 | MakePurchase(Int32) |
| 0.95% MoveNext | 6.1 | System.Linq.Enumerable+ RangeIterator.MoveNext() |
| 0.95% get_Current | 6.0 | System.Linq.Enumerable+ Iterator`1.get_Current() |

这份分析报告展示了 `foreach` 结构的工作方式；`get_Current` 和 `MoveNext` 方法属于 `IEnumerator<T>` 接口，正如其名称所示，它们允许我们获取当前元素并将迭代器移动到序列中的下一项。

这份报告还显示，我们手工编写的 `ToList` 比表 8-22 中报告的 LINQ 版本慢得多，但我们没有对 `List<Purchase>` 的功能进行最佳利用。由于我们事先知道所需项的数量，我们可以避免 `AddWithResize` 方法的大部分开销，并在构造函数调用中指定列表的容量，如下所示：

```
var items = new List<Purchase>(count);
```

