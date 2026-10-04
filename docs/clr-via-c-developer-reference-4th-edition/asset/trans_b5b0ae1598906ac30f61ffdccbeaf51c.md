
项，然后在内部获取一个 Monitor（监控器）从另一个线程的微型集合中提取一个项。我们称为从另一个线程“偷取”了该项。

你会发现，所有并发类都提供一个 `GetEnumerator` 方法，该方法通常用于 C# 的 `foreach` 语句，也可以用于语言集成查询 (LINQ)。对于 `ConcurrentStack`、`ConcurrentQueue` 和 `ConcurrentBag`，`GetEnumerator` 方法会获取集合内容的快照，并返回该快照中的元素；在枚举快照时，实际集合可能会发生变化。`ConcurrentDictionary` 的 `GetEnumerator` 则不会对其进行快照，因此在枚举字典时，字典的内容可能会发生；请注意这一点。此外，请注意 `Count` 属性返回的是你调用它时集合中的元素数量。如果其他线程同时向集合中添加或删除元素，计数可能会立即变得不准确。

三个并发类（`ConcurrentStack`、`ConcurrentQueue` 和 `ConcurrentBag`）实现了 `IProducerConsumer` 接口，该接口定义如下。

```csharp
public interface IProducerConsumerCollection<T> : IEnumerable<T>, ICollection, IEnumerable {
    Boolean TryAdd(T item);
    Boolean TryTake(out T item);
    T[] ToArray(T[] array, Int32 index);
    void CopyTo(T[] array, Int32 index);
}
```

任何实现此接口的类都可以转换为阻塞集合（blocking collection），其中生产（添加）项的线程会在集合满时被阻塞，而移除（获取）项的线程会在集合为空时被阻塞。当然，我会尽量避免使用阻塞集合，因为它们的目的是阻塞线程。要将非阻塞集合转换为阻塞集合，可以通过向其构造函数传递非阻塞集合的引用来构造一个 `System.Collections.BlockingCollection`。`BlockingCollection` 类如下所示（未显示某些方法）。

```csharp
public class BlockingCollection<T> : IEnumerable<T>, IEnumerable, IDisposable {
    public BlockingCollection(IProducerConsumerCollection<T> collection, Int32 boundedCapacity);

    public void Add(T item);
    public Boolean TryAdd(T item, Int32 timeout, CancellationToken cancellationToken);
    public void CompleteAdding();

    public T Take();
    public Boolean TryTake(out T item, Int32 timeout, CancellationToken cancellationToken);

    public Int32 BoundedCapacity { get; set; }
    public Int32 Count { get; set; }
    public Boolean IsAddingCompleted { get; set; } // 如果调用了 CompleteAdding 则为 true
    public Boolean IsAddingComplete { get; set; } // 如果 IsAddingComplete 为 true 且 Count==0 则为 true

    public IEnumerable<T> GetConsumingEnumerable(CancellationToken cancellationToken);

    public void CopyTo(T[] array, int index);
    public T[] ToArray();
    public void Dispose();
}
```

当你构造 `BlockingCollection` 时，`boundedCapacity` 参数表示你希望集合中包含的最大项数。如果线程在底层集合达到容量时调用 `Add`，该线程将被阻塞。如果需要，线程可以调用 `TryAdd` 并传入超时时间（毫秒）和/或一个 `CancellationToken`，这样线程将一直阻塞直到项被添加、超时过期或 `CancellationToken` 被取消（有关关于 `CancellationToken` 类的更多信息请参阅第 27 章）。

`BlockingCollection` 实现了 `IDisposable` 接口。如果你调用 `Dispose`，它会调用底层集合。它还会释放该类内部用于阻塞生产者和消费者的两个 `SemaphoreSlim` 对象。

当你不再向集合中添加任何项时，生产者应该调用 `CompleteAdding` 方法。这将向消费者发送信号，表示不再产生更多项。具体来说，这会导致使用 `GetConsumingEnumerable` 的 `foreach` 循环终止。下面的示例演示了如何设置生产者/消费者场景并发送完成信号。

```csharp
public static void Main() {
    var bl = new BlockingCollection<Int32>(new ConcurrentQueue<Int32>());

    // 线程池线程将进行消费
    ThreadPool.QueueUserWorkItem(ConsumeItems, bl);

    // 向集合中添加 5 个项
    for (Int32 item = 0; item < 5; item++) {
        Console.WriteLine("Producing: " + item);
        bl.Add(item);
    }

    // 告诉消费者线程（们）集合中不会再添加更多项了
    bl.CompleteAdding();

    Console.ReadLine();   // 用于测试目的
}
```

```csharp
private static void ConsumeItems(Object o) {
    var bl = (BlockingCollection<Int32>) o;

    // 阻塞直到项出现，然后处理它
    foreach (var item in bl.GetConsumingEnumerable()) {
        Console.WriteLine("Consuming: " + item);
    }
}
```

```csharp
// 集合为空且不再有更多项进入
Console.WriteLine("All items have been consumed");
```

当我执行上述代码时，我得到了如下输出。

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
All items have been consumed
```

如果你自己运行它，`Producing` 和 `Consuming` 的行可能会交错出现，但 `All items have been consumed` 这一行始终会在最后。

`BlockingCollection` 类还拥有静态的 `AddToAny`、`TryAddToAny`、`TakeFromAny` 和 `TryTakeFromAny` 方法。所有这些方法除了接收一个项、一个超时时间和 `CancellationToken` 外，还接收一个 `BlockingCollection<T>[]`。`(Try)AddToAny` 方法会遍历数组中的所有集合，直到找到一个可以接受该项的集合（因为其未达到容量）。`(Try)TakeFromAny` 方法会遍历数组中的所有集合，直到找到一个可以移除项的集合。

## 符号
- .NET Framework
- 检查, 8
- 旧代码, 459
- 反射 API, 583
- 与...稳定性, 34
- 投影, 655
- 版本, 268
- 与 WinRT 的互操作性, 654, 655
- .winmd 文件扩展名, 644

A
- AbandonedMutex 异常, 785
- Abort 方法, 579, 581
- Thread 类, 679
- 终止线程, 578
- 可访问性, 166
- 可访问修饰符, 156
- 访问器资源, 505
- 访问器方法, 228, 231
- 的可访问性, 248
- 泛型, 248
- 索引器, 244
- 内联, 247
- 命名, 245
- 性能, 247
- ReaderLock 方法, 355
- WriterLock 方法, 355

用于 .NET Framework 的 API
- .NET Framework 的 API, 583
- WinRT 的 API, 调用, 650
- AppDomain 类型, 实例方法, 595
- AppManager 类, 576
- AppMonitor 类, 573
- AppDomains, 17
- 终止线程, 跨边界访问对象, 559
- 应用输出, 562
- ASP.NET 应用和, 575
- 集合中的, 557
- 发现, 602
- 多个集合中的, 573
- 回调方法, 573
- 跨边界转换, 565
- CreateDomain 方法重载, 563
- 创建, 563
- 默认值, 556
- 定义, 556
- 演示, 563
- 可执行应用和, 574
- 特性, 556
- 第一机会异常通知, 573
- 前台/后台线程和, 688
- 友好名称, 563
- 垃圾回收, 571
- 垃圾回收表, 545
- 优雅偏移量, 577
- 实例字段和, 566, 567
- 隔离性提供的, 557, 566
- 托管代码和, 576
- 卸载, 477, 494, 566, 570
- 作为垃圾回收触发,579
- XML Web应用和, 575
- 针对特定的加载程序集, 585
- 加载到中, 564
- 多次加载到中, 586
- 托管代码和, 576
- 按值序列化对象, 568
- 按引用序列化对象, 564
- 内存使用监控, 524
- 跨边界方法调用, 566
- Microsoft Silverlight 应用和, 574
- 监控, 571
- 跨边界传递对象, 569
- 权限集继承, 563
- 代理类型, 定义, 564
- 目的, 553
- 只读属性中的, 572
- 健壮宿主应用, 577
- 单例类型和, 634
- SQL Server 和, 575
- 静态成员和, 567
- 线程池。见线程
- 线程和, 562
- 卸载
