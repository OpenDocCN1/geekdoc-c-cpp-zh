
``` 
public abstract class WaitHandle : MarshalByRefObject, IDisposable {
// Close & Dispose 内部调用 Win32 CloseHandle 函数。
public virtual void Close();
public virtual void Dispose();

// WaitOne 调用 Win32 WaitForSingleObject 函数。
public virtual Boolean WaitOne();
public virtual Boolean WaitOne(Int32 millisecondsTimeout);

// WaitAny 调用 Win32 WaitForMultipleObjects 函数
public static Int32 WaitAny(WaitHandle[] handles);
public static Int32 WaitAny(WaitHandle[] handles, Int32 millisecondsTimeout);

// WaitAll 调用 Win32 WaitForMultipleObjects 函数
public static Boolean WaitAll(WaitHandle[] handles);
public static Boolean WaitAll(WaitHandle[] handles, Int32 millisecondsTimeout);

// SignalAndWait 内部调用 Win32 SignalObjectAndWait 函数
public static Int32 SignalAndWait(WaitHandle hToSignal, WaitHandle hWaitOn);
public static Int32 SignalAndWait(WaitHandle hToSignal, WaitHandle hWaitOn, 
Int32 millisecondsTimeout, Boolean exitContext)
```
```
// 使用此获取原始等待句柄的访问
public SafeWaitHandle SafeWaitHandle { get; set; }
```
```
// 当 WaitAny 发生超时时返回
public const Int32 Timeout = 0x102;
```

关于这些方法有几点需要注意：

- 你使用 `WaitHandle` 的 `Close`（或 `IDisposable` 的无参数 `Dispose` 方法）来关闭底层内核对象句柄。内部，这些方法调用 Win32 `CloseHandle` 函数。

- 你使用 `WaitHandle` 的 `WaitOne` 方法等待底层内核对象被信号。内部，此方法调用 Win32 `WaitForSingleObject` 函数。如果对象变为信号状态，则返回 true，如果发生超时则返回 false。

- 你使用 `WaitHandle` 的静态方法 `WaitAny` 等待 `WaitHandle[]` 中指定的任何内核对象变为信号。返回的 `Int32` 是对应变为信号的内核对象的数组索引，如果在等待期间没有对象变为信号，则返回 `WaitHandle.WaitTimeout`。内部，此方法调用 Win32 `WaitForMultipleObjects` 函数，并将 `bWaitAll` 参数设置为 `FALSE`。

- 你使用 `WaitHandle` 的静态方法 `WaitAll` 让调用线程等待由 `WaitHandle[]` 信号的所有内核对象。如果所有对象都变为信号，则返回 true，如果发生超时则返回 false。内部，此方法调用 Win32 `WaitForMultipleObjects` 函数，并将 `bWaitAll` 参数设置为 `TRUE`。

- 你传递给 `WaitAny` 和 `WaitAll` 方法的数组包含不超过 64 个元素，否则 `WaitHandle` 将抛出 `ArgumentException`。

- 你使用 `WaitHandle` 的 `SignalAndWait` 方法信号一个对象并等待其他对象被信号。返回的 `Int32` 是对应变为信号的内核对象的数组索引，如果在等待期间没有对象变为信号，则返回 `WaitHandle.WaitTimeout`。内部，此方法调用 Win32 `WaitForMultipleObjects` 函数，并将 `bWaitAll` 参数设置为 `FALSE`。

## 28 原始线程同步构造结构 815

- 你使用 `WaitHandle` 的 `SignalAndWait` 方法信号一个对象并等待其他对象被信号。返回的 `Int32` 是对应变为信号的内核对象的数组索引，如果在等待期间没有对象变为信号，则返回 `WaitHandle.WaitTimeout`。内部，此方法调用 Win32 `WaitForMultipleObjects` 函数，并将 `bWaitAll` 参数设置为 `FALSE`。

内核模式构造结构检测到资源竞争时，Windows 会阻塞丢失的线程，使其不会在 CPU 上自旋等待处理器。

- 内核模式构造结构可以同步原生线程和托管线程之间。

- 内核模式构造结构可以同步运行在同一台机器上不同进程中的线程。

- 内核模式构造结构可以应用安全设置，以防止未经的账户访问它们。

- 线程可以阻塞，直到集合中的所有内核模式构造结构可用，或者直到集合中的一个内核模式构造结构可用。

- 线程可以在一个指定了超时值的内核模式构造结构上阻塞；如果线程在规定时间内无法获得所需的资源，则线程将被解阻塞并执行其他任务。

两种原始内核模式线程同步构造结构是事件和信号量。其他内核模式构造结构（如互斥量 mutex）构建在原始构造结构之上。有关 Windows 内核构造结构的更多信息，请参阅我们的书籍*Windows C/C++, 5th Edition*(Microsoft Press, 2007)。

`System.Threading` 命名空间提供了一个名为 `WaitHandle` 的抽象类。`WaitHandle` 类是一个简单的类，其唯一目的是封装 Windows 内核对象句柄。FCL 提供了几个派自 `WaitHandle` 的类。所有类都定义在 `System.Threading` 命名空间中，除了 `Semaphore`（在 System.dll 中实现）外，所有类都在 CoreLib 中实现。类层次结构如下：

```
WaitHandle
  EventHandle
    AutoResetEvent
    ManualResetEvent
  Semaphore
  Mutex
```

内部，`WaitHandle` 基类有一个 `SafeWaitHandle` 字段，持有 Win32 内核对象句柄。该字段在构造具体的 `WaitHandle` 派生类时初始化。此外，`WaitHandle` 公共暴露了所有派生类继承的方法。在内核模式构造结构上调用的每个方法代表一次全内存屏。`WaitHandle` 的接口方法默认是公共的（未显示某些方法的某些重载）：

```
public abstract class WaitHandle : MarshalByRefObject, IDisposable {
// Close & Dispose 内部调用 Win32 CloseHandle 函数。
public virtual void Close();
public virtual void Dispose();

// WaitOne 调用 Win32 WaitForSingleObject 函数。
public virtual Boolean WaitOne();
public virtual Boolean WaitOne(Int32 millisecondsTimeout);

// WaitAny 调用 Win32 WaitForMultipleObjects 函数
public static Int32 WaitAny(WaitHandle[] handles);
public static Int32 WaitAny(WaitHandle[] handles, Int32 millisecondsTimeout);

// WaitAll 调用 Win32 WaitForMultipleObjects 函数
public static Boolean WaitAll(WaitHandle[] handles);
public static Boolean WaitAll(WaitHandle[] handles, Int32 millisecondsTimeout);

// SignalAndWait 内部调用 Win32 SignalObjectAndWait 函数
public static Int32 SignalAndWait(WaitHandle hToSignal, WaitHandle hWaitOn);
public static Int32 SignalAndWait(WaitHandle hToSignal, WaitHandle hWaitOn, 
Int32 millisecondsTimeout, Boolean exitContext)
```
```
// 使用此获取原始等待句柄的访问
public SafeWaitHandle SafeWaitHandle { get; set; }
```
```
// 当 WaitAny 发生超时时返回
public const Int32 Timeout = 0x102;
```

关于这些方法有几点需要注意：

- 你使用 `WaitHandle` 的 `Close`（或 `IDisposable` 的无参数 `Dispose` 方法）来关闭底层内核对象句柄。内部，这些方法调用 Win32 `CloseHandle` 函数。

- 你使用 `WaitHandle` 的 `WaitOne` 方法等待底层内核对象被信号。内部，此方法调用 Win32 `WaitForSingleObject` 函数。如果对象变为信号状态，则返回 true，如果发生超时则返回 false。

- 你使用 `WaitHandle` 的静态方法 `WaitAny` 等待 `WaitHandle[]` 中指定的任何内核对象变为信号。返回的 `Int32` 是对应变为信号的内核对象的数组索引，如果在等待期间没有对象变为信号，则返回 `WaitHandle.WaitTimeout`。内部，此方法调用 Win32 `WaitForMultipleObjects` 函数，并将 `bWaitAll` 参数设置为 `FALSE`。

- 你使用 `WaitHandle` 的静态方法 `WaitAll` 让调用线程等待由 `WaitHandle[]` 信号的所有内核对象。如果所有对象都变为信号，则返回 true，如果发生超时则返回 false。内部，此方法调用 Win32 `WaitForMultipleObjects` 函数，并将 `bWaitAll` 参数设置为 `TRUE`。

- 你传递给 `WaitAny` 和 `WaitAll` 方法的数组包含不超过 64 个元素，否则 `WaitHandle` 将抛出 `ArgumentException`。

- 你使用 `WaitHandle` 的 `SignalAndWait` 方法信号一个对象并等待其他对象被信号。返回的 `Int32` 是对应变为信号的内核对象的数组索引，如果在等待期间没有对象变为信号，则返回 `WaitHandle.WaitTimeout`。内部，此方法调用 Win32 `WaitForMultipleObjects` 函数，并将 `bWaitAll` 参数设置为 `FALSE`。

## 事件构造 (Event Constructs)

事件简单来说是由内核维护的布尔值变量。等待事件的线程在事件为 false 时会阻塞，在事件为 true 时会解除阻塞。事件有两种类型。当一个自动重置事件（auto-reset event）为 true 时，它会唤醒一个阻塞的线程，因为内核在解醒第一个线程后会自动将该事件重置为 false。当手动重置事件（manual-reset event）为 true 时，它会解锁所有等待它的线程，因为内核不会自动将事件重置为 false；你的代码必须手动将事件重置为 false。与事件相关的类如下：

```
public class EventWaitHandle : WaitHandle {
    public Boolean SetWait();      // 将布尔设置为 true; 总是返回 true
    public Boolean ResetEvent();    // 将布尔设置为 false; 总是返回 true
}
```
```
public sealed class AutoResetEvent : EventWaitHandle {
    public AutoResetEvent(boolean initialState);
}
```
```
public sealed class ManualResetEvent : EventWaitHandle {
    public ManualResetEvent(boolean initialState);
}
```

使用自动重置事件，我们可以轻松地创建一个线程同步锁，其行为类似于我之前展示的 `SimpleSpinLock`：

```
internal sealed class SimpleWaitLock : IDisposable {
    private Event m_ResourceFree = new AutoResetEvent(true); // 初始为空闲
```
```public
public void Enter() {
    // 在内核中高效地等待资源释放，然后返回
    m_ResourceFree.WaitOne();
}
```
```
public void Dispose() {
    m_ResourceFree.Dispose();
}
```

你使用 `SimpleWaitLock` 的方式与使用 `SimpleSpinLock` 完全相同。事实上，它们的持久行为是完全一样的；然而，这两个锁的性能有巨大差异。当锁上没有竞争时，`SimpleWaitLock` 比 `SimpleSpinLock` 慢得多，因为每次调用 `SimpleWaitLock` 的 `Enter` 和 `Leave` 方法都会强制调用线程从托管代码切换到内核并切回来——这是很糟糕的。但当发生竞争时，被内核阻塞的线程不会进行自旋并浪费 CPU 周期——这是很好的。另外请注意，构造 `AutoResetEvent` 对象并对其调用 `Dispose` 也会导致内核切换，对性能产生负面影响。这些调用通常很少发生，所以通常不需要担心。

为了让你对性能差异有更好的感受，我写了以下代码：

```
public static void main() {
    Int32 x = 0;
    const Int32 iterations = 100000000; // 1 亿次

    // 增加 1 亿次 x 需多长时间？
    Stopwatch sw = Stopwatch.StartNew();
    for (Int32 i = 0; i < iterations; i++) {
        x++;
    }
    Console.WriteLine("Incrementing x: {0:N0}", sw.Milliseconds);

    // 增加 1 亿次 x 需多长时间，
    // 额外加上一个什么都不做的方法的开销？
    sw.Restart();
    for (Int32 i = 0; i < iterations; i++) {
        M(); M();
    }
    Console.WriteLine("Incrementing x in M: {0:N0}", sw.Milliseconds);

    // 增加 1 亿次 x 需多长时间，
    // 加上无竞争的 SimpleSpinLock 的开销？
    SimpleSpinLock ssl = new SimpleSpinLock();
    sw.Restart();
    for (Int32 i = 0; i < iterations; i++) {
        ssl.Enter(); x++; ssl.Leave();
    }
    Console.WriteLine("Incrementing x in SimpleSpinLock: {0:N0}", sw.Milliseconds);

    // 增加 1 亿次 x 需多长时间，
    // 加上无竞争的 SimpleWaitLock 的开销？
    SimpleWaitLock swl = new SimpleWaitLock();
    sw.Restart();
    for (Int32 i = 0; i < iterations; i++) {
        swl.Enter(); x++; swl.Leave();
    }
    Console.WriteLine("Incrementing x in SimpleWaitLock: {0:N0}", sw.Milliseconds);
}

[MethodImpl(MethodImplOptions.NoInlining)]
private static void M() { /* 此方法什么都不做，直接返回 */ }
```

当我运行上面的代码时，我得到了以下输出：

Incrementing x: 8

Incrementing x in M: 50

Incrementing x in SimpleSpinLock: 219

Incrementing x in SimpleWaitLock: 17,615

# 第五部分 线程

# 第28 章 原始线程同步构造
