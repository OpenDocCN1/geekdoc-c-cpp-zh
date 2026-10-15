
```vb
Sub ParallelGenerateAESKeysMaxDegree(ByVal maxDegree As Integer)
    Dim parallelOptions As New ParallelOptions()
    parallelOptions.MaxDegreeOfParallelism = maxDegree
    Dim sw = Stopwatch.StartNew()
    Parallel.For(1, NUM_AES_KEYS + 1, parallelOptions,
        Sub(i As Integer)
            Dim result() As Byte
            Dim hexString As String
            Dim aesM As New AesManaged()
            aesM.GenerateKey()
            result = aesM.Key
            hexString = ConvertToHexString(result)
            ' Console.WriteLine("AES:" + hexString)
        End Sub)
    Debug.WriteLine("AES: " + sw.Elapsed.ToString())
End Sub

Sub ParallelGenerateMD5HashesMaxDegree(ByVal maxDegree As Integer)
    Dim parallelOptions As New ParallelOptions
    parallelOptions.MaxDegreeOfParallelism = maxDegree
    Dim sw = Stopwatch.StartNew()
    Parallel.For(1, NUM_MD5_HASHES + 1, parallelOptions,
        Sub(i As Integer)
            Dim md5M As MD5 = MD5.Create()
            Dim result() As Byte
            Dim data() As Byte
            Dim hexString As String
            data = Encoding.Unicode.GetBytes(Environment.UserName + i.ToString())
            result = md5M.ComputeHash(data)
            hexString = ConvertToHexString(result)
            ' Console.WriteLine("MD5:" + hexString)
        End Sub)
    Debug.WriteLine("MD5: " + sw.Elapsed.ToString())
End Sub
```

> 使用静态值指定期望并行度并不方便，因为当有更多核心可用时，它会限制可扩展性。这些选项应谨慎使用；最好根据可用逻辑核心的数量使用相对值，或考虑该数量以便为代码的进一步可扩展性做好准备。

这样，可以使用考虑运行时逻辑核心数量的动态值调用这两个子例程：

```vb
ParallelGenerateAESKeysMaxDegree(Environment.ProcessorCount - 1)
ParallelGenerateMD5HashesMaxDegree(Environment.ProcessorCount - 1)
```

两个 `Parallel.For` 循环都将尝试使用逻辑核心数减 1 的数量工作。如果代码在四核微处理器上运行，则它将仅使用三个核心。

以下内容不是最终代码的最佳实践。然而，有时你想知道如果两个并行化的子例程同时执行，限制每个子例程的核心数是否能提供更好的性能。你可以使用以下行来测试这种情况：

```vb
Parallel.Invoke(Sub() ParallelGenerateAESKeysMaxDegree(2), Sub() ParallelGenerateAESKeysMaxDegree(2))
```

Code snippet from Listing12

两个子例程将并行启动，每个子例程都将尝试优化其执行以使用四核微处理器的四个核心中的两个。之前行的明显缺点是它使用了静态的核心数。尽管如此，这只是为了性能测试目的。

`ParallelOptions` 还提供了两个额外的属性来控制更高级的选项：

- `CancellationToken` — 允许分配新的 `System.Threading.CancellationToken` 实例以传播通知并行操作应被取消。该属性的使用将在本章后面详细介绍。
- `TaskScheduler` — 允许分配自定义的 `System.Threading.Tasks.TaskScheduler` 实例。除非你正在处理非常特定的算法，否则通常不需要定义自定义任务调度程序来调度并行任务。

### Understanding Hardware Threads and Logical Cores

`Environment.ProcessorCount` 属性提供逻辑核心的数量。然而，有时逻辑核心的数量，也称为硬件线程，与物理核心的数量不同。

例如，具有超线程技术的四物理核心的 Intel Core i7 微处理器会将数量翻倍至八个逻辑核心。因此，在这种情况下，`Environment.ProcessorCount` 为八，而不是四。操作系统也使用八个逻辑处理器。

使用 TPL 创建的所有代码都使用多个软件线程运行。线程是并行运行代码的多个部分的基础层级通道，利用底层硬件中多个核心的存在。然而，大多数时候，这些通道中运行的代码存在一些缺陷。它等待 I/O 数据或等待其他线程完成，或在等待数据从微处理器或系统内存中的不同缓存中获取时产生延迟。这意味着存在空闲的执行单元。

HyperThreading 技术通过为每个物理核心复制架构状态来提供更高程度的指令级并行，以减轻并行代码的缺陷，当第一个线程等待时从第二个线程运行代码。这样，它看起来就像一个具有两倍于实际物理核心数的微处理器。

> 逻辑核心与真实物理核心不同。虽然该技术有时通过增加指令级并行来提高性能，每个物理核心有两个具有独立指令流的线程，但如果软件线程没有太多数据依赖，性能提升可能低于预期。这取决于应用程序。

由于 TPL 使用硬件线程或逻辑核心的数量来优化其执行，有时某些算法在核心数量增加时不会提供预期的可扩展性，因为它们不是真正的物理核心。

例如，如果一个算法在八个物理核心上执行时提供了 6.5 倍的加速，那么在具有四个物理核心和八个逻辑核心的超线程微处理器上，它将提供更保守的 4.5 倍加速。

## CREATING AND MANAGING TASKS

TPL 引入了新的基于任务的编程模型，以将多核的强大功能转化为应用程序性能，而无需处理低级、更复杂且重量级的线程。非常重要的一点是，任务不是线程。任务使用线程运行。然而，这并不意味着它们取代了线程。事实上，之前示例中使用的所有并行循环都是通过创建任务运行的，并且它们的并行和并发执行由底层线程支持，如图 33-8 所示。

![](img/d99870e80390742f93963da7be0b2e61_1077_0.png)

FIGURE 33-8

当你使用任务时，它们使用底层线程运行其代码（软件线程，调度到某些硬件线程或逻辑核心上）。然而，任务与线程之间没有一对一的关系。这意味着你每次创建新任务时都不会创建一个新线程。CLR 创建必要的线程来支持任务的执行需求。当然，这是在创建任务时发生的事情的简化视图。

在多个线程中运行的代码同步确实很复杂。因此，基于任务的替代方案提供了一个很好的机会来摆脱一些同步问题，特别是关于工作调度机制的问题。CLR 使用工作窃取队列来减少锁并在不增加显著开销的情况下调度小块工作。创建新线程会引入很大的开销，但创建新任务会“窃取”现有线程的工作。因此，任务为能够利用多个核心的代码部分提供了一种新的轻量级机制。

默认任务调度程序依赖于底层的线程池引擎。因此，当你创建一个新任务时，它将使用窃取工作队列来找到最合适的线程来排队。它从现有线程窃取工作或在必要时创建新线程。任务中包含的代码将在一个线程中运行，但这发生在幕后，并且开销小于手动创建新线程。

### System.Threading.Tasks.Task

到目前为止，TPL 一直在幕后创建 `System.Threading.Tasks.Task` 的实例以支持迭代的并行执行。此外，调用 `Parallel.Invoke` 也会创建与调用的委托一样多的 `Task` 实例。

`Task` 表示异步操作。它提供了许多方法和属性，使你能够控制其执行并获取有关其状态的信息。`Task` 的创建与其执行是独立的。这意味着你完全控制关联操作的执行。`Task` 类提供以下属性：

> 当你启动许多异步操作作为 `Task` 实例时，任务调度程序将尝试并行运行它们，以便在运行时负载平衡所有可用的逻辑核心。然而，使用任务运行任何现有代码片段并不方便，因为任务会增加开销。有时使用任务没有意义。虽然这种开销小于线程的开销，但它仍然是一个需要考虑的开销。例如，为两个简单的计算创建任务来作为两个独立的异步任务运行是没有意义的。记住在并行执行和顺序版本之间测量加速，以决定并行是否合适。

表 33-2 解释了此示例中考虑的三种可能情况。

### TABLE 33-2: Task Read-only Properties

| PROPERTY | DESCRIPTION |
|---|---|
| AsyncState | 创建 `Task` 实例时提供的状态 `Object` |
| CreationOptions | 用于为任务调度程序提供提示以帮助其做出最佳调度决策的 `TaskCreationOptions` 枚举值 |
| CurrentId | 正在执行的 `Task` 的唯一 ID。它不等同于非托管代码中的线程 ID。 |
| Exception | 导致 `Task` 提前结束的 `AggregateException`。如果 `Task` 根本没有抛出异常或完成时未抛出异常，则为 null 值。 |
| 属性 | 说明 |
|---|---|
| `Factory` | 提供对工厂方法的访问，这些方法允许创建带结果和不带结果的 `Task` 实例 |
| `Id` | `Task` 实例的唯一 ID |
| `IsCanceled` | 一个布尔值，指示 `Task` 实例是否已被取消 |
| `IsCompleted` | 一个布尔值，指示 `Task` 是否已完成其执行 |
| `IsFaulted` | 一个布尔值，指示 `Task` 是否因未处理的异常而中止执行 |
| `Status` | `TaskStatus` 值，指示 `Task` 实例生命周期中的当前阶段 |

### 了解 Task 的生命周期

每个 `Task` 实例都有其生命周期，理解这一点非常重要。然而，它代表的是并发代码，这些代码可能根据底层硬件提供的可能性和运行时的资源可用性并行运行。因此，关于 `Task` 实例的任何信息都可能在你检索到它的瞬间发生变化，因为它的状态正在并发地改变。

`Task` 实例只会完成一次生命周期。一旦它达到三种可能的最终状态之一，就不会再回到任何之前的状态，如图 33-9 中的状态图所示。

![](img/d99870e80390742f93963da7be0b2e61_1079_0.png)

图 33-9

`Task` 实例有三种可能的初始状态，具体取决于它的创建方式，如表 33-3 所述。

### 表 33-3：Task 实例的初始状态

| 值 | 说明 |
|---|---|
| `TaskStatus.Created` | 使用 `Task` 构造函数创建的 `Task` 实例具有这个初始状态。一旦调用 `Start` 或 `RunSynchronously`，或者任务被取消，该状态就会改变。 |
| `TaskStatus.WaitingForActivation` | 这是通过允许定义延续任务的方法创建的任务的初始状态——也就是说，这些任务要等其他依赖任务完成执行后才会被调度。 |
| `TaskStatus.WaitingToRun` | 这是通过 `TaskFactory.StartNew` 创建的任务的初始状态。它正在等待指定的调度程序拾取并运行它。 |

接下来，任务状态可以转换为 `TaskStatus.Running` 状态，并最终进入最终状态。如果它附加了子任务，则该任务不会被视作完成，并将转换为 `TaskStatus.WaitingForChildrenToComplete` 状态。一旦其子任务完成，该任务就会转移到表 33-4 所示的三种可能的最终状态之一。

### 表 33-4：Task 实例的最终状态

| 值 | 说明 |
|---|---|
| `TaskStatus.Canceled` | 取消请求在任务开始执行之前或执行期间到达。`IsCanceled` 属性将为 True。 |
| `TaskStatus.Faulted` | 任务主体或其子任务主体中的未处理异常导致任务结束。`IsFaulted` 属性将为 True，并且 `Exception` 属性将非空，并将保存导致该任务或其子任务提前结束的 `AggregateException`。 |
| `TaskStatus.RanToCompletion` | 任务已完成其执行。它一直运行到主体结束，期间未被取消，也未抛出未处理的异常。`IsCompleted` 属性将为 True。此外，`IsCanceled` 和 `IsFaulted` 将均为 False。 |

### 使用 Task 并行化代码

在之前的示例中，你使用 `Parallel.Invoke` 并行启动了两个子程序：

```vb
Parallel.Invoke(Sub() GenerateAESKeys(), Sub() GenerateMD5Hashes())
```

如清单 33-13 所示，使用两个 `Task` 实例也可以完成同样的工作。使用 `Task` 实例可以更灵活地调度和启动独立及链式任务，从而利用多核优势。

### 清单 33-13：使用任务

```vb
' Create the tasks
Dim t1 = New Task(Sub() GenerateAESKeys())
Dim t2 = New Task(Sub() GenerateMD5Hashes())
' Start the tasks
t1.Start()
t2.Start()
' Wait for all the tasks to finish
Task.WaitAll(t1, t2)
```

前两行使用 lambda 表达式为 `GenerateAESKeys` 和 `GenerateMD5Hashes` 创建委托，从而创建两个 `Task` 实例。`t1` 与第一个子程序关联，`t2` 与第二个子程序关联。也可以使用多行 lambda 表达式语法来定义 `Task` 构造函数作为参数接收的操作。此时，两个 `Task` 实例的 `Status` 均为 `TaskStatus.Created`。子程序尚未运行，但代码将继续执行下一行。

### 启动任务

然后，下面一行开始 `t1` 的异步执行：

```vb
t1.Start()
```

`Start` 方法以独立方式启动委托的执行，即使委托尚未完成执行，程序流也会继续执行此方法之后的指令。与该任务关联的委托中的代码会并发运行，并可能与主程序流（主线程）并行运行。这意味着此时有一个主线程，以及其他一个或多个线程支持这个新任务的执行。

主程序流（主线程）的执行是同步的。这意味着它将继续执行下一条指令，也就是启动 `t2` 异步执行的那一行：

```vb
t2.Start()
```

现在，`Start` 方法以另一种独立方式启动委托的执行，即使这另一个委托尚未完成执行，程序流也会继续执行此方法之后的指令。与该任务关联的委托中的代码会并发运行，并可能与主线程以及已经在运行的 `GenerateAESKeys` 内部的代码并行运行。这意味着此时有一个主线程，以及支持这两个任务执行的其他线程。

> 使用 `Task` 实例和 Visual Basic 新增的最新语言改进，确实很容易运行异步代码。只需几行代码，就可以创建异步运行的代码、控制其执行流程，并利用多核微处理器或多处理器。

图 33-10 中的序列图显示了主线程和这两个任务的并行及异步执行流程。

![](img/d99870e80390742f93963da7be0b2e61_1081_0.png)

图 33-10

### 使用并行任务和并行堆栈可视化任务

Visual Basic 2010 IDE 提供了两个新的调试窗口：“并行任务”和“并行堆栈”。它们提供有关正在运行的任务的信息，包括其状态以及它们与底层线程的关系。这些新的调试窗口使你能够监视 .NET Framework 4 中任务和线程在底层发生的情况，同时还可以让你查看每个任务和线程中正在运行的 Visual Basic 代码。通过逐步运行代码，你可以看到同步执行和异步执行之间的差异。

例如，如果你在 `Task.WaitAll(t1, t2)` 这一行插入断点，并且你的微处理器至少有两个核心，你将能够看到两个任务并行运行。为此，请选择“调试”→“窗口”→“并行任务”（Ctrl + Shift + D, K）。IDE 将

![](img/d99870e80390742f93963da7be0b2e61_1081_0.png)

图 33-10

显示如图 33-11 所示的“并行任务”对话框，其中包含所有任务及其状态（已调度、运行中、等待、等待死锁等）的列表。

![](img/d99870e80390742f93963da7be0b2e61_1082_0.png)

## 图 33-11

有两个任务：

+ > 任务 ID 1：`<lambda12>()` — 分配给工作线程 ID 384
+ > 任务 ID 2：`<lambda13>()` — 分配给工作线程 ID 1020
