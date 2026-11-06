
```csharp
}
public static void DisplayHexadecimal(int dec)
{
    Console.WriteLine("Hexadecimal: {0:X}", dec);
}
}
```

该代码将输出以下结果：

```
Number: 1,000
Hexadecimal: 3E8
Money: $1,000.00
Number: 2,000
Money: $2,000.00
```

在上面的示例中，displayDel 指向三个方法，即 DisplayNumber、DisplayMoney 和 DisplayHexadecimal。这使它成为一个多播委托。这意味着当调用 displayDel 时，它会依次调用所有这三个方法。

## 示例

```csharp
using System;
namespace thread
{
    class MainThread
    {
        static void Main(string[] args)
        {
            Thread t1 = new Thread();
            t1.Name="Thread1";
            Console.WriteLine("Thread is:{0}", t1.Name);
            Console.Read();
        }
    }
}
```

**编译并执行代码后，输出为：**

```
Thread is: Thread1
```

## Thread 类的属性和方法

### 属性[^50]

- **IsAlive：** 显示当前线程执行状态的值
- **CurrentThread：** 获取当前正在运行的线程
- **CurrentContext：** 获取线程正在其中执行的当前上下文
- **ExecutionContext：** ExecutionContext 对象包含有关不同上下文的信息
- **Name：** 获取或设置线程的名称
- **ThreadState：** 包含当前线程状态的值
- **Priority：** 获取或设置表示线程调度优先级的值

### 方法

- **public static void BeginThreadAffinity()：** 宿主即将执行依赖于当前物理操作系统线程的指令。
- **public void Abort()：** 在其被调用的线程中引发 ThreadAbortException。
- **public void Interrupt()：** 中断处于 WaitSleepJoin 状态的线程。
- **public static AppDomain GetDomain()：** 返回唯一的域标识符。
- **public static void MemoryBarrier()：** 执行当前线程的处理器无法重新排序指令。
- **public void Start()：** 启动线程。
- **public static bool Yield()：** 使调用线程将执行让给处理器上已准备好运行的另一个线程。

## 创建和管理线程<sup>[32]</sup>

扩展线程类会创建线程。扩展线程类调用 **Start()** 方法来启动子线程执行。

### 示例

```csharp
using System;
using System.Threading;

namespace MultipleThread
{
    class ThreadProgram
    {
        public static void CallChild()
        {
            Console.WriteLine("Start child thread");
        }
        static void Main(string[] args)
        {
            ThreadStart child1 = new ThreadStart(CallChild);
            Console.WriteLine("Creating child thread");
            Thread child2 = new Thread(child1);
            child2.Start();
            Console.Read();
        }
    }
}
```

**编译并执行代码后，输出为：**

```
Start child thread

Creating child thread
```

## 管理线程

当需要将线程暂停一段时间以便另一个线程可以执行时，使用 **Thread.Sleep()** 方法。该方法接受一个参数，表示以毫秒为单位的时间。

### 示例

```csharp
using System;
using System.Threading;

namespace Multithreaded
{
    class Program
    {
        public static void ChildThread()
        {
            Console.WriteLine("Start child thread");
            int sleeptime = 4000;

            Console.WriteLine("Thread sleeping for {0}  seconds", sleeptime / 1000);
            Thread.Sleep(sleeptime);
            Console.WriteLine("Resume child thread");

        }
        public static void Main()
        {
            ThreadStart t1 = new ThreadStart(ChildThread);
            Console.WriteLine("child thread created");
            Thread child1 = new Thread(t1);
            child1.Start();
            Console.Read();
        }
    }
}
```

**编译并执行代码后，输出为：**

```
Start child thread
Thread sleeping for 4 seconds
Resume child thread
child thread created
```

## 销毁线程

使用 **Thread.Abort()** 方法销毁线程。当线程被销毁时，会引发 **ThreadAbortException**。捕获该异常，并将控制权发送到 **finally** 块。

### 示例

```csharp
using System;
using System.Threading;

namespace ThreadDemo
{
    class Program
    {
        public static void ChildThread()
        {
            try
            {
                Console.WriteLine("Child Thread started");
                for (int j = 0; j <= 10; j++)
                {
                    Thread.Sleep(1000);
                    Console.WriteLine(j);
                }
            }
            catch (ThreadAbortException e)
            {
                Console.WriteLine("Exception caught");
            }
            finally
            {
                Console.WriteLine("Exception is not handled");
            }
        }

        public static void Main()
        {
            ThreadStart t1 = new ThreadStart(ChildThread);
            Console.WriteLine(" Creating child thread");
            Thread t2 = new Thread(t1);
            t2.Start();

            // main thread is stopped
            Thread.Sleep(2000);

            // child thread aborted
            Console.WriteLine(" Aborting child thread ");
            t2.Abort();
            Console.Read();
        }
    }
}
```

**编译并执行代码后，输出为：**

```
Creating child thread

Child Thread started

0

1

Aborting child thread

Exception caught

Exception is not handled
```

## 第 21 章：事件

事件是预期会发生的事情。在 C# 中，事件是用户操作（如单击、按键、鼠标移动）或诸如系统生成的通知[52]之类的发生情况。应用程序应在事件发生后对其作出响应。一个很好的例子是中断的发生。事件用于促进进程间通信。

事件在类中声明，并通过同一类或另一个类中的委托与事件处理程序关联。包含事件的类用于发布事件。这样的类称为 *发布者* 类。接受事件的类称为 *订阅者* 类。这意味着事件依赖于发布者-订阅者模型。

*发布者* 是同时包含事件和委托定义的对象。事件与委托之间的关联在此对象中定义。发布者类的对象调用事件，而事件又会被通知给其他对象。

*订阅者* 是接受事件并提供事件处理程序的对象。发布者类有一个委托，该委托调用订阅者类的方法（事件处理程序）。

### 事件声明

要在类中声明事件，首先应为该事件声明一个委托类型。之后，才能使用 *event* 关键字[53]声明事件。下面是一个示例：

```csharp
public delegate void myEvent();
public event myEvent myEvent;
```

因此，我们使用了 *event* 关键字使其成为事件。下面是一个完整示例：

```csharp
using System;

public class DisplayHelper
{
    // declare the delegate
    public delegate void BeforeDisplay();

    // declare an event of type delegate
    public event BeforeDisplay beforeDisplayEvent;

    public DisplayHelper()
    {

    }

    public void DisplayNumber(int x)
    {
        // call the delegate method before moving to display
        if (beforeDisplayEvent != null)
            beforeDisplayEvent();

        Console.WriteLine("Number: {0,-12:N0}", x);
    }

    public void PrintDecimal(int dec)
    {
        if (beforeDisplayEvent != null)
            beforeDisplayEvent();

        Console.WriteLine("Decimal: {0:G}", dec);
    }

    public void DisplayMoney(int amount)
    {
        if (beforeDisplayEvent != null)
            beforeDisplayEvent();

        Console.WriteLine("Money: {0:C}", amount);
    }

    public void DisplayTemperature(int x)
    {
        if (beforeDisplayEvent != null)
            beforeDisplayEvent();

        Console.WriteLine("Temperature: {0:4:N1} F", x);
    }

    public void DisplayHexadecimal(int dec)
    {
        if (beforeDisplayEvent != null)
            beforeDisplayEvent();

        Console.WriteLine("Hexadecimal: {0:X}", dec);
    }
}
```

*DisplayHelper* 是一个发布者类，负责发布 *beforeDisplayEvent* 事件。在每个显示方法之前，它首先检查 *beforeDisplayEvent* 是否不为 null，然后调用 *beforeDisplayEvent()* 方法。

现在我们需要创建一个订阅者。考虑下面给出的类：

```csharp
using System;

public class MyProgram
```
