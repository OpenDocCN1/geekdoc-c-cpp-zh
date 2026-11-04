
```csharp
MyThread mt1 = new MyThread("My Thread");

Thread.Sleep(1000); // let child thread start executing

Console.WriteLine("Stopping thread.");
mt1.Thrd.Abort();

mt1.Thrd.Join(); // wait for thread to terminate

Console.WriteLine("Main thread terminating.");
}
```

该程序的输出如下所示：

```
My Thread starting.
1 2 3 4 5 6 7 8 9 10
11 12 13 14 15 16 17 18 19 20
21 22 23 24 25 26 27 28 29 30
31 32 33 34 35 36 37 38 39 40
Stopping thread.
Main thread terminating.
```

> **注意** *Abort( )* 不应作为停止线程的常规手段。它适用于特殊场合。通常，线程应在其入口点方法返回时结束。

## Abort() 的另一种形式

在某些情况下，你可能会发现 **Abort( )** 的第二种形式很有用。其一般形式如下所示：

```csharp
public void Abort(object info)
```

这里，*info* 包含在停止线程时要传递给线程的任何信息。此信息可通过 **ThreadAbortException** 的 **ExceptionState** 属性访问。你可以使用它向线程传递终止代码。以下程序演示了 **Abort( )** 的这种形式：

```csharp
// Using Abort(object).

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
        try {
```

如果线程没有取消中止所需的适当安全设置，则对 ResetAbort() 的调用可能会失败。

以下程序演示了 ResetAbort()：

```csharp
// Using ResetAbort().
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
            try {
                Console.Write(i + " ");
                if((i%10)==0) {
                    Console.WriteLine();
                    Thread.Sleep(250);
                }
            } catch(ThreadAbortException exc) {
                if((int)exc.ExceptionState == 0) {
                    Console.WriteLine("Abort Cancelled! Code is " +
                        exc.ExceptionState);
                    Thread.ResetAbort();
                }
                else
                    Console.WriteLine("Thread aborting, code is " +
                        exc.ExceptionState);
            }
        }
        Console.WriteLine(Thrd.Name + " exiting normally.");
    }
}

class ResetAbort {
    static void Main() {
        MyThread mt1 = new MyThread("My Thread");

        Thread.Sleep(1000); // let child thread start executing

        Console.WriteLine("Stopping thread.");
        mt1.Thrd.Abort(0); // this won't stop the thread
        Thread.Sleep(1000); // let child execute a bit longer
        Console.WriteLine("Stopping thread.");
        mt1.Thrd.Abort(100); // this will stop the thread
        mt1.Thrd.Join(); // wait for thread to terminate
        Console.WriteLine("Main thread terminating.");
    }
}
```

输出如下所示：

```
My Thread starting.
1 2 3 4 5 6 7 8 9 10
11 12 13 14 15 16 17 18 19 20
21 22 23 24 25 26 27 28 29 30
31 32 33 34 35 36 37 38 39 40
Stopping thread.
Abort Cancelled! Code is 0
41 42 43 44 45 46 47 48 49 50
51 52 53 54 55 56 57 58 59 60
61 62 63 64 65 66 67 68 69 70
71 72 73 74 75 76 77 78 79 80
Stopping thread.
Thread aborting, code is 100
Main thread terminating.
```

在此示例中，如果调用 Abort() 时参数等于零，则线程通过调用 ResetAbort() 取消中止请求，线程继续执行。任何其他值都会导致线程停止。

## 挂起和恢复线程

在早期版本的 .NET Framework 中，可以通过调用 Thread.Suspend() 挂起线程，并通过调用 Thread.Resume() 恢复线程。然而，如今这两个方法都被标记为过时，不应在新代码中使用。一个原因是 Suspend() 本身很危险，因为它可用于挂起当前持有锁的线程，从而阻止锁被释放，导致死锁。这可能会引发系统范围的问题。必须使用 C# 的其他同步功能（例如互斥体）来挂起和恢复线程。

## 确定线程的状态

线程的状态可以从 Thread 提供的 ThreadState 属性获取。如下所示：

```csharp
public ThreadState ThreadState{ get; }
```

线程的状态以 ThreadState 枚举定义的值返回。它定义了以下值：

| ThreadState.Aborted | ThreadState.AbortRequested |
| ThreadState.Background | ThreadState.Running |
| ThreadState.Stopped | ThreadState.StopRequested |
| ThreadState.Suspended | ThreadState.SuspendRequested |
| ThreadState.Unstarted | ThreadState.WaitSleepJoin |

除一个值外，所有这些值都一目了然。需要稍作解释的是 ThreadState.WaitSleepJoin。当线程因调用 Wait()、Sleep() 或 Join() 而等待时，会进入此状态。

## 使用主线程

正如本章开头所述，所有 C# 程序都至少有一个执行线程，称为主线程，它在程序开始运行时自动提供给程序。主线程可以像所有其他线程一样处理。

要访问主线程，必须获取一个引用它的 Thread 对象。可以通过 Thread 的成员 CurrentThread 属性来实现。其一般形式如下所示：

```csharp
public static Thread CurrentThread{ get; }
```

此属性返回对其所在线程的引用。因此，如果在执行位于主线程内时使用 CurrentThread，你将获得对主线程的引用。一旦拥有此引用，就可以像任何其他线程一样控制主线程。

以下程序获取对主线程的引用，然后获取并设置主线程的名称和优先级：

```csharp
// Control the main thread.
using System;
using System.Threading;

class UseMain {
    static void Main() {
        Thread Thrd;

        // Get the main thread.
        Thrd = Thread.CurrentThread;

        // Display main thread's name.
        if(Thrd.Name == null)
            Console.WriteLine("Main thread has no name.");
        else
            Console.WriteLine("Main thread is called: " + Thrd.Name);

        // Display main thread's priority.
        Console.WriteLine("Priority: " + Thrd.Priority);
    }
}
```

```csharp
Console.WriteLine();

// Set the name and priority.
Console.WriteLine("Setting name and priority.\n");
Thrd.Name = "Main Thread";
Thrd.Priority = ThreadPriority.AboveNormal;

Console.WriteLine("Main thread is now called: " +
                  Thrd.Name);

Console.WriteLine("Priority is now: " +
                  Thrd.Priority);
}
```

该程序的输出如下所示：

```text
Main thread has no name.
Priority: Normal

Setting name and priority.

Main thread is now called: Main Thread
Priority is now: AboveNormal
```

提醒一句：你需要小心对主线程执行哪些操作。例如，如果将以下对 `Join()` 的调用添加到 `Main()` 的末尾，

```csharp
Thrd.Join();
```

程序将永远不会终止，因为它将等待主线程结束！

## 多线程提示

有效利用多线程的关键是并发思考，而不是串行思考。例如，当程序中有两个可以并发执行的子系统时，将它们做成单独的线程。然而，需要提醒一句。如果创建过多线程，实际上可能会降低程序性能，而不是提升性能。请记住，上下文切换会带来一些开销。如果创建过多线程，花在切换上下文上的 CPU 时间将比执行程序的时间更多！

## 启动单独的任务

尽管在 C# 编程中最常用的是基于线程的多任务处理，但在适当的情况下也可以利用基于进程的多任务处理。使用基于进程的多任务处理时，不是在同一程序内启动另一个线程，而是一个程序启动另一个程序的执行。在 C# 中，通过使用 `Process` 类来实现。`Process` 定义在 `System.Diagnostics` 命名空间中。作为本章的结尾，下面简要介绍如何启动和管理另一个进程。

启动另一个进程最简单的方法是使用 `Process` 定义的 `Start()` 方法。其最简单的一种形式如下所示：

```csharp
public static Process Start(string name)
```
