
## 第一部分：C# 基础

![](img/a977a875c7c627b45d939729705a252e_319_0.png)

图 10-2

图 10-3 以图形方式展示了两个不同的执行线程。

![](img/a977a875c7c627b45d939729705a252e_319_1.png)

图 10-3

如 图 10-2 所示，恰好在 DoSomething() 方法获得执行机会之前，主线程已经继续执行其下一条语句。因此，输出显示主线程在 DoSomething() 方法之前执行。实际上，两个线程都有平等的执行机会，其中一种可能的输出可能是：

```
Doing something...
Doing something...
Continuing with the execution...
Doing something...
Doing something...
...
```

线程执行直到：

- [ ] 它到达生命终点（方法退出），或
- [ ] 你过早地终止（中止）它。

### 中止线程

你可以使用 Thread 类的 Abort() 方法在线程开始执行后中止该线程。
这里有一个示例：

```
class Program
{
    static void Main(string[] args)
    {
        Thread t = new Thread(new ThreadStart(DoSomething));
        t.Start();
        Console.WriteLine("Continuing with the execution...");

        while (!t.IsAlive) ;

        Thread.Sleep(1);
        t.Abort();

        Console.ReadLine();
    }

    static void DoSomething()
    {
        try
        {
            while (true)
            {
                Console.WriteLine("Doing something...");
            }
        }
        catch (ThreadAbortException ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

当线程启动时，你继续执行下一条语句并打印出消息 "Continuing with the execution..." 。你随后使用 Thread 类的 IsAlive 属性来了解线程的执行状态，并通过 while 语句阻塞 Main() 函数的执行，直到线程有机会启动。Thread 类的 Sleep() 方法会阻塞当前线程（Main()）指定的毫秒数。使用此语句，本质上是给 DoSomething() 函数一个执行的机会。最后，你使用 Thread 类的 Abort() 方法来终止线程。

## 第一部分：C# 基础

ThreadAbortException 异常会在你终止的任何线程上触发。理想情况下，你应该在此异常处理程序中清理资源（通过 finally 语句）：

```csharp
static void DoSomething()
{
    try
    {
        while (true)
        {
            Console.WriteLine("Doing something...");
        }
    }
    catch (ThreadAbortException ex)
    {
        Console.WriteLine(ex.Message);
    }
    finally {
        //---clean up your resources here---
    }
}
```

前述程序的输出可能如下所示：

```
Continuing with the execution...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread was being aborted.
```

请注意我说程序可能如下所示。当你的应用程序中有多个线程运行时，你无法控制哪个线程先执行。操作系统决定实际的执行顺序，这取决于 CPU 利用率、内存使用等多个因素。因此，输出也可能如下所示：

```
Doing something...
Continuing with the execution...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread was being aborted.
```

虽然你可以使用 Abort() 方法来终止线程，但只要有可能，优雅地退出总是更好的选择。

以下是前述程序的重写：

```
class Program
{
    private static volatile bool _stopThread = false;

    static void Main(string[] args)
    {
        Thread t = new Thread(new ThreadStart(DoSomething));
        t.Start();

        Console.WriteLine("Continuing with the execution...");

        while (!t.IsAlive) ;
        Thread.Sleep(1);
        _stopThread = true;
        Console.WriteLine("Thread ended.");
        Console.ReadLine();
    }

    static void DoSomething()
    {
        try
        {
            while (! _stopThread)
            {
                Console.WriteLine("Doing something...");
            }
        }
        catch (ThreadAbortException ex)
        {
            Console.WriteLine(ex.Message);
        }
        finally {
            //---clean up your resources here---
        }
    }
}
```

首先，你声明一个名为 _stopThread 的静态 Boolean 变量：

```
private static volatile bool _stopThread = false;
```

请注意你在声明前加上了 volatile 关键字，它用作编译器的提示，表明该变量将被多个线程访问。然后该变量不会受到编译器优化的影响，并且始终具有最新的值。

要使用 _stopThread 变量来停止线程，你可以像这样修改 DoSomething() 函数：

```
while (! _stopThread)
{
    Console.WriteLine("Doing something...");
}
```

## 第一部分：C# 基础

最后，要在 `Main()` 函数中停止线程，你只需将 `_stopThread` 变量设置为 `true`：

```
_stopThread = true;
Console.WriteLine("Thread ended.");
```

此程序的输出 *可能* 如下所示：

```
Continuing with the execution.
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread ended.
Doing something...
```

在 `"Thread ended."` 消息之后，`DoSomething()` 函数可能会再打印一条消息。这是因为线程可能不会立即结束。为了确保 `"Thread ended."` 消息仅在 `DoSomething()` 函数结束后再打印，你可以使用 Thread 类的 `Join()` 方法将两个线程连接起来：

```
static void Main(string[] args)
{
    Thread t = new Thread(new ThreadStart(DoSomething));
    t.Start();

    Console.WriteLine("Continuing with the execution...");

    while (!t.IsAlive) ;

    Thread.Sleep(1);
    _stopThread = true;

    //---joins the current thread (Main()) to t---
    t.Join();
    Console.WriteLine("Thread ended.");
    Console.ReadLine();
}
```

`Join()` 方法本质上会阻塞调用线程，直到线程终止。在这种情况下，Thread ended 消息将被阻塞，直到线程（`t`）终止。

程序的输出现在如下所示：

```
Continuing with the execution.
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Doing something...
Thread ended.
```

图 10-4 以图形方式展示了两个不同的执行线程。

![](img/a977a875c7c627b45d939729705a252e_324_0.png)

图 10-4

### 向线程传递参数

在之前的几个示例中，你已经看到如何使用 ThreadStart 委托指向一个方法来创建线程。不过，到目前为止，你指向的方法没有任何参数：

```csharp
static void DoSomething()
{
    ...
    ...
}
```

如果要作为线程调用的函数有一个参数呢？在这种情况下，你有两个选择：

- 将函数封装在类中，并通过属性传入参数。
- 改用 ParameterizedThreadStart 委托而不是 ThreadStart 委托。

使用相同的示例，第一种选择是将 DoSomething() 方法封装为一个类，然后公开一个属性来接收参数值：

```csharp
class Program
{
    static void Main(string[] args)
    {
        SomeClass sc = new SomeClass();
        sc.msg = "useful";
        Thread t = new Thread(new ThreadStart(sc.DoSomething));
        t.Start();
    }
}

class SomeClass
```

(continued)

```
{
    public string msg { get; set; }
    public void DoSomething()
    {
        try
        {
            while (true)
            {
                Console.WriteLine("Doing something... {0}", msg);
            }
        }
        catch (ThreadAbortException ex)
        {
            Console.WriteLine(ex.Message);
        }
        finally
        {
            //---clean up your resources here---
        }
    }
}
```

在此示例中，你通过创建 SomeClass 类的新实例来为 DoSomething() 方法创建线程，然后通过 msg 属性传入值。

对于第二种选择，你使用 ParameterizedThreadStart 委托而不是 ThreadStart 委托。ParameterizedThreadStart 委托接受一个 object 类型的参数，因此如果要作为线程调用的函数有一个参数，该参数必须是 object 类型。

要了解如何使用 ParameterizedThreadStart 委托，请通过添加参数来修改 DoSomething() 函数：

```csharp
static void DoSomething(object msg)
{
    try
    {
        while (true)
        {
            Console.WriteLine("Doing something... {0}", msg);
        }
    }
    catch (ThreadAbortException ex)
    {
        Console.WriteLine(ex.Message);
    }
    finally {
        //---clean up your resources here---
    }
}
```
