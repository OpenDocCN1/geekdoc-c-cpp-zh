
## 15.6.5 信号量

信号量类似于互斥体，不同之处在于信号量没有“所有者”——它与线程无关。任何线程都可以对信号量调用 Release，而对于 Mutex 和 lock，只有获得锁的线程才能释放它。信号量可用于限制并发——防止过多线程同时执行某段特定代码。

## 15.6.6 非阻塞同步

对于锁定，总有一个线程必须被阻塞，承受被临时取消调度所带来的开销和延迟。

.NET Framework 的非阻塞同步构造可以执行简单操作，而无需阻塞、暂停或等待。这些涉及使用严格原子性的指令，或指示编译器使用“volatile”读写语义。

## 两分题及答案

### Q.1 定义线程。解释多线程。

**答：** 线程是一组指令，执行时使程序能够进行并发处理。并发处理有助于同时执行多个进程。默认情况下，C# 只包含一个线程。可以创建其他线程，以与原始线程并行执行代码。

线程遵循生命周期：线程创建时开始，执行后立即终止。它使用的命名空间是 System.Threading，必须包含该命名空间才能创建线程并使用其成员。

通过扩展 Thread 类创建线程。Start() 方法标记线程执行的开始。

```csharp
// CallThread is our target method
ThreadStart methodThread = new ThreadStart(CallThread);
Thread childThread = new Thread(methodThread);
childThread.Start();
```

C# 还可以一次执行多个进程/任务，这通过在不同时间处理不同进程来实现，称为“多线程”。

其若干操作列出如下：
- Start
- Sleep
- Abort
- Suspend
- Resume
- Join

### Q.2 解释同步和异步操作。

**答：** 同步是一种创建线程安全代码的方式，在给定时间内只有一个线程访问该代码。同步调用会等待方法完成，然后继续程序流程。同步编程会对通常发生在用户尝试执行耗时操作时的 UI 操作产生不利影响，因为只使用了一个线程。

在异步操作中，方法调用立即返回，使程序能够执行其他操作，而被调用的方法在特定情况下完成其那部分工作。

### Q.3 什么是线程池？

**答：** 线程池是一组线程，它们执行任务而不干扰主线程。线程完成任务后，会返回主线程。

### Q.4 说明竞态条件。

**答：** 竞态条件发生在两个线程访问同一资源并试图同时修改它的情况下。无法预测哪个线程先访问资源。举一个小例子：两个线程 X1 和 X2 试图访问同一个名为 T 的共享资源。如果两个线程都试图向 T 写入值，那么最后写入 T 的值将被保存。

### Q.5 说出线程的不同状态。

**答：** 线程的不同状态如下：
- 未启动（Unstarted）：线程已创建
- 运行（Running）：线程开始执行
- 等待睡眠加入（WaitSleepJoin）：线程被要求睡眠、要求其他线程等待并要求其他线程加入
- 挂起（Suspended）：线程已被挂起
- 中止（Aborted）：线程已死亡但未改变状态
- 停止（Stopped）：线程已停止

### Q.6 线程类有哪些属性？

**答：** 线程类的属性如下：
- IsAlive：当线程处于活动状态时，其值为 true。
- Name：用于设置线程名称，也用于返回线程名称。
- Priority：返回根据操作系统设置的任务值。
- IsBackground：它是决定线程应位于后台还是前台的判定因素。
- ThreadState：说明线程的状态。

### Q.7 说出一些用于处理多线程操作的方法。

**答：** 以下是一些用于处理多线程操作的方法：
- Start
- Sleep
- Abort
- Suspend
- Resume
- Join

### Q.8 如何在 C# 中访问线程？AU : Dec.-19

**答：**
- 要访问主线程，需要 Thread 类对象来引用它。可以通过使用 Thread 类的 CurrentThread 属性创建该对象。它将返回对使用它的线程的引用。因此，当在主线程内部使用 CurrentThread 属性时，将获得主线程的引用。之后，就能像控制另一个线程一样控制主线程。一旦获得此控制权，那么如果应用程序中创建了更多线程，它们都可以使用 Thread 类进行访问。
- System.Threading 命名空间提供实现多线程编程的类和接口。此命名空间中的一个类是 Thread 类。此类用于创建和控制线程。

## 长答题

- Q.1 讨论 C# 线程。（参见第 15.1 节）
- Q.2 线程的优点和应用是什么？（参见第 15.5 节）
- Q.3 线程间通信如何发生？（参见第 15.6 节）
- Q.4 解释 C# 支持的线程编程类。（参见第 15.3 节）
- Q.5 讨论线程生命周期。（参见第 15.2 节）

### Q.6 编写一个 C# 程序以获取当前线程的状态。AU : Dec.-18, Marks 7

**答：**

```csharp
/*
 * C# Program to Obtain Status of the Current Thread
 */
using System;
using System.Threading;

namespace threademos
{
    class ProgramThreadStatus
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Current information");
            Thread t = Thread.CurrentThread;
            t.Name = "primarythread";
            Console.WriteLine("Thread Name: {0}", t.Name);
            Console.WriteLine("Thread Status: {0}", t.IsAlive);
            Console.ReadKey();
        }
    }
}
```

### Q.7 编写一个 C# 程序来说明向线程传递参数的概念。AU : May-18, Marks 6

**答：**

```csharp
/*
 * C# Program to illustrate the Concept of Passing Parameter for Thread
 */
using System;
using System.Threading;

public class ThreadDemo
{
    public static void Main()
    {
        Thread newThread = new Thread(ThreadDemo.task1);
        newThread.Start(20);
        ThreadDemo p = new ThreadDemo();
        newThread = new Thread(p.task2);
        newThread.Start("Instance");
```

## 笔记

# 第三单元

# 第16章

# ADO.NET 与事务

教学大纲：事务、ADO.NET

| 章节号 | 主题名称 | 页码 |
|---|---|---|
| 16.1 | ADO.NET——通过 .NET 环境处理数据 | 16-2 |
| 16.2 | 断开式数据访问体系结构 | 16-3 |
| 16.3 | 数据提供程序 | 16-4 |
| 16.4 | ADO.NET 对象 | 16-5 |
| 16.5 | 数据集 | 16-7 |
| 16.6 | 处理数据 | 16-8 |
| 16.7 | 使用 ADO.NET 进行异常处理 | 16-40 |
| 16.8 | ADO.NET 中的事务 | 16-44 |
|  | 两分题及答案 | 16-49 |
|  | 长答题 | 16-53 |

## 16.1 ADO.NET——通过 .NET 环境处理数据

AU : May-19

### 概念

- ADO.NET 是一组面向对象的库，允许开发者与数据源交互。通常，数据源是数据库，但也可能是文本文件、Excel 电子表格或 XML 文件。

### 说明

- 有许多不同类型的数据库可用于访问数据。例如，Microsoft SQL Server、Microsoft Access、Oracle、Borland Interbase 和 IBM DB2，仅举几例。

### ADO.NET 体系结构

![](img/3005a4307e6d8f3bb7e76eea28a92357_459_0.png)

图 16.1.1 ADO.NET 体系结构（标题）

### 3. ADO.NET 的优点

- ADO.NET 依赖于由 .NET 公共语言运行时定义的托管提供程序。
- ADO.NET 可以具有表示与不同数据源连接的独立对象。
- 在 ADO.NET 中，可以创建多个数据提供程序命名空间，以专门连接特定数据源，从而使访问更快、更高效，并允许每个命名空间利用其目标数据提供程序的功能。
- ADO.NET 提供使用客户端游标或服务器端游标的选择。

