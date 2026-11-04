
前四个参数构成了任何一种连接，指定了数据源以及从其元素中提取键值的方式。这种特定连接的分组特性体现在 resultSelector 的存在上，它接收外部元素和对应的内部元素，并要求一个结果值。

## 连接

现在我们已经了解 GroupJoin 如何将单个外部元素与所有对应的内部元素组合起来，是时候来看一种更通用的连接类型了，它允许共享相同键的单个外部元素和内部元素进行组合。存在两个重载：

```
static IEnumerable<R> Join<O,I,K,R>(
    this IEnumerable<O> outer,
    IEnumerable<I> inner,
    Func<O, K> outerKeySelector,
    Func<I, K> innerKeySelector,
    Func<O, I, R> resultSelector);
```

```
static IEnumerable<R> Join<O,I,K,R>(
    this IEnumerable<O> outer,
    IEnumerable<I> inner,
    Func<O, K> outerKeySelector,
    Func<I, K> innerKeySelector,
    Func<O, I, R> resultSelector,
    IEqualityComparer<K> comparer);
```

如前所述，关键区别在于第五个参数，它不再使用整个内部元素组，而是基于键相等，接收一个外部元素和一个关联内部元素的配对。

在查询表达式方面，这对应于使用 join 子句，但后面不跟 into 延续。示例如下：

```
// from product in northwind.Products
// join order in northwind.Orders on product.ID equals order.Product
// select product.Name + " is ordered by " + order.Customer.Name
northwind.Products.Join(
    northwind.Orders,
    product => product.ID,  // role of "primary key"
    order => order.Product,  // role of "foreign key"
    (product, order) => product.Name + " is ordered by " + order.Customer.Name
)
```

再次，立即使用 select 会导致投影函数的主体被嵌入到最后一个参数的选择器函数中。一旦在 join 使用之后跟随其他子句，透明标识符就会出现：

```
from product in northwind.Products
join order in northwind.Orders on product.ID equals order.Product
where order.Quantity >= 10
select product.Name + " is ordered by " + order.Customer.Name
```

这里，product 和 order 将被打包到一个匿名类型中，以便在查询表达式后续的子句中可以引用它们（对查询表达式语法用户来说是透明的）。前述内容大致可翻译为如下：

```
northwind.Products.Join(
    northwind.Orders,
    product => product.ID,
    order => order.Product,
    (product, order) => new { product, order }
).Where(
    transparentId => transparentId.order.Quantity >= 10
).Select(
    transparentId => transparentId.product.Name + " is ordered by "
                    + transparentId.order.Customer.Name
)
```

幸运的是，作为查询表达式语法的用户，你不必担心为在查询中传递对象而必须跳过的各种环节。

GroupJoin 与 Join 的比较如 图 20.9 所示。

### 左外连接

有时人们会寻找左外连接，其中每个外部（左）元素都会被返回，无论它是否有对应的内部（右）元素。虽然没有直接的运算符用于此操作，但你可以结合 GroupJoin 和 DefaultIfEmpty 来实现相同的效果。有关更多信息，请在 MSDN 中搜索 "LINQ left outer join"。

## 聚合

信息分析通常需要减少数据量，计算所涉及数据的某些统计信息。这些操作称为聚合，它们将对象集合转换为单个值，表示以某种形式组合的原始信息。

由于所有聚合在概念上是相同的，我们首先来看通用 Aggregate 运算符，并稍后讨论更具体的聚合运算符。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1038_0.png)

图 20.9 连接操作类型的比较。

### Aggregate

聚合运算符接收类型为 T 的元素序列，并将其转换为另一种类型 A 的单个值，A 代表累积或聚合，具体取决于你的用词选择。但我们如何将任意数量的类型为 T 的元素转换为另一种类型的单个值呢？让我们从最简单的情况开始，即两种类型相同，并查看如何创建整数值序列的和，如图 20.10 所示。

基于此，我们可以看到计算未知数量整数值的和并不需要任何花哨的东西：我们只需要一个可以相加两个数字的二元函数。通过重复使用该函数，一次从输入序列中消费一个元素（按从左到右的方式），我们可以计算出总和。

到目前为止，我们的输入序列和聚合结果仍保持在相同的值域中，但在更通用的世界里，我们希望这些类型有所不同。事实上，对于求和，我们可能希望整数值的和结果为 long，以降低溢出 32 位精度的风险。更一般地说，我们可能希望做诸如将数字序列聚合为连接它们的字符串之类的操作。在这种情况下，输入类型（整数序列）与聚合输出类型（单个字符串）明显不同。

为了使之在一般情况下可行，我们对第一次尝试的聚合操作引入了两个进一步的更改。特别是，我们添加一个种子值来启动计算，并将聚合函数泛化为接收迄今为止的聚合值和下一个要聚合的元素。在使用泛型的 C# 术语中，它看起来像这样：

```
A Aggregate<T, A>(this IEnumerable<T> source,
                 A seed,
                 Func<A, T, A> accumulate);
```

例如，给定一个等于空字符串 "" 的种子和一个接收字符串和输入中某个元素并将其连接以产生新的聚合值的函数，我们可以将聚合字符串与下一个元素连接起来产生新的聚合值。

### 左折叠

在函数式编程语言中，这种形式的聚合被称为左折叠。给定一个元素序列，我们一次折叠一个元素，从左侧开始，逐步向右侧末尾推进。相反的操作，即右折叠，在 LINQ 中没有直接可用；然而，你可以用左折叠来表达右折叠。（提示：累积类型将是一个函数。）不过，实际上左折叠通常更有用，并且具有更好的内存特征，因为在能够组合右侧末尾的值之前，不必先扫描整个输入序列。

图 20.11 所示的示例可以用 C# 写成如下形式：

```
new[] { 3, 7, 1, 5, 0, 8, 0, 4, 2 }
  .Aggregate("", (s, n) => s + n.ToString())
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1039_0.png)

图 20.10 求和是一个简单的聚合操作。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1040_0.png)

图 20.11 具有不同元素类型和累积类型的聚合。

总之，Aggregate 运算符的一般示意表示如 图 20.12 所示。

```
A Aggregate<T,A>(IEnumerable<T>source,A seed,Func<A,T,A>accumulate)
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1040_1.png)

图 20.12 具有不同元素类型和累积类型的聚合。

请注意，由于连接操作的部分结果分配了大量中间字符串，字符串连接示例效率非常低。使用 StringBuilder 会好得多，这也可以使用 Aggregate 实现：

```
new[] { 3, 7, 1, 5, 0, 8, 0, 4, 2 }
.Aggregate(new StringBuilder(), (sb, n) => sb.Append(n.ToString()))
```

StringBuilder 类型有一个 Append 方法，它将给定字符串追加到缓冲区的末尾，并返回 StringBuilder 本身，以便可以以流畅的方式继续向其追加内容。这次，聚合类型是 StringBuilder，这意味着返回类型也将是 StringBuilder。我们更可能希望将此结果转换为字符串，这可以通过对结果调用 ToString 来完成。或者，可以使用 Aggregate 的重载来对结果执行此最终转换：

```
R Aggregate<T, A, R>(this IEnumerable<T> source,
    A seed,
    Func<A, T, A> accumulate,
    Func<A, R> resultSelector);
```

在我们的示例中，我们可以使用此重载来指定将已使用的 StringBuilder 转换为字符串的最后一步：

```
new[] { 3, 7, 1, 5, 0, 8, 0, 4, 2 }
.Aggregate(new StringBuilder(),
    (sb, n) => sb.Append(n.ToString()),
    sb => sb.ToString())
```

### 计数和长计数

最简单的聚合操作之一是统计源序列中出现的元素数量。Count 和 LongCount 正是这样做，分别返回 Int32 和 Int64 值。签名如下所示：

```
int Count<T>(this IEnumerable<T> source);
long LongCount<T>(this IEnumerable<T> source);
```

基于前面关于 Aggregate 的讨论，应该很清楚可以通过依赖 Aggregate 实现相同的效果，如下所示：

```
source.Aggregate(0, (n, item) => n + 1)
```

这种形式的聚合唯一有点奇怪的地方在于，输入序列中的元素并未在聚合结果中使用。
