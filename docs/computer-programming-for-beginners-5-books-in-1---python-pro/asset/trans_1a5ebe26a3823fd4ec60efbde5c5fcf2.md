
```csharp
Console.WriteLine("Number: {0,-12:N0}", x);
}

public static void DisplayMoney(int amount)
{
    Console.WriteLine("Money: {0:C}", amount);
}
public static void DisplayHexadecimal(int dec)
{
    Console.WriteLine("Hexadecimal: {0:X}", dec);
}
}
```

该代码将输出以下结果：

![](img/239ff1e8a63502805c86c4dfbd71509a_619_0.png)

在上面的示例中，我们将 Display 指向三个方法，即 DisplayNumber、DisplayMoney 和 DisplayHexadecimal。这使它成为一个多播委托。这意味着当调用 displayDel 时，它会依次调用所有三个方法。

## 第20章：C# 中的多线程

线程定义控制流。线程是操作系统分配线程的基本单位。线程的执行在程序内是独立的。

单个进程使用一个线程执行。这样的进程称为单线程进程。一次只能执行一个任务。用户必须等待任务完成后才能执行新任务。

为了同时执行多个线程，会创建多个线程。创建两个或更多线程的进程称为多线程。[45]

### 线程的生命周期

线程的生命周期始于创建 **System.Threading.Thread** 类的对象时。任务完成后生命周期即结束。线程的生命周期中有多种状态。

- **未启动状态：** 当创建 **Thread** 类的实例时，线程进入未启动状态。
- **就绪状态：** 线程处于此状态，直到程序调用 **Start()** 方法。
- **不可运行状态：** 使线程不处于可运行状态的一些因素包括：
  1. **等待：** 调用 Wait() 方法使线程等待指定条件
  2. **阻塞：** 线程被 I/O 操作阻塞
  3. **休眠：** 调用 Sleep() 方法使线程进入休眠模式。
- **死亡状态：** 一旦线程完成执行或被中止，它便处于死亡状态

### 主线程

在使用线程时，我们会使用 **System.Threading.Thread** 类。主线程在程序开始执行时即被创建。**Thread** 类用于创建线程。这些线程称为子线程。用户可以使用 Thread 类的 **CurrentThread** 属性访问主线程。

*示例：*

```csharp
using System;
namespace thread
{
    class MainThread
    {
        static void Main(string[] args)
        {
            Thread t1 = Thread.CurrentThread;
            t1.Name="Thread1";
            Console.WriteLine("Thread is:{0}",t1.Name);
            Console.Read();
        }
    }
}
```

编译并执行代码后，输出为：

Thread is: Thread1

### Thread 类的属性和方法

属性<sup>ds</sup>：

- **IsAlive：** 显示当前线程执行状态的值
- **CurrentThread：** 检索当前正在运行的线程
- **CurrentContext：** 检索线程执行所在的当前上下文
  - **ExecutionContext：** ExecutionContext 对象包含有关不同上下文的信息
- **Name：** 获取或设置线程的名称
- **ThreadState：** 包含当前线程状态的值
- **Priority：** 获取或设置表示线程调度优先级的值

**方法：**

- **public static void BeginThreadAffinity()：** 宿主即将执行依赖于当前物理操作系统线程的指令。
- **public void Abort()：** 在其上调用时，线程中会引发 ThreadAbortException。
- **public void Interrupt()：** 处于 WaitSleepJoin 状态的线程被中断
- **public static AppDomain GetDomain()：** 返回唯一的域标识符
- **public static void MemoryBarrier()：** 处理器执行当前线程。指令不能重新排序。
- **public void Start()：** 启动线程
- **public static bool Yield()：** 调用线程将执行让给另一个已准备好在该处理器上运行的线程

### 创建和管理线程 [42]

扩展的线程类会创建线程。扩展的线程类调用 **Start()** 方法来启动子线程执行。

#### 示例：

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

Creating child thread

Start child thread

#### 管理线程

当需要将线程暂停一段时间以便另一个线程可以执行时，可使用 **Thread.Sleep()** 方法。该方法接受一个以毫秒为单位表示时间的参数。

#### 示例：

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

            Console.WriteLine("Thread sleeping for {0} seconds",sleeptime / 1000);
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

child thread created

Start child thread

Thread sleeping for 4 seconds

Resume child thread

### 销毁线程

**Thread.Abort()** 方法用于销毁线程。销毁线程时会引发 **ThreadAbortException**。该异常不会被捕获，并会被发送到 **finally** 块。

#### 示例：

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
                for(int j = 0; j <= 10; j++)
                {
                    Thread.Sleep(1000);
                    Console.WriteLine("Child thread finished");
                }
            }
            catch(ThreadAbortException e)
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
            Console.WriteLine("Creating child thread");
            Thread t2 = new Thread(t1);
            t2.Start();

            //main thread is stopped
            Thread.Sleep(2000);

            //child thread aborted
            Console.WriteLine("Aborting child thread");
            t2.Abort();
            Console.Read();
        }
    }
}
```

**编译并执行代码后，输出为：**

Creating child thread

Child Thread started

0

1

Aborting child thread

Exception caught

Exception is not handled

## 第21章：事件

事件是预期会发生的事情。在 C# 中，事件是用户操作（如单击、按键、鼠标移动）或系统生成的通知<sup>148</sup> 等发生情况。应用程序应在事件发生后对其作出响应。一个很好的例子是中断的发生。事件用于促进进程间通信。

事件在类中声明，并通过同一类或另一个类中的委托与事件处理程序关联。包含事件的类用于发布事件。这样的类称为 *发布者* 类。接受事件的类称为 *订阅者* 类。这意味着事件依赖于发布者-订阅者模型。

发布者是同时包含事件和委托定义的对象。事件与委托之间的关联在此对象中定义。发布者类的对象调用事件，而事件又会通知其他对象。

订阅者是接受事件并提供事件处理程序的对象。发布者类有一个委托，用于调用订阅者类的方法（事件处理程序）。

### 事件声明

要在类中声明事件，首先应为事件声明委托类型。在此之后，你可以使用 *event* 关键字<sup>149</sup> 声明事件。以下是一个示例：

```csharp
public delegate void myEvent();
public event myEvent myEvent;
```

因此，我们使用了 *event* 关键字将其设为事件。以下是一个完整示例：

```csharp
using System;
public class DisplayHelper
{
    // declare the delegate
    public delegate void BeforeDisplay();
```
