
实现这些操作符的任务留作练习，供你运用已掌握的迭代器知识手动完成。你会发现查询操作符往往只有几行代码（忽略输入验证逻辑）。

## Take 和 TakeWhile

与“跳过”相反的是“取用”，即返回一个序列，其中的元素来自输入序列的开头，可以基于数量或条件。Take 只是取一定数量的元素来产出，而 TakeWhile 表示“只要条件成立就产出”。示例如下：

```
var res1 = Enumerable.Range(0, 10).Take(5); // { 0, 1, 2, 3, 4 }
var res2 = Enumerable.Range(0, 10).TakeWhile(n => n < 8);
    // { 0, 1, 2, 3, 4, 5, 6, 7 }
```

请注意某些不变性质成立。我们在下面的示例中使用 Concat 和 SequenceEqual 操作符来演示这些性质，它们应该很容易理解。这两个方法每次都应返回 true：

```
bool AssertSkipTake<T>(IEnumerable<T> source, int n) {
    return source.SequenceEqual(source.Take(n).Concat(
        source.Skip(n)));
}
```

```
bool AssertSkipTakeWhile<T>(IEnumerable<T> source, Func<T, bool> predicate) {
    return source.SequenceEqual(source.TakeWhile(predicate).Concat(
        source.SkipWhile(predicate)));
}
```

## 使用 SKIP 和 TAKE 进行分页

Skip 和 Take 的组合对于数据源分页很有用（例如，每次显示十个元素）：

```
// For example, page 3 = Skip(30).Take(10)
var onePageOfData = source.Skip(page * pageSize).Take(pageSize);
```

这说明了将不同查询操作符组合起来的能力。

## First 和 FirstOrDefault

有些限制性很强的限制操作符只返回单个元素。First 就是其中之一，返回序列的第一个元素。如果不存在任何元素，它会抛出 InvalidOperationException。如果输入序列为空，你可以使用 FirstOrDefault 操作符返回该序列元素类型的默认值：

```
int first = new [] { 42, 24, 12, 123 }.First(); // 42
int zero  = new int[0].FirstOrDefault();
```

还存在基于谓词的重载，用于检索序列中符合特定条件的第一个元素。如果找不到这样的元素，就会产生 InvalidOperationException，这同样可以通过使用 FirstOrDefault 来缓解：

```
int first = new [] { 42, 24, 12, 123 }.First(n => n < 30); // 24
int zero = new [] { 42, 24, 12, 123 }.FirstOrDefault(n => n > 999);
```

这些方便的重载常被初学 LINQ 的用户忽视，导致他们使用 Where 和 First 的组合来实现类似结果。

## Last 和 LastOrDefault

Last 和 LastOrDefault 查询操作符与 First 和 FirstOrDefault 完全类似。它们不是取第一个元素（可能基于谓词，或具有默认值回退行为），而是取最后一个元素：

```
int last = new [] { 42, 24, 12, 123 }.Last(); // 123
int zero = new int[0].LastOrDefault();
```

使用谓词时，会针对序列中的每个元素对该谓词求值，同时记住最后一个使谓词求值为 true 的元素：

```
int last = new [] { 42, 24, 12, 123 }.Last(n => n < 30); // 12
int zero = new [] { 42, 24, 12, 123 }.LastOrDefault(n => n > 999);
```

请注意，无限序列会使 Last（以及各种其他查询操作符）永远卡住。幸运的是，在 .NET 世界中无限序列的使用相当少见，尽管迭代器使创建此类序列成为可能。如果你在某个时候依赖无限迭代器，只需当心这类病态情况。

## Single 和 SingleOrDefault

在某些情况下，你期望序列中只有一个元素，或只有一个元素符合特定条件。此时，Single 操作符就很有用。与 First 和 Last 不同，当没有元素或有多个元素时，它会抛出 InvalidOperationException。同样，可以使用带 OrDefault 的变体来覆盖抛出异常的行为：

```
int oneAndOnly = new [] { 42 }.Single(); // 42
int zero = new [] { 1, 2, 3 }.SingleOrDefault(); // More than one element
```

基于对 First 和 Last 的讨论，带谓词函数的重载不言自明。

## ElementAt 和 ElementAtOrDefault

IEnumerable<T> 和 IEnumerator<T> 接口缺少基于索引的访问，尽管它们的顺序特性显然允许此类检索操作。ElementAt 提供了这种能力；如果指定的索引无效，则会抛出 ArgumentOutOfRangeException。带 OrDefault 后缀的变体再次允许以不抛异常的方式处理：

```
var two = new [] { "Zero", "One", "Two", "Three" }.ElementAt(2);
```

## 谨慎使用 ORDEFAULT 操作符

如果你预期存在第一个或最后一个元素、序列只包含一个元素，或特定索引有效，就不要使用 OrDefault 变体。无谓地使用不抛异常的操作符，很容易掩盖代码中的 bug，而这些 bug 往往会揭示无效的假设。SingleOrDefault 尤其危险，因为它不仅会掩盖序列为空的情况，还会掩盖序列包含的元素比预期更多的情况。

## OfType

给定一个异构的对象集合，你有时希望按类型筛选，就像这里显示的查询：

```
// { 42, 123 }
var src = new object[] { 42, "Bart", DateTime.Now, 123 };
IEnumerable<object> res = src.Where(o => o is int);
```

虽然前面的查询可以正常工作，但它的缺点是不会对所有通过类型检查的元素执行强制转换。我们更希望有一种方式，能取回所有按整数类型返回的整数值：

```
// { 42, 123 }
IEnumerable<int> res = src.Where(o => o is int).Select(o => (int)o);
```

OfType 操作符以更简洁的方式实现这一点：将目标类型指定为方法调用的泛型参数：

```
static IEnumerable<T> OfType<T>(this IEnumerable source);
```

请注意，此操作符的输入使用非泛型 IEnumerable（例如，用于 ArrayList）。但每个 IEnumerable<T> 也是非泛型 IEnumerable，因此该操作符也可用于基于子类型进行筛选：

```
var res = new Animal[] { elephant, ant, giraffe }.OfType<Mammal>();
```

事实上，OfType 操作符并不只是限制操作符；它还通过应用强制转换来转换输入序列中的对象。因此，我们把它作为限制类别的最后一个操作符来介绍，紧邻投影操作符。

## 投影

投影操作符用于将序列中的对象转换为输出序列中的对应对象。它们保留源序列的元素数量，同时转换每个元素，可能实现垂直分区。数据库世界中的典型示例是选择列的子集。

## Select

基本的投影操作符是 Select，它通过我们之前见过的 select 子句在 C# 语言中体现。它有两个重载，其中一个为选择器委托额外接收一个整数参数，表示元素在序列中的索引。请注意，转换特性通过两个泛型参数的存在体现出来（一个表示输入序列元素的类型，一个表示输出序列元素的类型）：

```
static IEnumerable<R> Select<T,R>(this IEnumerable<T> source,
Func<T, R> selector);
static IEnumerable<R> Select<T,R>(this IEnumerable<T> source,
Func<T, int, R> selector);
```

虽然 Select 方法可以转换输入对象的类型，但显然这不是必需的用法。例如：

```
IEnumerable<int> twice = Enumerable.Range(0, 10).Select(n => n * 2);
IEnumerable<string> s = Enumerable.Range(0, 10).Select(n => n.ToString());
```

注意，泛型类型参数是如何从用作选择器函数的 lambda 表达式中推断出来的。虽然这在大多数时候只是一种便利，但在使用匿名类型时，它就成为必需。

最后，是一个使用提供索引的重载来创建带编号项目列表的示例：

```
// { "0 is Zero", "1 is One", "2 is Two", "3 is Three" }
IEnumerable<string> numbers = new [] { "Zero", "One", "Two", "Three" }
    .Select((s, i) => i + " is " + s);
```

## Cast

Cast 操作符与我们之前看到的 OfType 操作符相当相似。它以类似方式转换输入元素，但不会丢弃与指定目标类型不兼容的元素。如果在枚举过程中遇到这样的元素，它会改为抛出 InvalidCastException：

```
foreach (int x in new object[] { 1, "2", 3 }) {
    // Will blow up on the second iteration.
}
```
