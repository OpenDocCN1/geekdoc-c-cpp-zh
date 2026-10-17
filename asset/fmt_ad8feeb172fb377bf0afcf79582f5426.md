
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace MyThreadsPriority
{
    class Program
    {
        static void Main(string[] args)
        {
            Thread FirstThread = new Thread(FirstFunction);
            Thread SecondThread = new Thread(SecondFunction);
            Thread ThirdThread = new Thread(ThirdFunction);
            FirstThread.Name = "First Thread";
            SecondThread.Name = "Second Thread";
            ThirdThread.Name = "Third Thread";

            //Setting priorities for threads
            FirstThread.Priority = ThreadPriority.Lowest;
            SecondThread.Priority = ThreadPriority.Highest;
            ThirdThread.Priority = ThreadPriority.AboveNormal;
            Console.WriteLine("Threading Starts...\n");
            ThirdThread.Start();
            SecondThread.Start();
            FirstThread.Start();
        }
        public static void FirstFunction()
        {
            for (int number = 1; number <= 5; number++)
            {
                Console.WriteLine("First Thread Displays: " + number);
            }
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
        public static void SecondFunction()
        {
            for (int number = 1; number <= 5; number++)
            {
                Console.WriteLine("Second Thread Displays: " + number);
            }
        }
        public static void ThirdFunction()
        {
            for (int number = 1; number <= 5; number++)
            {
                Console.WriteLine("Third Thread Displays: " + number);
            }
        }
    }
}
```

在清单 31.7 中，你可以看到我们已将 `FirstThread` 线程、`SecondThread` 线程和 `ThirdThread` 线程的优先级分别设置为 `Lowest`、`Highest` 和 `AboveNormal`。

图 31.7 显示了清单 31.7 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1504_0.png)

Figure 31.7: Setting a Thread's Priority

让我们学习如何确定线程状态。

## Determining State of a Thread

线程状态表示线程的状态。它由 `Thread` 类的 `ThreadState` 属性决定。清单 31.8 显示了 `MyThreadsState` 应用程序的代码，该应用程序也可在光盘上获得，您可以在其中学习在不同层级确定线程的状态：

### Listing 31.8: Showing the Code of the `MyThreadsState` Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
namespace MyThreadsState
{
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
        FirstThread.Name = "First Thread";
        SecondThread.Name = "Second Thread";
        ThirdThread.Name = "Third Thread";
        StateOfThreads("Main() Before Starting the Threads..");
        FirstThread.Start();
        SecondThread.Start();
        ThirdThread.Start();
        StateOfThreads("Main() Before Ending the Threads...");
    }
    // writing a function for determining the state of the threads
    public static void StateOfThreads(string position)
    {
        Console.WriteLine("\r\nIn {0}", position);
        Console.WriteLine("Thread Name : {0}, Thread State : {1}", FirstThread.Name, FirstThread.ThreadState);
        Console.WriteLine("Thread Name : {0}, Thread State : {1}", SecondThread.Name, SecondThread.ThreadState);
        Console.WriteLine("Thread Name : {0}, Thread State : {1}\r\n", ThirdThread.Name, ThirdThread.ThreadState);
    }
}
public static void FirstFunction()
{
    for (int number = 1; number <= 5; number++)
    {
        Console.WriteLine("First Thread Displays: " + number);
        Thread.Sleep(200);
    }
    StateOfThreads("FirstFunction()");
}
public static void SecondFunction()
{
    for (int number = 1; number <= 5; number++)
    {
        Console.WriteLine("Second Thread Displays: " + number);
        Thread.Sleep(500);
    }
    StateOfThreads("SecondFunction()");
}
public static void ThirdFunction()
{
    for (int number = 1; number <= 5; number++)
    {
        Console.WriteLine("Third Thread Displays: " + number);
        Thread.Sleep(700);
    }
    StateOfThreads("ThirdFunction()");
    Console.Write("\nPress ENTER to quit...");
    Console.ReadLine();
}
```

在清单 31.8 中，您可以看到在设置线程名称后，通过在应用程序的各个层级调用名为 `StateOfThreads()` 的静态方法来显示三个线程的当前状态。

图 31.8 显示了清单 31.8 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1505_0.png)

Figure 31.8: Determining a Thread State

现在让我们学习如何加入线程。

## Joining Threads

您可以通过调用 `Thread` 类的 `Join()` 方法来加入两个或多个线程。为了理解线程加入的概念，让我们创建一个名为 `ThreadJoin` 的项目，并在其中添加另一个名为 `NoJoin` 的应用程序，该应用程序有助于在不加入线程的情况下执行线程。清单 31.9 显示了 `NoJoin` 应用程序的代码：

### Listing 31.9: Showing the Code of the `NoJoin` Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace NoJoin
{
class Program
{
    static void Main(string[] args)
    {
        Thread FirstThread = new Thread(FirstFunction);
        Thread SecondThread = new Thread(SecondFunction);
        Thread ThirdThread = new Thread(ThirdFunction);
        Console.WriteLine("\nthreading Starts...\n");
        FirstThread.Start();
        SecondThread.Start();
        ThirdThread.Start();
        Console.WriteLine("\nThe Main() is Ending...\n");
    }
    public static void FirstFunction() {
        for (int number = 1; number <= 5; number++)
        {
            Console.WriteLine("First Thread Displays: " + number);
            Thread.Sleep(200);
        }
    }
    public static void SecondFunction() {
        for (int number = 1; number <= 5; number++)
        {
            Console.WriteLine("Second Thread Displays: " + number);
            Thread.Sleep(500);
        }
    }
    public static void ThirdFunction() {
        for (int number = 1; number <= 5; number++)
        {
            Console.WriteLine("Third Thread Displays: " + number);
            Thread.Sleep(700);
        }
        Console.Write("\nPress ENTER to quit...");
        Console.ReadLine();
    }
}
}
```

图 31.9 显示了清单 31.9 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1507_0.png)

Figure 31.9: Displaying the Output Without Using the `Join()` Method

在图 31.9 中，您可以看到 `Main()` 线程在启动 `FirstThread` 线程和 `SecondThread` 线程后迅速终止。但是，如果您希望 `Main()` 线程在 `FirstThread` 线程存活期间保持存活，则可以对 `FirstThread` 线程应用 `Join()` 方法。为了更清楚地理解这一点，让我们在 `ThreadJoin` 项目的 `ThreadJoin` 应用程序中实现 `Join()` 方法，该应用程序也可在光盘上获得，并显示 `Join()` 方法的实现。

### Listing 31.10: Showing the Code of the `ThreadJoin` Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
namespace ThreadJoin
{
class Program {
    static void Main(string[] args)
    {
        Thread FirstThread = new Thread(FirstFunction);
        Thread SecondThread = new Thread(SecondFunction);
        Thread ThirdThread = new Thread(ThirdFunction);
        Console.WriteLine("\nThreading Starts...\n");
        FirstThread.Start();
        SecondThread.Start();
        ThirdThread.Start();
        FirstThread.Join(); //Code to join the threads
        Console.WriteLine("\nThe Main() is Ending...\n");
    }
    public static void FirstFunction()
    {
        for (int number = 1; number <= 5; number++)
        {
            Console.WriteLine("First Thread Displays: " + number);
            Thread.Sleep(200);
        }
    }
    public static void SecondFunction()
{
Console.WriteLine("First Thread Displays: " + number);
Thread.Sleep(500);
}
public static void SecondFunction()
{
for (int number = 1; number <= 5; number++)
{
Console.WriteLine("Second Thread Displays: " + number);
Thread.Sleep(500);
}
}
public static void ThirdFunction()
{
for (int number = 1; number <= 5; number++)
{
Console.WriteLine("Third Thread Displays: " + number);
Thread.Sleep(700);
}
Console.Write("\nPress ENTER to quit...");
Console.ReadLine();
}
```

图 31.10 显示了清单 31.10 的输出。
