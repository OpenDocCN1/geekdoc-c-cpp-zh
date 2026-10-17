
这一系列事件——处理程序执行、结束后进程崩溃——是典型的但并非绝对的。一旦程序中出现未处理异常，一切都变得不可控；程序现在处于不稳定状态。在本章前面的部分，我们描述了为什么粗暴地中止线程是一个坏主意。TPL 使用协作取消，这是一种更礼貌、健壮且可靠的技术，用于安全取消不再需要的任务。任务通过 `CancellationToken`（位于 `System.Threading` 命名空间）支持取消，通过定期轮询它来查看是否发起了取消请求。代码列表 19.8 演示了取消请求及其响应。输出 19.5 显示了结果。

- 避免编写在任何线程上产生未处理异常的程序。
- 考虑注册未处理异常事件，用于调试、日志记录和紧急关闭目的。
- 取消未完成的任务，而不是让它们在应用程序关闭期间继续运行。

![](img/b18af4770e91956282437ff1469b4_881_0.png)

# 输出 19.5

按回车退出。

3.1415926535897323846264338327950288419716939937510582097494592307816

40628628099862803842352411706928140086531282306647938446095508223172

535904812841117450

任务开始后，`Console.Read()` 会阻塞主线程。

与此同时，任务继续执行，计算 pi 的下一位并打印出来。当用户按下回车时，执行遇到一个调用 `CancellationTokenSource.Cancel()`。在列表 19.8 中，我们将 `task.Cancel()` 的调用与 `task.Wait()` 的调用分开，并在它们之间打印了一行星号。此目的是为了说明在取消令牌被观察到之前，可能会发生额外的迭代——因此在输出 19.5 中，任务后面多了一个 2。这个 2 的出现是因为 `CancellationTokenSource.Cancel()` 不会粗暴地停止任务的执行。任务会一直运行，直到它检查令牌，并在发现令牌所有者请求取消任务时，才会礼貌地关闭。

`Cancel()` 调用有效地设置了所有从 `CancellationSourceToken` 拷贝的取消令牌上的 `IsCancellationRequested` 属性。然而，有几点需要注意：

- 传递给异步任务的是 `CancellationToken` 而不是 `CancellationSource`。`CancellationToken` 允许对取消请求进行轮询；`CancellationSource` 提供令牌并在被取消时发出信号（见图 19.3）。通过传递 `CancellationToken` 而不是 `CancellationSource`，我们就不需要担心 `CancellationSource` 上的线程同步问题，因为后者仅对原始线程可见。
- `CancellationToken` 是一个结构体（struct），因此它是按值拷贝的。`CancellationSource.Token` 返回的值产生令牌的副本。由于 `CancellationToken` 是值类型且创建了副本，这导致了对 `CancellationSource.Token` 的线程安全访问——它仅在 `WritePi()` 方法内部可用。

![](img/b18af4770e9195628243fa73ff1469b4_883_0.png)

# 第 19 章：引入多线程

IDisposable

![](img/b18af4770e9195628243fa73ff1469b4_884_0.png)

图 19.3：CancellationTokenSource 和 CancellationToken 类图

为了监控 `IsCancellationRequested` 属性，一个从 `CancellationSourceToken` 获取的 `CancellationToken` 副本被传递给任务。在列表 19.7 中，我们随后会偶尔检查 `CancellationToken` 参数上的 `IsCancellationRequested` 属性；在这种情况下，我们在每次计算数字后进行检查。如果 `IsCancellationRequested` 返回 `true`，则 `while` 循环退出。与基本上在随机点抛出异常的线程强制终止不同，我们使用正常的控制流退出循环。我们通过频繁轮询，保证了代码对取消请求的响应性。

关于 `CancellationToken` 的重载 `Register()` 方法，有一点需要注意。通过此方法，你可以注册一个在令牌被取消时将调用的动作（action）。换句话说，调用 `Register()` 方法相当于订阅了相应 `CancellationSource` 的 `Cancel()` 方法上的一个监听委托（delegate）。

鉴于在完成之前取消是该程序的预期行为，列表 19.7 中的代码没有抛出 `System.Threading.Tasks.TaskCanceledException`。因此，`task.Status` 返回 `TaskStatus.RanToCompletion`——这没有指示任务的工作实际上被取消了。在例示例中，不需要这样的指示；但 TPL（任务并行库）确实包含了此功能。如果取消调用在某种程度上具有破坏性——例如阻止有效结果的返回——那么抛出 `TaskCanceledException`（派自 `System.OperationCanceledException`）将是 TPL 的处理模式。`CancellationToken` 并不是抛出异常，而是包含一个 `ThrowIfCancellationRequested()` 方法以便更轻松地报告异常，假设 `CancellationToken` 实例可用。

如果你尝试对抛出 `TaskCanceledException` 的任务调用 `Wait()`（或获取 `Result`），其行为与任务中抛出任何异常相同：该调用将抛出一个 `AggregateException`。该异常是在任务执行可能不完整的情况下通信执行状态的手段。与所有预期工作都成功执行的已完成任务不同，被取消的任务可能有部分完成的工作——工作状态是不可信的。

此示例演示了长时间的 CPU 密集型操作（几乎无限地计算 pi）如何监控取消请求并在发生请求时做出响应。然而，在某些情况下，取消可以在未在目标任务中显式编写代码的情况下发生。例如，第 21 章讨论的 `Parallel` 类默认就提供了这种行为。

> 指南
>
> 务必取消未完成的任务，而不是让它们在应用程序关闭期间继续运行。

# Task.Run(): Task.Factory.StartNew() 的快捷方式与简化

在 .NET 中，获取任务的通用做法是 `Task.Factory.StartNew`。在 .NET 4.5 中，通过 `Task.Run()` 提供了一种更简单的方法。`Task.Run()` 不支持 `TaskCreationOptions` 参数。如果你需要该参数，则应使用 `Task.Factory.StartNew`。

## 使用 System.Threading

并行扩展库（Parallel Extensions Library）极其有用，因为它允许你操作更高层次的抽象——任务（task），而不是直接操作线程。有时，你可能需要处理在 TPL 和 PLINQ 出现之前（.NET 4.0 之前）编写的代码，或者你可能遇到了一个它们无法直接解决的编程问题。为了实现这一点，你可以利用 `System.Threading` 中的 `Thread` 类和相关 API。`System.Threading.Thread` 代表封装系统线程的控制点，而该命名空间提供了额外的托管 API 来管理这些线程。

`Thread` 中的一个常用方法是 `Sleep()`；然而，尽管它方便，但应该避免使用。`Thread.Sleep()` 会当前线程进入睡眠，本质上是告诉操作系统在（至少）指定的时间过去之前，不要为该线程分配任何时间片。这听起来是一个合理的做法，但它是一个“代码异味（bad code smell）”，表明程序的设计可能可以更好。让线程睡眠是一种糟糕的编程实践，因为分配线程这样昂贵的资源的初点是为了让它工作。（你不会付钱让员工睡觉；同样，你不应该为了让一个昂贵的线程睡眠数百万或数十亿个处理器周期而支付分配它的代价。）尽管如此，它也有几个用例。

第一种情况是让线程带有零延迟地睡眠，以告诉操作系统“如果有其他可以使用剩余量子线程，当前线程将礼貌地放弃它的剩余量子。”随后该礼貌的线程将会被正常调度，没有任何进一步的延迟。第二种用例是在测试代码中模拟一个正在执行某些高延迟操作的线程，而无需通过执行无意义的算术运算来消耗处理器。生产代码中的其他用户应经过仔细审查，以确保没有更好的方法来实现所需的效果。

`System.Threading` 中的另一种类型是 `ThreadPool`，它旨在限制可能对性能产生负影响的过度线程。线程是昂贵的资源，线程上下文切换不是免费的，通过时间分片模拟并行运行两个任务可能比接接运行它们要慢得多。虽然线程池很好地完成了它的工作，但它没有提供处理长时间运行任务或需要与主线程或彼此进行同步的任务的服务。我们真正需要做的是构建一个可以将线程和线程池作为实现细节的高层次抽象。由于 TPL 正好提供了这种抽象，`ThreadPool` 本质上可以完全弃用，转而使用基于 TPL 的 API。

有关在 .NET 4 之前常用的管理工作线程的其他技术的更多细节，请参阅 https://IntelliTect.com/EssentialCSharp 中的 Essential C# 3.0 多线程章节。

![](img/b18af4770e9195628243fa73ff1469b4_889_0.png)

关于 `System.Threading.ThreadPool` 和 `System.Thread.Sleep()` 方法的更多信息，请参阅 https://IntelliTect.com/legacy-system-threading。

## 总结

在本章开始，我们简要概述了开发者在编写多线程程序时经常面临的一些困难问题：原子性问题、死锁以及其他为多线程程序引入不确定性和不良行为的竞态条件。随后，我们深入研究了任务并行库（TPL）及其基于任务的异步模式（TAP），这是一种用于创建和调度由 `Task` 对象表示的工作单元的新 API，并且看到了它们如何通过允许你自动重写程序来简化多线程编程，从而维护由较小任务组成较大任务的连续性“布线”。在第 20 章和第 21 章中，我们引入了额外的高级抽象，涵盖了更多场景并进一步简化了 TAP。

在第 22 章中，我们将转向介绍如何通过同步访问共享资源来避免原子性问题，同时不引入死锁。

# 20 编写基于任务的异步模式

我们在第 19 章中看到，任务为操作异步工作提供了一种抽象。任务会被自动调度到数量正确的线程上，大任务可以通过链链小任务来组合，就像大程序可以由多个小方法组成一样。

然而，任务也有一些缺点。任务的主要困难在于它们让你的程序逻辑变得“颠倒倒”。为了说明这一点，本章将从一个阻塞在 I/O 绑定高延迟操作上的同步方法开始。

# 第 20 章：编写基于任务的异步模式

我们在本章结束处查看了异步流——定义和利用异步迭代器。

# 列表 20.1：同步 Web 请求

```csharp
using System;
using System.IO;
using System.Net;

public class Program
{
    public const string DefaultUrl = "https://IntelliText.com";

    public static void Main(string[] args)
    {
        if (args.Length == 0)
        {
            Console.WriteLine("ERROR: No find argument specified.");
            return;
        }
        string findText = args[0];

        string url = DefaultUrl;
        if (args.Length > 1)
        {
            url = args[1];
            // Ignore additional parameters
        }
        Console.Write("Searching for {findText}' at {url}");

        Console.WriteLine("Downloading...");
        using WebClient webClient = new WebClient();
        byte[] downloadData = webClient.DownloadData(url);

        Console.WriteLine("Searching...");
        int textOccurrenceCount = CountOccurrences(downloadData, findText);

        Console.WriteLine($"{Environment.NewLine}{findText}' appears");
    }

    private static int CountOccurrences(byte[] downloadData, string findText)
    {
        int textOccurrence = 0;

        using MemoryStream stream = new MemoryStream(downloadData);
        using StreamReader reader = new StreamReader(stream);

        int findIndex = 0;
        int length = 0;
        do
        {
            char[] data = new char[reader.BaseStream.Length];
            length = reader.Read(data);
            for (int i = 0; i < length; i++)
            {
                if (findText[findIndex] == data[i])
                {
                    findIndex++;
                    if (findIndex == findText.Length)
                    {
                        // Text was found
                        textOccurrence++;
                        findIndex = 0;
                    }
                }
                else
                {
                    findIndex = 0;
                }
            }
        } while (length != 0);
        return textOccurrence;
    }
}
```

OUTPUT 20.1

Searching for 'IntelliTect'...

://www.IntelliTect.com

Downloading...

Searching...

'IntelliTect' appears 35 times at URL 'http://www.IntelliTect.com'.

列表 20.1 中的逻辑相对直接——使用了常用的 C# 惯用法。在确定了 url 和 findText 值后，Main()

## 第 20 章：基于任务的异步模式编程

调用 `CountOccurrences()`，实例化一个 `WebClient`，并调用同步方法 `DownloadData()` 来下载内容。获取下载的数据后，将其传递给 `CountOccurrences()`，该方法将其加载到 `MemoryStream` 中，并利用 `StreamReader` 方法检索一段数据并搜索 `FindText` 值。（在列表 20.2 和 20.3 中，我们使用了 `Download()` 方法而不是更简单的 `DownloadString()` 方法，这样我们就可以在从流中读取时演示额外的异步调用。）

这种方法的问题在于，当然是调用线程在 I/O 操作完成之前一直被阻塞；这在操作执行期间浪费了一个本可以执行有用工作的线程。由于这个原因，例如我们无法执行任何其他代码，例如异步指示进度的代码。换句话说，“下载...”和“正在搜索...”是在相应操作**之前**调用的，而不是在操作**期间**调用。虽然这样做无关紧要，但想象一下我们想要并发执行额外工作，或者至少提供一个动画化的忙碌指示器。

## 使用 TPL 异步调用高延迟操作

为了解决并行执行其他工作的问题，方法 20.2 采用了类似的方法，但使用的是基于 TPL 任务的异步模式。

列表 20.2：异步网络请求
