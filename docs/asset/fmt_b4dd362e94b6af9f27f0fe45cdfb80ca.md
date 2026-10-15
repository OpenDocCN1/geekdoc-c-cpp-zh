
多线程功能使你的应用程序能够同时拥有多个执行路径。你已经了解 Windows 多任务功能，它允许你同时执行多个任务。在多任务中，你可以同时执行多个任务，例如使用 MS-Word 编写文章、在 Windows Media Player (WMP) 中听歌，以及使用 Internet Download Manager 下载电影。同样，你可以使用多线程同时执行程序的不同方法。几乎所有 Windows 应用程序都使用多线程概念，例如 MS-Word 在一个线程中接收用户输入并将其显示在屏幕上，同时在第二个线程中继续检查拼写和语法错误，同时第三个线程在定期间隔自动保存文档。同样，WMP 在一个线程中播放音乐，在第二个线程中显示可视化效果，并在第三个线程中接收用户输入。在 C# 中，多线程可以通过在单个应用程序中创建多个线程来实现。下面的代码片段展示了创建多线程应用程序的语法：

```
static void Main(string[] args)
{
    Thread FirstThread = new Thread(FirstFunction);
    Thread SecondThread = new Thread(SecondFunction);
    Thread ThirdThread = new Thread(ThirdFunction);
    Console.WriteLine("\nThreading Starts...\n");
    FirstThread.Start();
    SecondThread.Start();
    ThirdThread.Start();
}
public static void FirstFunction()
{
....
}
public static void SecondFunction()
{
....
}
public static void ThirdFunction()
{
...
}
```

在前面的代码片段中，你可以看到单个应用程序由三个线程组成，例如`FirstThread`、`SecondThread`和`ThirdThread`。

现在让我们学习线程的优先级。

## Thread Priorities

根据在多任务环境中分配给线程的任务的顺序和重要性，确定线程的优先级级别。优先级较高的线程比优先级较低的线程执行得更频繁。考虑一个应用程序的案例，该应用程序在第一个线程中接收用户输入，并在第二个线程中向用户显示一条消息，指示表单打开后经过的时间。在这种情况下，由于接收用户输入的任务需要在任何其他任务之前完成，你可以将负责接收用户输入的线程定义为比控制用户响应的线程具有更高优先级的线程。在 C# 中，`ThreadPriority`枚举定义了线程优先级的所有可能值。你可以使用`Thread`类的`Priority`属性获取或设置线程的优先级。

Table 31.3: Priorities of a Thread

| Name | Description |
|------|-------------|
| `Lowest` | Refers to the least important priority level that can be assigned to a thread. A thread with this priority can be scheduled after threads with any other priority. |
| `BelowNormal` | Refers to the priority level that is just below the `Normal` level. The thread with this priority can be scheduled after threads having the `Normal` priority and before those with the `Lowest` priority. |
| `Normal` | Refers to the priority level that is neither lowest nor the highest. The thread with this priority can be scheduled after threads with the `AboveNormal` priority and before those with the `BelowNormal` priority. All the threads have the `Normal` priority by default. |
| `AboveNormal` | Refers to the priority level that is just below the `Highest` level. The thread with this priority can be scheduled after threads with the `Highest` priority and before those with the `Normal` priority. |
| `Highest` | Refers to the most important priority level that can be assigned to a thread. The thread with this priority can be scheduled before threads with any other priority. |

下面的代码片段展示了如何为线程设置不同的优先级级别：

```
static void Main(string[] args)
{
    Thread FirstThread = new Thread(FirstFunction);
    Thread SecondThread = new Thread(SecondFunction);
    Thread ThirdThread = new Thread(ThirdFunction);
    FirstThread.Priority = ThreadPriority.Lowest;
    SecondThread.Priority = ThreadPriority.Highest;
    ThirdThread.Priority = ThreadPriority.Normal;
    FirstThread.Start();
    SecondThread.Start();
    ThirdThread.Start();
}
```

前面的代码片段定义了三个线程——`FirstThread`、`SecondThread`和`ThirdThread`。`FirstThread`线程被分配了`Lowest`优先级，`SecondThread`线程被分配了`Highest`优先级，`ThirdThread`线程被分配了`Normal`优先级。这意味着当你执行程序时，`SecondThread`线程首先执行，然后是`ThirdThread`线程，最后是`FirstThread`线程。

现在让我们学习线程的不同状态。

## Thread States

每个对象都有其状态。例如，水有三种状态，如固态、液态和气态，并且可以从一种状态转变为另一种状态。同样，线程也有其状态，并且可以从一种状态转变为另一种状态。线程的状态决定了其在给定时间点的实际状态。你可以通过`Thread`类的`ThreadState`属性确定线程的状态。

Table 31.4: States of a Thread

| Name | Description |
|------|-------------|
| `Running` | Refers to a state in which the thread is in the execution mode. |
| `StopRequested` | Refers to a state in which a thread is requested to stop its execution. |
| `SuspendRequested` | Refers to a state in which a thread is requested to suspend its execution. |
| `Background` | Refers to a state in which a thread is executed as a background thread, as opposed to a foreground thread. This state is controlled by setting the `IsBackground` property of the `Thread` class. |
| `Unstarted` | Refers to a state in which the `Start()` method of the `Thread` class has not yet been invoked. |
| `Stopped` | Refers to a state in which a thread has already stopped executing. |
| `WaitSleepJoin` | Refers to a state that occurs when the `Wait()`, `Sleep()`, and `Join()` methods are simultaneously invoked. A thread in this state stops executing and is considered to be blocked. |
| `Suspended` | Refers to a state in which a thread has been suspended. |
| `AbortRequested` | Refers to a state in which a thread is requested to stop its functioning permanently. |
| `Aborted` | Refers to a state in which a thread is considered to be dead forever. |

下面的代码片段展示了确定线程状态的语法：

```csharp
public class Program
{
    static Thread FirstThread;
    static Thread SecondThread;
    static Thread ThirdThread;

    public static void Main(string[] args)
    {
        FirstThread = new Thread(FirstFunction);
        SecondThread = new Thread(SecondFunction);
        ThirdThread = new Thread(ThirdFunction);
    }

    public static void StateOfThreads(string position)
    {
        Console.WriteLine("\n {0}", position);
        Console.WriteLine(FirstThread.ThreadState);
        Console.WriteLine(SecondThread.ThreadState);
        Console.WriteLine(ThirdThread.ThreadState);
    }

    public static void FirstFunction()
    {
        StateOfThreads("FirstFunction()");
    }

    public static void SecondFunction()
    {
        StateOfThreads("SecondFunction()");
    }

    public static void ThirdFunction()
    {
        StateOfThreads("ThirdFunction()");
    }
}
```

在前面的代码片段中，你可以看到线程的状态是在应用程序的各个层级中确定的，例如在`FirstFunction()`方法中、在`SecondFunction()`方法中以及在`ThirdFunction()`方法中。

让我们现在学习同步。

## 线程同步

同步是在这样一种方式下协调事件和任务，使得所有任务都能在不受到其他任务干扰和中断的情况下完成。如果一个任务使用的是单个独立对象，则无需同步该任务；然而，如果一个任务使用的是共享对象，则需要同步任务，以避免不同线程对同一对象进行多次请求访问和使用。为了更好地理解同步的概念，让我们举一个例子：你和你的朋友共享同一个电视遥控器。你想看新闻频道并录制新闻，而你的朋友想看电影并录制它。当轮到你时，你切换到新闻频道，然后你的时间片也结束了。现在，你从上次的操作继续并开始录制，等等。结果会怎样？你们两人都无法完成各自的预期任务。在 C# 编程中，多个线程尝试访问单个共享资源（对象）时也会出现同样的情况。在这种情况下，必须以一种方式同步分配给线程的任务，以确保对象一次只被一个线程使用。

## 立即可行的解决方案

### 创建线程

要学习如何创建线程，你首先需要创建一个应用程序。打开 Microsoft Visual Studio 2010 并创建一个名为 MyThread 的控制台应用程序（也可在光盘上获得）。现在，打开 MyThread 应用程序的 Program.cs 文件并添加以下命名空间以在你的应用程序中启用线程：

```
using System.Threading;
```

现在，将以下代码行添加到 Program.cs 文件的 Main() 方法中：

```
Thread FirstThread = new Thread(FirstFunction);
```

这会在 MyThread 应用程序中创建 FirstThread 线程。FirstThread 线程以 FirstFunction() 方法作为参数。现在，将以下代码添加到 MyThread 应用程序的 Program.cs 文件中以提供 FirstFunction() 方法的定义：

```
public static void FirstFunction()
{
    for (int number = 1; number <= 5; number++)
    {
        Console.WriteLine("First Thread Displays: " + number);
    }
    Console.Write("\nPress ENTER to quit...");
    Console.ReadLine();
}
```

现在，MyThread 线程已创建；然而，它尚未执行，因为它尚未启动。让我们在下一节学习如何启动线程。

### 启动线程

要启动线程，你需要调用 Thread 类的 Start() 方法。

清单 31.1 显示了 MyThread 应用程序的完整代码，展示了如何创建和启动线程：

#### 清单 31.1：显示 MyThread 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading; //Namespace required to enable threading
namespace MyThread
{
class Program
{
    static void Main(string[] args)
    {
        Thread FirstThread = new Thread(FirstFunction); //Code to create a thread
        Console.WriteLine("Threading Starts...\n");
        FirstThread.Start();//Starting the thread
    }
    public static void FirstFunction()
    {
        for (int number = 1; number <= 5; number++)
        {
            Console.WriteLine("First Thread Displays: "+number);
        }
        Console.Write("\nPress ENTER to quit...");
```

在清单 31.1 中，你可以看到在创建 FirstThread 线程后，调用了 Thread 类的 Start() 方法。FirstThread 线程在调用 Start() 方法后开始执行。

图 31.1 显示了清单 31.1 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1496_0.png)

图 31.1：创建和启动线程

让我们现在学习如何让线程休眠。

### 让线程休眠

让线程休眠意味着延迟其执行一段时间。Thread 类的 Sleep() 方法会导致当前执行的线程暂时暂停指定的时间。Sleep() 方法接受一个以毫秒为单位的时间作为参数，表示你希望暂停线程的时间。

清单 31.2 显示了 ThreadSleep 应用程序的代码（也可在光盘上获得），展示了如何让线程休眠：

#### 清单 31.2：显示 ThreadSleep 应用程序的代码
