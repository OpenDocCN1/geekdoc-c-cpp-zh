
# 第29 章 混合同步 857

所有这些集合类都是是非阻塞的。也就是说，如果线程尝试在不存在此类元素时提取元素，该线程将不会阻塞。

（注：原文中存在大量重复描述，此处已根据原文逻辑进行翻译）

所有这些集合类都是是非阻塞的。也就是说（由于原文此处存在大量重复，以下为对应翻译的逻辑内容）：

`FCL`（框架类库）附带了线程安全的集合类，它们都位于 `System.Collections.Concurrent` 命名空间。`ConcurrentQueue`、`ConcurrentStack` 和 `ConcurrentDictionary` 位于 `MSCorLib.dll` 中，而 `ConcurrentBag` 位于 `System.dll` 中。以下是它们最常用的成员，例如：

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

# 第 V 部分线程

当你构造 `BlockingCollection` 时，`boundedCapacity` 参数指示集合中项的最大数量。如果线程调用 `Add` 时底层集合已达到容量，生产者（添加项）的线程将阻塞。如果需要好，消费者（移除项）的线程会在集合为空时阻塞。要将非阻塞集合转换为阻塞集合，你需要构造 `System.Collections.Concurrent.BlockingCollection`，并传入非阻塞集合的引用。`BlockingCollection` 类（定义在 `System.dll` 中）如下（未显示部分方法）：

```cs
public class BlockingCollection<T> : IEnumerable<T>, ICollection, IEnumerable<T>, Disposable {

    public BlockingCollection(IConsumerCollection<T> collection, Int32 boundedCapacity);

    public void Add(T item);

    public Boolean TryAdd(T item, Int32 msTimeout, CancellationToken cancellationToken);

    public void CompleteAdding();

    public T Take();

    public Boolean TryTake(out T item, Int32 msTimeout, CancellationToken cancellationToken);

    public Int32 BoundedCapacity { get; }

    public Int32 Count { get; }

    public Boolean IsAddingComplete { get; } // 如果调用了 AddingComplete 则真

    public Boolean IsCompleted { get; } // 如果 IsAddingComplete且 Count==0 则真

    public IEnumerable<T> GetConsumingEnumerable(CancellationToken cancellation);

    public void CopyTo(T[] array, int index);

}
```

`BlockingCollection` 类实现了 `Disposable` 接口。调用 `Dispose` 时，它会调用底层集合的 `Dispose`，并释放该类内部用于阻塞生产者和消费者的两个 `SemaphoreSlim` 对象。

当生产者不再向集合中添加任何项时，生产者应该调用 `CompleteAdding` 方法。这向消费者指示不再有更多项产生。具体而言，这将导致 `GetConsumingEnumerable` 的 `foreach` 循环终止。下面的示例代码演示了如何设置生产者消费者场景并发送完成信号：

# 第29章 混合线程同步 859

```cs
public static void Main() {

  var bl = new BlockingCollection<Int32>(new ConcurrentQueue<Int32>());

  // A thread pool will be the consuming

  ThreadPool.QueueUserWorkItem(ConsumeItems, bl);

  // Add 5 items to the collection

  for (Int32 item = 0; item < 5; item++) {

    Console.WriteLine("Producing: " + item);

    bl.Add(item);

  }

  // Tell the consuming thread(s) that no more items will be added to the collection

  bl.CompleteAdding();

  Console.ReadLine(); // For testing purposes

}

private static void ConsumeItems(Object o) {

  var bl = (BlockingCollection<Int32>)o;

  // Block until an item shows up, then process it

  foreach (var item in bl.GetConsumingEnumerable()) {

    Console.WriteLine("Consuming: " + item);

  }

  // The collection is empty and no more items are going into it

  Console.WriteLine("All items have been consumed");

}
```

当我执行上述代码时，得到以下输出：

```
Producing: 0
Producing: 1
Producing: 2
Producing: 3
Producing: 4
Consuming: 0
Consuming: 1
Consuming: 2
Consuming: 3
Consuming: 4
```
