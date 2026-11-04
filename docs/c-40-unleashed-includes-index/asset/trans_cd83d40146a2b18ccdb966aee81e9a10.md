
```
// If this would be here, there'd be an additional state.
yield return default(T);
}
```

最后，我们到达了状态 3，它应当对应于从尾部枚举器中检索下一个对象，并将它们暴露给迭代器的消费者。这是通过一条简单的分支（`goto`）指令从状态 2 跳转到循环内部来完成的：

```
bool MoveNext() {
    try {
        switch (_state) {
            case 0:
                ...
            case 1:
                _enum = _tail.GetEnumerator();
                while (_enum.MoveNext()) {
                    _current = _enum.Current; // yield return item;
                    _state = 3;
                    return true;                // we got an object in Current
Resume:
                }
                Finally();
                break;
            case 3:
                goto Resume;
        }
        return false;
    }
```

这会导致 while 循环重新求值 `_enum.MoveNext()`，并可能通过我们之前看到的相同逻辑生成下一个对象。如果该调用返回 false，我们会再次进入 `Finally()` 清理调用，并跳出 switch 语句，从而使迭代器向调用者返回 false。

总而言之，迭代器的内部并没有那么吓人，尽管编译器确实需要将迭代器块的代码拆解得相当零散。幸运的是，你不需要对此了解很多（甚至完全不需要），但感受一下实现迭代器所需的底层机制仍然很有意义，因为这清楚地展示了它们的执行模型。

你可以随意使用 .NET Reflector 更深入地研究生成的代码，请将其置于 .NET 2.0 反编译模式，以清楚地看到这些底层机制。还可以尝试对一个更复杂的迭代器进行逆向工程，比如包含更多 yield 语句、嵌套循环等。关键要点是：每个 yield 语句都需要从 `MoveNext` 方法返回，从而使迭代器挂起；要在正确的点恢复执行，迭代器对象中需要捕获足够的状态。图 20.7 展示了一个迭代器的内部结构，你可以清楚地看到一个 switch 跳转表，用来跟踪在 `MoveNext` 调用时需要执行的下一个操作。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1019_0.png)

图 20.7 一个被展开的迭代器。

## 标准查询运算符

LINQ 的核心优势之一在于，它将跨不同数据域（从内存中的对象到关系数据库）的查询运算符统一起来。为此，它不仅为 C# 和 Visual Basic 等主流语言提供了查询语法，还建立了一组常用的查询运算符。

在本节中，我们来看一下 .NET Framework 附带的所有标准查询运算符，包括一些不太常用但有用的重载。请记住，其中一些是通过语言集成查询语法公开的，而另一些则不是。对于后者，你可以直接使用方法调用语法来使用它们。

### 源生成器

源生成器是标准查询运算符的第一大类。尽管不同的源对象可以启用 LINQ（例如，通过实现 `IEnumerable<T>` 进行本地查询执行，或实现 `IQueryable<T>` 进行远程查询执行；例如 LINQ to SQL 中所使用的），但有时动态创建序列也是有意义的。

这里讨论的所有方法都位于 `Enumerable` 类型上，并且由于惰性求值，它们提供了一种无需在内存中持久化即可生成源的手段。显然，你也可以使用数组、列表或其他集合类型作为内存中数据源，但这些需要立即分配内存。

### Range

第一个源生成器叫做 `Range`，它从给定数字开始生成 `Int32` 值。其第二个参数用于指定向消费者生成多少个数字：

```
IEnumerable<int> firstTen = Enumerable.Range(0, 10); // { 0 .. 9 }
```

虽然它的用途看起来有限，但与其他查询运算符结合时，可以生成更有用的对象（例如字符）：

```
IEnumerable<char> aToz = Enumerable.Range(0, 26).Select(i => (char)('a' + i));
```

此外，对于简单的查询运算符探索，使用 `Range` 提供了一种简便的方法来创建用于实验的序列。

### Repeat

给定一个元素，有时需要重复它多次来创建一个具有恒定值的序列。这可以使用 `Repeat` 运算符来实现：

```
IEnumerable<string> heyHeyHey = Enumerable.Repeat("Hey", 3);
```

请注意，结果序列的类型是如何从指定给 `Repeat` 的第一个参数的元素推断出来的。

### Empty

在某些需要 `IEnumerable<T>` 的场景中，你可能想要传递一个默认序列。`Empty` 会生成一个不包含任何元素的静态类型序列：

```
IEnumerable<int> nothing = Enumerable.Empty<int>();
```

### Return

标准查询运算符集合中缺少的一个运算符是 `Return`，或称为 `Singleton`，它会返回一个包含单个指定元素的序列：

```
static IEnumerable<T> Return<T>(T element) {
    yield return element;
}
```

这很容易通过创建一个单元素数组来实现，正如我们所知，该数组实现了 `IEnumerable<T>`。这个运算符之所以有趣，是因为查询运算符的数学基础——称为单子（monads）——基于两个基本运算符：`Bind` 和 `Return`。后者刚刚已经展示，它在 LINQ 运算符中不存在，但前者实际上是存在的。它叫做 `SelectMany`，提供了一种组合序列的方法，你将在讨论该运算符的“投影”一节中看到。

### DefaultIfEmpty

`Empty` 在某种程度上扮演了空引用的角色，而 `DefaultIfEmpty` 则扮演了空合并运算符 `??` 的角色。如果交给此运算符的序列为空，它会生成一个单独的“默认”元素。这个默认元素既可以显式指定，也可以根据序列的元素类型推断：

```
var src1 = Enumerable.Empty<int>();
var res1 = src1.DefaultIfEmpty(); // { 0 }
var res2 = src1.DefaultIfEmpty(99); // { 99 }

var src2 = Enumerable.Range(1, 9);
var res3 = src2.DefaultIfEmpty(); // { 1 .. 9 }
```

这个运算符的用途相当有限，但了解一下仍然有好处。

### 限制

最常见的查询操作之一显然是基于某些条件过滤元素。这些条件既可以是逐元素级别的（如 `Where` 运算符），也可以具有更全局的性质（如 `Skip` 或 `Take`）。本质上，这里讲的是水平分区：将输入序列中的一定数量对象过滤得到一个子集。这些限制运算符不会改变数据形态，并保持输入序列的类型。

### Where

第一个限制运算符是我们已经熟悉的。`Where` 运算符对输入序列中的每个元素求值一个条件，只保留条件求值为 true 的对象。有两个重载：

```
static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, bool> predicate);
static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, int, bool> predicate);
```

从我们之前关于查询表达式语法和迭代器的讨论中，我们对第一个重载已相当熟悉。该运算符遍历 `source` 参数，将每个对象送入谓词函数。当该函数求值为 true 时，它将对象生成为输出序列。任何返回布尔值的表达式都可以，无论你让它多么复杂。为了举例说明，我们保持谓词函数简单：

```
// { "Bart", "Lisa" }
var res = new [] { "Bart", "Homer", "Lisa" }.Where(s => s.Length == 4);
```

第二个重载向谓词函数传入一个额外参数，代表元素在输入序列中的从零开始的索引。下面展示了一个示例用法，保留位于偶数位置的元素：

```
// { "Zero", "Two" }
var res = new [] { "Zero", "One", "Two", "Three" }.Where((s, i) => i % 2 == 0);
```

这里，`s` 代表输入序列中的字符串对象，而 `i` 代表对象在输入序列中的索引。我们在这里并没有使用 `s`（尽管我们显然可以使用）来进行基于索引的过滤。

### Distinct

序列可能包含重复对象，这可能是我们不希望的。为了去除这些重复项，可以使用 `Distinct` 运算符。由于这涉及对象之间的相等性检查，你可以预期会有两个重载（一个使用元素类型的默认比较器，另一个允许使用特定的相等比较器）：

```
static IEnumerable<T> Distinct<T>(this IEnumerable<T> source);
static IEnumerable<T> Distinct<T>(this IEnumerable<T> source,
    IEqualityComparer<T> comparer);
```

使用非常简单：

```
var nums = new [] { 5, 2, 1, 3, 1, 4, 5 }.Distinct(); // { 5, 2, 1, 3, 4 }
```

更为专用的重载的用法就留给你想象了。关于 `IEqualityComparer<T>` 的更多信息，请参阅第 16 章“集合类型”中关于集合类型的讨论。一个示例用法是为 `Person` 对象实现一个比较器，仅查看人的标识号来确定对象是否相等。然而，如果这就是 `Person` 对象的语义，那么你很可能已经有一个重写的 `Equals` 方法，默认的相等比较器会为 `Person` 类型使用它。

### Skip 和 SkipWhile

要从一个序列的开头跳过一定数量的元素，可以使用 `Skip` 运算符。它更通用的兄弟 `SkipWhile` 可以在给定条件成立时跳过元素。几个例子足以说明一切：

```
var res1 = Enumerable.Range(0, 10).Skip(5); // { 5, 6, 7, 8, 9 }
var res2 = Enumerable.Range(0, 10).SkipWhile(n => n < 8); // { 8, 9 }
```

如果跳过的数量大于输入序列的长度，或者谓词从未变为 false，则结果序列为空。注意 `SkipWhile` 显然不同于简单的 `Where`：

```
var res1 = new [] { 1, 2, 3, 4, 3, 2, 1 }.SkipWhile(n => n < 4); // { 4, 3, 2, 1 }
var res2 = new [] { 1, 2, 3, 4, 3, 2, 1 }.Where(n => n >= 4); // { 4 }
```

