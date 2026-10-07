

## 避免不必要的锁定

在不损害数据完整性的前提下，程序员应尽可能避免不必要的同步。例如，在线程之间您应该使用不可变类型，这样就不需要任何同步了（这种方法在 F# 等函数式编程语言中被证明极具价值）。同样，您应该避免对线程安全的操作进行加锁，例如小于原生（指针大小）整数的值的简单读写操作，因为此类操作是自动原子的。

## 指南

-   **不要**以不同的顺序请求同一两个或多个同步同步目标的独占所有权。
-   **务必**确保并发持有多个锁的代码以相同的顺序获取这些锁。
-   **务必**将可变静态数据封装在公共 API 的同步逻辑中。
-   **避免**对不大于原生（指针大小）整数的值的简单读取或写入进行同步，因为此类操作是自动原子的。

## 更多同步类型

除了 System.Threading.Monitor 和 System.Threading.Interlocked 之外，还有其他同步技术可用。

## 使用 System.Threading.Mutex

System.Threading.Mutex 在概念上与 System.Threading.Monitor 类相似（但不支持 Pulse() 方法），不同之处在于 `lock` 关键字没有使用它，并且 Mutex 可以命名，以便支持跨进程的同步。使用 Mutex 类，您可以同步对文件或某些跨进程资源的访问。由于 Mutex 是一种跨进程资源，.NET 2.0 增加了支持，允许通过 System.Security.AccessControl.MutexSecurity 对象设置访问控制。Mutex 类的一个用途是限制应用程序使其无法同时运行多次，如列表 22.9 结合输出 22.4 所示。

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

在这种情况下，应用程序在机器上只能运行一次，即使是由不同的用户启动的。要限制每个用户只能运行一次，请可以在分配 mutexName 时将 System.Environment.UserName（这需要 Microsoft .NET Framework 或 .NET Standard 2.0）作为后缀。

Mutex 继承自 System.Threading.WaitHandle，因此包含了 WaitAll()、WaitAny() 和 SignalAndWait() 方法。这些方法允许它自动获取多个锁——这是 Monitor 不支持的。

## WaitHandle

Mutex 的基类是 System.Threading.WaitHandle。它是 Mutex、EventWaitHandle 和 Semaphore 同步类使用的基础同步类。WaitHandle 上的方法是 WaitOne() 方法，它会阻塞执行，直到 WaitHandle 实例被信号或被设置。WaitOne() 方法包含多个重载，允许无限等待：void WaitOne()、以毫秒计时的等待；bool WaitOne(int milliseconds) 以及 bool WaitOne(TimeSpan timeout)（基于 TimeSpan 的等待）。返回布尔值的版本将在 WaitHandle 在超时之前接收到信号时始终返回 `true` 值。

除了 WaitHandle 实例方法外，还有两个静态成员：WaitAll() 和 WaitAny()。与它们的亲属方法不同，这些静态成员支持超时。此外，它们接收一个数组形式的 WaitHandles 集合，以便它们能够响应来自集合内部的信号。

注意，WaitHandle 包含一个实现了 IDisposable 的句柄（类型为 `SafeWaitHandle`）。因此，需要确保在 WaitHandles 不再需要时对其进行释放（dispose）。

## 重置事件：ManualResetEvent 和 ManualResetEventSlim

控制线程中特定指令相对于另一个线程指令的执行不确定性的一种方法是使用重置事件（reset events）。尽管使用了“事件（events）”一词，但重置事件与 C# 的委托（delegates）和事件没有关系。相反，重置事件是一种强制代码等待另一个线程执行，直到另一个线程发送信号的方法。它们在测试多线程代码时特别有用，因为可以在验证结果之前等待某个特定状态。

重置事件有 System.Threading.ManualResetEvent 和 Microsoft .NET Framework 4 添加的轻量级版本 System.Threading.ManualResetEventSlim。（在接后的“高级主题：优先使用 ManualResetEvent 和 Semaphores 而非 AutoResetEvent”中讨论，还有第三种类型 System.Threading.AutoResetEvent，但程序员应避免使用）。重置事件的关键方法是 Set() 和 Wait（在 ManualResetEvent 上调用）。Wait 方法会导致线程阻塞，直到另一个线程调用 Set() 或等待超时。列表 22.10 展示了其工作原理，输出 22.6 显示了结果。

### 列表 22.10：等待 ManualResetEvent

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    static ManualResetEventSlim _MainResetEvent = new();
    static ManualResetEventSlim _DoWorkResetEvent = new();

    public static void Main()
    {
        using (_MainResetEvent = new());
        using (_DoWorkResetEvent = new());
        Console.WriteLine("应用程序已启动...");
        Console.WriteLine("启动线程...");

        // 用于 .NET 4.0 的 Task 替换
        Task task = Task.Run(() => DoWork());

        // 等待 DoWork() 执行
        _DoWorkResetEvent.Wait();
        Console.WriteLine("等待线程执行...");
        _MainResetEvent.Set();
        task.Wait();
        Console.WriteLine("线程已完成");
        Console.WriteLine("应用程序正在退出...");
    }

    static void DoWork()
    {
        Console.WriteLine("DoWork 已启动...");
        _DoWorkResetEvent.Set();
        _MainResetEvent.Wait();
        Console.WriteLine("DoWork 结束...");
    }
}
```

### 输出 22.6

应用程序已启动...
启动线程...
DoWork 已启动...
等待线程执行...
DoWork 结束...
线程已完成
应用程序正在退出...

列表 22.10 首先实例化并启动新的 Task。表格 22.3 显示了执行路径，每列代表一个线程。在代码出现在同一行的情况下，不确定由哪侧先执行。

| 表格 22.3：带有 ManualResetEvent 同步的执行路径 | Main() | DoWork() |
| :--- | :--- |
| Console.WriteLine("应用程序已启动..."); | |
| Task task = new Task(DoWork); | |
| Console.WriteLine("启动线程..."); | |
| task.Start(); | |
| _DoWorkResetEvent.Wait(); | Console.WriteLine("DoWork 已启动..."); |
| | _DoWorkResetEvent.Set(); |
| Console.WriteLine("等待线程执行..."); | _MainResetEvent.Wait(); |
| _MainResetEvent.Set(); | Console.WriteLine("DoWork 结束..."); |
| task.Wait(); | |
| Console.WriteLine("应用程序正在退出..."); | |

