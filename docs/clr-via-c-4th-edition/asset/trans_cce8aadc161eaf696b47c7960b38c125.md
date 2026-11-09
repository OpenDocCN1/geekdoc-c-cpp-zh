
```csharp
private readonly Queue<TaskCompletionSource<Object>> m_qWaitingWriters =
    new Queue<TaskCompletionSource<Object>>();

// All waiting readers wake up by signaling a single TaskCompletionSource
private TaskCompletionSource<Object> m_waitingReadersSignal =
    new TaskCompletionSource<Object>();
private Int32 m_numWaitingReaders = 0;

public AsyncOneManyLock() {
    m_noContentionAccessGranter = Task.FromResult<Object>(null);
}

public Task WaitAsync(OneManyMode mode) {
    Task accessGranter = m_noContentionAccessGranter; // Assume no contention

    Lock();
    switch (mode) {
        case OneManyMode.Exclusive:
            if (IsFree) {
                MakeWriter(); // No contention
            } else {
                // Contention: Queue new writer task & return it so writer waits
                var tcs = new TaskCompletionSource<Object>();
                m_qWaitingWriters.Enqueue(tcs);
                accessGranter = tcs.Task;
            }
            break;

        case OneManyMode.Shared:
            if (IsFree || (IsOwnedByReaders && m_qWaitingWriters.Count == 0)) {
                AddReaders(1); // No contention
            } else { // Contention
                // Contention: Increment waiting readers & return reader task so reader waits
                m_numWaitingReaders++;
                accessGranter = m_waitingReadersSignal.Task.ContinueWith(t => t.Result);
            }
            break;
    }
    Unlock();

    return accessGranter;
}

public void Release() {
    TaskCompletionSource<Object> accessGranter = null; // Assume no code is released

    Lock();
    if (IsOwnedByWriter) MakeFree(); // The writer left
    else SubtractReader(); // A reader left

    if (IsFree) {
        // If free, wake 1 waiting writer or all waiting readers
```
```

```csharp
// Process items in a last-in, first-out order (LIFO)
public class ConcurrentStack<T> : IProducerConsumerCollection<T>,
    IEnumerable<T>, ICollection, IEnumerable {

    public ConcurrentStack();
    public void Push(T item);
    public Boolean TryPop(out T result);
    public Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// An unordered set of items where duplicates are allowed
public class ConcurrentBag<T> : IProducerConsumerCollection<T>,
    IEnumerable<T>, ICollection, IEnumerable {

    public ConcurrentBag();
    public void Add(T item);
    public Boolean TryTake(out T result);
    public Int32 Count { get; }
    public IEnumerator<T> GetEnumerator();
}

// An unordered set of key/value pairs
public class ConcurrentDictionary<TKey, TValue> : IDictionary<TKey, TValue>,
    ICollection<KeyValuePair<TKey, TValue>>, IEnumerable<KeyValuePair<TKey, TValue>>,
    IDictionary, ICollection, IEnumerable {

    public ConcurrentDictionary();
    public Boolean TryAdd(TKey key, TValue value);
    public Boolean TryGetValue(TKey key, out TValue value);
    public TValue this[TKey key] { get; set; }
    public Boolean TryUpdate(TKey key, TValue newValue, TValue comparisonValue);
    public Boolean TryRemove(TKey key, out TValue value);
    public TValue AddOrUpdate(TKey key, TValue addValue,
        Func<TKey, TValue> updateValueFactory);
    public TValue GetOrAdd(TKey key, TValue value);
    public Int32 Count { get; }
    public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator();
}
```

所有这些集合类都是非阻塞的。也就是说，如果某个线程试图提取一个元素，但不存在这样的元素，该线程会立即返回；该线程不会阻塞等待元素出现。这就是为什么 TryDequeue、TryPop、TryTake 和 TryGetValue 等方法在成功获取项时返回 true，在未获取时返回 false。

这些非阻塞集合不一定是无锁的。ConcurrentDictionary 类在内部使用 Monitor，但在操作集合中的项时，锁只被持有很短的时间。ConcurrentQueue 和 ConcurrentStack 是无锁的；它们都在内部使用 Interlocked 方法来操作集合。单个 ConcurrentBag 对象在内部由每个线程一个迷你集合对象组成。当线程向包中添加项时，会使用 Interlocked 方法将该项添加到调用线程的迷你集合中。当线程试图从包中提取元素时，包会检查调用线程的迷你集合中是否有该项。如果该项存在，则使用 Interlocked 方法提取该项。如果线程的迷你集合中没有该项，则在内部获取 Monitor，从另一个线程的迷你集合中提取一项。我们说该线程正在从另一个线程窃取该项。

你会注意到，所有并发类都提供一个 GetEnumerator 方法，该方法通常与 C# 的 foreach 语句一起使用，但也可以与语言集成查询（LINQ）一起使用。对于 ConcurrentStack、ConcurrentQueue 和 ConcurrentBag，GetEnumerator 方法会获取集合内容的快照，并从该快照返回元素；在枚举快照期间，实际集合的内容可能会发生变化。ConcurrentDictionary 的 GetEnumerator 方法不会获取其内容的快照，因此在对字典进行枚举期间，字典的内容可能会发生变化；请注意这一点。另请注意，Count 属性返回查询那一刻集合中的元素数量。如果其他线程同时向集合添加元素或从集合移除元素，该计数可能会立即变得不准确。

并发集合类中有三个——ConcurrentStack、ConcurrentQueue 和 ConcurrentBag——实现了 IProducerConsumerCollection 接口，其定义如下。

```csharp
    public interface IProducerConsumerCollection<T> : IEnumerable<T>, ICollection, IEnumerable {
       Boolean TryAdd(T item);
       Boolean TryTake(out T item);
       T[] ToArray();
       void CopyTo(T[] array, Int32 index);
    }
```

任何实现此接口的类都可以转换为阻塞集合，其中生产（添加）项的线程在集合已满时会阻塞，消费（移除）项的线程在集合为空时会阻塞。当然，我会尽量避免使用阻塞集合，因为它们存在的目的就是阻塞线程。要将非阻塞集合转换为阻塞集合，可以通过向其构造函数传入非阻塞集合的引用来构造 System.Collections.Concurrent.BlockingCollection 类。BlockingCollection 类如下所示（未显示某些方法）。

```csharp
    public class BlockingCollection<T> : IEnumerable<T>, ICollection, IEnumerable, IDisposable {
       public BlockingCollection(IProducerConsumerCollection<T> collection,
          Int32 boundedCapacity);

       public void Add(T item);
       public Boolean TryAdd(T item, Int32 msTimeout, CancellationToken cancellationToken);
       public void CompleteAdding();

       public T Take();
       public Boolean TryTake(out T item, Int32 msTimeout, CancellationToken cancellationToken);

       public Int32  BoundedCapacity  { get; }
       public Int32  Count            { get; }
       public Boolean IsAddingCompleted { get; }  // true if CompleteAdding is called
       public Boolean IsCompleted       { get; }  // true if IsAddingComplete is true and Count==0

       public IEnumerable<T> GetConsumingEnumerable(CancellationToken cancellationToken);

       public void CopyTo(T[] array, int index);
       public T[] ToArray();
       public void Dispose();
    }
```

构造 BlockingCollection 时，boundedCapacity 参数表示你希望在集合中容纳的最大项数。如果底层集合已达到容量，而线程调用 Add，则生产线程将阻塞。如果愿意，生产线程可以调用 TryAdd，并传入超时（以毫秒为单位）和/或 CancellationToken，以便线程阻塞直到项被添加、超时到期或 CancellationToken 被取消（有关 CancellationToken 类的更多信息，请参见第 27 章）。

BlockingCollection 类实现 IDisposable 接口。调用 Dispose 时，它会对底层集合调用 Dispose。它还会释放该类在内部用于阻塞生产者和消费者的两个 SemaphoreSlim 对象。

当生产者不再向集合中添加任何项时，生产者应调用 CompleteAdding 方法。这将向消费者发出信号：不会再生产更多项。具体来说，这会导致使用 GetConsumingEnumerable 的 foreach 循环终止。下面的示例代码演示如何设置生产者/消费者场景并发出完成信号。

```csharp
public static void Main() {
    var bl = new BlockingCollection<Int32>(new ConcurrentQueue<Int32>());

    // A thread pool thread will do the consuming
    ThreadPool.QueueUserWorkItem(ConsumeItems, bl);

    // Add 5 items to the collection
    for (Int32 item = 0; item < 5; item++) {
        Console.WriteLine("Producing: " + item);
        bl.Add(item);
    }

    // Tell the consuming thread(s) that no more items will be added to the collection
    bl.CompleteAdding();

    Console.ReadLine();   // For testing purposes
}

private static void ConsumeItems(Object o) {
    var bl = (BlockingCollection<Int32>) o;

    // Block until an item shows up, then process it
    foreach (var item in bl.GetConsumingEnumerable()) {
        Console.WriteLine("Consuming: " + item);
    }

    // The collection is empty and no more items are going into it
    Console.WriteLine("All items have been consumed");
}
```
