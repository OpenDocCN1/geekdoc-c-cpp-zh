

**BlockingCollection** 类，向其构造函数传入一个对非阻塞集合的引用。**BlockingCollection** 类（定义在 System.dll 程序集中）如下所示（未显示某些方法）：

```csharp
public class BlockingCollection<T> : IEnumerable<T>, ICollection, IEnumerable, IDisposable {
    public BlockingCollection(IProducerConsumerCollection<T> collection,
        Int32 boundedCapacity);

    public void Add(T item);
    public Boolean TryAdd(T item, Int32 msTimeout, CancellationToken cancellationToken);
    public void CompleteAdding();

    public T Take();
    public Boolean TryTake(out T item, Int32 msTimeout, CancellationToken cancellationToken);

    public Int32 BoundedCapacity { get; }
    public Int32 Count { get; }
    public Boolean IsAddingCompleted { get; } // true if CompleteAdding is called
    public Boolean IsCompleted { get; } // true if IsAddingCompleted and Count==0

    public IEnumerable<T> GetConsumingEnumerable(CancellationToken cancellationToken);

    public void CopyTo(T[] array, int index);
    public T[] ToArray();
    public void Dispose();
}
```

构造 **BlockingCollection** 时，**boundedCapacity** 参数表示你希望集合中容纳的最大项数。如果底层集合已达到容量，而某个线程调用 **Add**，则生产线程将阻塞。如果愿意，生产线程可以调用 **TryAdd**，并传入超时时间（以毫秒为单位）和/或 **CancellationToken**，以便该线程阻塞，直到项被添加、超时到期或 **CancellationToken** 被取消（有关 **CancellationToken** 类的更多信息，参见第 26 章）。

**BlockingCollection** 类实现 **IDisposable** 接口。调用 **Dispose** 时，它会调用底层集合的 **Dispose**，还会释放该类内部用于阻塞生产者和消费者的两个 **SemaphoreSlim** 对象。

当生产者不再向集合中添加任何项时，生产者应调用 **CompleteAdding** 方法。这会向消费者发出信号，表示不会再有项被生产。具体来说，这会使使用 **GetConsumingEnumerable** 的 **foreach** 循环终止。下面的示例代码演示如何设置生产者/消费者场景并发出完成信号：

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

    Console.ReadLine();  // For testing purposes
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

执行上述代码时，我得到以下输出：

```text
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

如果你自己运行这段代码，**Producing** 和 **Consuming** 行可能会交错出现，但 **All items have been consumed** 行始终会在最后。

**BlockingCollection** 类还具有静态 **AddToAny**、**TryAddToAny**、**TakeFromAny** 和 **TryTakeFromAny** 方法。所有这些方法都接受一个 **BlockingCollection<T>[]**，以及一个项、一个超时时间和一个 **CancellationToken**。（**Try**）AddToAny 方法会遍历数组中的所有集合，直到找到一个因低于容量而可以接受该项的集合。（**Try**）TakeFromAny 方法会遍历数组中的所有集合，直到找到一个可以从中移除项的集合。

## 索引

### 符号与数字

- NET Framework。参见 Microsoft .NET Framework

### A

- abstract 关键字，167, 187
- 访问器方法
  - 可访问性，258
- AIP 支持，241-242
  - 定义，238
  - 泛型，258
  - 无参数属性以及，239-241
  - 性能注意事项，257
- Action 委托类型，422-423
- 地址空间布局随机化 (ASLR)，2
- 管理控制
  - 高级，84-89
  - 简单，61-64
- AIP（自动实现的属性），241-242
- AL.exe。参见程序集链接器实用工具
- 匿名类型，247-250
- APM（异步编程模型）
  - AsyncEnumerator 类以及，765-768
  - BeginXxx 方法，761-762, 769, 774, 776, 778
  - 与 EAP 比较，788
  - 计算密集型操作，774-776
  - 将 IAsyncResult 转换为任务，783-784
  - 缺点，765-766, 776-780
  - EndXxx 方法，761-762, 769, 774, 777-778
  - 异常以及，769-770
  - 异步实现服务器，773-774
  - 概述，761-765
- AppDomain 类，622
- AppDomainManager 类，615
- AppDomain
  - 跨边界访问对象，597-608
  - 高级宿主控制，615-620
  - 首次异常通知，612
  - GC 句柄表，555-557
  - 宿主支持，612-614
  - 监视，610-611
  - 概述，591, 594-597
  - 进程性能，16
  - 未处理异常，609
  - 卸载，609-610
- 参数。参见类型参数
- 算术运算，基元类型，117-120
- 元数，定义，284
- Array 类，281, 385, 392
- 数组
  - 访问性能，396-401
  - 强制转换，390-391
  - 定义，385
  - 派生自 Array 类，392
  - 固定大小，401-403
  - 实现接口，393-394
  - 初始化元素，388-389
  - 交错，387
  - 多维，387, 396
  - 非零下限，395-396
  - 概述，385-387
  - 传递/返回，394-395
  - SZ，387, 396
  - 不安全访问，401-403
- as 运算符，使用其进行强制转换，95-97
- ASLR（地址空间布局随机化），2
- ASP.NET Web Form，613-614, 770
- 程序集链接器 (AL.exe) 实用工具
  - 添加资源文件，52-53
  - 生成附属程序集，59
  - 命令行开关，88
  - 创建程序集，50-52
  - 延迟签名，78
  - 版本资源信息，53-56
- 程序集。另请参见强命名程序集
  - 添加模块，46
  - 添加资源文件，52-53
  - 添加到项目，49-50
  - 应用程序开发示例，20-21
  - 绑定，77
  - 生成，43, 45
  - 特征，43
  - 类支持，68
  - 合并托管代码，5-6
  - 合并模块，43-53
  - 控制成员访问，23-24
  - 使用程序集链接器创建，50-52
  - 区域性标记，58-59
  - 定义，5, 43, 101
  - 延迟签名，77-79
  - 执行代码，9-17
  - 友元，159-160
  - 种类，66-67
  - 命名空间以及，97-101
  - 重写，689-690
  - 打包，59-60
- Assembly 类
  - 私有部署，59–60
  - 探测，62–64
  - 反射支持，628
  - 注册，75
  - 附属，59
  - 自描述，6
  - 版本资源信息，53–58
- Assembly 类，622
- 程序集显示名称，68
- 程序集加载，621–625
- AssemblyDef 元数据表，45
- assemblyIdentity 元素，85–86
- AssemblyName 类，68
- AssemblyRef 元数据表，38, 621
- 赋值运算符，223
- AsyncEnumerator 类，765–768
- 异步异常，509
- 异步操作。另请参见 APM（异步编程模型）
  - 应用程序与线程模型，770–773
  - AsyncEnumerator 类以及，765–768
  - 缓存行，752–754
  - 取消，778
  - 协作式取消，722–726
  - 专用线程以及，704–705
  - 基于事件的模式，784–788
  - 执行上下文，721–722
  - 伪共享，752–754
  - I/O 操作，755–760
  - I/O 请求优先级，780–782
  - 实现服务器，773–774
  - 管理线程，750–752
  - 内存消耗，778
  - Parallel 类，739–743
  - 并行 LINQ，743–747
  - 定期，747–749
  - 简单，719–720
  - 支持的任务，726–739
  - 线程池以及，718–719
- 异步编程模型。参见 APM（异步编程模型）
- Attribute 类
  - 派生类，438
  - 匹配实例，448–451
  - 支持的方法，445–446
- 特性。参见自定义特性
- AttributeUsageAttribute 类，440–442
- 自动内存管理。参见垃圾回收
- 自动实现的属性 (AIP)，241–242

### B

- 后台线程，713–714
- Barrier 类，841–842
- 基类
  - 加载项支持，634–637
  - 设计注意事项，325–326
- before-field-init 语义，198
- 二元运算符，202
- 绑定
  - 程序集，77
  - 内存管理以及，658–659
  - 类型成员，650–659
  - 类型，83
- BindingFlags 枚举类型，643–644
- bindingRedirect 元素，85–86
- 位标志，379–383
- Boolean 类型，114, 181
- 装箱值类型
  - 更改字段，140–142
  - 可空，463
  - 对象相等性/同一性，143–146
  - 概述，127–140
- Byte 类型，114, 181
- 字节，编码/解码，361–369

### C

- 缓存行，752–754
- call (IL) 指令，168–170
- 回调函数，405–406
- 回调方法
  - 委托链，415–419
  - FirstChanceException，612
  - 调用，259, 408–410
- callvirt (IL) 指令，168–170
- CancellationTokenSource 类，723–726
- 取消
  - 异步操作，778
  - 操作，722–726
  - 任务，729–730
- CAS（代码访问安全），165
- 强制转换
  - 数组，390–391
  - 类型之间，93–95
  - 泛型类型变量，302
  - 使用 as 运算符，95–97
  - 使用 is 运算符，95–97
- catch 块，469–470, 494–495
- CER（受约束的执行区域），509–512
- Char 类型，114, 181, 327–329
- 字符
  - 编码/解码，361–369
  - 检查，343–345
- 子任务，733
- 类库，793–794
- 类。另请参见特定类型的类
  - 程序集支持，68

