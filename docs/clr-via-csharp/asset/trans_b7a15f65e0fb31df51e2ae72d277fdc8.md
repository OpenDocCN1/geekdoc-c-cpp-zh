
如今，CLR 并未利用处理器组，因此它创建的所有线程都在处理器组 0（默认组）中运行，并且在 64 位 Windows 上运行时最多只能使用 64 个核心。由于 32 位版本的 Windows 只支持处理器组 0，并且 32 位版本的 Windows 只支持 32 个 CPU，因此托管应用程序在 32 位版本的 Windows 上运行时最多可以使用 32 个核心。

## CLR 线程与 Windows 线程

如今，CLR 使用 Windows 的线程处理能力，因此本书第 V 部分实际上重点讨论 Windows 的线程处理能力如何暴露给使用 CLR 编写代码的开发人员。我将解释 Windows 中的线程如何工作，以及 CLR 如何改变其行为（如果确实会改变的话）。不过，如果你希望获得关于线程的更多信息，我建议阅读我早先关于该主题的一些著作，例如我的书 *Windows via C/C++，第 5 版*（Microsoft Press，2007）。

尽管如今 CLR 线程直接映射到 Windows 线程，但 Microsoft CLR 团队保留在未来与 Windows 线程脱钩的权利。将来某一天，CLR 可能会引入自己的逻辑线程概念，使 CLR 逻辑线程不一定映射到物理 Windows 线程。例如，曾有人讨论创建比物理线程占用资源少得多的逻辑线程，然后你可以让许多逻辑线程运行在极少数物理线程之上。例如，CLR 可以判定你的某个线程处于等待状态，并重新分配该线程去执行不同的任务。这样做的好处包括简化编码、减少资源占用以及可能提升性能。遗憾的是，实现这种解决方案对 CLR 团队来说将是巨大的工作量，因此我认为这样的功能不会很快进入 CLR。

对你而言，这一切意味着你的代码在操作线程时应尽可能少做假设。例如，你应避免 P/Invoke 到本机 Windows 函数，因为这些函数不了解 CLR 线程。^5 通过尽可能避免本机 Windows 函数并坚持使用框架类库（FCL）类型，你可以确保自己的代码在将来这些性能增强功能可用时能够轻松利用它们。

5 如果你需要 P/Invoke 到本机代码，并且代码使用当前物理操作系统线程执行很重要，那么应调用 `System.Threading.Thread` 的静态 `BeginThreadAffinity` 方法。当线程不再需要由物理操作系统线程运行时，它可以调用 `Thread` 的静态 `EndThreadAffinity` 方法通知 CLR。

## 使用专用线程执行异步计算密集型操作

在本节中，我将向你展示如何创建一个线程，并让它执行异步计算密集型操作。尽管我将带你逐步完成这一过程，但我强烈建议你避免使用我在这里展示的技术。相反，你应尽可能使用 CLR 的线程池来执行异步计算密集型操作，我会在第 26 章“计算密集型异步操作”中详细说明如何做到这一点。

然而，有些场合你也许希望显式创建一个专用于执行特定计算密集型操作的线程。通常，如果你要执行的代码要求线程处于线程池线程不常见的特定状态，你就会希望创建一个专用线程。例如，如果以下任一情况成立，就显式创建你自己的线程：

- 你需要线程以非正常线程优先级运行。所有线程池线程都以正常优先级运行。虽然你可以更改此设置，但不建议这样做，而且优先级更改不会在线程池操作之间保持。
- 你需要线程表现为前台线程，从而防止应用程序在线程完成任务之前退出。有关更多信息，请参阅本章后面的“前台线程与后台线程”一节。线程池线程始终是后台线程，如果 CLR 想要终止进程，它们可能无法完成任务。
- 计算密集型任务运行时间极长；这样，我就不会在它试图判断是否要创建额外线程时给线程池的逻辑增加负担。
- 我希望启动一个线程，并可能通过调用 **Thread 的 Abort** 方法（在第 22 章“CLR 宿主与 AppDomain”中讨论）提前中止它。

要创建专用线程，你需要构造 **System.Threading.Thread** 类的实例，并向其构造函数传入方法名。下面是 **Thread 的** 构造函数原型。

```csharp
public sealed class Thread : CriticalFinalizerObject, ... {
    public Thread(ParameterizedThreadStart start);
    // Less commonly used constructors are not shown here
}
```

**start** 参数标识专用线程将执行的方法，并且该方法必须与 **ParameterizedThreadStart** 委托的签名匹配。⁶

```csharp
delegate void ParameterizedThreadStart(Object obj);
```

6 顺便提一下，**Thread** 还提供了一个构造函数，它接受一个不接收参数并返回 **void** 的 **ThreadStart** 委托。就个人而言，我建议你避免使用这个构造函数和委托，因为它们限制更多。如果你的线程方法接受 **Object** 并返回 **void**，那么你可以使用专用线程调用方法，也可以使用线程池调用方法（如第 26 章所示）。

构造 **Thread** 对象是相对轻量级的操作，因为它实际上不会创建物理操作系统线程。要真正创建操作系统线程并让它开始执行回调方法，必须调用 **Thread 的 Start** 方法，并向其传入你希望作为回调方法参数传递的对象（状态）。以下代码演示如何创建专用线程并让它异步调用方法：

```csharp
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        Console.WriteLine("Main thread: starting a dedicated thread " +
            "to do an asynchronous operation");
        Thread dedicatedThread = new Thread(ComputeBoundOp);
        dedicatedThread.Start(5);

        Console.WriteLine("Main thread: Doing other work here...");
        Thread.Sleep(10000);      // Simulating other work (10 seconds)

        dedicatedThread.Join();   // Wait for thread to terminate
        Console.WriteLine("Hit <Enter> to end this program...");
        Console.ReadLine();
    }

    // This method's signature must match the ParameterizedThreadStart delegate
    private static void ComputeBoundOp(Object state) {
        // This method is executed by a dedicated thread

        Console.WriteLine("In ComputeBoundOp: state={0}", state);
        Thread.Sleep(1000); // Simulates other work (1 second)

        // When this method returns, the dedicated thread dies
    }
}
```

当我编译并运行这段代码时，得到以下输出：

```text
Main thread: starting a dedicated thread to do an asynchronous operation
Main thread: Doing other work here...
In ComputeBoundOp: state=5
```

有时运行这段代码时，由于我无法控制 Windows 如何调度这两个线程，我会得到以下输出：

```text
Main thread: starting a dedicated thread to do an asynchronous operation
In ComputeBoundOp: state=5
Main thread: Doing other work here...
```

请注意，**Main** 方法调用了 **Join**。**Join** 方法会使调用线程停止执行任何代码，直到由 **dedicatedThread** 标识的线程已销毁自身或被终止。

5 机器以 100% CPU 利用率运行，因为让 CPU 全功率运行往往会产生热量，这就需要冷却系统，而为一套 HVAC 冷却系统供电可能比让更多计算机以降低的容量运行更昂贵。尽管数据中心发现维护多台机器的成本越来越高，因为每台机器都必须定期进行硬件和软件升级与监控，但这必须与运行冷却系统的费用权衡。

现在，如果你同意我的理论，下一步就是弄清楚 CPU 应该做什么。在给出我在这里的想法之前，让我先说点别的。过去，开发人员和最终用户总觉得计算机不够强大。因此，我们开发人员绝不会随意执行代码，除非最终用户允许我们这样做，并通过菜单项、按钮和复选框等 UI 元素表明应用程序可以消耗 CPU 资源。

但现在时代变了。计算机出厂时便具备惊人的计算能力，而且在不久的将来还会承诺提供更强大的计算能力。在本章前面，我展示了任务管理器如何报告我的 CPU 仅有 0% 的时间处于忙碌状态。如果我的计算机配备的是四核 CPU，而不是现在的双核 CPU，那么任务管理器会更频繁地报告 0%。当 80 核处理器问世时，机器几乎在所有时间看起来都像什么都没做。对计算机购买者来说，看起来他们花了更多钱购买更强大的 CPU，而计算机却做更少的工作！

这就是硬件制造商难以向用户销售多核计算机的原因：软件没有利用硬件，用户购买带有更多 CPU 的机器也得不到好处。我想说的是，我们现在拥有充足的计算能力，而且还有更多即将到来，因此开发人员可以积极消耗它。没错——过去，除非我们知道最终用户想要某个计算结果，否则我们绝不会梦想让应用程序执行某些计算。但现在我们有了额外的计算能力，我们可以这样梦想。

这里有一个例子：当你在 Visual Studio 编辑器中停止输入时，Visual Studio 会自动启动编译器并编译你的代码。这使开发人员的生产力极高，因为他们可以在输入时看到源代码中的警告和错误，并立即修复。事实上，开发人员今天所认为的“编辑-生成-调试”循环将变成只是“编辑-调试”循环，因为生成（编译）代码将一直自动发生。作为最终用户，你不会注意到这一点，因为有大量 CPU 能力可用，而且你正在做的其他事情几乎不会受到编译器频繁运行的影响。事实上，我预计在 Visual Studio 的某个未来版本中，“生成”菜单项将完全消失，因为生成将变成自动的。应用程序的 UI 不仅变得更简单，而且应用程序还会向最终用户提供“答案”，使他们更有生产力。
