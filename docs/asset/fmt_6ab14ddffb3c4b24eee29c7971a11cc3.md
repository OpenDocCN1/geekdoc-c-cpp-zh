
即使 `lock` 与其同步的工作相比显得微不足道，程序员也应该避免无节目的同步，以避免发生死锁的可能，并避免在可能并行执行代码的多处理器计算机上产生不必要的同步。对象设计的通用最佳实践是同步可变的静态状态，而不是任何实例数据。（没有必要对永远不会改变的内容进行同步。）允许多个线程访问特定对象的程序员必须为该对象提供同步保护。任何显式处理线程的类都可能希望在某种程度上安全地管理线程。

# 无 await 的任务返回

在列表 22.1 中，尽管 `Task.Run(() => Decrement())` 返回一个 `Task`，但并没有使用 `await` 运算符。其原因是在 C# 7.1 之前，`Main()` 不支持使用 `async`。然而，考虑到 C# 7.1，代码可以重构为 `async/await` 模式，如列表 22.5 所示。

## 选择 lock 对象

无论是否显式使用 `lock` 关键字或 `Monitor` 类，程序员仔细选择 `lock` 对象都是至关重要的。

## 避免使用 MethodAttribute 进行同步

.NET 1.0 引入的一种同步机制是 `MethodAttribute`。通过结合 `MethodImplOptions.synchronized` 使用，该属性将方法标记为同步，以便同一时间只有一个线程可以执行该方法。

## 将字段声明为 volatile

有时，编译器或 CPU 可能会对代码进行优化，导致指令的执行顺序与代码编写不完全一致，或者某些指令被优化掉。这些优化在单线程执行时是无害的。然而，在多线程的情况下，此类优化可能会产生意外后果：优化可能会改变字段读写操作相对于另一个线程访问同一字段的执行顺序。

# 使用 System.Threading.Interlocked 类

到目前为止的互斥模式为处理进程（应用程序域）内的同步提供了最小的工具集。然而，使用 `System.Threading.Monitor` 进行同步是一项开销较大的操作，而处理器直接支持的替代方案针对的是同步模式。

列表 22.6 显示*只要前一个值为 null，则将 Data 设置为新值*。正如方法名所示，这种模式是比较/交换模式。`Interlocked.CompareExchange` 并不是在行为上等价的比较交换代码周围加锁，而是提供了一个内置的同步操作方法，对一个值（null）执行相同的操作，如果该值等于第二个参数，则更新第一个参数。表 22.2 显示了 `Interlocked` 支持的其他同步方法。

### 列表 22.6：使用 System.Threading.Interlocked 进行同步

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
| public static T CompareExchange<T>(T location, T value, T comparand); | 检查 `location` 是否等于 `comparand` 中的值。如果值相等，则将 `location` 设置为 `value` 并返回存储在 `location` 中的原始数据。 |

# 为什么要同步？

### 表 22.2：Interlocked 的同步相关方法（续）

| 方法签名 | 描述 |
| :--- | :--- |
| public static T Exchange<T>(T location, T value); | 将 `location` 赋值为 `value` 并返回之前的值。 |
| public static int Decrement(ref int location); | 将 `location` 减 1。它等同于 `--` 运算符，不同在于 `Decrement()` 是线程安全的。 |
| public static int Increment(ref int location); | 将 `location` 加 1。它等同于 `++` 运算符，不同在于 `Increment()` 是线程安全的。 |
| public static int Add(ref int location, int value); | 将 `value` 加到 `location` 并将结果赋值给 `location`。它等同于 `+=` 运算符。 |
| public static long Read(ref int location); | 在单次原子操作中返回 64 位值。 |

这些方法中的大多数都重载了额外的数据类型签名，以支持 `Long`。表 22.2 提供了通用的签名和描述。

注意，你可以使用 `Increment()` 和 `Decrement()` 来替代列表 22.5 中的同步 `++` 和 `--` 运算符，这样做会产生更好的性能。此外，请注意，如果另一个线程使用非 `interlocked` 方法访问 `_Count`，那么这两个访问将不会被同步。

# 多线程中的事件通知

这是开发者在触发事件时经常忽略同步的一个领域。用于发布事件的非安全线程代码与列表 22.7 类似。

### 列表 22.7：触发事件通知

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

只要此方法与事件订阅者之间没有产生竞态条件，此代码就是有效的。然而，代码不是原子的，因此多个线程可能会引入竞态条件。在检查 `OnTemperatureChange` 是否为 `null` 到到实际触发事件之间，`OnTemperatureChange` 可能会被设置为 `null`，从而抛出 `NullReferenceException`。换句话说，如果多个线程可能同时访问委托，则有必要对委托的赋值和触发进行同步。

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

随着同步的引入，出现了死锁的可能。当两个或多个线程等待对方释放资源时就会发生死锁。例如，假设线程 1 请求 `_Sync1` 的锁，然后请求 `_Sync2` 的锁。同时，线程 2 请求 `_Sync2` 的锁，然后请求 `_Sync1` 的锁。这为死锁埋定了基础。要发生死锁，必须满足四个基本条件：

- **互斥**：一个线程（线程 A）独占一个资源，其他任何线程（线程 B）都无法获取。
- **持有并等待**：一个持有互斥资源的线程（线程 A）正在等待获取另一个线程（线程 B）持有的资源。
- **非抢夺**：线程（线程 A）持有的资源不能被强制移除（线程 A 需要释放其资源）。
- **循环等待条件**：两个或多个线程形成一个环形链，它们锁定同一个或多个资源，并且每个线程都在等待链中下一个线程持有的资源。

消除这些条件中的任何一个都可以防止死锁。一种可能导致死锁的情况是，两个或多个线程请求同一个或多个同步目标（资源）的所有权，并且请求锁的顺序不同。当开发者仔细确保多次锁获取始终以相同的顺序发生时，就可以避免这种情况。另一个潜在的死锁原因是是非重入锁。当一个线程的锁可能会阻塞该线程本身——即它重新请求同一个锁——由于锁已被占用（被自己）而被阻塞，它不是重入的，额外的请求会导致死锁。

由 `lock` 关键字（带有底层 `Monitor` 类）生成的代码是重入的。然而，正如我们在“更多同步类型”节中看到的，某些锁类型不是重入的。

# 何时提供同步

如前所述，所有静态数据都应该是线程安全的。因此，同步需要围绕可变的静态数据。通常，程序员应该声明私有变量并提供修改数据的公共方法。如果存在多线程访问，此类方法应在内部处理同步。

相反，实例状态预计不包含同步。同步可能会显著降低性能并增加锁竞争或死锁的概率。除了专门设计用于多线程访问的类外，在多个线程间共享对象的程序员被期望自行处理所共享数据的的同步。

## 避免不必要的锁定

在不损害数据完整性的前提下，程序员应尽可能避免不必要的同步。例如，在线程之间您应该使用不可变类型，这样就不需要任何同步了（这种方法在 F# 等函数式编程语言中被证明极具价值）。同样，您应该避免对线程安全的操作进行加锁，例如小于原生（指针大小）整数的值的简单读写操作，因为此类操作是自动原子的。

## 指南

- **不要**以不同的顺序请求同一两个或多个同步同步目标的独占所有权。
- **务必**确保并发持有多个锁的代码以相同的顺序获取这些锁。
- **务必**将可变静态数据封装在公共 API 的同步逻辑中。
- **避免**对不大于原生（指针大小）整数的值的简单读取或写入进行同步，因为此类操作是自动原子的。

# 更多同步类型

除了 `System.Threading.Monitor` 和 `System.Threading.Interlocked` 之外，还有其他同步技术可用。

## 使用 System.Threading.Mutex

`System.Threading.Mutex` 在概念上与 `System.Threading.Monitor` 类相似（但不支持 `Pulse()` 方法），不同之处在于 `lock` 关键字没有使用它，并且 `Mutex` 可以命名，以便支持跨进程的同步。使用 `Mutex` 类，您可以同步对文件或某些跨进程资源的访问。由于 `Mutex` 是一种跨进程资源，.NET 2.0 增加了支持，允许通过 `System.Security.AccessControl.MutexSecurity` 对象设置访问控制。`Mutex` 类的一个用途是限制应用程序使其无法同时运行多次，如列表 22.9 结合输出 22.4 所示。

### 列表 22.9：创建一个单实例应用程序

```csharp
using System;
using System.Reflection;
using System.Threading;

public class Program
{
    public static void Main()
    {
        // 从全程序集（assembly）
        // 名称中获取互斥锁（mutex）名称。
        string mutexName = Assembly.GetEntryAssembly()!.FullName!;

        // firstApplicationInstance 指明
        // 是否为第一个
        // 应用程序实例。
        using Mutex mutex = new(false, mutexName,
            out bool firstApplicationInstance);

        if (!firstApplicationInstance)
        {
            Console.WriteLine("此应用程序已经在运行。");
        }
        else
        {
            Console.WriteLine("ENTER 退出");
            Console.ReadLine();
        }
    }
}
```

### 输出 22.4

ENTER 退出

当第一个实例仍在运行时，运行应用程序的第二个实例的结果将出现在输出 22.5 中。

## 为什么需要同步？

### 输出 22.5

此应用程序已经在运行。

在这种情况下，应用程序在机器上只能运行一次，即使是由不同的用户启动的。要限制每个用户只能运行一次，请可以在分配 `mutexName` 时将 `System.Environment.UserName`（这需要 Microsoft .NET Framework 或 .NET Standard 2.0）作为后缀。

`Mutex` 继承自 `System.Threading.WaitHandle`，因此包含了 `WaitAll()`、`WaitAny()` 和 `SignalAndWait()` 方法。这些方法允许它自动获取多个锁——这是 `Monitor` 不支持的。

## WaitHandle

`Mutex` 的基类是 `System.Threading.WaitHandle`。它是 `Mutex`、`EventWaitHandle` 和 `Semaphore` 同步类使用的基础同步类。`WaitHandle` 上的方法是 `WaitOne()` 方法，它会阻塞执行，直到 `WaitHandle` 实例被信号或被设置。`WaitOne()` 方法包含多个重载，允许无限等待：`void WaitOne()`、`以毫秒计时的等待；bool WaitOne(int milliseconds)` 以及 `bool WaitOne(TimeSpan timeout)`（基于 `TimeSpan` 的等待）。返回布尔值的版本将在 `WaitHandle` 在超时之前接收到信号时始终返回 `true` 值。

除了 `WaitHandle` 实例方法外，还有两个静态成员：`WaitAll()` 和 `WaitAny()`。与它们的亲属方法不同，这些静态成员支持超时。此外，它们接收一个数组形式的 `WaitHandles` 集合，以便它们能够响应来自集合内部的信号。

注意，`WaitHandle` 包含一个实现了 `IDisposable` 的句柄（类型为 `SafeWaitHandle`）。因此，需要确保在 `WaitHandles` 不再需要时对其进行释放（dispose）。

## 重置事件：ManualResetEvent 和 ManualResetEventSlim

控制线程中特定指令相对于另一个线程指令的执行不确定性的一种方法是使用重置事件（reset events）。尽管使用了“事件（events）”一词，但重置事件与 C# 的委托（delegates）和事件没有关系。相反，重置事件是一种强制代码等待另一个线程执行，直到另一个线程发送信号的方法。它们在测试多线程代码时特别有用，因为可以在验证结果之前等待某个特定状态。

重置事件有 `System.Threading.ManualResetEvent` 和 Microsoft .NET Framework 4 添加的轻量级版本 `System.Threading.ManualResetEventSlim`。（在接后的“高级主题：优先使用 ManualResetEvent 和 Semaphores 而非 AutoResetEvent”中讨论，还有第三种类型 `System.Threading.AutoResetEvent`，但程序员应避免使用）。重置事件的关键方法是 `Set()` 和 `Wait`（在 `ManualResetEvent` 上调用）。`Wait` 方法会导致线程阻塞，直到另一个线程调用 `Set()` 或等待超时。列表 22.10 展示了其工作原理，输出 22.6 显示了结果。

### 列表 22.10：等待 ManualResetEvent
