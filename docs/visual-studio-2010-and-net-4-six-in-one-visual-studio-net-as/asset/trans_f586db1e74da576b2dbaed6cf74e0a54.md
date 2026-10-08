
源自 Task，因此你可以在任何地方将 Task 实例替换为 Task<Result> 实例。
当然，代表任务体的委托程序必须是 `Func<T>` 的实例，而不是 `Action` 实例，因为它们必须返回一个 `TResult`。可以通过 `Task<TResult>.Result` 属性查询已计算的值（对象）。

Result 具有非常实用的行为。如果任务尚未完成，Result 将在检索属性值之前等待任务完成。请注意，Result 不会启动任务，因此对于未运行的任务，你应该对 Result 进行无限期等待。

列表 10-16 显示了一个演示 `Task<Result>` 概念的简短示例。

# 列表 10-16：使用 Task<Result>

![](img/b5597c749e848b27b0d305153ae16106_488_0.png)

```sharp
using System;
using System.Threading;
using System.Threading.Tasks;

namespace TasksWithResults
{
    class Program
    {
        static void Main(string[] args)
        {
            var task1 = Task.Factory.StartNew<int>(() =>
            {
                int result = 0;
                for (int i = 0; i < 1000000; i++) result = i + i%10;
                return result;
            });
            var task2 = Task.Factory.StartNew<double>(() =>
            {
                double result = Math.PI;
                for (int i = 0; i < 10; i++)
                {
                    Thread.Sleep(10);
                    result *= (i+1)*Math.E;
                }
                return result;
            });
            var task3 = Task.Factory.StartNew<string>(() => "The result is: " +
                Console.WriteLine(task1.Result + task2.Result));
            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
        }
    }
}
```

代码文件 [Program.cs] 可在 Wrox.com 下载。

三个任务 task1、task2 和 task3 用于通过最后一条语句中的 `Console.WriteLine` 调用计算一个字符串。由于它们是占位计数器，因此非常适合演示。所有任务在实例化后立即启动，这种良好的流程在到达 `Console.WriteLine` 调用时，很有可能 task1 和 task3 已经完成，但 task2 还没有（因为内部有一个 `Thread.Sleep(10)` 调用）。然而，你不需要处理这种情况。`Result` 属性会确保在计算出最终结果之前，每个特定因素都已计算。

# 执行任务

在启动任务后，TPL 负责执行它们。归根结底，每个任务都是在 `System.Threading.ThreadPool` 和 `System.Threading.TaskScheduler` 类的帮助下在工作线程上执行的。TPL 不会为每个任务创建一个线程。它使用了一种更轻级的机制来提供并发性。

通过一个简单的示例更容易理解这种机制的本质。让我们假设一个代码应用程序按顺序创建了两个任务：Task 1 和 Task 2。随后，当 Task 2 运行时，它又创建了另外三个任务，即 Task 2A、Task 2B 和 Task 2C，同样遵循这个顺序。

![](img/b5597c749e848b27b0d305153ae16106_489_0.png)

现在，当 Task 2 创建新任务时，这些任务将进入 WT#N 的本地队列，而不是全局队列（Global Queue）。假设 WT#N 首先完成对 Task 2 的处理，稍后，WT#1 完成了对 Task 1 的处理。工作线程此时并不会停止，也不会变为其他工作项目的可用状态！图 10-20 显示了接下来发生了什么。

# CLR 线程池

![](img/b5597c749e848b27b0d305153ae16106_490_0.png)

图 10-20：工作窃（Work-stealing）

现在，WT#N 的本地队列不是空的；有三个任务等待执行。该线程从队列中取出 Task 2C（就像队列是一个栈一样）并开始执行它。但 Task 2C 是最新创建的任务，它在 Task 2A 和 2C 之后被放入本地队列的。为什么 WT#N 选取这一个而不是 Task 2A？原因是性能——因为 Task 2C 比 Task 2A 创建得晚，更有可能 Task 2C 的更多资源已缓存到内存中，供 Task 2A 的资源使用。

当 WT#1 完成时（稍晚于 WT#N），它发现自己的本地队列是空的。然而，它也查看了本地队列，发现 WT#N 的队列中有两个任务。WT#1 从 WT#N 的本地队列中“窃取”了 Task 2A 并开始执行。这被称为“工作窃”（work-stealing）术语。“被窃取”的任务是有意地从队列头部取出的，否则就是出于性能考虑。

如果 WT#N 完成 Task 2C 的时间早于 WT#1 完成 Task 2A，WT#N 将抓取 Task 2B 执行；否则，WT#1 将窃取它。

# 与任务相关的类型

有几种类型可以帮助你处理与任务相关的活动；它们大多数位于 `System.Threading.Tasks` 命名空间中。表 10-4 列出了它们并附有简要描述。

# 表 10-4：并发集合类

| TYPE NAME | DESCRIPTION |
|---|---|
| Task | 此类表示一个异步操作，并实现了之前讨论的任务抽象。 |
| Task<TResult> | 此类表示一个返回 TResult 类型的任务。 |
| TaskCanceledException | 此异常用于通信任务已取消。通过其 Task 属性可以访问已取消的任务。 |
| TaskCompletionSource<TResult> | 此类作为 Task<Result> 的生产者。 |
| TaskFactory, TaskFactory<Result> | 这些类提供了创建和调度任务的支持。其方法如 StartNew、ContinueAll、ContinueAny、FromAsync 以及泛型。 |
| TaskScheduler | 此类表示一个负责将任务调度到线程的对象。 |

# 协调数据结构

.NET Framework 4.0 引入了若干用于并行编程的新类型。这些类型被 TPL 和 PLINQ 执行引擎大量使用。它们仅供内部使用。此外，鼓励将它们构建到并发算法中这些类型可以分为以下几类：

- 并发集合类 —— `System.Collections.Concurrent` 中的集合类提供了线程安全的添加和删除操作。
- 同步原语 —— `System.Threading` 命名空间有了新的同步原语，通过避免遗留多线程代码中的昂贵锁实现了细粒度并发和更高的性能。
- 懒初始化类 —— 这些类帮助你将自定义类型封装在“懒”类中，直到需要时才分配内存和资源。
- 取消原语 —— 多线程中最困难的事情之一就是正确取消。取消原语可以帮助简化这一点。
