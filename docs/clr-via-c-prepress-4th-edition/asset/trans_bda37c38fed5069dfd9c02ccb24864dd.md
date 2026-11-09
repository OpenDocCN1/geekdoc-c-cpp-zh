
让 CPU 时间有机会运行。如果某个线程想要一个当前由另一个线程拥有的资源，它就会调用此方法。希望 Windows 会调度当前拥有该资源的线程，并且该线程会释放该资源。然后，当调用 Yield 的线程再次运行时，这个线程就能获得该资源。

Yield 是调用 Thread.Sleep(0) 和 Thread.Sleep(1) 的折中方案。Thread.Sleep(0) 不会让较低优先级的线程运行，而 Thread.Sleep(1) 总是会强制进行上下文切换，并且由于内部系统计时器的分辨率，Windows 会强制该线程休眠超过 1 毫秒。

超线程 CPU 实际上一次只让一个线程运行。因此，在这些 CPU 上执行自旋循环时，你需要强制当前线程暂停，以便 CPU 切换到另一个线程并允许它运行。线程可以通过调用 Thread 的 SpinWait 方法强制自己暂停，从而让超线程 CPU 切换到它的另一个线程：

```csharp
public static void SpinWait(Int32 iterations);
```

调用此方法实际上会执行一条特殊的 CPU 指令；它不会告诉 Windows 做任何事情（因为 Windows 已经认为它在该 CPU 上调度了两个线程）。在非超线程 CPU 上，这条特殊 CPU 指令会被直接忽略。

**注意** 有关这些方法的更多信息，请参阅它们在 Win32 中的对应项：Sleep、SwitchToThread 和 YieldProcessor。你还可以通过查找 Win32 的 timeBeginPeriod 和 timeEndPeriod 函数，了解更多关于调整系统计时器分辨率的信息。

FCL 还包含一个 System.Threading.SpinLock 结构，它类似于前面展示的 SimpleSpinLock 类，不同之处在于它使用 SpinWait 结构来提高性能。SpinLock 结构还提供超时支持。顺便提一下，有趣的是，我的 SimpleSpinLock 和 FCL 的 SpinLock 都是值类型。这意味着它们是轻量、内存友好的对象。例如，如果你需要将锁与集合中的每一项关联，SpinLock 是一个不错的选择。但是，你必须确保不要传递 SpinLock 实例，因为它们会被复制，你将失去任何及所有同步。另外，虽然你可以定义实例 SpinLock 字段，但不要将该字段标记为 readonly，因为随着锁被操作，其内部状态必须改变。

## Interlocked 任意操作模式

许多人查看 Interlocked 方法时会想，为什么 Microsoft 不创建一组更丰富的互锁方法，以便能在更广泛的场景中使用。例如，如果 Interlocked 类提供 Multiply、Divide、Minimum、Maximum、And、Or、Xor 以及许多其他方法，那就好了。虽然 Interlocked 类不提供这些方法，但有一个众所周知的模式，允许你通过使用 Interlocked.CompareExchange 以原子方式对 Int32 执行任何操作。事实上，由于 Interlocked.CompareExchange 会在 currentVal 中提供额外的值。如果这些值相同，那么没有线程在我们线程背后更改 target，target 现在包含 desiredVal 中的值，while 循环不再继续，方法返回。如果 startVal 不等于 currentVal，那么确实有线程在我们线程背后更改了 target 中的值，target 没有被改成 desiredVal 中的值，while 循环将再次循环并重试该操作，这一次使用反映另一个线程更改的 currentVal 中的值。

就个人而言，我在自己的许多代码中使用过这个模式，事实上，我还编写了一个泛型方法 Morph 来封装这个模式。<sup>71</sup>

```csharp
delegate Int32 Morpher<TResult, TArgument>(Int32 startValue, TArgument argument,
    out TResult morphResult);

static TResult Morph<TResult, TArgument>(ref Int32 target, TArgument argument,
    Morpher<TResult, TArgument> morpher) {

    TResult morphResult;
    Int32 currentVal = target, startVal, desiredVal;
    do {
        startVal = currentVal;
        desiredVal = morpher(startVal, argument, out morphResult);
        currentVal = Interlocked.CompareExchange(ref target, desiredVal, startVal);
    } while (startVal != currentVal);
    return morphResult;
}
```

### 内核模式构造

Windows 提供了几种用于同步线程的内核模式构造。内核模式构造比用户模式构造慢得多。这是因为它们需要 Windows 操作系统本身进行协调。此外，对内核对象的每次方法调用都会导致调用线程从托管代码转换到本机用户模式代码，再转换到本机内核模式代码，然后一路返回。这些转换需要大量 CPU 时间，如果频繁执行，可能会对你的应用程序的整体性能产生不利影响。

然而，与基本的用户模式构造相比，内核模式构造提供了一些好处，例如：

- 当内核模式构造检测到对资源的争用时，Windows 会阻塞竞争失败的线程，使其不会在 CPU 上自旋，从而浪费处理器资源。
- 内核模式构造可以使本机线程和托管线程彼此同步。
- 内核模式构造可以同步同一台机器上不同进程中运行的线程。
- 可以对内核模式构造应用安全设置，以防止未经授权的帐户访问它们。
- 线程可以阻塞，直到一组中的所有内核模式构造都可用，或直到该组中任意一个内核模式构造变为可用。
- 线程可以在指定超时值的情况下阻塞在内核模式构造上；如果该线程在指定时间内无法访问其所需的资源，那么该线程会被解除阻塞，并可以执行其他任务。

<sup>71</sup> 显然，由于要调用 morpher 回调方法，Morph 方法会带来性能损失。为了获得最佳性能，请像 Maximum 示例那样内联执行该操作。

两种基本的内核模式线程同步构造是事件和信号量。其他内核模式构造（例如互斥体）构建在这两种基本构造之上。有关 Windows 内核模式构造的更多信息，请参阅我的书 *Windows via C/C++（第 5 版）*（Microsoft Press，2007）。

System.Threading 命名空间提供了一个名为 WaitHandle 的抽象基类。WaitHandle 类是一个简单的类，其唯一目的是包装 Windows 内核对象句柄。FCL 提供了几个派生自 WaitHandle 的类。所有类都定义在 System.Threading 命名空间中。类层次结构如下：

```
WaitHandle
    EventWaitHandle
        AutoResetEvent
        ManualResetEvent
    Semaphore
    Mutex
```

在内部，WaitHandle 基类有一个 SafeWaitHandle 字段，用于保存 Win32 内核对象句柄。当构造具体的 WaitHandle 派生类时，该字段会被初始化。此外，WaitHandle 类公开提供了一些由所有派生类继承的方法。对内核模式构造调用的每个方法都代表一个完整的内存栅栏。WaitHandle 一些有意思的公共方法如下所示（某些方法的某些重载未显示）：

```csharp
public abstract class WaitHandle : MarshalByRefObject, IDisposable {
    // WaitOne internally calls the Win32 WaitForSingleObjectEx function.
    public virtual Boolean WaitOne();
    public virtual Boolean WaitOne(Int32 millisecondsTimeout);
    public virtual Boolean WaitOne(TimeSpan timeout);

    // WaitAll internally calls the Win32 WaitForMultipleObjectsEx function
    public static Boolean WaitAll(WaitHandle[] waitHandles);
    public static Boolean WaitAll(WaitHandle[] waitHandles, Int32 millisecondsTimeout);
    public static Boolean WaitAll(WaitHandle[] waitHandles, TimeSpan timeout);

    // WaitAny internally calls the Win32 WaitForMultipleObjectsEx function
    public static Int32 WaitAny(WaitHandle[] waitHandles);
    public static Int32 WaitAny(WaitHandle[] waitHandles, Int32 millisecondsTimeout);
    public static Int32
```
