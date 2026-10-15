

```
Console.Write('-');
}
    thread.Join();
}

public static void DoWork()
{
    for(int count = 0; count < Repetitions; count++)
    {
        Console.Write('+');
    }
}
```

# OUTPUT 18.1

![](img/25683ccec0773ba5b8794b11f2b12877_780_0.png)

正如你所见，线程似乎在轮流执行，每个线程在上下文切换前打印出几百个字符。两个循环是“并行”运行的，而不是先让第一个循环执行完再开始第二个循环，就像委托被同步执行时那样。

要让代码在不同线程的上下文中运行，你需要一个类型为 ThreadStart 或 ParameterizedThreadStart 的委托来标识要执行的代码。 后者允许一个类型为 object 的单个参数；两者都位于 System.Threading 命名空间中。 给定使用线程启动委托构造函数创建的 Thread 实例，你可以通过调用 thread.Start() 来启动线程执行。 Listing 18.1 显式创建了一个 ThreadStart 类型的变量，以在源代码中显示委托类型。 方法组 DoWork 本可以被直接传递给线程构造函数。 对 Thread.Start() 的调用告诉操作系统开始新线程的并发执行；主线程上的控制会立即从调用中返回并执行 Main() 方法中的 for 循环。 线程现在是独立的，并且在调用 Join() 之前彼此不会等待。

## 线程管理

线程包含许多用于管理其执行的方法和属性。以下是一些基本方法：

- 正如我们在 Listing 18.1 中看到的，你可以使用 Join() 使一个线程等待另一个线程。这告诉操作系统在另一个线程终止之前暂停当前线程的执行。 Join() 方法被重载以接受 int 或 TimeSpan，以支持在继续执行之前等待线程完成的最长时间。
- 默认情况下，新线程是“前台”线程；当其所有前台线程完成后，操作系统将终止进程。你可以通过将 IsBackground 属性设置为 true 来将线程标记为“后台”线程。然后操作系统将允许在后台线程仍在运行的情况下终止进程。然而，仍然最好确保所有线程都不会被中止，而是在进程退出前干净地退出；有关线程中止的更多细节，请参阅本章后面的部分。
- 每个线程都有一个关联的优先级，你可以通过将 Priority 属性设置为新的 ThreadPriority 枚举值来更改它。可能的值为 Lowest、BelowNormal、Normal、AboveNormal 和 Highest。操作系统更倾向于为更高优先级的线程调度时间片。小心；如果你设置优先级不正确，可能会出现“饥饿”情况，其中一个高优先级线程阻止许多低优先级线程永远运行。
- 如果你只是想知道线程是否仍“存活”或已完成所有工作，可以使用布尔值 `IsAlive` 属性。线程状态的更详细视图可通过 `ThreadState` 属性访问。 `ThreadState` 枚举值有 `Aborted`、`AbortRequested`、`Background`、`Running`、`Stopped`、`StopRequested`、`Suspended`、`SuspendRequested`、`Unstarted` 和 `WaitSleepJoin`。这些是标志；其中一些值可以组合。

有两种常用的、且常被滥用的用于控制线程的方法值得在各自的章节中讨论：`Sleep()` 和 `Abort()`。

## 不要在生产代码中让线程休眠

静态 `Thread.Sleep()` 方法使当前线程休眠，本质上是告诉操作系统在给定时间过去之前不要为此线程调度任何时间片。单个参数——要么是毫秒数，要么是 `TimeSpan`——指定操作系统在继续执行前等待多长时间。在等待期间，操作系统当然会为可能正在等待执行机会的任何其他线程调度时间片。这听起来似乎是个合理的做法，但它是一种“坏代码味道”，表明程序的设计可能可以更好。

线程经常被置于休眠状态以尝试将线程与某个时间事件同步。然而，操作系统并不保证其计时的任何精度。也就是说，如果你说“让我休眠 123 毫秒”，操作系统将使线程休眠 *至少* 123 毫秒，可能更长。线程从进入休眠到再次唤醒之间的实际时间是不确定的，可能任意长。不要尝试将 `Thread.Sleep()` 用作高精度计时器，因为它不是。

更糟的是，`Thread.Sleep()` 常常被用作“穷人的同步系统”。也就是说，如果你有一些异步工作，而当前线程在该工作完成前无法继续，你可能会诱惑线程休眠远长于你认为异步工作所需的时间，希望它在当前线程唤醒时已完成。这是个坏主意：异步工作本质上可能比你想象的要花费更长时间。使用下一章中描述的适当的线程同步机制来同步线程。 我们将在 Listing 18.2 中给出这种滥用的例子。

让线程休眠也是糟糕的编程实践，因为休眠的线程显然无法响应在其上运行代码的尝试。如果你让 Windows 应用程序的主线程休眠，该线程将不再处理来自用户界面的消息，因此看起来会挂起。

更一般地说，让线程休眠是糟糕的编程实践，因为分配线程这种昂贵资源的目的就是从该资源中获取工作。你不会付钱让员工睡觉，所以不要付出分配昂贵线程的代价，只为让它休眠数百万或数十亿个处理器周期。

话虽如此，Thread.Sleep() 也有一些有效用途。首先，使用零时间延迟让线程休眠告诉操作系统“当前线程礼貌地放弃其剩余的量子，如果有其他线程可以使用的话”。然后礼貌的线程将正常调度，而不会有进一步延迟。其次，Thread.Sleep() 常用于测试代码中，以模拟正在处理某种高延迟操作的线程，而无需真正消耗处理器做无意义的算术。生产代码中的其他用途应仔细审查，以确保没有更好的方法来获得所需效果。

在 C# 5 的基于任务的异步编程中，你可以在 Task.Delay() 方法的结果上使用 await 运算符来引入异步延迟，而不会阻塞当前线程。有关更多细节，请参阅第 19 章中的“计时器”部分。

## 指南

AVOID 在生产代码中调用 Thread.Sleep()。

## 不要在生产代码中中止线程

Thread 对象有一个 Abort() 方法，当执行时，尝试销毁线程。它通过导致运行时在线程中抛出 ThreadAbortException 来实现；此异常可以被捕获，但即使被捕获并忽略，它也会自动重新抛出以尝试

## 指南

AVOID 在生产代码中中止线程；这样做会导致不可预测的结果并可能使程序不稳定。

## 线程池

正如我们在“性能考虑”初学者主题中讨论的那样，过多的线程可能会对性能产生负面影响。线程是昂贵的资源，线程上下文切换不是免费的，并且通过时间片模拟并行运行两个作业可能比一个接一个运行慢得多。

为缓解这些问题，BCL 提供了线程池。不是直接分配线程，你可以告诉线程池你想要执行的工作。当工作完成后，线程不会终止并被销毁，而是返回到池中，从而节省了当有更多工作到来时分配新线程的成本。 Listing 18.2 展示了如何使用池化线程做与 Listing 18.1 相同的事情。

## LISTING 18.2: 使用 ThreadPool 而不是显式实例化线程

```
using System;
using System.Threading;

public class Program
{
    public const int Repetitions = 1000;
    public static void Main()
    {
        ThreadPool.QueueUserWorkItem(DoWork, '+');

        for(int count = 0; count < Repetitions; count++)
        {
            Console.Write('-');
        }

        // Pause until the thread completes.
        // This is for illustrative purposes; do not
        // use Thread.Sleep for synchronization in
        // production code.
        Thread.Sleep(1000);
    }
    public static void DoWork(object state)
    {
        for(int count = 0; count < Repetitions; count++)
```

