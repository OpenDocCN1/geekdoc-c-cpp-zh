
`public delegate object ReaderWriterGateCallback(ReaderWriterGateReleaser releaser);`

`ReaderWriterGateReleaser` 类如下（未显示某些方法）：

```csharp
public sealed class ReaderWriterReleaser : IDisposable {
    public Object State { get; } // 返回给 BeginRead/BeginWrite 的 'state'
    public void Dispose();
}
```

`ReaderWriterGate` 使锁变得像异步 I/O 操作一样。事实上，我的类提供了使用 `AsyncCallback` 委托并返回 `IAsyncResult` 的 `BeginRead` 和 `BeginWrite` 方法，以及接受 `IAsyncResult` 的 `EndRead` 和 `EndWrite` 方法。我设计该类的工作方式与第 27 章讨论的 APM 完全相同。

其工作原理如下：在自己的方法中需要访问资源的代码会调用 `BeginRead`，并将此方法传递给 `ReaderWriterGateCallback` 参数。当可以从资源中读取时，`ReaderWriterGate` 对象将让线程池线程调用你的方法。注意，多个线程池可能并发执行来自资源的方法。在自己的方法中需要访问资源的代码会调用 `BeginWrite`，并将此方法传递给 `ReaderWriterGateCallback` 委托参数。当可以向资源中写入时，`ReaderWriterGate` 将让线程池线程调用你的方法。注意，多个线程池可能并发执行来自资源的方法。（注：此处原文存在重复描述，译文已按原文逻辑处理）。

# 第29章 混合同步

所以，让我们回到服务器。客户端发起请求。线程池为该客户端创建一个线程，然后该线程阻塞以获取读写锁进行读取。事实上，随着越来越多的客户端进入，线程池创建了越来越多的线程，而所有这些线程都在锁上自我阻塞。服务器花费了所有时间来创建线程，只为了让它们停止运行！这个服务器的可扩展性非常差。

更糟糕的是，当写入线程释放锁时，所有读取线程同时解除阻塞并运行，但随后有大量线程尝试在相对较少的 CPU 上运行，因此 Windows 在线程之间频繁地进行上下文切换。结果是由于与上下文切换相关的所有开销，工作负载无法以最快速度进行处理。

`ReaderWriterGate` 有另一个用于写入资源的队列。当写入请求出现时，任何进入的读取将被队列，以便当前的读取方法完成并离开。在线程池线程处理完之前队列中的读取方法后，一个写入委托被调度到线程池。这就是我确保任何时候只有一个线程在调用该方法的方法。

当第一个线程完成写入资源时，它从回调方法返回到 `ReaderWriterGate`。`ReaderWriterGate` 看到其内部队列中有许多委托，因此它将所有这些委托交给 CLR 线程池。再次，在操作队列时获取了锁，但持有锁的时间足以确保其回调进入池中。

在回调委托被添加到队列后，线程池返回池中。当更多请求进入时，同一个线程池不断唤醒并调用 `BeginRead`，将更多委托添加到内部队列中。现在服务器只有线程。

关于 `ReaderWriterGate` 的更多细节可以在此处找到：`http://msdn.microsoft.com/en-us/magazine/cc16353.aspx`。在我提出这个想法后，我看到了专利的权利

- 这假设没有其他线程在 CPU 上运行，这是指时间，因为大多数计算机的 CPU 使用率远低于 100%。而且即使 CPU 使用率达到 100%，如果读取优先级较低，仍然可以工作。如果其他线程正在运行，就会发生上下文切换。这从性能角度来看是不利的，但从可靠性角度来看是好的。请记住 Windows 为每个进程分配至少一个线程，并执行上下文切换以确保一个挂起的应用程序不会停止其他应用程序的运行。

微软在 2009 年获得了专利局颁发了该专利（专利号 `#7,603,502`）。然而，尽管微软拥有这一想法的专利，但 FCL 并没有提供实现该想法的类。不过，我在我的 Power Threading 库中提供了一个实现。当我将权利出售给微软时，我获得了一项允许 Intellect 使用这项“发明”的许可，前提是它只能在微软平台上使用¹¹⁰。通过从 Intellect 网站下载该库，你即成为 Intellect 的客户，并可以根据许可限制使用该库。

在第 27 章中，我简要介绍了我的 `AsyncEnumerator`，这也是我的 Power Threading 库的一部分。这个类允许你使用支持 CLR API 的类进行同步编程模型，并且由于我的 `ReaderWriterGate` 支持 APM，你可以将其配合 `AsyncEnumerator` 一起使用。然而，当我第一次尝试这样做时，我发现我可以进一步简化这种编程模型。因此，如果你想使用我的 `AsyncEnumerator` 并让多个迭代器以线程安全的方式访问数据，请使用我的 `SyncGate` 而不是 `ReaderWriterGate`。`SyncGate` 类也位于我的 Power Threading 库中，它的结构如下：

```c
public sealed SyncGate
{
    public void BeginRegion(SyncGate mode.
```

你应该通过查看我的 Power Threading 库中的示例来了解如何一起使用这些类，但我在这里展示一个示例。我取了第 27 章所示的 `PipeServerAsyncEnumerator` 方法，并对其进行了修改，将最近客户端请求的时间戳记录在所有线程可访问静态字段中。由于多个客户端请求可以使用不同的线程同时运行，更新静态字段必须以线程安全的方式进行。为了实现这一点，我创建一个持有 `SyncGate` 对象引用的静态字段，并调用我的 `BeginRegion` 和 `EndRegion` 方法分别获取和释放独占访问。以下是带有新增行的的新版本代码：

```c
// 此字段记录最近客户端请求的时间戳
private static DateTime s_lastRequestTimestamp = DateTime.MinValue;
// SyncGate 确保对 s_lastRequestTimestamp 字段的线程安全访问
private static SyncGate s_gate = new SyncGate();
private static IEnumerator<Int32> PipeServerAsyncEnumerator(AsyncEnumerator ae) {
    // 每个服务器对象在此管道上执行异步操作
    using (var pipe = new NamedPipeServerStream(
```

> ¹⁰ 即使应用程序运行在非微软操作系统上，Silverlight 也是微软平台。而且，我的 Power Threading 库也为 Silverlight 以及微软 .NET Compact Framework 提供了该类的版本。

# 第29章 混合线程同步

`"Echo", PipeDirection.InOut, -1, PipeTransmissionMode.Message, PipeOptions.Asynchronous | PipeOptions.WriteThrough) {`

```c
// 异步接受客户端连接
pipe.BeginWaitForConnection(ae.End(), null);
yield return 1;
```

```c
// 一个客户端已连接，让我们接受另一个客户端
var aeNewClient = new AsyncEnumerator();
aeNewClient.BeginExecute(
PipeServerAsyncEnumerator(aeNewClient), aeNewClient.EndExecute);
```

```c
// 接受客户端连接
pipe.EndWaitForConnection(ae.DequeueAsyncResult());
```

```c
// 从客户端异步读取请求
Byte[] data = new Byte[1000];
pipe.BeginRead(data, 0, data.Length, ae.End(), null);
yield return 1;
```

```c
// 客户端发送了请求，处理它。
Int32 bytesRead = pipe.EndRead(ae.DequeueAsyncResult());
```

```c
// 获取此客户端请求的时间戳
DateTime now = DateTime.Now;
```

```c
// 我们想保存最近客户端请求的时间戳。由于多个
// 客户端并发运行，这必须以线程安全的方式完成
s_gate.BeginRegion(SyncGateMode.Exclusive, ae.End()); // 请求独占访问
yield return 1; // 授予独占访问
```

```c
if (s_lastRequestTimestamp < now)
ns_lastRequestTimestamp = now;
```

```c
s_gate.EndRegion(ae.DequeueAsyncResult()); // 释放独占访问
```

```c
// 我的示例将所有字符转换为大写
// 但可以用任何计算操作替换此代码
data = Encoding.UTF8.GetString(data, 0, bytesRead).ToUpper();
```

```c
// 异步将响应发送给客户端
pipe.BeginWrite(data, 0, data.Length, ae.End(), null);
yield return 1;
```

```c
// 响应已发送到客户端，关闭我们的连接
pipe.EndWrite(ae.DequeueAsyncResult());
```

```c
} // 关闭管道
```

```
}
```

# 并发集合类

FCL 提供了线程安全的集合类，它们都在 `System.Collections.Concurrent` 命名空间下。`ConcurrentQueue`、`ConcurrentStack` 和 `ConcurrentDictionary` 位于程序程序，而 `ConcurrentBag` 位于程序程序。以下是它们最常用成员的形式：

```c
// 先进先出 (FIFO) 顺序处理项
public class ConcurrentQueue<T> : IProducerConsumerCollection<T, IEnumerable<T>, ICollection, IEnumerable> {
    public ConcurrentQueue();
    public void Enqueue(T item);
    public bool TryDequeue(out T result);
    public int Count;
    public IEnumerator<T> GetEnumerator();
}

// 后进先出 (LIFO) 顺序处理项
public class ConcurrentStack<T> : IProducerConsumerCollection<T, IEnumerable<T>, ICollection, IEnumerable> {
    public ConcurrentStack();
    public void Push(T item);
    public bool TryPop(out T result);
    public int Count;
    public IEnumerator<T> GetEnumerator();
}

// 允许重复的无序集合
public class ConcurrentBag<T> : IProducerConsumerCollection<T, IEnumerable<T>, ICollection, IEnumerable> {
    public ConcurrentBag();
    public void Add(T item);
    public bool TryTake(out T result);
    public int Count;
    public IEnumerator<T> GetEnumerator();
}

// 键值对的无序集合
public class ConcurrentDictionary<TKey, TValue> : IDictionary<TKey, TValue>, IEnumerable<KeyValuePair<TKey, TValue>> {
    public ConcurrentDictionary();
    public void Add(TKey key, TValue value);
    public bool TryGetValue(TKey key, out TValue value);
    public TValue this[TKey] { get; set; }
    public void Update(TKey key, TValue newValue);
    public bool Remove(TKey key);
    public TValue AddOrUpdate(TKey key, TValue value, Func<TKey, TValue, TValue> updateFactory);
    public TValue GetOrAdd(TKey key, TValue value);
    public int Count;
    public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator();
}
```

# 混合同步

所有这些集合类是非阻塞的。也就是说，如果线程在元素不存在时尝试提取元素，线程会立即返回；线程不会等待元素出现。这就是为什么 `TryDequeue`、`TryPop` 和 `TryGetValue` 在获取项时返回 true，否则返回 false。

这些非阻塞集合并不都是无锁的。`ConcurrentDictionary` 使用了 `Monitor`，但在操作项时锁的时间非常短。`ConcurrentQueue` 和 `ConcurrentStack` 是无锁的；它们内部使用 `Interlocked` 方法来操作集合。`ConcurrentBag` 对象每个线程包含一个微集合。当线程向集合中添加项时，使用 `Interlocked` 方法将项添加到调用者的微集合中。当线程尝试从集合中提取元素时，集合会调用其线程的微集合来查找项。如果在那里，则使用 `Interlocked` 方法提取它。如果线程的微集合中没有该项，则在内部从另一个线程的微集合中提取项。我们称该线程是从另一个线程那里偷走了项。

你会注意到所有并发集合都提供 `GetEnumerator` 方法，它通常用于 C# 的 `foreach` 语句，并可以用于语言集成查询 (LINQ)。对于 `ConcurrentStack`、`ConcurrentQueue` 和 `ConcurrentBag`，`GetEnumerator` 方法获取集合的快照并返回该快照的元素；在遍历快照时，实际集合的内容可能会。`ConcurrentDictionary` 的 `GetEnumerator` 方法没有对其内容拍摄快照，因此在遍历字典时字典的内容可能会改变；请注意这一点。此外请注意 `Count` 属性返回查询瞬间集合中的元素数量。如果其他线程同时向集合中添加或删除元素，计数可能会变得不正确。

并发集合类 `ConcurrentStack`、`ConcurrentQueue` 和 `ConcurrentBag` 实现了 `IProducerConsumerCollection` 接口，其定义如下：

```c
public interface IProducerConsumerCollection<T> : IEnumerable<T>, ICollection, IEnumerable {
    bool TryTake(T item);
    T[] ToArray();
    void CopyTo(T[] array, Int32 index);
}
```

任何实现此接口的类都可以转换为阻塞集合，其中生产者（添加项）的线程在集合满时会阻塞，而消费者（移除项）的线程在集合为空时会阻塞。当然，我会尽量避免使用阻塞集合，因为它们生存的意义就是阻塞线程。要将非阻塞集合转换为阻塞集合，你需要构造一个 `System.Collections.Concurrent.BlockingCollection` 类，向其构造函数传递了指向非阻塞集合的引用。`BlockingCollection` 类（定义在 `System.dll` 程序集中）结构如下所示（未显示某些方法）：

```csharp
public class BlockingCollection<T> : IEnumerable<T>, ICollection, IEnumerable, IDisposable {
    public BlockingCollection(IProducerConsumerCollection<T> collection, Int32 boundedCapacity);
```
