
当程序的某一部分正在通过互联网发送文件时，另一部分可以读取键盘输入，还有一部分可以缓冲下一个要发送的数据块。

线程可以处于几种状态之一。总体而言，它可以正在运行。它可以准备好在获得 CPU 时间后立即运行。正在运行的线程可以被挂起，即暂时停止其执行。之后可以恢复。一个线程在等待资源时可以被阻塞。一个线程可以被终止，在这种情况下其执行结束且无法恢复。

.NET Framework 定义了两种类型的线程：前台和后台。默认情况下，创建线程时它是前台线程，但你可以将其更改为后台线程。前台线程和后台线程之间的唯一区别是，当其进程中的所有前台线程都已停止时，后台线程将被自动终止。

随着基于线程的多任务处理而来的是对一种特殊功能的需求，称为同步，它允许线程的执行以某些明确定义的方式进行协调。C# 拥有一个专门用于同步的完整子系统，其关键特性也在这里描述。

所有进程至少有一个执行线程，通常称为主线程，因为它是程序开始时执行的线程。因此，主线程就是本书中前面示例程序一直使用的线程。从主线程中，你可以创建其他线程。

C# 和 .NET Framework 都支持基于进程和基于线程的多任务处理。因此，使用 C#，你可以创建和管理进程和线程。然而，启动新进程所需的编程工作很少，因为每个进程在很大程度上彼此独立。相反，C# 对多线程的支持才是重要的。由于对多线程的支持是内置的，C# 比某些其他语言更容易构建高性能的多线程程序。

支持多线程编程的类在 System.Threading 命名空间中定义。因此，你通常会在任何多线程程序的开头包含以下语句：

```
using System.Threading;
```

## 线程类

多线程系统建立在 Thread 类之上，该类封装了一个执行线程。Thread 类是密封的，这意味着它不能被继承。Thread 定义了多个方法和属性来帮助管理线程。本章将探讨其中一些最常用的成员。

## 创建和启动线程

创建和启动线程有多种方法。本节描述基本机制。本章后面将描述各种选项。

```
Thread.Sleep(100);
} while (mt.Count != 10);
}
Console.WriteLine("Main thread ending.");
}
```

让我们仔细看看这个程序。MyThread 定义了一个类，将用于创建第二个执行线程。在其 Run() 方法内部，建立了一个从 0 数到 9 的循环。注意对 Sleep() 的调用，它是 Thread 定义的静态方法。Sleep() 方法会导致调用它的线程暂停执行指定的毫秒数。当线程挂起时，另一个线程可以运行。程序中使用的形式如下所示：

```
public static void Sleep(int milliseconds)
```

要暂停的毫秒数以毫秒为单位指定。如果 milliseconds 为零，则调用线程仅被挂起以允许等待的线程执行。

在 Main() 内部，通过以下语句序列创建新的 Thread 对象：

```
// First, construct a MyThread object.
MyThread mt = new MyThread("Child #1");

// Next, construct a thread from that object.
Thread newThrd = new Thread(mt.Run);

// Finally, start execution of the thread.
newThrd.Start();
```

正如注释所建议的，首先创建 MyThread 的一个对象。然后使用该对象通过将 mt.Run() 方法作为入口点传递来构造 Thread 对象。最后，通过调用 Start() 启动新线程的执行。这会导致 mt.Run() 在其自己的线程中开始执行。调用 Start() 后，主线程的执行返回到 Main()，并进入 Main() 的 do 循环。两个线程继续运行，共享 CPU，直到它们的循环结束。该程序产生的输出如下。（你看到的确切输出可能会因执行环境、操作系统和任务负载的差异而略有不同。）

```
Main thread starting.
Child #1 starting.
.....In Child #1, Count is 0
.....In Child #1, Count is 1
.....In Child #1, Count is 2
.....In Child #1, Count is 3
.....In Child #1, Count is 4
.....In Child #1, Count is 5
.....In Child #1, Count is 6
.....In Child #1, Count is 7
.....In Child #1, Count is 8
.....In Child #1, Count is 9
Child #1 terminating.
Main thread ending.
```

在多线程程序中，通常希望主线程是最后一个完成运行的线程。从技术上讲，程序会一直运行直到其所有前台线程都已完成。因此，主线程最后完成并不是必需的。然而，这通常是良好的实践，因为它明确定义了程序的结束点。前面的程序试图通过在 Main() 的 do 循环中检查 Count 的值，在 Count 等于 10 时停止，并通过调用 Sleep() 来确保主线程最后完成。然而，这是一种不完美的方法。本章后面你将看到线程等待另一个线程完成更好的方法。

## 一些简单改进

虽然前面的程序完全有效，但一些简单的改进会使其更高效。首先，可以让线程在创建后立即开始执行。对于 MyThread 来说，这是在 MyThread 的构造函数内部实例化 Thread 对象来完成的。其次，MyThread 无需存储线程的名称，因为 Thread 定义了一个名为 Name 的属性，可用于此目的。Name 的定义如下：

```
public string Name { get; set; }
```

由于 Name 是一个读写属性，你可以使用它来设置线程的名称或检索线程的名称。

以下是对前一个程序进行这三项改进的版本：

```
// An alternate way to start a thread.

using System;
using System.Threading;

class MyThread {
    public int Count;
    public Thread Thrd;

    public MyThread(string name) {
        Count = 0;
        Thrd = new Thread(this.Run);
        Thrd.Name = name; // set the name of the thread
        Thrd.Start(); // start the thread
    }

    // Entry point of thread.
    void Run() {
        Console.WriteLine(Thrd.Name + " starting.");
        do {
            Thread.Sleep(500);
            Console.WriteLine("In " + Thrd.Name + ", Count is " + Count);
            Count++;
        } while (Count < 10);
        Console.WriteLine(Thrd.Name + " terminating.");
    }
}

class MultiThreadImproved {
    static void Main() {
Console.WriteLine("Main thread starting.");
// First, construct a MyThread object.
MyThread mt = new MyThread("Child #1");
do {
    Console.Write(".");
    Thread.Sleep(100);
} while (mt.Count != 10);
Console.WriteLine("Main thread ending.");
}
```

这个版本产生的输出与之前相同。请注意，线程对象存储在 MyThread 内部的 Thrd 中。

## 创建多个线程

前面的示例只创建了一个子线程。然而，你的程序可以根据需要生成任意数量的线程。例如，以下程序创建了三个子线程：

```
// Create multiple threads of execution.
using System;
using System.Threading;

class MyThread {
    public int Count;
    public Thread Thrd;

    public MyThread(string name) {
        Count = 0;
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {
        Console.WriteLine(Thrd.Name + " starting.");
        do {
            Thread.Sleep(500);
            Console.WriteLine("In " + Thrd.Name + ", Count is " + Count);
            Count++;
        } while (Count < 10);
        Console.WriteLine(Thrd.Name + " terminating.");
    }
}

