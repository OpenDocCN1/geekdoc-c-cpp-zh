
如今使用 Windows 或 .NET Framework，如果应用程序仍能停止操作系统和其他应用程序。因此，Windows 为每个进程提供自己的线程，以提高系统可靠性和响应能力。例如，在我的机器上，当我运行任务管理器并选择“性能”选项卡时，我看到图26-1所示的图像。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_666_0.png)

**图26-1** 显示系统性能的任务管理器。

它显示我的机器当前有 55 个进程在运行，因此我们预期我的机器上至少有 55 个线程，因为每个进程至少获得 1 个线程。但任务管理器还显示，我的机器当前有 864 个线程！所有这些线程最终在我的机器上分配了大量 MB 的内存，而我的机器只有 4 GB 的 RAM。这也意味着平均每个进程大约有 15.7 个线程，而在我的双核机器上，理想情况下每个进程应该只有 2 个线程！

更糟的是，当我查看 CPU 使用率时，它显示我的 CPU 只有 5% 的时间处于忙碌状态。这意味着在 95% 的时间里，这 864 个线程实际上无事可做——它们只是在占用内存，而这些内存在线程不运行时肯定没有被使用。你不得不问自己：这些应用程序真的需要所有这些线程在 95% 的时间里什么都不做吗？这个问题的答案只能是“不”。现在，如果你想看看哪些进程最浪费，请单击任务管理器的“详细信息”选项卡，添加“线程”列，⁴³ 并按降序排列该列，如图26-2所示。

⁴³ 你可以右键单击现有列，然后选择“选择列”菜单项来添加该列。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_667_0.png)

**图26-2** 显示详细信息的任务管理器。

如你所见，System 已创建 105 个线程，并占用 1% 的 CPU。Explorer 已创建 47 个线程，占用 0% 的 CPU；Microsoft Visual Studio (Devenv.exe) 已创建 36 个线程，占用 0% 的 CPU；Outlook 已创建 24 个线程，占用 0% 的 CPU；如此等等。这里到底发生了什么？

当开发者学习 Windows 时，他们了解到 Windows 中的进程是非常昂贵的。创建进程通常需要几秒钟，必须分配大量内存，这些内存必须初始化，EXE 和 DLL 文件必须从磁盘加载，等等。相比之下，在 Windows 中创建线程非常廉价，因此开发者决定不再创建进程，而是开始创建线程。所以现在我们有了大量线程。但是，尽管线程比进程便宜，但与大多数其他系统资源相比，它们仍然非常昂贵，因此应该节省并恰当地使用它们。

毫无疑问，我们可以肯定地说，我们刚刚讨论的所有应用程序都在低效地使用线程。系统中根本不需要存在所有这些线程。在应用程序内部分配资源是一回事；分配了资源却不使用它们则完全是另一回事。这纯粹是浪费，而且为线程栈分配所有这些内存意味着用于更重要数据（例如用户文档）的内存更少。⁴⁴

⁴⁴ 我忍不住要再给你演示一下这种情况有多糟糕。试试这个：打开 Notepad.exe，并使用任务管理器查看其中有多少个线程（你应该会看到 1 个）。然后选择记事本的“文件打开”菜单项，以显示通用的“文件打开”对话框。对话框出现后，查看任务管理器，看看刚刚创建了多少个新线程。在我的机器上，仅仅显示这个对话框就创建了 31 个额外线程！事实上，每个使用通用“文件打开”或“文件保存”对话框的应用程序，都会在其内部创建许多额外的线程

## 使用专用线程执行异步的计算密集型操作

在本节中，我将向你展示如何创建线程并让它执行异步的计算密集型操作。虽然我会带你完成这一过程，但我强烈建议你避免使用我在这里展示的技术。而且事实上，如果你要构建 Windows 应用商店应用，这种技术甚至是不可能的，因为 Thread 类不可用。相反，只要有可能，你就应该使用线程池来执行异步的计算密集型操作。我将在第27章“计算密集型异步操作”中详细介绍如何做到这一点。

然而，在一些非常特殊的情况下，你可能希望显式创建一个专用于执行特定计算密集型操作的线程。通常，如果你要执行的代码要求线程处于线程池线程不常见的特定状态，你就会希望创建专用线程。例如，如果以下任一情况为真，就显式创建你自己的线程：

- 你需要线程以非正常的线程优先级运行。所有线程池线程都以正常优先级运行。虽然你可以更改这一点，但不建议这样做，而且优先级更改不会在线程池操作之间保持。
- 你需要线程作为前台线程运行，从而在线程完成其任务之前防止应用程序终止。有关详细信息，请参阅本章后面的“前台线程与后台线程”一节。线程池线程始终是后台线程，如果 CLR 想要终止进程，它们可能无法完成任务。
- 计算密集型任务运行时间极长；这样，我就不会给线程池的逻辑增加负担，因为它试图判断是否需要创建额外的线程。
- 你想启动一个线程，并可能通过调用 Thread 的 Abort 方法来提前中止它（在第22章“CLR 宿主和 AppDomain”中讨论）。

要创建专用线程，你需要构造 System.Threading.Thread 类的实例，并将方法名称传入其构造函数。下面是 Thread 构造函数原型：

```
public sealed class Thread : CriticalFinalizerObject, ... {
   public Thread(ParameterizedThreadStart start);
   // Less commonly used constructors are not shown here
}
```

start 参数标识专用线程将执行的方法，该方法必须匹配 ParameterizedThreadStart 委托的签名。⁴⁵

```
delegate void ParameterizedThreadStart(Object obj);
```

构造 Thread 对象是相对轻量的操作，因为它实际上并不会创建物理操作系统线程。要真正创建操作系统线程并让它开始执行回调方法，你必须调用 Thread 的 Start 方法，并将你希望作为回调方法参数传入的对象（状态）传递给它。以下代码演示如何创建专用线程并让它异步调用方法：

```
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        Console.WriteLine("Main thread: starting a dedicated thread " +
            "to do an asynchronous operation");
        Thread dedicatedThread = new Thread(ComputeBoundOp);
        dedicatedThread.Start(5);

        Console.WriteLine("Main thread: Doing other work here...");
        Thread.Sleep(10000);    // Simulating other work (10 seconds)

        dedicatedThread.Join(); // Wait for thread to terminate
        Console.WriteLine("Hit <Enter> to end this program...");
        Console.ReadLine();
    }

    // This method's signature must match the ParameterizedThreadStart delegate
    private static void ComputeBoundOp(Object state) {
        // This method is executed by a dedicated thread

        Console.WriteLine("In ComputeBoundOp: state={0}", state);
        Thread.Sleep(1000);  // Simulates other work (1 second)

        // When this method returns, the dedicated thread dies
    }
}
```

当我编译并运行这段代码时，得到以下输出：

```
Main thread: starting a dedicated thread to do an asynchronous operation
Main thread: Doing other work here...
In ComputeBoundOp: state=5
```

有时当我运行这段代码时，会得到以下输出，因为我无法控制 Windows

⁴⁵ 顺便说明，Thread 还提供了一个构造函数，它接受一个不接受参数并返回 void 的 ThreadStart 委托。就个人而言，我建议你避免使用这个构造函数和委托，因为它们限制更多。如果你的线程方法接受一个 Object 并返回 void，那么你可以使用专用线程调用方法，也可以使用线程池调用它（如第27章所示）。
