
```csharp
for (int i = 0; i < 1000; i++)
{
    if (shouldStop(i))
        break;
    // Do work otherwise.
}
```

这里使用 break 语句根据某个条件退出循环，该条件可以（但并非必须）依赖于循环迭代变量。break 语句的工作方式是发出分支指令，跳转到整个 for 循环之外。不过，这种控制流在 lambda 表达式内部不能以相同方式工作。虽然可以跳出此类函数内部包含的循环，但不能跳出 lambda 表达式，毕竟它不过是一个匿名方法。我们说，使用 break 语句无法进行非局部跳转。

为缓解这一问题，引入了 ParallelLoopState 类。它用于从循环内部传达已请求停止循环：

```csharp
Parallel.For(0, 1000, (i, state) =>
{
    if (shouldStop(i))
    {
        state.Break();
        return;
    }
    // Do work otherwise.
});
```

通过调用 Break，Parallel.For 代码不再为超过当前请求中断点的迭代生成新任务。例如，如果 shouldStop 在第 10 次迭代中求值为 true，则调用 Break 将导致第 10 次之后的迭代不会被调度。话虽如此，由于并行执行的性质，超过当前迭代的迭代可能已经在执行中。这些迭代已无法阻止运行，因此中断是一种尽力而为的服务。

Break 确保的一个不变式是：在发出 Break 调用之前的所有迭代都会执行。在前面第 10 次迭代从循环中中断的示例中，这确保第 10 次之前的迭代会被调度并运行。这尽可能贴近 C# break 语句的行为：break 调用之前的所有迭代都可以执行，但超过该点的迭代会（在尽可能的范围内）被阻止运行。

停止并行循环的另一种方式是在 ParallelLoopState 对象上调用 Stop。与 Break 相比的唯一区别是，不保证当前迭代之前的工作会运行。在我们的示例中，在第 10 次迭代期间调用 Stop 并不保证前面的 9 次迭代会执行。

```csharp
static ParallelLoopResult For<TLocal>(int fromInclusive, int toExclusive,
    Func<TLocal> localInit,
    Func<int, ParallelLoopState, TLocal, TLocal> body,
    Action<TLocal> localFinally);
```

第一个函数参数名为 localInit，用于初始化线程局部状态。每次调用循环体都会接收循环变量、ParallelLoopState（上一节已解释）以及当前线程局部值。在这些重载中，循环体不再是 Action，而是变成了一个函数，它返回因该迭代执行而更新后的线程局部状态。最后一个参数会针对循环执行期间初始化的每个线程局部状态执行一次，用于在循环完成时聚合这些结果。

下面是一个示例，同样展示在 MSDN 上：

```csharp
var xs = Enumerable.Range(0, 1000000).ToArray();
long total = 0;

Parallel.For<long>(0, xs.Length,
    () => 0,
    (j, loop, subtotal) => {
        subtotal += xs[j];
        return subtotal;
    },
    subtotal => Interlocked.Add(ref total, subtotal)
);

Console.WriteLine("The total is {0}", total);
```

对于参与执行并行 for 循环的每个唯一工作线程，都会调用局部状态初始化函数（这里只是返回 0）。从此以后，初始化后的数据会存储在线程局部存储中，每当工作线程处理一个新迭代时，都会将其提供给循环体函数。随后，更新后的 subtotal 会从循环体返回，并再次存储到该工作线程的线程局部存储中。当所有工作线程完成该循环的所有工作后，会调用聚合函数，在那里我们以线程安全的方式将这些小计汇总为全局总计。

我建议执行图 30.10 所示的调试器实验。首先，你会看到对初始化函数的调用次数相对较少，大致与可用的处理器核心数（或指定的并行度）成正比。这是因为初始化对每个工作线程只发生一次，而工作线程不过是一个会在多个工作项之间重复使用的线程。

在所有循环体都在活动工作线程上执行完毕后，位于各工作线程线程局部状态中的小计将通过 finally 函数进行聚合，该函数会对每个工作线程调用一次。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1564_0.png)

图 30.10 观察带线程局部状态的并行循环期间的函数调用情况。

使用并行 for 循环的线程局部状态选项意味着你不必自行管理此类状态（否则很容易出错）。通常，当结果循环需要计算某种聚合值时，会使用此技术。

## AggregateException 再次来袭

很明显，并行循环构造的所有重载（以及“并行调用”一节中讨论的 Parallel.Invoke 方法）都可能抛出 AggregateException，该异常会收集由数据并行构造所生成并行任务上发生的所有异常。

## 并行 foreach 循环

正如 Parallel.For 方法类似于 C# for 循环，Parallel.ForEach 方法旨在对应 C# foreach 循环。给定一个可枚举序列，ForEach 方法允许针对给定序列中的每个元素并行执行循环体。

我们在讨论 For 时介绍的大多数概念也适用于 ForEach 情形，包括使用 ParallelLoopOptions、带有 Break 和 Stop 方法的 ParallelLoopState，以及 ParallelLoopResult。同样，线程局部状态可以与执行循环工作的工作线程相关联。

在下文中，我们将重点介绍为 Foreach 循环引入的、此类循环特有的附加概念。但首先，让我们考虑一个简单示例，展示如何将这一数据并行操作与最全面的重载之一一起使用：

```csharp
var xs = Enumerable.Range(0, 1000000);
long total = 0;

Parallel.ForEach(xs,
    () => 0L,
    (x, loop, subtotal) => {
        subtotal += x;
        return subtotal;
    },
    subtotal => Interlocked.Add(ref total, subtotal)
);

Console.WriteLine($"The total is {0}", total);
```

这里我们通过并行执行循环体来遍历该可枚举序列。同样，我们使用 long 类型的线程局部状态来计算序列元素总和的小计，这些小计会被聚合为最终总和。

## 分区器的作用

要并行地对序列元素运行操作，需要将序列划分为工作块。这就是分区器概念发挥作用的地方。它们在 PLINQ 实现中也起着至关重要的作用（参见第 20 章“并行 LINQ”一节）。

分区器的思想是让执行循环体的工作线程一次处理多个元素，而不仅仅是单个元素。例如，如果你有 100 个元素和四个核心，让每个核心负责 25 个元素的工作是合理的。这种常见的分区方案称为范围分区，其中必须预先知道输入序列的大小，以便为每个工作线程创建基于索引的范围。不过，这种方案有一个缺点：如果一个工作线程远在其他工作线程完成其那部分工作之前就完成了，那么空闲的工作线程无法窃取工作。

划分序列的另一种方式是块分区，即工作线程处理给定大小的块。这与范围分区的不同之处在于，工作的拆分不是静态地基于工作线程数量。例如，给定 100 个元素和块大小 5，我们得到 20 个工作单元。假设有四个核心，每个核心分配一个工作线程，那么它们平均各执行五个块。不过，这并不是将块静态分配给工作线程；如果一个工作线程拿到一个块，它可能比其他工作线程处理其块快得多，并且可以随时继续处理下一个块。总体而言，系统的吞吐量更高。负载均衡分区是使用动态基于块的分区的另一个名称。

你可以使用 Partitioner.Create 工厂方法创建分区器。一组重载基于 from 和 to 边界并结合范围大小，创建采用范围分区的分区器。其他重载可以接收数组或 IList<> 对象，其长度可立即得知。根据名为 loadBalance 的布尔标志，生成的分区器会使用范围分区或负载均衡块分区。

有关分区器的使用以及创建自定义分区器的更多信息，请参阅 MSDN 上关于该主题的文档。
