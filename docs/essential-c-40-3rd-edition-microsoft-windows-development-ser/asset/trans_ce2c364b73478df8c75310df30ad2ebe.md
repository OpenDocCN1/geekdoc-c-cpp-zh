

比原生（指针大小）整数大的值不会被部分读取或写入。因此，假设是 64 位操作系统，对 long（64 位）的读取和写入将是原子的。但是，对 128 位变量（如 decimal）的读取和写入可能不是原子的。因此，更改 decimal 变量的写入操作可能在仅复制了 32 位后被中断，导致读取到错误的值，称为撕裂读。

## 初学者主题

### 多线程与局部变量

请注意，无需同步局部变量。局部变量被加载到堆栈上，每个线程都有自己的逻辑堆栈。因此，每个局部变量对每个方法调用都有自己的实例。默认情况下，局部变量不在方法调用之间共享；因此，它们也不在多个线程之间共享。

但是，这并不意味着局部变量完全没有并发问题，因为代码很容易将局部变量暴露给多个线程。例如，一个在迭代之间共享局部变量的并行 for 循环，会将变量暴露给并发访问和竞态条件（请参阅清单 19.2）。

### 清单 19.2: 未同步的局部变量

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    public static void Main()
    {
        int x = 0;
        Parallel.For(0, int.MaxValue, i =>
        {
            x++;
            x--;
        });
        Console.WriteLine("Count = {0}", x);
    }
}
```

在此示例中，x（一个局部变量）在并行 for 循环中被访问，因此多个线程将同时修改它，创建一个与清单 19.1 非常相似的竞态条件。尽管 x 递增和递减的次数相同，输出不太可能产生值 0。

### 使用 Monitor 进行同步

要同步多个线程，使它们无法同时执行特定的代码段，请使用监视器在第一个线程退出该代码段之前阻止第二个线程进入受保护的代码段。监视器功能是名为 System.Threading.Monitor 的类的一部分，受保护代码段的开始和结束分别通过调用静态方法 Monitor.Enter() 和 Monitor.Exit() 来标记。

### 清单 19.3: 显式使用 Monitor 进行同步

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    readonly static object _Sync = new object();
    const int _Total = int.MaxValue;
    static long _Count = 0;

    public static void Main()
    {
        Task task = Task.Factory.StartNew(Decrement);

        // Increment
        for (int i = 0; i < _Total; i++)
        {
            bool lockTaken = false;
            Monitor.Enter(_Sync, ref lockTaken);
            try
            {
                _Count++;
            }
            finally
            {
                if (lockTaken)
                {
                    Monitor.Exit(_Sync);
                }
            }
        }

        task.Wait();
        Console.WriteLine("Count = {0}", _Count);
    }

    static void Decrement()
    {
        for (int i = 0; i < _Total; i++)
        {
            bool lockTaken = false;
            Monitor.Enter(_Sync, ref lockTaken);
            try
            {
                _Count--;
            }
            finally
            {
                if (lockTaken)
                {
                    Monitor.Exit(_Sync);
                }
            }
        }
    }
}
```

清单 19.3 的结果显示在输出 19.2 中。

### 输出 19.2:

```
Count = 0
```

请注意，Monitor.Enter() 和 Monitor.Exit() 的调用通过共享作为参数传递的相同对象引用（在此例中为 _Sync）相互关联。

接受 lockTaken 参数的 Monitor.Enter() 重载方法仅在 .NET 4.0 中添加到框架。在此之前，没有这样的 lockTaken 参数可用，也无法可靠地捕获在 Monitor.Enter() 和 try 块之间发生的异常。将 try 块紧跟在 Monitor.Enter() 调用之后在发布代码中是可靠的，因为 JIT 阻止了任何此类异步异常混入。但是，除了紧跟在 Monitor.Enter() 之后的 try 块之外的任何内容（包括编译器可能在调试代码中注入的任何指令）都可能阻止 JIT 可靠地将执行返回到 try 块中。因此，如果确实发生异常，它将泄漏锁（锁保持获取状态），而不是执行 finally 块并释放它——这可能会在另一个线程尝试获取锁时导致死锁。

Monitor 还支持 Pulse() 方法，允许线程进入“就绪队列”，表明它是下一个要执行的线程。这是同步生产者-消费者模式的常见手段，以确保在有“生产”之前不会发生“消费”。拥有监视器的生产者线程（通过调用 Monitor.Enter()）调用 Monitor.Pulse() 来向消费者线程（可能已经调用了 Monitor.Enter()）发出信号，表明有项目可供消费，所以“准备好”。对于单个 Pulse() 调用，只有一个线程（在此例中为消费者）可以进入就绪队列。当生产者线程调用 Monitor.Exit() 时，消费者线程获取锁（Monitor.Enter() 完成）并进入临界区以开始“消费”项目。一旦消费者处理完等待的项目，它就会调用 Exit()，从而允许生产者（当前因 Monitor.Enter() 而阻塞）再次生产。在此示例中，一次只能有一个线程进入就绪队列，确保没有“生产”就不会有“消费”，反之亦然。

## 使用 lock 关键字

由于多线程代码中频繁需要使用 Monitor 进行同步，而且 try/finally 块很容易被遗忘，C# 提供了一个特殊关键字来处理这种锁定同步模式。清单 19.4 演示了 lock 关键字的用法，输出 19.3 显示了结果。

### 清单 19.4: 使用 lock 关键字进行同步

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    readonly static object _Sync = new object();
    const int _Total = int.MaxValue;
    static long _Count = 0;

    public static void Main()
    {
        Task task = Task.Factory.StartNew(Decrement);

        // Increment
        for (int i = 0; i < _Total; i++)
        {
            lock (_Sync)
            {
                _Count++;
            }
        }

        task.Wait();
        Console.WriteLine("Count = {0}", _Count);
    }

    static void Decrement()
    {
        for (int i = 0; i < _Total; i++)
        {
            lock (_Sync)
            {
                _Count--;
            }
        }
    }
}
```

### 输出 19.3:

```
Count = 0
```

通过锁定访问 _Count 的代码段（使用 lock 或 Monitor），您使 Main() 和 Decrement() 方法成为线程安全的，这意味着它们可以从多个线程同时安全调用。（在 C# 4.0 之前，概念是相同的，只是编译器生成的代码依赖于不带 lockTaken 参数的 Monitor.Enter() 方法，并且 Monitor.Enter() 调用是在 try 块之前发出的。）

同步会带来性能开销。例如，清单 19.4 的执行时间比清单 19.1 长一个数量级，这表明 lock 的执行相对较慢，相比于递增和递减计数的执行。

即使 lock 与其同步的工作相比微不足道，程序员也应避免不加选择地进行同步，以避免死锁的可能性，以及在多处理器计算机上本可以并行执行代码时进行不必要的同步。对象设计的一般最佳实践是同步可变的静态状态（无需同步永不更改的内容），而不是任何实例数据。允许多个线程访问特定对象的程序员必须为该对象提供同步。任何显式处理线程的类都可能希望在一定程度上使其实例成为线程安全的。

### 选择 lock 对象

无论是否显式使用 lock 关键字或 Monitor 类，程序员仔细选择锁对象都至关重要。

在前面的示例中，同步变量 _Sync 被声明为 private 和 readonly。它被声明为 readonly 是为了确保在 Monitor.Enter() 和 Monitor.Exit() 调用之间值不会更改。这使得进入和退出同步块之间能够相互关联。

