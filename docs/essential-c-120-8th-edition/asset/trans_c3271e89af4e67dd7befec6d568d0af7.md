

# 使用 System.Threading.Interlocked 类

到目前为止的互斥模式为处理进程（应用程序域）内的同步提供了最小的工具集。然而，使用 System.Threading.Monitor 进行同步是一项开销较大的操作，而处理器直接支持的替代方案针对的是同步模式。

列表 22.6 显示*只要前一个值为 null，则将 Data 设置为新值*。正如方法名所示，这种模式是比较/交换模式。Interlocked.CompareExchange 并不是在行为上等价的比较交换代码周围加锁，而是提供了一个内置的同步操作方法，对一个值（null）执行相同的操作，如果该值等于第二个参数，则更新第一个参数。表 22.2 显示了 Interlocked 支持的其他同步方法。

列表 22.6：使用 System.Threading.Interlocked 进行同步

```csharp
public class SynchronizationUsingInterlocked
{
    private static object? _Data;

    // 如果未赋值，则初始化数据
    public static void Initialize(object newValue)
    {
        // 如果 _Data 为 null，则将其设置为 newValue
        Interlocked.CompareExchange(
            ref _Data, newValue, null);
    }
    
    // ...
}
```

# 表 22.2：Interlocked 的同步相关方法

| 方法签名 | 描述 |
| :--- | :--- |
| public static T CompareExchange<T>(T location, T value, T comparand); | 检查 location 是否等于 comparand 中的值。如果值相等，则将 location 设置为 value 并返回存储在 location 中的原始数据。 |

# 为什么要同步？

表 22.2：Interlocked 的同步相关方法（续）

| 方法签名 | 描述 |
| :--- | :--- |
| public static T Exchange<T>(T location, T value); | 将 location 赋值为 value 并返回之前的值。 |
| public static int Decrement(ref int location); | 将 location 减 1。它等同于 -- 运算符，不同在于 Decrement() 是线程安全的。 |
| public static int Increment(ref int location); | 将 location 加 1。它等同于 ++ 运算符，不同在于 Increment() 是线程安全的。 |
| public static int Add(ref int location, int value); | 将 value 加到 location 并将结果赋值给 location。它等同于 += 运算符。 |
| public static long Read(ref int location); | 在单次原子操作中返回 64 位值。 |

这些方法中的大多数都重载了额外的数据类型签名，以支持 Long。表 22.2 提供了通用的签名和描述。
注意，你可以使用 Increment() 和 Decrement() 来替代列表 22.5 中的同步 ++ 和 -- 运算符，这样做会产生更好的性能。此外，请注意，如果另一个线程使用非 interlocked 方法访问 _Count，那么这两个访问将不会被同步。

# 多线程中的事件通知

这是开发者在触发事件时经常忽略同步的一个领域。用于发布事件的非安全线程代码与列表 22.7 类似。

列表 22.7：触发事件通知

```csharp
// 线程安全
if (OnTemperatureChanged != null)
{
    // 调用订阅者
    OnTemperatureChanged(
```

# 第 22 章：线程同步

```csharp
    this, new TemperatureEventArgs(value);
}
```

只要此方法与事件订阅者之间没有产生竞态条件，此代码就是有效的。然而，代码不是原子的，因此多个线程可能会引入竞态条件。在检查 OnTemperatureChange 是否为 null 到到实际触发事件之间，OnTemperatureChange 可能会被设置为 null，从而抛出 NullReferenceException。换句话说，如果多个线程可能同时访问委托，则有必要对委托的赋值和触发进行同步。

所需要的仅仅是使用空条件操作符：

```csharp
OnTemperature?.Invoke(
    this, new TemperatureEventArgs( value ));
```

空条件操作符专门设计为是原子的，因此委托的调用实际上是原子的。关键点——显然——是记住利用空条件操作符。

尽管这需要更多的代码，但线程安全的委托调用并不困难。这种方法之所以有效，是因为添加和移除监听器的运算符是线程安全且静态的（运算符重载是通过静态方法完成的）。为了修正列表 22.7 并使其线程安全，请分配。

# 列表 22.8：线程安全的事件通知

```csharp
// 线程安全
var handler = OnTemperatureChanged;
if (handler != null)
{
    // 调用订阅者
    handler(this, new TemperatureEventArgs(value));
}
```

# 同步设计实践

随着同步的引入，出现了一些处理这些复杂性的最佳实践。

# 避免死锁

随着同步的引入，出现了死锁的可能。当两个或多个线程等待对方释放资源时就会发生死锁。例如，假设线程 1 请求 _Sync1 的锁，然后请求 _Sync2 的锁。同时，线程 2 请求 _Sync2 的锁，然后请求 _Sync1 的锁。这为死锁埋定了基础。要发生死锁，必须满足四个基本条件：

-   **互斥**：一个线程（线程 A）独占一个资源，其他任何线程（线程 B）都无法获取。
-   **持有并等待**：一个持有互斥资源的线程（线程 A）正在等待获取另一个线程（线程 B）持有的资源。
-   **非抢夺**：线程（线程 A）持有的资源不能被强制移除（线程 A 需要释放其资源）。
-   **循环等待条件**：两个或多个线程形成一个环形链，它们锁定同一个或多个资源，并且每个线程都在等待链中下一个线程持有的资源。

消除这些条件中的任何一个都可以防止死锁。一种可能导致死锁的情况是，两个或多个线程请求同一个或多个同步目标（资源）的所有权，并且请求锁的顺序不同。当开发者仔细确保多次锁获取始终以相同的顺序发生时，就可以避免这种情况。另一个潜在的死锁原因是是非重入锁。当一个线程的锁可能会阻塞该线程本身——即它重新请求同一个锁——由于锁已被占用（被自己）而被阻塞，它不是重入的，额外的请求会导致死锁。

由 lock 关键字（带有底层 Monitor 类）生成的代码是重入的。然而，正如我们在“更多同步类型”节中看到的，某些锁类型不是重入的。

# 何时提供同步

如前所述，所有静态数据都应该是线程安全的。因此，同步需要围绕可变的静态数据。通常，程序员应该声明私有变量并提供修改数据的公共方法。如果存在多线程访问，此类方法应在内部处理同步。

相反，实例状态预计不包含同步。同步可能会显著降低性能并增加锁竞争或死锁的概率。除了专门设计用于多线程访问的类外，在多个线程间共享对象的程序员被期望自行处理所共享数据的的同步。

