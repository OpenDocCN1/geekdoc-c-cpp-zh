
```
lock (syncRoot)
{
    return ++state;
}
}
```

代码片段 SynchronizationSamples/SharedState.cs

然而，有一种更快的方式来锁定 state 的递增，如下所示。

## Interlocked

Interlocked 类用于使变量的简单语句具有原子性。i++ 不是线程安全的。i++ 包括从内存中获取值、将值递增 1、并将值写回内存。这些操作可能被线程调度程序中断。Interlocked 类提供了在线程安全方式下递增、递减、交换和读取值的方法。

使用 Interlocked 类比其他同步技术快得多。然而，你只能将其用于简单的同步问题。

例如，而不是使用 lock 语句在将 someState 设置为新值（当其为 null 时）时锁定对变量 someState 的访问，你可以使用更快的 Interlocked 类：

```
lock (this)
{
    if (someState == null)
    {
        someState = newState;
    }
}
```

代码片段 SynchronizationSamples/SharedState.cs

具有相同功能的更快版本使用 Interlocked.CompareExchange() 方法：

```
Interlocked.CompareExchange<SomeState>(ref someState, newState, null);
```

而是不要在 lock 语句内部执行递增：

```
public int State
{
    get
    {
        lock (this)
        {
            return ++state;
        }
    }
}
```

你可以使用更快的 Interlocked.Increment()：

```
public int State
{
    get
    {
        return Interlocked.Increment(ref state);
    }
}
```

## Monitor

C# 编译器将 lock 语句解析为使用 Monitor 类。下面的 lock 语句：

```
lock (obj)
{
    // synchronized region for obj
}
```

被解析为调用 Enter() 方法，该方法会等待线程获得对象的锁。一次只有一个线程可以成为对象锁的所有者。一旦锁被解除，线程就可以进入同步区。Monitor 类的 Exit() 方法释放锁。编译器将 Exit() 方法放入 try 块的 finally 处理程序中，以便在抛出异常时锁也能被释放。

> try/finally 在第 15 章“Errors and Exceptions”中有所介绍。

```
Monitor.Enter(obj);
try
{
    // synchronized region for obj
}
finally
{
    Monitor.Exit(obj);
}
```

代码片段 SynchronizationSamples/Program.cs

Monitor 类相比 C# 的 lock 语句具有很大的优势：你可以为等待获取锁添加超时值。因此，与无限期等待获取锁不同，你可以使用 TryEnter() 方法，在其中可以传递一个超时值来定义等待获取锁的最长时间。如果成功获取 obj 的锁，TryEnter() 将 Boolean ref 参数设为 true 并对对象 obj 保护的状态进行同步访问。如果 obj 被其他线程锁定超过 500 毫秒，TryEnter() 将变量 lockTaken 设为 false，线程不再等待而去做其他事情。也许在稍后某个时间，线程可以再次尝试获取锁。

```
bool lockTaken = false;
Monitor.TryEnter(obj, 500, ref lockTaken);
if (lockTaken)
{
    try
    {
        // acquired the lock
        // synchronized region for obj
    }
    finally
    {
        Monitor.Exit(obj);
    }
}
else
{
    // didn't get the lock, do something else
}
```

Mutex、EventWaitHandle 和 Semaphore 类都派生自基类 WaitHandle，因此你可以使用等待来使用所有这些类。

## Mutex

Mutex（互斥）是 .NET Framework 中的一个类，提供跨多个进程的同步。它与 Monitor 类非常相似，因为只有一个所有者。只有一个线程可以获得对互斥体的锁并访问由互斥体保护的同步代码区域。

使用 Mutex 类的构造函数，你可以定义互斥体是否应由调用线程初始拥有，为互斥体定义名称，并获取互斥体是否已存在的相关信息。在示例代码中，第三个参数被定义为 out 参数，用于接收互斥体是否新创建的布尔值。如果返回的值为 false，则互斥体已存在。互斥体可能在不同的进程中定义，因为带名称的互斥体为操作系统所知，并在不同进程间共享。如果互斥体未分配名称，则互斥体为无名且不在不同进程间共享。

```csharp
bool createdNew;
Mutex mutex = new Mutex(false, "ProCSharpMutex", out createdNew);
```

要打开已存在的互斥体，你也可以使用 Mutex.OpenExisting() 方法，它不需要与使用构造函数创建互斥体相同的 .NET 权限。

由于 Mutex 类派生自基类 WaitHandle，你可以执行 WaitOne() 来获取互斥体锁并在该期间成为互斥体的所有者。通过调用 ReleaseMutex() 方法释放互斥体。

```csharp
if (mutex.WaitOne())
{
    try
    {
        // synchronized region
    }
    finally
    {
        mutex.ReleaseMutex();
    }
}
else
{
    // some problem happened while waiting
}
```

由于命名互斥体在系统范围内已知，你可以使用它防止应用程序被启动两次。在下面的 Windows Forms 应用程序中，Mutex 对象的构造函数被调用。然后验证名称为 SingletonWinAppMutex 的互斥体是否已存在。如果存在，应用程序退出。

```csharp
static class Program
{
    [STAThread]
    static void Main()
    {
        bool createdNew;
        Mutex mutex = new Mutex(false, "SingletonWinAppMutex",
            out createdNew);
        if (!createdNew)
        {
            MessageBox.Show("You can only start one instance " +
                "of the application");
            Application.Exit();
            return;
        }
```

```
}

Application.EnableVisualStyles();
Application.SetCompatibleTextRenderingDefault(false);
Application.Run(new Form1());
}
```

## Semaphore

信号量与互斥体非常相似，但与之相反，信号量可以同时被多个线程使用。信号量是一个计数互斥体，这意味着使用信号量你可以定义允许同时访问信号量保护的资源 的线程数。这可以用于你有多个资源可用且只能允许特定数量的线程访问资源的情况。例如，假设你想访问系统上的物理 I/O 端口，并且有三个端口可用。因此，三个线程可以同时访问 I/O 端口，但第四个线程需要等待其中一个线程释放资源。

.NET 4 为你提供了两个具有信号量功能的类：Semaphore 和 SemaphoreSlim。Semaphore 可以命名、使用系统范围的资源并允许不同进程之间的同步。SemaphoreSlim 是轻量级版本，针对更短的等待时间进行了优化。

在示例应用程序中，在 Main() 方法中创建了六个线程和一个计数为 4 的信号量。在 Semaphore 类的构造函数中，你可以定义使用信号量可以获取的锁的数量（第二个参数）和初始可用的锁的数量（第一个参数）。如果第一个参数的值低于第二个参数，则两者之间的差值定义了已分配的信号量计数。与互斥体一样，你也可以为信号量分配名称以在不同进程间共享。这里未为信号量定义名称，因此它仅在此进程中使用。创建 SemaphoreSlim 对象后，启动了六个线程，它们都使用同一个信号量。

```
using System;
using System.Threading;
using System.Diagnostics;

namespace Wrox.ProCSharp.Threading
{
    class Program
    {
        static void Main()
        {
            int threadCount = 6;
            int semaphoreCount = 4;
            var semaphore = new SemaphoreSlim(semaphoreCount, semaphoreCount);
            var threads = new Thread[threadCount];

            for (int i = 0; i < threadCount; i++)
            {
                threads[i] = new Thread(ThreadMain);
                threads[i].Start(semaphore);
            }

            for (int i = 0; i < threadCount; i++)
            {
                threads[i].Join();
            }
            Console.WriteLine("*All threads finished*");
        }
    }
}
```
