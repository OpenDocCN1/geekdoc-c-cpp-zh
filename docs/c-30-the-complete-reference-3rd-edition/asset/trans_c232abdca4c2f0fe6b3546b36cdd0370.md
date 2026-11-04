

信号量已存在，此时 initial 和 max 的值将被忽略。（Semaphore 构造函数还有第三种形式，允许指定 SemaphoreSecurity 对象，用于控制访问。）使用命名信号量可以管理进程间同步。

## 使用事件

C# 支持另一种同步对象：事件。事件有两种类型：手动重置和自动重置。它们分别由 ManualResetEvent 和 AutoResetEvent 类支持。这些类派生自顶层类 EventWaitHandle。这些类用于一个线程等待另一个线程中发生某个事件的情况。当事件发生时，第二个线程向第一个线程发出信号，使其恢复执行。

ManualResetEvent 和 AutoResetEvent 的构造函数如下所示：

```
public ManualResetEvent(bool status)
public AutoResetEvent(bool status)
```

这里，如果 status 为 true，则事件初始为已发出信号状态。如果 status 为 false，则事件初始为未发出信号状态。

事件易于使用。对于 ManualResetEvent，过程如下。等待某个事件的线程只需在表示该事件的事件对象上调用 WaitOne()。如果事件对象处于已发出信号状态，WaitOne() 会立即返回。否则，它会暂停调用线程的执行，直到事件被发出信号。另一个线程执行事件后，该线程通过调用 Set() 将事件对象设置为已发出信号状态。因此，对 Set() 的调用可以理解为发出事件已发生的信号。事件对象被设置为已发出信号状态后，对 WaitOne() 的调用将返回，第一个线程将恢复执行。通过调用 Reset() 可将事件恢复为未发出信号状态。

AutoResetEvent 和 ManualResetEvent 的区别在于事件如何被重置。对于 ManualResetEvent，事件会一直保持已发出信号状态，直到调用 Reset()。对于 AutoResetEvent，一旦等待该事件的线程收到事件通知并恢复执行，事件就会自动变为未发出信号状态。因此，使用 AutoResetEvent 时不需要调用 Reset()。

下面是一个演示 ManualResetEvent 的示例：

```
// Use a manual event object.

using System;
using System.Threading;

// This thread signals the event passed to its constructor.
class MyThread {
    public Thread Thrd;
    ManualResetEvent mre;

    public MyThread(string name, ManualResetEvent evt) {
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        mre = evt;
        Thrd.Start();
    }
}
```
// Entry point of thread.
void Run() {
    Console.WriteLine("Inside thread " + Thrd.Name);
    for(int i=0; i<5; i++) {
        Console.WriteLine(Thrd.Name);
        Thread.Sleep(500);
    }
    Console.WriteLine(Thrd.Name + " Done!");
    // Signal the event.
    mre.Set();
}
class ManualEventDemo {
    static void Main() {
        ManualResetEvent evtObj = new ManualResetEvent(false);
        MyThread mt1 = new MyThread("Event Thread 1", evtObj);
        Console.WriteLine("Main thread waiting for event.");
        // Wait for signaled event.
        evtObj.WaitOne();
        Console.WriteLine("Main thread received first event.");
        // Reset the event.
        evtObj.Reset();
        mt1 = new MyThread("Event Thread 2", evtObj);
        // Wait for signaled event.
        evtObj.WaitOne();
        Console.WriteLine("Main thread received second event.");
    }
}
```

输出如下所示。（你看到实际输出可能略有不同。）

```
Inside thread Event Thread 1
Event Thread 1
Main thread waiting for event.
Event Thread 1
Event Thread 1
Event Thread 1
Event Thread 1
Event Thread 1 Done!
Main thread received first event.
Inside thread Event Thread 2
```

```
Event Thread 2
Event Thread 2
Event Thread 2
Event Thread 2
Event Thread 2
Event Thread 2
Event Thread 2 Done!
Main thread received second event.
```

首先，请注意 MyThread 在其构造函数中接收一个 ManualResetEvent。当 MyThread 的 Run() 方法结束时，它会在该事件对象上调用 Set()，这会将事件对象置于已发出信号状态。在 Main() 中，创建了一个名为 evtObj 的 ManualResetEvent，并将其传递给 MyThread。接下来，主线程等待该事件对象。由于 evtObj 的初始状态未发出信号，这会使主线程等待，直到 MyThread 的实例调用 Set()，从而将 evtObj 置于已发出信号状态。这使主线程能够再次运行。然后事件被重置，并对第二个线程重复该过程。如果不使用事件对象，所有线程将同时运行，其输出会混乱不堪。

在前面的程序中，如果使用 AutoResetEvent 对象而不是 ManualResetEvent 对象，则 Main() 中对 Reset() 的调用将不再需要。原因是当等待事件的线程恢复执行时，事件会自动设置为未发出信号状态。要做到这一点，只需将所有对 ManualResetEvent 的引用改为 AutoResetEvent，并移除对 Reset() 的调用。这个版本将像之前一样执行。

## Interlocked 类

与同步相关的另一个类是 Interlocked。当你只需要更改共享变量的值时，这个类提供了其他同步功能的替代方案。Interlocked 提供的方法保证其操作作为单个不可中断的操作执行。因此，不需要其他同步。Interlocked 提供静态方法，用于将两个整数相加、递增整数、递减整数、比较并设置对象、交换对象以及获取 64 位值。所有这些操作都在不中断的情况下进行。

下面的程序演示两个 Interlocked 方法：Increment() 和 Decrement()。这里将使用这些方法的以下形式：

```
public static int Increment(ref int v)
public static int Decrement(ref int v)
```

这里，v 是要递增或递减的值。

// Use Interlocked operations.

using System;
using System.Threading;

// A shared resource.
class SharedRes {
    public static int Count = 0;
}
```
```csharp
// This thread increments SharedRes.Count.
class IncThread {
    public Thread Thrd;

    public IncThread(string name) {
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {

        for(int i=0; i<5; i++) {
            Interlocked.Increment(ref SharedRes.Count);
            Console.WriteLine(Thrd.Name + " Count is " + SharedRes.Count);
        }
    }
}

// This thread decrements SharedRes.Count.
class DecThread {
    public Thread Thrd;

    public DecThread(string name) {
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {

        for(int i=0; i<5; i++) {
            Interlocked.Decrement(ref SharedRes.Count);
            Console.WriteLine(Thrd.Name + " Count is " + SharedRes.Count);
        }
    }
}

class InterlockedDemo {
    static void Main() {

        // Construct two threads.
        IncThread mt1 = new IncThread("Increment Thread");
        DecThread mt2 = new DecThread("Decrement Thread");

        mt1.Thrd.Join();
        mt2.Thrd.Join();
    }
}
```

## 终止线程

有时在线程正常结束之前停止它是有用的。例如，调试器可能需要停止一个失控的线程。线程一旦终止，就会从系统中移除，并且无法重新启动。

要在正常结束点之前终止线程，请使用 Thread.Abort()。其最简单的形式如下所示：

```
public void Abort()
```

Abort() 会导致向调用 Abort() 的线程抛出 ThreadAbortException。该异常会导致线程终止。你的代码也可以捕获此异常（但为了停止线程，它会自动重新抛出）。Abort() 可能并不总能立即停止线程，因此，如果必须确保线程在你的程序继续执行之前停止，你需要在调用 Abort() 之后再调用 Join()。此外，在极少数情况下，Abort() 可能无法停止线程。一种可能发生的情况是 finally 块进入无限循环。

下面的示例展示如何使用 Abort() 停止线程：

```
// Stopping a thread by use of Abort().
using System;
using System.Threading;

class MyThread {
    public Thread Thrd;

    public MyThread(string name) {
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // This is the entry point for thread.
    void Run() {
        Console.WriteLine(Thrd.Name + " starting.");
        for(int i = 1; i <= 1000; i++) {
            Console.Write(i + " ");
            if((i%10)==0) {
                Console.WriteLine();
                Thread.Sleep(250);
            }
        }
        Console.WriteLine(Thrd.Name + " exiting.");
    }
}

class StopDemo {
    static void Main() {

