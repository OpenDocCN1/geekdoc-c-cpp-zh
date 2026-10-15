

```
' firstKey has the last key added to the ConcurrentStack
Else
' It wasn't possible to remove an element from the ConcurrentStack
End If
```

TryPop 也返回一个布尔值，表示操作是否成功。

## 将 LINQ 转换为 PLINQ

你已经了解到 LINQ 对于查询和处理不同的数据源非常有用。如果你使用的是 LINQ to Objects，现在就可以利用其并行实现 Parallel LINQ（PLINQ）来利用并行性。

> PLINQ 实现了完整的 LINQ 查询运算符集合，并添加了用于并行执行的新运算符。PLINQ 相比其 LINQ 对应版本可以实现显著的加速，但这始终取决于场景，如同并行编程一样。如果查询涉及可观数量的计算和内存密集型操作，并且顺序无关紧要，加速可能非常显著。然而，当顺序很重要时，加速可能会降低。

正如你可能预料的那样，LINQ 和 PLINQ 可以与前面解释的并发集合一起工作。以下代码定义了一个简单但计算密集的函数，用于计算并返回作为参数接收的字符串中的字母数量：

```
Function CountLetters(ByVal key As String) As Integer
    Dim letters As Integer = 0
    For i As Integer = 0 To key.Length() - 1
        If Char.IsLetter(key, i) Then letters += 1
    Next
    Return letters
End Function
```

来自 Snippet06 的代码片段

一个简单的 LINQ 表达式，用于返回所有至少包含 10 个字母、包含 A、F、9 且不包含 B 的 AES 密钥，其外观如下：

```
Dim keysWith10Letters = From key In Keys
    Where CountLetters(key) >= 10 And key.Contains("A")
    And key.Contains("F") And key.Contains("9") And Not
    key.Contains("B")
```

为了将上述 LINQ 表达式转换为可以利用并行的 PLINQ 表达式，需要使用 AsParallel 方法，如下所示：

```
Dim keysWith10Letters = From key In Keys.AsParallel()
    Where CountLetters(key) >= 10 And key.Contains("A")
    And key.Contains("F") And key.Contains("9") And Not
    key.Contains("B")
```

这样，查询将尝试利用运行时可用的所有逻辑核心，以比其顺序版本运行得更快。

可以在 Main 子程序末尾添加代码，根据 PLINQ 查询返回一些结果：

```
Dim sw = Stopwatch.StartNew()

Dim keysWith10Letters = From key In Keys.AsParallel()
    Where CountLetters(key) >= 10 And key.Contains("A")
And key.Contains("F") And key.Contains("9") And Not key.Contains("B")

Console.WriteLine("The code generated {} keys with at least ten letters, A, F and 9 but no B in the hexadecimal code.", keysWith10Letters.Count())
Console.WriteLine("First key (0): ", keysWith10Letters(0))
Console.WriteLine("Last key (0): ", keysWith10Letters(keysWith10Letters.Count() - 1))
Debug.WriteLine(sw.Elapsed.ToString())

Console.ReadLine()
```

来自 Snippet06 的代码片段

此代码显示了符合条件的密钥数量、第一个和最后一个，这些都存储在针对 ConcurrentQueue(Of String) 运行的 PLINQ 查询结果中。

## ParallelEnumerable 及其 AsParallel 方法

System.Linq.ParallelEnumerable 类负责公开 PLINQ 的大部分附加功能，包括其最重要的功能：AsParallel 方法。表 33-6 总结了 ParallelEnumerable 提供的 PLINQ 特定方法。

### 表 33-6：ParallelEnumerable 提供的 PLINQ 运算符

| VALUE | DESCRIPTION |
|---|---|
| AsOrdered() | PLINQ 必须为查询的其余部分保留源序列的顺序，直到使用 Order By 子句更改为止。 |
| AsParallel() | 查询的其余部分应尽可能并行化。 |
| AsSequential() | 查询的其余部分应按顺序运行，如传统 LINQ。 |
| AsUnordered() | PLINQ 不必保留源序列的顺序。 |
| ForAll() | 一种枚举方法，使结果能够使用多个任务并行处理 |
| WithCancellation | 启用使用取消令牌的工作，以允许取消查询执行，如前面用任务解释的那样 |
| WithDegreeOfParallelism | PLINQ 将被优化，就好像可用核心总数等于为此方法指定的并行度参数一样。 |
| WithExecutionMode | 这可以强制并行执行，而默认行为将是像传统 LINQ 一样按顺序运行。 |
| WithMergeOptions | 这可以提供有关 PLINQ 应如何将并行结果片段合并到正在消费查询的线程上的提示。 |

此外，AsParallel 提供了一个 Aggregate 重载，使能够实现并行归约算法。它允许在查询的每个并行部分上进行中间聚合，以及一个最终聚合函数，能够提供将所有生成分区的结果组合起来的逻辑。

有时运行 PLINQ 查询并使用许多不同的并行度来衡量其可扩展性是有用的。例如，以下行运行前面显示的 PLINQ 查询，以利用不超过三个核心：

```
Dim keysWith10Letters = From key In Keys.AsParallel().WithDegreeOfParallelism(3)
Where CountLetters(key) >= 10 And key.Contains("A") And
```

## AsOrdered 和 Order By

由于在 PLINQ 查询中使用 AsOrdered 和 Order By 子句可能会降低任何速度提升，因此在请求有序结果之前，非常重要的是将实现的加速与顺序版本进行比较。

如果 PLINQ 查询没有实现显著的性能改进，你还有另一个利用并行的有趣选项：以独立任务运行多个 LINQ 查询或使用 Parallel.Invoke。

## 使用 ForAll 和 ConcurrentBag 工作

ForAll 扩展方法非常有用，可用于并行处理查询结果，而无需编写并行循环。它接收一个操作作为参数，提供与 Task 构造函数接收的相同参数相同的可能性。因此，使用 lambda 表达式，你可以将来自 PLINQ 查询结果的并行化处理操作组合起来。以下行将元素并行添加到新的 ConcurrentBag（keysBag）中，ConcurrentBag 是一个无序的 Integer 集合，统计前一个 PLINQ 查询结果中每个密钥的字母数：

```
Dim keysWith10Letters = From key In Keys.AsParallel()
    Where CountLetters(key) >= 10 And key.Contains("A")
    And key.Contains("F") And key.Contains("9") And Not
    key.Contains("B")

Dim keysBag As New ConcurrentBag(Of Integer)
keysWith10Letters.ForAll(Sub(i) keysBag.Add(CountLetters(i)))
```

来自 Snippet07 的代码片段

> 这种并行处理是可能的，因为 ConcurrentBag 是并发集合之一，允许多个任务并行添加多个元素。

## 摘要

本章通过介绍其一些类、结构和枚举，对随 .NET Framework 4 引入的新基于任务的编程模型进行了概述。为了帮助你应对多核革命，它还解释了在基本并发和并行编程设计中使用的几个相关概念，包括以下要点：

- 你必须以并发和并行为目标进行规划和设计。TPL 提供了简化利用多核架构创建代码的过程的结构。
- 你无需重新编译代码即可利用额外的核心。TPL 使用根据运行时可用硬件资源进行负载平衡调度的底层线程优化并行循环和任务分配。
- 你可以并行化现有循环并衡量实现的性能提升。
- 你可以启动任务并结合迄今为止学到的关于列表和数组的一切来处理多个任务并管理其执行。
- 并发集合提供了一种在并行和并发任务中更新集合的方式，而无需担心复杂的同步机制。
- 你可以将 LINQ 查询转换为 PLINQ，以测试多核架构实现的加速。
- 与在 Visual Basic 和 .NET Framework 早期版本中编写的线程代码的向后兼容是可能的。

