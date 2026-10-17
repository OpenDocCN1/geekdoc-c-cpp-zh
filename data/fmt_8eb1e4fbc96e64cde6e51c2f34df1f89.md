
# 使用集合避免长时间持有锁

我不喜欢任何用于阻塞线程的同步原语，因为创建线程的代价太高了。这里有一个示例有助于澄清这个问题。

想象有一个客户端发送请求的网站。当客户端请求到达时，线程池开始处理该请求。假设该客户端想要以线程安全的方式修改服务器上的某些数据，因此它获取了一个读写锁进行写入。假设这个锁被持有了很长时间。在锁被持有期间，另一个客户端进，因此线程池为该客户端创建了一个新线程，然后该线程在尝试获取读取读写锁时阻塞。事实上，随着越来越多的客户端进入，线程池创建了越来越多的线程，所有这些线程都在锁上阻塞。服务器花费了所有时间创建线程，导致它们停止了运行！这台服务器的可扩展性非常差。

糟糕的是，当写入线程释放锁时，所有读取线程同时解除阻塞并运行，但可能有许多线程尝试在相对较少的 CPU 上运行，因此 Windows 在线程之间不断进行上下文切换。结果是由于与上下文切换相关的开销，工作负载的处理速度无法达到应有的最快。

如果你回顾本章显示的所有结构，这些结构试图解决的许多问题可以使用第 26 章讨论的 `Task` 类来更好地更好地完成。以 `Barrier` 类为例：你可以产生几个 `Task` 对象来处理某个阶段，然后当所有这些任务完成后，你就可以继续处理一个或多个对象。

读写锁（Reader-writer locks）非常流行且有用。尝试用 `Task` 对象构建一个这样的锁是非常有挑战性的。然而，我的并发线程库（Power Threading library）包含了一个非阻塞的读写类，我将其称为 `ReaderWriterGate`。它的看起来如下所示（未显示部分方法）：

```cs
public sealed class ReaderWriterGate : IDisposable {
    public ReaderWriterGate();
    public void Dispose();
}
```

```cs
public IAsyncResult BeginRead(ReaderWriterGateCallback callback, Object state,
    AsyncCallback asyncCallback, Object asyncState);
public Object EndRead(IAsyncResult result);
```

```cs
public IAsyncResult BeginWrite(ReaderWriterGateCallback callback, Object state,
    AsyncCallback asyncCallback, Object asyncState);
public Object EndWrite(IAsyncResult result);
```

`ReaderWriterGateCallback` 是一个如下所示的委托：

```cs
public delegate object ReaderWriterGateCallback(ReaderWriterGateReleaser releaser);
```

`ReaderWriterGateReleaser` 类如下所示（未显示部分方法）：

```cs
public sealed class ReaderWriterGateReleaser {
    public Object State { get; } // 返回传递给 BeginRead/BeginWrite 的 'state'
    public void Dispose();
}
```

`ReaderWriterGate` 让锁看起来就像一个异步 I/O 操作。事实上，我的类提供了返回 `AsyncCallback` 委托的 `BeginRead` 和 `BeginWrite` 方法，以及接受 `IAsyncResult` 的 `EndRead` 和 `EndWrite` 方法。我设计该类的工作方式与第27章中讨论的 APM 完全相同。

工作原理如下：将需要访问资源的代码放在自己的方法中，然后调用 `BeginRead`，并将此方法作为 `ReaderWriterGetBytes` 委托参数传递。当可以从从资源读取时，`ReaderWriterGate` 对象将让线程池线程调用你的方法。注意，多个线程池可能并发执行来自资源的方法。将需要访问资源的代码放在自己的方法中并调用 `BeginWrite`，并将此方法作为 `ReaderWriterGetCallback` 委托参数传递。当可以安全写入资源时，`ReaderWriterGate` 对象将让线程池调用你的方法。注意，`ReaderWriterGate` 对象确保在特定时刻只有一个线程池在执行对该资源重要的操作。

> 8 当然，如果你只需要对资源进行互斥访问，你始终可以使用读写锁，并仅对它保护的资源请求写访问。

## 第29章 混合线程同步

当你的方法完成资源处理并返回时，`ReaderWriter` 对象将调用你传递给 `BeginRead` 或 `BeginWrite-asyncCall` 参数的任何内容；这就是你知道操作何时完成的方法。

所以，让我们回到 Web 服务器的讨论。客户端发起写入资源的请求，线程池调用 `ReaderWriter` 的 `BeginWrite` 方法。当线程正在处理回调方法时，另一个客户端发起请求。线程池创建一个新线程，该线程调用 `BeginRead`。`ReaderWriter` 对象发现此时不允许读取，它将回调委托添加到内部队列中。该队列是一个集合类，需要以线程安全的方式进行填充，因此在操作集合时会加锁。然而，锁仅在从队列中添加和移除项时持有，这需要的时间非常短。这意味着其他也使用 `ReaderWriter` 的线程也不会阻塞很长时间（如果发生阻塞的话！）

在回调委托被添加到队列后，线程池返回到池中。当客户端请求进入时，同一个线程池被唤醒并调用 `BeginRead`，向内部队列中添加越来越多的委托。现在服务器在所有工作中只有两个线程。

当第一个线程完成向资源写入时，它从回调方法返回到 `ReaderWriter` 对象。`ReaderWriter` 看到其内部队列有一许多委托，因此它将所有这些委托发布到 CLR 的线程池。再次，在操作队列时必须加锁，但锁的持有时间仅足够确保其回调委托进入线程池。线程池在不多于现有线程数的情况下完成此工作，且没有发生上下文切换。现在，我们拥有了一个消耗资源极少且运行性能卓越的可扩展服务器。

`ReaderWriter` 对象还有另一个内部队列，用于那些想要写入写入资源的委托。当写请求出现时，任何新进入的读取委托都会被入队，以便当前的读取方法能够完成并从队列中排空。当线程池线程处理完之前队列中的读取方法后，一个写委托会被入队到线程池中。这就是我确保在任何给定时间只有一个其他线程在运行的方法。

关于 `ReaderWriterGate` 的更多细节可以在此处查找到：`http://msdn.microsoft.com/en-us/magazine/cc163532.aspx`。在我想到这个主意后，保留了专利权。

> 9 这假设了计算机上没有其他线程在运行，这很讽刺，因为大多数计算机的 CPU 使用率远低于 100%。而且即使 CPU 使用率必须达到 100%，它仍然可以工作。

## 第五部分 线程处理

微软在2009年获得了专利局授予了该专利（`#7,603,502`）。然而，尽管微软拥有该专利，FCL（框架类库）并没有提供任何实现此想法的类。但在我的线程库中提供了一个实现。当我将权利卖给微软时，我获得了一个允许 Intellect 使用此“发明”的许可，前提是它只能在微软平台上使用。

在第27章中，我对我的 `AsyncEnumerator` 类进行了简要介绍，它是我的线程库的一部分。该类允许你使用支持 CLR 的类进行同步编程模型，而我的 `ReaderWriterGate` 支持 APM。然而，当我第一次尝试这样做时，发现可以进一步简化编程模型。因此，如果你想使用我的 `AsyncEnumerator` 并以线程安全的方式访问数据，请使用我的 `SyncGate` 而不是 `ReaderWriterGate`。`SyncGate` 类也在我的线程库中，它看起来如下：

```cs
public class SyncGate {
    public void BeginRegion(SyncGate mode, AsyncCallback asyncCallback, object asyncState);
    public void EndRegion(AsyncResult result);
}
```

你应该查看我的线程库中的示例来了解这些类的用法，但我提取了 `PipeServerAsyncEnumerator` 方法并对其修改，将最新客户端的时间戳记录在所有线程可访问的静态字段中。由于多个客户端可以使用不同的线程同时运行，更新静态字段必须以线程安全的方式进行。为了实现这一点，创建一个持有 `SyncGate` 对象的静态字段，并分别调用我的 `BeginRegion` 和 `EndRegion` 方法来获取和释放排斥访问。以下是增加了行的代码版本：

```cs
// 此字段记录最新客户端请求的时间戳
private static DateTime s_lastClientRequestTimestamp = DateTime.MinValue;
// SyncGate 确保对 s_lastClientRequestTimestamp 字段的线程安全
private static ReaderGate s_gate = new SyncGate();
private static IEnumerator<int32> PipeServerAsyncEnumerator(AsyncEnumerator ae) {
    // 每个服务器对象在此管道上执行异步操作
    using (var pipe = new NamedPipeServerStream(
```

> ¹⁰ 即使你的 Silverlight 应用程序运行在非微软操作系统上，Silverlight 也是微软的平台。而且，我的线程库也有该类的版本，微软 .NET Compact Framework 也是如此。

# 第29 章 混合线程同步 855

`"Echo", PipeDirection.InOut, -1, PipeTransmissionMode.Message, POptions.Asynchronous | PipeOptions.WriteThrough) {`

```cs
// 异步等待客户端连接
pipe.BeginWaitForConnection(ae.End(), null);
yield return 1;
```

```cs
// 客户端已连接，让我们接受另一个客户端
var aeNewClient = new AsyncEnumerator();
aeNewClient.BeginExecute(
pipeServerAsyncEnumerator(aeNewClient), aeNewClient.EndExecute);
```

```cs
// 接受客户端连接
pipe.EndWaitForConnection(ae.DequeueAsyncResult());
```

```cs
// 异步从客户端读取请求
Byte[] data = new Byte[1000];
pipe.BeginRead(data, 0, data.Length, ae.End(), null);
yield return 1;
```

```cs
// 客户端向我们发送了请求，并对其进行处理。
Int32 bytesRead = pipe.EndRead(ae.DequeueAsyncResult());
```

```cs
// 获取此客户端请求的时间戳
DateTime now = DateTime.Now;
```

> // 我们想保存最近一次客户端请求的时间戳。由于多个
> 客户端正在并发运行，因此必须以线程安全的方式完成。
s_gate.BeginRegion(SyncGateMode.Exclusive, ae.End()); // 请求排斥访问
yield return 1; // 当授予排斥访问时，迭代器恢复

```cs
if (s_lastClientRequestTimestamp < now)
s_lastClientRequestTimestamp = now;
```

```cs
s_gate.EndRegion(ae.DequeueAsyncResult()); // 释放排斥访问
```

> // 我的示例服务器将所有字符转换为大写字母
> // 但是，你可以用任何计算密集型操作来替换此代码
data = Encoding.UTF8.GetBytes(
Encoding.UTF8.GetString(data, 0, bytesRead).ToUpper().CharArray());

```cs
// 异步将响应发回客户端
pipe.BeginWrite(data, 0, data.Length, ae.End(), null);
yield return 1;
```

```cs
// 响应已发送到客户端，关闭我们这一端的管道
pipe.EndWrite(ae.DequeueAsyncResult());
```

```cs
} // 关闭管道
}
```

# 并发集合类

FCL（框架类库）附带了线程安全的集合类，它们都位于 `System.Collections.Concurrent` 命名空间。`ConcurrentQueue`、`ConcurrentStack` 和 `ConcurrentDictionary` 位于 `MSCorLib.dll` 中，而 `ConcurrentBag` 位于 `System.dll` 中。以下是它们最常用的常用的成员，例如：

```cs
// 按先入先出（FIFO）顺序处理项
public class ConcurrentQueue<T> : IProducerConsumerCollection<T>, IEnumerable<T>, ICollection, IEnumerable {
    public ConcurrentQueue();
    public void Enqueue(T item);
    public Boolean TryDequeue(out T result);
    public int Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// 按后入先出（LIFO）顺序处理项
public class ConcurrentStack<T> : IProducerConsumerCollection<T>, IEnumerable<T>, ICollection, IEnumerable {
    public ConcurrentStack();
    public void Push(T item);
    public Boolean TryPop(out T result);
    public int Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// 一个允许重复项的无序集合
public class ConcurrentBag<T> : IProducerConsumerCollection<T>, IEnumerable<T>, ICollection, IEnumerable {
    public ConcurrentBag();
    public void Add(T item);
    public Boolean TryTake(out T result);
    public int Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// 一个无序的键值对集合
public class ConcurrentDictionary<TKey, TValue> : IDictionary<TKey, TValue>, IEnumerable<KeyValuePair<TKey, TValue>>, IDictionary, ICollection, IEnumerable {
    public ConcurrentDictionary();
    public Boolean Add(TKey key, TValue value);
    public Boolean TryGetValue(TKey key, out TValue value);
    public TValue this[TKey key] { get; set; }
    public Boolean Update(TKey key, TValue newValue, TValue comparisonValue);
    public Boolean Remove(TKey key, TValue value);
    public TValue AddOrUpdate(TKey key, TValue add, Func<TKey, TValue, TValue> updateFactory);
    public TValue GetOrAdd(TKey key, TValue value);
    public int Int32 Count { get; }
    public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator();
}
```
