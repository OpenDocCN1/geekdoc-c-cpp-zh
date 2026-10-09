

TeamName: "Italy",
IEnumerable<string> players =
worldCup2006Finalists.SelectMany(
team => team.Players);
Print(players);
// ...

此列表的输出会在单独的行中按代码中出现的顺序显示每个球员的名字。Select() 和 SelectMany() 之间的区别在于，Select() 将返回两个项，分别对应原始集合中的每个项。Select() 可能会从原始类型中投影出转换，但项的数量不会改变。例如，teams.Select(team => team.Players) 将返回一个 IEnumerable<string[]>。

相比之下，SelectMany() 会遍历由 lambda 表达式标识的每个项（即之前由 Select() 选择的数组），并将每个子集合中的项提升到一个包含所有子集合中项的并集的新集合中。SelectMany() 不是选择两个球员数组，而是结合每个选定的数组，生成包含所有项的单个集合。

## 更多标准查询运算符

列表 15.25 展示了使用由 Enumerable 启用的某些简单 API 的代码；输出 15.12 显示了结果。

### 列表 15.25：更多 System.Linq.Enumerable 方法调用

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

class Program
{
    static void Main()
    {
        IEnumerable<object> stuff =
            new object[] { new object(), 1, 3, 5, 7, 9,
                "\"thing\"", Guid.NewGuid() };
        Print("Stuff: {0}", stuff);
        IEnumerable<int> even = new int[] { 0, 2, 4, 6, 8 };
        Print("Even integers: {0}", even);

        IEnumerable<int> odd = stuff.OfType<int>();
        Print("Odd integers: {0}", odd);

        IEnumerable<int> numbers = even.Union(odd);
        Print("Union of odd and even: {0}", numbers);

        Print("Union with even: {0}", numbers.Union(even));
        Print("Concat with odd: {0}", numbers.Concat(odd));
        Print("Intersection with even: {0}",
            numbers.Intersect(even));
        Print("Distinct: {0}", numbers.Concat(odd).Distinct());
        if (!numbers.SequenceEqual(
                numbers.Concat(odd).Distinct()))
        {
            throw new Exception("Unexpectedly unequal");
        }
        else
        {
            Console.WriteLine(
                @"Collection ""SequenceEquals""" +
                $" {nameof(numbers)}.Concat(odd).Distinct()"
            );
        }
        Print("Reverse: {0}", numbers.Reverse());
        Print("Average: {0}", numbers.Average());
        Print("Sum: {0}", numbers.Sum());
        Print("Max: {0}", numbers.Max());
        Print("Min: {0}", numbers.Min());
    }

    private static void Print<T>(
        string format, IEnumerable<T> items) =>
        Console.WriteLine(format, string.Join(
            ", ", items.Select(x => x.ToString())));

    private static void Print<T>(string format, T item)
    {
        Console.WriteLine(format, item);
    }
}
```

### 输出 15.12

```
Stuff: System.Object, 1, 3, 5, 7, 9, "thing"
24c24a41-ee05-41b9-958e-50dd12e3981e
Even integers: 0, 2, 4, 6, 8
Odd integers: 1, 3, 5, 7, 9
Union of odd and even: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9
Union with even: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9
Concat with odd: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9, 1, 3, 5, 7, 9
Intersection with even: 0, 2, 4, 6, 8
Distinct: 0, 2, 4, 6, 8, 1, 3, 5, 7, 9
Collection "SequenceEquals" numbers. Concat(odd). Distinct()
Reverse: 9, 7, 5, 3, 1, 8, 6, 4, 2, 0
Average: 4.5
Sum: 45
Max: 9
Min: 0
```

列表 15.25 中的 API 调用均不需要 lambda 表达式。表 15.1 和 15.2 描述了每种方法并提供了一个示例。System.Linq.Enumerable 包含一组聚合函数，它们枚举集合并计算结果（如表 15.2 所示）。Count 是本章中已经展示的一个聚合函数的例子。

### 表 15.1：更简单的标准查询运算符

| 注释类型 | 描述 |
| :--- | :--- |
| OfType<T>() | 对集合形成一个查询，该查询仅返回特定类型的项，其中类型在 OfType<T>() 方法调用的类型参数中指定。 |
| Union() | 组合两个集合以形成两个集合中所有项的超集。即使最初两个集合中存在相同的项，最终集合也不包含重复项。 |
| Concat() | 组合两个集合以形成两个集合的超集。结果集合中不删除重复项。Concat() 将保留顺序。也就是说，将 {A, B} 与 {C, D} 连接将产生 {A, B, C, D}。 |
| Intersect() | 提取存在于两个原始集合中的项的集合。 |
| Distinct() | 从集合中过滤出重复项，使得结果集合中的每个项都是唯一的。 |
| SequenceEquals() | 比较两个集合，并返回一个布尔值，指示集合是否相同，包括集合内项的顺序。（这在测试预期结果时非常有帮助。） |
| Reverse() | 反转集合内的项，使得在遍历集合时它们以相反顺序出现。 |

### 表 15.2：System.Linq.Enumerable 上的聚合函数

| 注释类型 | 描述 |
| :--- | :--- |
| Count() | 提供集合中项数的总计数 |
| Average() | 计算数字键选择器的平均值 |
| Sum() | 计算数字集合内的总和值 |
| Max() | 确定一组数字值中的最大值 |
| Min() | 确定一组数字值中的最小值 |

请注意，表 15.1 和 15.2 中列出的每个方法都将触发延迟执行。

## 高级主题

## IQueryable<T> 的可查询扩展

IQueryable<T> 是 IEnumerable<T> 的一个几乎完全相同的接口。由于 IQueryable<T> 继承自 IEnumerable<T>，它拥有 IEnumerable<> 的所有成员，但仅指直接声明的成员（例如 GetEnumerator()）。扩展方法不被继承，因此 IQueryable<> 没有任何 Enumerable 扩展方法。然而，它有一个类似的扩展类，称为 System.Linq.Queryable，该类为 IQueryable<> 添加了与 Enumerable 为 IEnumerable<> 添加的几乎相同的方法。因此，它提供了非常相似的编程接口。

使 IQueryable<> 独特的地方在于它支持自定义 LINQ 提供程序。LINQ 提供程序将表达式分解为其组成部分。分解后，表达式可以被翻译成另一种语言、序列化以用于远程执行、注入异步执行模式等。本质上，LINQ 提供程序允许对标准集合 API 进行拦截机制，并借此看似无限的功能，可以注入与查询和集合相关的行为。

例如，LINQ 提供程序允许将查询表达式从 C# 翻译成 SQL，然后在远程数据库上执行。通过这种方式，C# 程序员可以保持在她的主要面向对象语言中，并将到 SQL 的翻译留给底层的 LINQ 提供程序。通过这种类型的表达式，编程语言可以跨越面向对象世界和关系数据库之间的阻抗失配。

在 IQueryable<> 的情况下，关于延迟执行的警惕性甚至更加关键。例如，想象一个从数据库返回数据的 LINQ 提供程序。无论选择标准如何，lambda 表达式都会提供 IQueryable<> 的实现，可能包括上下文信息（如连接字符串），但不包括数据本身。数据检索不会发生，直到调用 GetEnumerator() 甚至 MoveNext()。然而，GetEnumerator() 调用通常是隐式的，例如在 foreach 遍历集合或调用 Count<>() 或 Cast<>() 等 Enumerable 方法时。显然，像这样的情况需要开发人员警惕延迟执行可能涉及的昂贵操作的微妙且重复的调用。例如，如果调用 GetEnumerator() 涉及通过网络对数据库进行分布式调用，明智的做法是避免对 Count() 或 foreach 进行意外的重复迭代调用。

