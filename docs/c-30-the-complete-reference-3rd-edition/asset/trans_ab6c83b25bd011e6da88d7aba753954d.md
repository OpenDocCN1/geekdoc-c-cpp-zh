
```
class MoreThreads {
    static void Main() {
        Console.WriteLine("Main thread starting.");

        // Construct three threads.
        MyThread mt1 = new MyThread("Child #1");
        MyThread mt2 = new MyThread("Child #2");
        MyThread mt3 = new MyThread("Child #3");

        do {
            Console.Write(".");
            Thread.Sleep(100);
        } while (mt1.Count < 10 ||
            mt2.Count < 10 ||
            mt3.Count < 10);

        Console.WriteLine("Main thread ending.");
    }
}
```

此程序的示例输出如下所示：

```
Main thread starting.
.Child #1 starting.
Child #2 starting.
Child #3 starting.
....In Child #1, Count is 0
In Child #2, Count is 0
In Child #3, Count is 0
.....In Child #1, Count is 1
In Child #2, Count is 1
In Child #3, Count is 1
.....In Child #1, Count is 2
In Child #2, Count is 2
In Child #3, Count is 2
.....In Child #1, Count is 3
In Child #2, Count is 3
In Child #3, Count is 3
.....In Child #1, Count is 4
In Child #2, Count is 4
In Child #3, Count is 4
.....In Child #1, Count is 5
In Child #2, Count is 5
In Child #3, Count is 5
.....In Child #1, Count is 6
In Child #2, Count is 6
In Child #3, Count is 6
.....In Child #1, Count is 7
In Child #2, Count is 7
In Child #3, Count is 7
.....In Child #1, Count is 8
In Child #2, Count is 8
In Child #3, Count is 8
.....In Child #1, Count is 9
Child #1 terminating.
In Child #2, Count is 9
Child #2 terminating.
In Child #3, Count is 9
Child #3 terminating.
Main thread ending.
```

如你所见，三个子线程一旦启动，便会共享 CPU。此外，由于系统配置、操作系统和其他环境因素的差异，当你运行该程序时，看到的输出可能与这里显示的略有不同。

## 确定线程何时结束

通常，了解线程何时结束非常有用。在前面的示例中，我们通过观察 Count 变量来尝试实现这一点——这很难算是一种令人满意或可推广的解决方案。幸运的是，Thread 提供了两种方法来确定线程是否已结束。首先，你可以查询线程的只读 IsAlive 属性。它的定义如下：

```
public bool IsAlive { get; }
```

如果调用该属性的线程仍在运行，IsAlive 返回 true；否则返回 false。若要试验 IsAlive，请用下面这个版本的 MoreThreads 替换前面程序中的版本：

```
// Use IsAlive to wait for threads to end.
class MoreThreads {
  static void Main() {
    Console.WriteLine("Main thread starting.");

    // Construct three threads.
    MyThread mt1 = new MyThread("Child #1");
    MyThread mt2 = new MyThread("Child #2");
    MyThread mt3 = new MyThread("Child #3");

    do {
      Console.Write(".");
      Thread.Sleep(100);
    } while (mt1.Thrd.IsAlive &&
            mt2.Thrd.IsAlive &&
            mt3.Thrd.IsAlive);

    Console.WriteLine("Main thread ending.");
  }
}
```

该版本产生的输出与之前相同。唯一区别是它使用 IsAlive 来等待子线程终止。

另一种等待线程结束的方法是调用 Join()。其最简单的形式如下所示：

```
public void Join()
```

Join() 会一直等待，直到在其上被调用的线程终止。其名称源于调用线程等待指定线程加入它的概念。如果线程尚未启动，将抛出 ThreadStateException。Join() 的其他重载形式允许你指定希望等待指定线程终止的最长时间。

下面是一个使用 Join() 来确保主线程最后一个停止的程序：

```
// Use Join().
using System;
using System.Threading;

class MyThread {
    public int Count;
    public Thread Thrd;

    public MyThread(string name) {
        Count = 0;
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {
        Console.WriteLine(Thrd.Name + " starting.");
        do {
            Thread.Sleep(500);
            Console.WriteLine("In " + Thrd.Name +
                ", Count is " + Count);
            Count++;
        } while(Count < 10);
        Console.WriteLine(Thrd.Name + " terminating.");
    }
}

// Use Join() to wait for threads to end.
class JoinThreads {
    static void Main() {
        Console.WriteLine("Main thread starting.");

        // Construct three threads.
        MyThread mt1 = new MyThread("Child #1");
        MyThread mt2 = new MyThread("Child #2");
        MyThread mt3 = new MyThread("Child #3");

        mt1.Thrd.Join();
        Console.WriteLine("Child #1 joined.");

        mt2.Thrd.Join();
        Console.WriteLine("Child #2 joined.");

        mt3.Thrd.Join();
        Console.WriteLine("Child #3 joined.");
        Console.WriteLine("Main thread ending.");
    }
}
```

该程序的示例输出如下所示。请记住，当你运行程序时，你的输出可能会略有不同。

```
Main thread starting.
Child #1 starting.
Child #2 starting.
Child #3 starting.
In Child #1, Count is 0
In Child #2, Count is 0
In Child #3, Count is 0
In Child #1, Count is 1
In Child #2, Count is 1
In Child #3, Count is 1
In Child #1, Count is 2
In Child #2, Count is 2
In Child #3, Count is 2
In Child #1, Count is 3
In Child #2, Count is 3
In Child #3, Count is 3
In Child #1, Count is 4
In Child #2, Count is 4
In Child #3, Count is 4
In Child #1, Count is 5
In Child #2, Count is 5
In Child #3, Count is 5
In Child #1, Count is 6
In Child #2, Count is 6
In Child #3, Count is 6
In Child #1, Count is 7
In Child #2, Count is 7
In Child #3, Count is 7
In Child #1, Count is 8
In Child #2, Count is 8
In Child #3, Count is 8
In Child #1, Count is 9
Child #1 terminating.
In Child #2, Count is 9
Child #2 terminating.
In Child #3, Count is 9
Child #3 terminating.
Child #1 joined.
Child #2 joined.
Child #3 joined.
Main thread ending.
```

如你所见，在调用 Join() 返回之后，线程已经停止执行。

## 向线程传递参数

在 .NET Framework 的早期，线程启动时无法向其传递参数，因为作为线程入口点的方法不能有参数。如果需要向线程传递信息，就需要各种变通方法（例如使用共享变量）。不过，这一缺陷后来得到了修复，如今已经可以向线程传递参数了。要做到这一点，你必须使用不同形式的 Start()、Thread 构造函数和入口点方法。

通过下面这个版本的 Start() 可以将参数传递给线程：

```
public void Start(object arg)
```

传递给 arg 的对象会被自动传递给线程的入口点方法。因此，要向线程传递参数，只需将其传递给 Start() 即可。

要使用带参数的 Start() 版本，你必须使用以下形式的 Thread 构造函数：

```
public Thread(ParameterizedThreadStart entryPoint)
```

这里，entryPoint 是将被调用来开始执行线程的方法的名称。注意，在此版本中，entryPoint 的类型是 ParameterizedThreadStart，而非前面示例中使用的 ThreadStart。ParameterizedThreadStart 是一个委托，其声明如下：

```
public delegate void ParameterizedThreadStart(object arg)
```

如你所见，该委托接受一个 object 类型的参数。因此，要使用这种形式的 Thread 构造函数，线程入口点方法必须有一个 object 参数。

下面是一个演示向线程传递参数的示例：

```
// Passing an argument to the thread method.
using System;
using System.Threading;

class MyThread {
    public int Count;
    public Thread Thrd;

    // Notice that MyThread is also passed an int value.
    public MyThread(string name, int num) {
        Count = 0;

        // Explicitly invoke ParameterizedThreadStart constructor
        // for the sake of illustration.
        Thrd = new Thread(this.Run);

        Thrd.Name = name;

        // Here, Start() is passed num as an argument.
        Thrd.Start(num);
    }
}
```

