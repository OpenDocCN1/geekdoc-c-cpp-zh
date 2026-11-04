
你可以将 Cast 与典型的 C# 强制转换语法进行类比，其中 OfType 更接近 C# 的 as 关键字与 null 检查的结合。

该运算符像 OfType 一样，为源定义在非泛型 IEnumerable 类型上，因此提供了一种让旧的非泛型集合类型具备 LINQ 能力的方法。当查询表达式的范围变量显式指定了类型时，对 Cast 的调用会被省略：

```
from int x in new ArrayList { 1, 2, 3 } ...
```

前面的写法会变成下面这样：

```
from x in new ArrayList { 1, 2, 3 }.Cast<int>() ...
```

## SelectMany

LINQ 中最重要的运算符大概就是 SelectMany。但为什么呢？回答这个问题有两种方式：一种走单子的理论路线，另一种走查询的实践路线。我们先从后者开始，等对运算符的作用有了扎实理解后，再回到前者。

SelectMany 是 LINQ 中存在的核心“胶水”之一，因为它允许组合跨多个数据源的查询。事实上，下面这个带有多个 from 子句的查询表达式会转换为对 SelectMany 运算符的使用：

```
from product in northwind.Products
from supplier in product.Suppliers
select new { product.Name, supplier.City }
```

这里我们做的是：为正在查询的数据库中定义的每个产品，选出与之对应的所有供应商。仔细看，你可以认出两个交织在一起的查询：一个获取产品，另一个为每个已检索到的产品获取供应商。这大致对应于两个嵌套的 foreach 循环，不过查询可以整体远程执行，而且如你现在所知，它是惰性执行的。

要看清 SelectMany 在哪里登场，你可以通过 .NET Reflector（或者直接阅读 C# 语言规范）验证前面的形式会转换为以下内容：

```
northwind.Products.SelectMany(
    product => product.Suppliers,
    (product, supplier) => new { product.Name, supplier.City }
)
```

这里使用的 SelectMany 重载如下：

```
static IEnumerable<R> SelectMany<T,C,R>(
    this IEnumerable<T> source,
    Func<T, IEnumerable<C>> collectionSelector,
    Func<T, C, R> resultSelector);
```

这里存在三个泛型参数。一个表示源序列中使用的元素类型（T），另一个表示结果元素类型（R）。正中间，我们看到 C 表示中间元素类型。在前面的示例中，T 会被替换为某个 Product 类型，C 代表 Supplier 类型，R 代表投影后的结果类型（一个包含两个字符串的匿名类型，一个用于产品名称，一个用于供应商所在城市）。

还有其他重载可用，例如这里展示的这个：

```
static IEnumerable<R> SelectMany<T,R>(
    this IEnumerable<T> source,
    Func<T, IEnumerable<R>> resultSelector);
```

这个重载本质上会扁平化那些通过对源序列元素应用结果选择器而获得的序列。该运算符的定义使用迭代器，如下所示：

```
static IEnumerable<R> SelectMany<T,R>(this IEnumerable<T> source,
                                      Func<T, IEnumerable<R>> resultSelector)
{
    foreach (T item in source)
        foreach (R result in resultSelector(item))
            yield return result;
}
```

我们前面展示的那个重载，其 SelectMany 实现就留作你的练习。还存在另外两个重载，它们向选择器函数提供整数索引值，指示元素在序列中的位置，类似于 Where 和 Select 上找到的类似重载。

## 语言集成的单子与伪装下的 Bind

LINQ 基于单子（monads）的概念，这是一个来自范畴论的术语，由 Philip Wadler 在 Haskell 语境中引入函数式编程世界。因此，LINQ 并不只局限于查询操作，它可以用于任何类型的单子计算。

事实证明，SelectMany 具有单子 bind 操作的签名，从而允许组合单子计算。由于查询表达式的存在，这个神秘的单子 bind 被伪装在查询表达式中多个 from 子句的使用背后，但我们真正拥有的其实是语言集成的单子。

从更大的图景看，LINQ 实际上是一个作用于序列（这些序列位于本地内存中，或远程存在于某个数据存储中）的查询单子的实现。然而，还存在其他单子，它们并非由 BCL 直接提供，但可以通过为某些类型提供 SelectMany（以及其他运算符）的自定义实现来轻松定义。一个例子是用于可空值计算的假想单子，其中隐藏了检查 null 并传播这些 null 的计算方面，而不求值未使用的值：

```
from x in (int?)null
from y in (int)Console.ReadLine() // would never get called, because...
select x + y // ...SelectMany sees x is null and returns null immediately
```

另一个利用 LINQ 的单子实现是 .NET Framework 的反应式扩展，也称为 Rx 或 LINQ to Events。使用查询表达式这种漂亮的语法，你可以查询事件源提供的可观察数据。这里的单子计算所提供的是隐藏所有涉及并发以及协调挂钩和接收事件与数据的复杂性。更理论地说，Rx 是延续单子的实现。

## Zip

.NET 4 中引入的唯一新查询运算符是 Zip。它没有任何查询表达式语法表面（就像许多其他运算符也没有一样），但它在 LINQ 用户的工具箱中绝对占有一席之地。Zip 所做的是以逐元素配对的方式组合两个输入序列。给定两个序列（元素类型可能不同）以及一个用于组合对应位置元素的函数，它会生成一个输出序列，只要两个输入序列都还有剩余元素，输出序列就会继续产生元素。

图 20.8 以类似于衣物上所用机械装置的形状说明了 Zip 的操作，它把拉链两侧的齿组合起来。

到现在，你应该能够通过阅读像这里提供的文字定义，推断出查询运算符的签名。两个元素类型不同的序列、一个组合器函数以及一个结果序列，应该看起来像这样：

```
static IEnumerable<R> Zip<T1,T2,R>(
    this IEnumerable<T1> left,
    IEnumerable<T2> right,
    Func<T1, T2, R> resultSelector);
```

只要两个序列中有一个元素耗尽，结果序列也会终止，这类似于你夹克上不对称的拉链。此外，当其中一个输入抛出异常时，结果序列也会抛出异常，就像拉链上的一个坏齿破坏了拉链过程，让你受冻。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1030_0.png)

图 20.8 Zip 实际操作。

下面展示了一个在基元类型上使用 Zip 的示例：

```
Enumerable.Range(0, 26).Zip(
    from i in Enumerable.Range(0, 26) select (char)(i + 'a'),
    (n, c) => "The " + n + "th character of the Latin alphabet is " + c + "."
);
```

这里，n 会在左侧输入上取值（即第一行中 Range 运算符的输出），而 c 会在第二行中嵌入的查询表达式所提供的右侧输出上取值。

## 无查询表达式语法

许多标准查询运算符在 C# 和 Visual Basic 中没有对应的查询表达式语法。这样做通常是为了减少不必要的语言表面，避免语言因为较少使用的运算符而老化。Zip 是撰写本文时没有查询表达式语法的运算符之一，但思考它可能长什么样仍然很有趣，因为这会让人更深入地理解该运算符在类型层面的对称性。

暂且假设 C# 已经有了元组类型。元组是二元组、三元组等的推广，把一组值包装起来。元组的一种常用语法是把值放在圆括号之间，以逗号分隔，如下所示：

```
var person = ("Bart", 27);
```
