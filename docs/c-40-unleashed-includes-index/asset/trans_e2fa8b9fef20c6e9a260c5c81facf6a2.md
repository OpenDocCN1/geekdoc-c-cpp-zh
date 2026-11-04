

用于对元素进行排序。按键排序既可以按升序（默认），也可以按降序，具体使用相应的关键字。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_965_0.png)

图 19.19 筛选是水平分区。

除了只进行单一排序（因而只选择单一键）之外，还可以指定次要排序和 n 元排序。例如，你可能希望先按价格降序对产品列表排序，然后按名称升序排序。这样，对于所有价格相同的产品组，会再按名称进行排序。稍后你会看到一个这样的例子。

## 恒等键选择器

如果序列中的元素本身就可以排序（例如，因为它们是某种基本数据类型），可以使用一个平凡的恒等键选择器函数。例如：

```
var nums = new List<int> { 3, 5, 4, 2, 1 };
var sorted = from n in nums
    orderby n /* ascending */
    select n;
```

使用 `ascending` 关键字是可选的。给定元素 n，我们直接使用 n 本身来执行排序。在内部，这会转换为以下代码：

```
var nums = new List<int> { 3, 5, 4, 2, 1 };
var sorted = nums.OrderBy(n => n);
```

由此，恒等函数的使用就很清楚了。同样的恒等函数也可以用于降序排序，如下所示：

```
var nums = new List<int> { 3, 5, 4, 2, 1 };
var sortedDesc = from n in nums
    orderby n descending
    select n;
```

这会转换为一个 `OrderByDescending` 调用，看起来像这样：

```
var nums = new List<int> { 3, 5, 4, 2, 1 };
var sortedDesc = nums.OrderByDescending(n => n);
```

除非另有指定，否则排序基于元素类型的默认 `IComparer`（如你所见，通过 `IComparer<T>.Default` 获取）。我们在第 16 章“集合类型”中讨论比较器的概念。

## 稍微更急切

要建立排序，必须知道源序列中的所有元素，然后才能从有序序列中返回任何元素。尽管在查询表达式中使用排序仍然保持整个查询的惰性，但从结果序列中请求第一个元素的效果却是一个相当急切的操作，因为它会“耗尽”整个源序列以建立排序。

将其与 `Where` 和 `Select` 进行比较，后者只是从源中取出足够的元素来一次生成一个结果序列元素。对于 `Select`，这是一对一的关系：向结果请求下一个元素会导致 `Select` 从源中获取下一个元素并应用投影函数。`Where` 有时会更贪婪一些，因为它需要从源中消耗元素，直到筛选函数求值为 true。

`OrderBy` 只能加载源中的所有元素来对所有元素执行排序。请注意，我们这里只讨论 LINQ to Objects，在这种情况下，所有源元素最终都会进入一个适合执行排序操作的内存集合。对于远程 LINQ 执行（例如，使用 LINQ to SQL），排序操作将被远程化到服务器并在那里执行。

## 非平凡排序

你现在应该已经猜到，`orderby` 子句只是需要一个产生键值的表达式来排序。任何表达式都可以，从荒诞到有用的：

```
// 并不特别有用，但常量也是表达式。注意这并不能保证按输入顺序返回产品！
var orderByConstant = from product in products
    orderby 1
    select product;

// 从昂贵到便宜需要降序排序。
var decreasingPrice = from product in products
    orderby product.Price descending
    select product;

// 调用方法，并使用对捕获的局部变量的闭包。
DateTime from = DateTime.Now - TimeSpan.FromDays(100);
var topSellers = from p in products
    orderby p.GetNumberOfSalesSince(from) descending
    select p;
```

（表达式的）天空是极限。回想一下前面的查询表达式如何转换为带有 lambda 表达式参数的方法调用，你就能明白这种灵活性从何而来。例如：

```
// 调用方法，并使用对捕获的局部变量的闭包。
DateTime from = DateTime.Now - TimeSpan.FromDays(100);
var topSellers = products
    .OrderByDescending(p => p.GetNumberOfSalesSince(from));
```

图 19.20 说明了此查询的执行过程，从顶部的键选择开始。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_967_0.png)

图 19.20 排序的执行。

## 次要排序和 n 元排序

使用带有单个键选择器表达式的 `orderby` 子句只会创建主排序。通常，人们希望在此基础上建立次要排序和 n 元排序，如图 19.21 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_968_0.png)

图 19.21 建立次要排序和 n 元排序。

后续排序使用逗号分隔的键选择器列表来声明，如下所示：

```
var priceThenName = from product in products
    orderby product.Price, product.Name
    select product;
```

显然，每个键选择器都可以加上 `ascending`（可选关键字）或 `descending` 后缀（例如，按 Price 降序和按 Name 升序排序）。不过，上述写法与下面的写法并不相同：

```
var priceThenName = from product in products
    orderby product.Price
    orderby product.Name
    select product;
```

这会先按 Price 排序，建立主排序，然后再按 Name 排序，重新建立主排序。这在语义上等同于（忽略运行键选择器表达式 `product.Price` 可能产生的副作用）：

```
var priceThenName = from product in products
    orderby product.Name
    select product;
```

`orderby` 子句中逗号分隔的键选择器被翻译成使用单独的方法：主要的（也可能是唯一的）排序会生成 `OrderBy` 或 `OrderByDescending` 调用，而 n 元排序会追加 `ThenBy` 或 `ThenByDescending` 调用。例如，这里显示的 Name-then-Price 排序会变成以下等价代码：

```
var priceThenName = products
    .OrderBy(product => product.Price)
    .ThenBy(product => product.Name);
```

虽然 `OrderBy` 方法在 LINQ to Objects 中被定义为 `IEnumerable<T>` 接口上的扩展方法，但 `ThenBy` 不是。事实上，这里还有另一个类型在起作用，通过查看 `OrderBy` 的签名可以揭示这一点：

```
public static IOrderedEnumerable<TSource> OrderBy<TSource, TKey>(
    this IEnumerable<TSource> source, Func<TSource, TKey> keySelector);
```

`IOrderedEnumerable<T>` 不过是一个普通的 `IEnumerable<T>`，但其类型揭示了已经建立了主排序。该接口上的扩展方法用于建立次要排序和 n 元排序，通过 `ThenBy` 方法：

```
public static IOrderedEnumerable<TSource> ThenBy<TSource, TKey>(
    this IOrderedEnumerable<TSource> source, Func<TSource, TKey> keySelector);
```

一旦排序，就始终保持排序：`ThenBy` 从 `IOrderedEnumerable<T>` 开始，并返回一个 `IOrderedEnumerable<T>`，从而允许继续链接更多的 `ThenBy` 调用。图 19.22 将其表示为类型（节点）和方法（边）的状态机。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_969_0.png)

图 19.22. OrderBy 和 ThenBy 查询运算符。

## 查询模式

前面展示了具有一个或多个排序键选择器表达式的 `orderby` 子句的查询表达式转换。让我们像之前对 `select` 和 `where` 子句所做的那样将其形式化，如图 19.23 所示。同样，lambda 表达式用作被调用的查询运算符方法的参数。对于降序排序，使用带 `Descending` 后缀的对应方法。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_970_0.png)

图 19.23 orderby 子句的转换。

n 元排序的数量不受限制，只是会向方法调用链中添加更多的 `ThenBy` 调用。

## 自定义排序

排序的概念通过 `System.Collections.Generic` 命名空间中的 `IComparer<T>` 接口来形式化。在某些情况下，通过实现具有专门比较语义的 `IComparer<T>` 来覆盖默认排序行为是有意义的。

`OrderBy` 和 `ThenBy` 方法（及其降序变体）提供了接受 `IComparer<TKey>` 对象的重载，其中 `TKey` 表示用于键选择器表达式结果的键类型。

```
public static IOrderedEnumerable<TSource> OrderBy<TSource, TKey>(
    this IEnumerable<TSource> source, Func<TSource, TKey> keySelector,
    IComparer<TKey> comparer
);
```

这个重载没有查询表达式语法，因为它被认为主要用于专门用途，所以你必须使用方法调用语法来使用它。

## 查询语法 = 全有或全无？

有些人认为查询语法是全有或全无的。事实并非如此。例如：

```
from product in products.OrderBy(p => p.Price) select product.Name
(from p in products where p.IsInStock select p).OrderBy(p => p.Price)
```

查询表达式（由）仅仅是表达式（组成）。

