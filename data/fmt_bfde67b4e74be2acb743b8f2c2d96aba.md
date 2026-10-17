
调试器和跟踪工具无法提供足够的支持来单步多线程程序。想想在被多个线程使用的代码行上放置断点吧！有时，当某个线程到达该断点时，很难告诉调试器何时停止。

一旦你有了几年的并发编程经验，你可能避免一些常见的陷阱。遗憾的是，很多开发者并没有这种背景。

## 微软的方法

从顺序执行的应用程序向并行应用程序转型有许多方法。这些专门的编程语言、模式库、检查代码并重构代码的工具、并行感知编译器等。

微软有一种不同的基于“80/20原则”的方法。它自己的解决方案（称为并行计算平台 Parallel Computing Platform）提供了一种技术，有效解决了来自使用多个 CPU 核心带来的问题。它不是在线程模型中进行规范，也不是自动实现并行并向开发者隐藏，而是使用了一种声明式方法。它提供了一个简单的模型，允许开发者显式声明其程序的某些部分可以并行执行。平台负责实现。

并行计算平台建立在以下简单的设计目标之上：

- 开发者应该从并行编码任务的复杂性中解放，专注于解决业务问题，从而提高生产力。
- 创建工作正常、可维护且可扩展的并行应用程序的过程必须大大简化。
- 必须考虑到原生代码和托管代码开发者的预期。

这是该方法的三个主要支柱（特性）：

- 高级并行编程概念和抽象允许以对现有代码极微的更改来利用并行编程的价值。
- 该方法降低了开发者开始处理并行编程的门槛。
- 该方法提供了工具，在表达并行性的之外，还为开发者提供了极大的支持（调试、性能分析等）。

## 工具、编程模型、运行时

微软随 `.NET 4` 和 `Visual Studio 2010` 一发了其并行计算平台的基础元素。图 10-10 显示了这些元素的堆栈。

### 托管代码栈

| 集成工具 | | 编程模型 | | 原生代码栈 |
|---|---|---|---|---|---|
| | 并行调试器窗口 | `PLINQ` | 协调数据结构 | 并行模式库 | 代理库 |
| | | 任务并行库 (`TPL`) | | | |
| 性能分析器并发分析 | 并发运行时 | | | 任务调度器 |
| | | 线程池 (`ThreadPool`) | | | |
| `HPC MPI` 调试器 | | 任务调度器 | | 资源管理器 | |
| | | | 资源管理器 | | |

**图 10-10：并行计算平台运行时栈**

主要模块（由编程模型和并发运行时表示）随 `.NET Framework` 和 `Visual C++ 2010` 运行时一起发布，其中集成工具是 `Visual Studio 2010` 的一部分。如你所见，针对托管代码（图 10-10 的中间部分）和原生代码（图的右部分）有独立的（但非常相似的）栈。本讨论仅针对托管栈。

与开发者长期以来使用的基于线程的模型不同，新的编程模型是声明式的。开发者可以拆分算法并将代码分组为较小的任务，并声明它们之间的控制流。例如，他们可以声明某些任务并发运行，而其他任务则应该按照正确、定义的顺序运行。根据定义的控制流执行任务是运行时的责任。线程管理、同步和异常恢复均由运行时完成。

以下是托管代码栈的关键组件：

- **`任务并行库 (TPL)`** — 这是通过其高级编程概念提供此类功能的运行时。
- **`并行集成查询 (PLINQ)`** — 它利用 `TPL` 实现数据并行。标准的 `LINQ` 表达式可以很容易地标记为并发执行（甚至可以设置并行度），因此可以在不知道任何线程或 `TPL` 概念的情况下以多线程方式处理数据。
- **`并发运行时`** — 它负责将使用任务的概念转换为线程。它使用 `ThreadPool` 作为其基本工具来管理 `.NET Framework` 级别和操作系统级别的线程。
- **`任务调度器`** — 拥有成千上万可以同时运行的任务并不意味着将启动成千上万个线程。任务调度器负责将任务分配给线程，并考虑可以实现的并行度。
- **`协调数据结构`** — 这包括高性能的无锁且线程安全的集合类，还包括其他用于同步和延迟初始化的轻量级对象。

## 并行编程架构概述

虽然图 10-10 是并行计算平台元素的非常好的概述，但它并没有反映开发者的意图如何在并行执行中体现。图 10-11 提供了架构的另一个视角，可以帮助你理解特定元素的作用。

![](img/b5597c749e848b27b0d305153ae16106_461_0.png)

图 10-11：并行编程架构

使用 `.NET 4 Framework` 开发的应用可能包含你打算以运行运行的代码部分。你可以编写 `PLINQ` 查询，这些查询是扩展的表达式声明，带有微小的指令以标记其并行执行。此外，你还可以编写命令式算法，显式地声明可以并发运行的部分（称为任务）。

归根底，并行构造结构由 `TPL` 执行，`TPL` 提供了构造结构和任务调度。协调数据结构为你的提供了某些类型（如 `ConcurrentBag`、`ConcurrentQueue`、`Barrier`、`CountdownEvent` 等），帮助你进行任务的资源管理和同步。

使用任何 `.NET` 编译器，生成的中间语言代码将目标指向 `TPL` 层（命令式算法）或使用 `PLINQ` 执行引擎（声明式查询）。并行查询表达式在查询执行期间将使用 `TPL` 层。

## 并行 LINQ

`LINQ` 表达式非常适合将数据处理算法转换为声明式算法。它不再要求开发者使用标准编程语言指令以循环、过滤或结果聚合的形式编写算法，而是使用查询来定义开发者的意图。

`PLINQ` 是一项新技术，允许在具有更多 CPU 核心的机器上并发执行 `LINQ` 表达式。`PLINQ` 的主要目的是通过更有效地利用系统资源，实现内存数据查询执行的加速，特别是在多核硬件上。“加速”意味着查询的顺序执行与完全或部分并行模式执行之间的执行时间差异。在本章稍后的部分，你将了解到使用 `LINQ` 实际上简单。

10-11 显示了 `PLINQ` 如何增强标准 `LINQ` 表达式的执行。并行执行基于将原始数据分分区到多个任务中，以便它们能够以最小的锁定和其他协调开销并行运行。`.NET` 查询操作符实现在 `PLINQ` 引擎中，因此它们支持并行。在每个分区上执行查询后，部分结果应合并为最终的聚合结果。

### LoremIsumQuery 示例

`PLINQ` 在将顺序查询转换为并行查询方面表现出色。证明这一点的最佳方法是向你展示一个清晰指出 `LINQ` 相对于命令式编程优势的示例。当你从本书的网站（`www.vroc.com`）下载第 10 章的源代码时，你会发现一个名为 `LoremIsumQuery` 的示例，它在这里用于介绍 `PLINQ` 的优势。

`LoremIsumQuery` 是一个小型 `WPF` 应用，允许你查询文本中的单词。查询结果由一个 `IEnumerable<LI>` 表示，其中 `LIResult` 是由两个字段 `Book` 和 `WordCount` 组成的简单结构。图 10-12 显示了 " Ipsum " 的统计信息。

![](img/b5597c749e848b27b0d305153ae16106_462_0.png)

图 10-12：LoremsumQuery 截图

你可以通过遍历记录并使用 `Dictionary` 对象计算指定单词的出现次数来编写查询。列表 10-9 显示了其中一种实现方法。这种并行算法的基本思想是根据机器上的 CPU 核心数来划分工作。

### 列表 10-7：手动查询定义

```csharp
private IEnumerable<LIResult> ManualQuery(string wordToSearch)
{
    var result = new Dictionary<int, LIResult>();
    foreach (var record in LIRecords)
    {
        if (String.Compare(record.Word, wordToSearch, true) == 0)
        {
            LIResult book;
            if (result.TryGetValue(record.Book, out book))
                book.WordCount++;
            else
                result.Add(record.Book, new LIResult(record.Book, 1));
        }
    }
    return result.Values;
}
```

`LINQ` 方案很好，但它是顺序的，并且只使用一个 CPU 核心。让我们暂时忘记你有 `PLINQ`。列表 10-7 中的手动查询可以使用 `.NET` 内置的线程架构转换为多线程查询。

使用 `LINQ` 的实现更加直观，并能立即告知查询的意图。

### 列表 10-8：使用 LINQ 定义查询

```csharp
private IEnumerable<LIResult> UsingLINQ(string wordToSearch)
{
    return from record in LIRecords
        where String.Compare(record.Word, wordToSearch, true) == 0
        group record by record.Book.Key
        select new LIResult(book.Key, book.Count());
}
```

每个线程从数据库中获取一条记录，并在线程内部本地处理该部分结果。当一个线程完成其工作（即没有更多记录需要处理）时，它会将部分结果合并到聚合后的结果中。

![](img/b5597c749e848b27b0d305153ae16106_464_0.png)

### 列表 10-9：手动实现的并行查询

```csharp
private IEnumerable<LIResult> ManualParallelQuery(string wordToSearch)
{
    var result = new Dictionary<int, LIResult>();
    int partitionsCount = Environment.ProcessorCount;
    int remainingCount = partitionsCount;
    IEnumerable<LIRecord> enumerator = LIRecords.GetEnumerator();
    // enumerator 的资源块
    try {
        // 分区同步
        using (var done = new ManualResetEvent(false))
            // 每个分区都有自己的线程
            for (int i = 0; i < partitionsCount; i++)
            ThreadPool.QueueUserItem((obj) => {
                var partialResult = new Dictionary<int, LIResult>();
                while (true)
                {
                    LIRecord record;
                    // 锁（低效）以访问下一个元素
                    lock (enumerator)
                    {
                        if (!enumerator.MoveNext()) break;
                        record = enumerator.Current;
                    }
                    if (String.Compare(record.Word, wordToSearch, true) == 0)
                    {
                        LIResult book;
                        // 锁（低效）以聚合结果
                        lock (partialResult)
                        {
                            if (partialResult.TryGetValue(record.Book, out book))
                                book.WordCount++;
                            else
                                partialResult.Add(record.Book,
                                    new LIResult(record.Book, 1));
                        }
                    }
                }
                // 将部分结果合并到聚合结果
                lock (result)
```

### 列表 10-9（续）

```csharp
foreach (var item in partialResult.Values)
{
    LIResult book;
    if (result.TryGetValue(item.Book, out book))
        book.WordCount += item.WordCount;
    else
        result.Add(item.Book, item);
}
// 当最后一个分区完成后，标记工作完成
if (Interlocked.Decrement(ref remainingCount) == 0) done.Set();
});
// 等待分区完成其工作
done.WaitOne();
}
finally{
    enumerator.Dispose();
}
return result.Values;
```

代码文件 [`MainWindow.xaml.cs`] 可在 `Wrox.com` 下载。

你首先注意到的是这段代码非常复杂，尽管有注释，但理解它并不容易。代码中只有一小部分处理实际的计算逻辑。所有其他部分都用于同步线程和协调资源访问。

使用 `PLINQ`，这种编码噩梦就像 `LINQ` 实现一样简单。列表 10-10 显示了这些代码，它消除了手动并行查询实现中的所有痛点。

### 列表 10-10：使用 PLINQ 的查询定义

```csharp
private IEnumerable<LIResult> UsingParallelLinq(string wordToSearch)
{
    return from record in LIRecords.AsParallel()
        where String.Compare(record.Word, wordToSearch, true) == 0
        group record by record.Book into book
        select new LIResult(book.Key, book.Count());
}
```

代码文件 [`MainWindow.xaml.cs`] 可在 `Wrox.com` 下载。

此查询定义与列表 10-8 中的 `PLINQ` 解决方案几乎相同。唯一的区别在于 `AsParallel()` 方法，它告诉对 `LIRecord` 的操作是并行的。`AsParallel()` 方法指示操作可以在多核心上执行。`PLINQ` 这种方式将查询拆分为多个块，并合并结果。

## 比较查询实现方式

表 10 显示了不同实现方式的执行时间和性能百分比。

**表 10 显示：**

| 查询实现类型 | 执行时间 (MS) | 性能 |
| --- | --- | --- |
| 命令行式查询 | 386 | 100% |
| 使用 PLINQ 的声明 | 780 | 97% |
| 命令行式查询 | 125 | 57% |
| 使用 PLINQ 的声明 | 271 | 340% |

这表明 `PLINQ` 在某些情况下可能比手动实现更慢，但在另一些情况下则快得多。`PLINQ` 具有更好的执行策略。

## 影响 PLINQ 行为

`AsParallel()` 方法将顺序查询转换为并行查询，返回一个 `ParallelQuery<TSource>` 对象。有几个带有 `With` 前缀的扩展方法可以影响并行查询的执行方式。表 10-2 描述了这些方法。

### 表 10-2：影响 PLINQ 行为的扩展方法

| 方法 | 描述 |
| --- | --- |
| `WithDegreeOfParallelism` | 设置查询的并行度。*并行度*是用于处理查询的最大并发任务数。该方法接受一个整数参数来设置该值。截至本文，尚未文档当该值大于 CPU 核心数时查询如何工作。 |
| `WithExecutionMode` | 设置查询的执行模式。该方法接受一个 `ParallelExecutionMode` 枚举参数，具有两个值：<br>`Default` —— 默认，系统将使用适用于并行的算法，并避免可能导致并行执行变慢的算法。<br>`ForceParallel` —— 强制并行化整个查询，即使这意味着高开销算法。`PLINQ` 设计用于利用并行机会。然而，并非所有查询都能受益于并行执行。例如，当查询包含一个工作极少的用户委托时，查询的顺序执行速度更快。这是因为并行化执行的开销大于获得的加速效果。 |
