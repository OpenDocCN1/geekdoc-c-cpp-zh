
使用动态定义的匿名类型。同时，我们摆脱了那些不关心查询的属性。

有了这种新的数据形态，我们想开始基于它编写查询表达式。其中一种做法是使用中间查询表达式。例如：

```
var products2 = from product in products
                 select new { Name = product.ProductName,
                              Price = product.UnitPrice };
```

这里，products2 的类型是 IEnumerable<T>，其中 T 代表投影中使用的匿名类型。只要存在可枚举序列，就可以使用查询表达式：

```
var expensiveProducts = from product in products2
                         where product.Price > 100m
                         select product;
```

这里，范围标识符 product 引用 products2 中的对象，而这些对象是在第一个查询表达式中创建的匿名类型。编写 where 子句时，你可以在代码编辑器中清楚地看到这一点（如图 19.34 所示）。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_985_0.png)

图 19.34  链接查询表达式。

## 注意延迟求值

请记住，LINQ 查询采用延迟求值；一旦我们了解各种 LINQ 提供程序如何工作，这一点就会变得更加清楚。

在前面的示例中，products2 尚未求值：只有当有人开始枚举 products2 时，它的求值才会开始发生。在这个特定示例中，将是 expensiveProducts 查询“从” products2 中“拉取数据”，而 products2 又从 products 中拉取数据。因此，对 expensiveProducts 查询表达式进行枚举会导致 products2 求值。

这种查询表达式求值的级联效应起初可能令人意外，但对于 LINQ 的工作方式来说至关重要。如果不是这样，就需要大量中间存储，而且可能存储的是永远不会被请求的内容。举例来说，假设 products2 包含数千个对象，而 expensiveProducts 查询只保留其中几十个。如果 products2 作为中间查询结果持久化到内存中，就会毫无理由地浪费大量存储空间。

为了声明我们前面看到的查询而必须创建中间查询表达式，似乎没有必要。事实上，使用 into 子句可以简化：

```
var expensiveProducts = from product in products
                            select new { Name = product.ProductName,
                                         Price = product.UnitPrice } into product
                            where product.Price > 100m
                            select product;
```

图 19.35 展示了在代码编辑器中编写此查询表达式时的外观和体验，其中新的 product 标识符显然指向上游投影子句中创建的匿名类型对象。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_986_0.png)

图 19.35  新的范围标识符引用 select 子句生成的对象。

这里，into 子句指定一个新的范围标识符，用于表示其左侧序列中出现的对象。我们可以使用新的范围标识符，也可以像这里所做的那样重用现有标识符。就像你考虑该语言中其他任何地方的变量作用域一样：最内层的 product 标识符会隐藏外层的标识符，如图 19.36 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_986_1.png)

图 19.36  投影后使用 into。

毫不意外，into 子句基于嵌套查询表达式，就像我们通过引入自己的中间表达式手动完成一样。图 19.37 展示了使用 into 子句时编译器执行的转换。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_987_0.png)

图 19.37  into 子句的转换。

## 分组后的延续

分组通常只是更复杂数据分析任务的开始。例如，如果要求你按类别为产品创建销售统计，分组将是你的好帮手。同样，要按供应商计算产品的平均价格，分组是合乎逻辑的第一步。

一旦拥有可用分组的序列，就需要更进一步，对每个已创建的分组表达操作。为此，你希望像我们处理投影时那样继续查询。为了让给出的示例更有变化，这次我们考虑反射信息。虽然我们会在第 21 章“反射”中更详细地讨论反射，但本质很简单：使用反射，你可以在运行时获取关于类型的信息：

```
typeof(Enumerable).GetMethods()
```

前面的表达式返回一个 MethodInfo 对象数组，这些对象描述 Enumerable 类型上可用的方法，而该类型位于 System.Linq 中。正是在这里，所有 LINQ to Objects 查询运算符都被定义为方法，第 20 章将对此详细说明。数组是可枚举的，因此我们可以基于它们编写 LINQ 查询。

由于许多查询运算符方法都有重载，GetMethods 调用会返回名称相同但不同的 MethodInfo 对象，每个重载对应一个对象。例如，Where 方法会有多个条目，分别对应那些重载：

```
public static IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source, Func<TSource, bool> predicate);
public static IEnumerable<TSource> Where<TSource>(
    this IEnumerable<TSource> source, Func<TSource, int, bool> predicate);
```

我们会在更详细讨论查询运算符的提供时讨论第二个重载的含义，但简而言之，谓词的 int 参数表示输入序列中正在被筛选的对象的索引。

现在，我们想定义一个基于 LINQ to Objects 方法的查询，显示不同的方法名称以及它们各自的重载数量。显然，第一步是按名称对它们分组：

```
var query = from m in typeof(Enumerable).GetMethods()
            group m by m.Name;
```

如你所知，这会返回一个 IEnumerable<IGrouping<TKey, TValue>> 对象，其中泛型 TKey 类型参数将被替换为 string（因为我们按方法的 Name 属性分组），而 TSource 将对应 MethodInfo，即输入序列中对象的类型。

如果没有 into 子句，我们的顺利之旅到这里就结束了，因为我们没有标识符可以引用每个生成的分组对象。要输出重载数量，我们可以这样做：

```
var queryOperators = from m in typeof(Enumerable).GetMethods()
                      group m by m.Name;

foreach (var queryOperator in queryOperators) {
    int n = 0;
    foreach (var overload in queryOperator)
        n++;
    Console.WriteLine("{0} has {1} overload(s)", queryOperator.Key, n);
}
```

这就进入了一种相当命令式的编码风格，在查询表达式和 LINQ 的世界里显得不自然。计算序列中元素的数量是一种聚合运算符，查询运算符原生支持它，使我们能够如下简化上面的代码：

```
var queryOperators = from m in typeof(Enumerable).GetMethods()
                      group m by m.Name;

foreach (var queryOperator in queryOperators) {
    int n = queryOperator.Count();
    Console.WriteLine("{0} has {1} overload(s)", queryOperator.Key, n);
}
```

但我们还能做得更好。在查询表达式本身内部表达 Count() 运算符调用怎么样？为此，我们需要使用 into 继续现有查询：

```
var queryOperators = from m in typeof(Enumerable).GetMethods()
                      group m by m.Name into queryOperator
                      select new { Name = queryOperator.Key,
                                   Overloads = queryOperator.Count() };
```

```
foreach (var queryOperator in queryOperators) {
    Console.WriteLine("{0} has {1} overload(s)", queryOperator.Name,
        queryOperator.Overloads);
}
```

这里，新的 queryOperator 范围标识符表示分别为每个运算符方法创建的分组（即 IGrouping<string, MethodInfo> 对象）。随后，我们应用投影，将 IGrouping 的 Key 属性重命名为 Name，并使用通过属性 Overloads 暴露的 Count() 方法计算重载数量。图 19.38 从 IntelliSense 的视角展示了这样一个分组对象。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_989_0.png)

图 19.38  新的范围标识符表示分组对象。

Count() 方法定义为 IEnumerable<T> 上的扩展方法，它之所以可用于分组对象，是因为正如我们所见，每个 IGrouping<K, T> 对象都实现 IEnumerable<T>。这也允许在分组上任意嵌套查询表达式。

对分组对象执行的最常见操作之一是聚合，Count 只是其中一种。其他常用的聚合运算符包括 Min、Max、Sum 和 Average：

```
var categoryStats = from product in products
    group product by product.Category into category
    select new { Category = category.Key,
        AvgPrice = category.Average(p => p.Price) };
```

Average 聚合扩展方法接受一个 lambda 表达式，用于将源中的对象映射到要计算平均值的值。由于分组将某个类别映射到该类别中的产品，Average 会遍历每个分组中的所有产品，提取 Price 以计算平均值。因此，前面的查询会生成一个 IEnumerable<T>，其中 T 是匿名类型，包含类别以及该类别中所有产品的平均价格。其他聚合运算符的使用方式类似。

由于分组对象也是其包含元素上的序列，因此查询运算符也可以在分组内使用（例如，使用嵌套查询）：
