
```csharp
Console.WriteLine($"Element {i} has value {data[i]}");
}
}
static void doAdditionalProcessing()
{
    Thread.Sleep(10);
}
static void doMoreAdditionalProcessing()
{
    Thread.Sleep(10);
}
}
```

`SerialTest` 方法以一种相当冗长的方式填充整数数组，然后遍历此列表，打印数组中每个项目的索引以及相应项目的价值。`doAdditionalProcessing` 和 `doMoreAdditionalProcessing` 方法只是模拟作为处理的一部分可能导致运行时放弃处理器控制的长时间运行操作。程序方法的输出如下所示：

```
Element  0 has value 0
Element  1 has value 1
Element  2 has value 2
Element  3 has value 3
Element  4 has value 4
Element  5 has value 5
Element  6 has value 6
Element  7 has value 7
Element  8 has value 8
Element  9 has value 9
```

现在考虑接下来显示的 `ParallelTest` 方法。此方法与 `SerialTest` 方法相同，只是它使用 `Parallel.For` 构造通过运行并发任务来填充 `data` 数组。每个任务运行的 lambda 表达式中的代码与 `SerialTest` 方法中的初始 for 循环中的代码相同。

```csharp
using System.Threading.Tasks;
...
static void ParallelTest()
{
    int[] data = new int[NUMELEMENTS];
    int j = 0;
    Parallel.For (0, NUMELEMENTS, (i) =>
    {
        j = i;
        doAdditionalProcessing();
        data[i] = j;
        doMoreAdditionalProcessing();
    });
    for (int i = 0; i < NUMELEMENTS; i++)
    {
        Console.WriteLine($"Element {i} has value {data[i]}");
    }
}
```

目的是让 `ParallelTest` 方法执行与 `SerialTest` 方法相同的操作，只是使用并发任务，并且如果运气好因此运行得稍快一些。问题是它可能并不总是按预期工作。`ParallelTest` 方法生成的一些示例输出如下所示：

```
Element  0 has value 1
Element  1 has value 1
Element  2 has value 4
Element  3 has value 8
Element  4 has value 4
Element  5 has value 1
Element  6 has value 4
Element  7 has value 8
Element 8 has value 8
Element 9 has value 9
```

分配给 `data` 数组中每个项目的数值并不总是与使用 `SerialTest` 方法生成的值相同。此外，进一步运行 `ParallelTest` 方法可能会产生不同的结果集。

如果你检查 `Parallel.For` 构造中的逻辑，你应该能看出问题所在。lambda 表达式包含以下语句：

```
j = i;
doAdditionalProcessing();
data[i] = j;
doMoreAdditionalProcessing();
```

代码看起来无害。它将变量 `i` 的当前值复制到变量 `j`，稍后它将 `j` 的值存储在 `data` 数组中由 `i` 索引的元素中。如果 `i` 包含 5，则 `j` 被赋值为 5，稍后 `j` 的值存储在 `data[5]` 中。但在将值赋给 `j` 之后再读回之前，代码会执行更多工作；它调用 `doAdditionalProcessing` 方法。如果此方法执行时间很长，运行时可能会挂起线程并安排另一个任务。运行 `Parallel.For` 构造的另一个迭代的并发任务可能会运行并为 `j` 分配新值。因此，当原始任务恢复时，它分配给 `data[5]` 的 `j` 的值不是它存储的值，结果是数据损坏。更麻烦的是，有时这段代码可能会按预期运行并产生正确的结果，有时可能不会；一切都取决于计算机的繁忙程度以及各种任务的调度方式。因此，这类错误可能在测试期间潜伏，然后突然在生产环境中显现。

变量 `j` 由所有并发任务共享。如果任务将值存储在 `j` 中然后稍后读回，它必须确保在此期间没有其他任务修改了 `j`。这需要在可以访问它的所有并发任务之间同步对变量的访问。你可以通过锁定数据来实现同步访问的一种方式。

## Locking data

C# 语言通过 `lock` 关键字提供锁定语义，你可以使用它来保证对资源的独占访问。你这样使用 `lock` 关键字：

```csharp
object myLockObject = new object();
...
lock (myLockObject)
{
    // Code that requires exclusive access to a shared resource
}
```

`lock` 语句尝试对指定的对象获取互斥锁，如果该对象当前正被另一个线程锁定，则会阻塞。当线程获得锁后，`lock` 语句之后的代码块开始运行。在该块结束时，锁会被释放。如果另一个线程被阻塞等待锁，它就可以获取锁并继续其处理。

## 用于协调任务的同步原语

`lock` 关键字对于许多简单场景来说已经足够，但在某些情况下你可能有更复杂的需求。`System.Threading` 命名空间包含许多额外的同步原语，你可以用它们来解决这些情况。这些同步原语是为与任务一起使用而设计的类；它们公开锁定机制，在任务持有锁时限制对资源的访问。它们支持多种锁定技术，你可以用它们来实现不同风格的并发访问，从简单的独占锁，到信号量，再到读写锁。

下面的列表总结了一些这些原语。有关更多信息和示例，请参阅随 Visual Studio 2015 提供的文档。

### Note

.NET Framework 自首次发布以来就包含了一套体面的同步原语。下列表仅描述了 `System.Threading` 命名空间中包含的较新的原语。新原语与之前提供的原语之间存在一些重叠。在功能重叠的情况下，你应该使用较新的替代方案，因为它们是为多 CPU 计算机而设计和优化的。

对构建多线程应用程序可用的所有可能的同步机制的理论的详细讨论超出了本书的范围。有关多线程和同步的一般理论的更多信息，请参阅随 Visual Studio 2015 提供的文档中的主题“Synchronizing Data for Multithreading”。

### ManualResetEventSlim

`ManualResetEventSlim` 类提供了一种功能，允许一个或多个任务等待一个事件。`ManualResetEventSlim` 对象可以处于两种状态之一：已发出信号和未发出信号。任务创建 `ManualResetEventSlim` 对象并指定其初始状态。其他任务可以通过调用 `Wait` 方法等待 `ManualResetEventSlim` 对象被发出信号。如果 `ManualResetEventSlim` 对象处于未发出信号状态，`Wait` 方法会阻塞任务。另一个任务可以通过调用 `Set` 方法将 `ManualResetEventSlim` 对象的状态更改为已发出信号。此操作会释放所有等待 `ManualResetEventSlim` 对象的任务，使其可以继续运行。`Reset` 方法会将 `ManualResetEventSlim` 对象的状态更改回未发出信号。

### SemaphoreSlim

你可以使用 `SemaphoreSlim` 类来控制对资源池的访问。

`SemaphoreSlim` 对象有一个初始值和一个可选的最大值。通常，`SemaphoreSlim` 对象的初始值是资源池中的资源数量。访问资源池中的资源的任务首先调用 `Wait` 方法。此方法尝试递减 `SemaphoreSlim` 对象的值，如果结果不为零，则线程被允许继续并可以从池中取出一个资源。完成后，任务应调用 `SemaphoreSlim` 对象的 `Release` 方法。此操作会递增信号量的值。

如果任务调用 `Wait` 方法并且递减 `SemaphoreSlim` 对象的值会导致负值，则任务会等待直到另一个任务调用 `Release`。

`SemaphoreSlim` 类还提供了 `CurrentCount` 属性，你可以使用它来确定 `Wait` 操作是否可能立即成功或会导致阻塞。

### CountdownEvent

可以把 `CountdownEvent` 类看作是信号量的逆向与手动重置事件的结合。

当任务创建 `CountdownEvent` 对象时，它会指定一个初始值。一个或多个任务可以调用 `CountdownEvent` 对象的 `Wait` 方法，如果其值不为零，则任务会被阻塞。`Wait` 不会递减 `CountdownEvent` 对象的值；相反，其他任务可以调用 `Signal` 方法来减少该值。当 `CountdownEvent` 对象的值达到零时，所有被阻塞的任务都会被发出信号并可以继续运行。

任务可以通过使用 `Reset` 方法将 `CountdownEvent` 对象的值设置回其构造函数中指定的值，并且任务可以通过调用 `AddCount` 方法增加此值。你可以通过检查 `CurrentCount` 属性来确定对 `Wait` 的调用是否可能阻塞。

### ReaderWriterLockSlim

`ReaderWriterLockSlim` 类是一种高级同步原语，支持单个写入者和多个读取者。其思想是修改资源需要独占访问，但读取资源不需要；多个读取者可以同时访问同一资源，但不能与写入者同时访问。

想要读取资源的任务调用 `ReaderWriterLockSlim` 对象的 `EnterReadLock` 方法。此操作在对象上获取读锁。当任务完成对资源的使用时，它调用 `ExitReadLock` 方法，该方法释放读锁。多个任务可以同时读取同一资源，并且每个任务都获得自己的读锁。

当任务修改资源时，它可以调用同一个 `ReaderWriterLockSlim` 对象的 `EnterWriteLock` 方法来获取写锁。如果一个或多个任务当前对该对象持有读锁，则 `EnterWriteLock` 方法会阻塞，直到它们全部释放。任务获得写锁后，即可修改资源并调用 `ExitWriteLock` 方法来释放锁。

`ReaderWriterLockSlim` 对象只有一个写锁。如果另一个任务尝试获取写锁，它将被阻塞，直到第一个任务释放该写锁。

为了确保写入任务不会被无限期阻塞，一旦任务请求写锁，其他任务随后对 `EnterReadLock` 的所有调用都会被阻塞，直到写锁被获取并释放。

### Barrier

使用 `Barrier` 类，你可以暂时在应用程序中的特定点暂停一组任务的执行，并且只有当所有任务都到达该点时才继续。它对于需要按步骤同步执行一系列并发操作的任务非常有用。

当任务创建 `Barrier` 对象时，它会指定将被同步的任务集的数量。你可以把这个值看作是 `Barrier` 类内部维护的任务计数器。此值稍后可以通过调用 `AddParticipant` 或 `RemoveParticipant` 方法进行修改。当任务到达同步点时，它调用 `Barrier` 对象的 `SignalAndWait` 方法，该方法递减 `Barrier` 对象内部的线程计数器。如果该计数器大于零，则任务会被阻塞。只有当计数器达到零时，所有等待 `Barrier` 对象的任务才会被释放，并且只有在此时它们才能继续运行。

`Barrier` 类提供了 `ParticipantCount` 属性，该属性指定它同步的任务数量，以及 `ParticipantsRemaining` 属性，该属性指示有多少个任务需要在屏障被解除且被阻塞的任务可以继续运行之前调用 `SignalAndWait`。

你也可以在 `Barrier` 构造函数中指定一个委托。此委托可以引用一个方法，该方法在所有任务到达屏障时运行。`Barrier` 对象作为参数传递给此方法。屏障不会被解除且任务不会被释放，直到此方法完成。

### Canceling synchronization

`ManualResetEventSlim`、`SemaphoreSlim`、`CountdownEvent` 和 `Barrier` 类都通过第 23 章中描述的取消模型支持取消。这些类的每个等待操作都可以采用可选的 `CancellationToken` 参数，从 `CancellationTokenSource` 对象中检索。如果调用 `CancellationTokenSource` 对象的 `Cancel` 方法，则每个引用由此源生成的 `CancellationToken` 的等待操作都会以 `OperationCanceledException` 异常中止。

以下代码显示了如何调用 `SemaphoreSlim` 对象的 `Wait` 方法并指定取消令牌。如果等待操作被取消，则 `OperationCanceledException` 捕获处理程序会运行。

```csharp
CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();
CancellationToken cancellationToken = cancellationTokenSource.Token;
// Semaphore that protects a pool of 3 resources
SemaphoreSlim semaphoreSlim = new SemaphoreSlim(3);
...
// Wait on the semaphore, and catch the OperationCanceledException
if
// another thread calls Cancel on cancellationTokenSource
try
{
    semaphoreSlim.Wait(cancellationToken);
}
catch (OperationCanceledException e)
{
    ...
}
```
