
## 使用 MethodImplAttribute

可以通过使用 MethodImplAttribute 属性来同步整个方法。这种方法可作为 lock 语句的替代方案，用于需要锁定方法全部内容的情况。MethodImplAttribute 定义在 System.Runtime.CompilerServices 命名空间中。适用于同步的构造函数如下所示：

```
public MethodImplAttribute(MethodImplOptions opt)
```

这里，opt 指定实现属性。要同步方法，请指定 MethodImplOptions.Synchronized。该属性会导致整个方法在实例上被锁定（即通过 this）。（对于静态方法，则锁定类型。）因此，它不得用于公共对象或与公共类一起使用。

以下是使用 MethodImplAttribute 提供同步的 TickTock 类的重写版本：

// Use MethodImplAttribute to synchronize a method.
using System;
using System.Threading;
using System.Runtime.CompilerServices;
// Rewrite of TickTock to use MethodImplOptions.Synchronized.
class TickTock {
    /* The following attribute synchronizes the entire
    Tick() method. */
    [MethodImplAttribute(MethodImplOptions.Synchronized)]
    public void Tick(bool running) {
        if(!running) { // stop the clock
            Monitor.Pulse(this); // notify any waiting threads
            return;
        }
        Console.Write("Tick ");
        Monitor.Pulse(this); // let Tock() run
        Monitor.Wait(this); // wait for Tock() to complete
    }
    /* The following attribute synchronizes the entire
    Tock() method. */
    [MethodImplAttribute(MethodImplOptions.Synchronized)]
    public void Tock(bool running) {
        if(!running) { // stop the clock
            Monitor.Pulse(this); // notify any waiting threads
            return;
        }
        Console.WriteLine("Tock");
        Monitor.Pulse(this); // let Tick() run
        Monitor.Wait(this); // wait for Tick() to complete
    }
}

class MyThread {
  public Thread Thrd;
  TickTock ttOb;

  // Construct a new thread.
  public MyThread(string name, TickTock tt) {
    Thrd = new Thread(this.Run);
    ttOb = tt;
    Thrd.Name = name;
    Thrd.Start();
  }

  // Begin execution of new thread.
  void Run() {
    if (Thrd.Name == "Tick") {
      for (int i=0; i<5; i++) ttOb.Tick(true);
      ttOb.Tick(false);
    }
    else {
      for (int i=0; i<5; i++) ttOb.Tock(true);
      ttOb.Tock(false);
    }
  }
}

class TickingClock {
  static void Main() {
    TickTock tt = new TickTock();
    MyThread mt1 = new MyThread("Tick", tt);
    MyThread mt2 = new MyThread("Tock", tt);

    mt1.Thrd.Join();
    mt2.Thrd.Join();
    Console.WriteLine("Clock Stopped");
  }
}
```

正确的 Tick Tock 输出与之前相同。

只要被同步的方法不是由公共类定义或在公共对象上调用，那么使用 lock 还是 MethodImplAttribute 由你决定。两者产生相同的结果。由于 lock 是 C# 内置的关键字，本书中的示例将使用这种方法。

> **记住** 不要对公共类或公共实例使用 MethodImplAttribute。相反，请使用 lock，并在私有对象上加锁（如前所述）。

## 使用 Mutex 和 Semaphore

尽管 C# 的 lock 语句足以满足许多同步需求，但某些情况，例如限制对共享资源的访问，有时更方便地由 .NET Framework 内置的其他同步机制处理。这里描述的两个机制相互关联：互斥体和信号量。

### Mutex

互斥体是一个互斥的同步对象。这意味着它一次只能被一个且仅一个线程获取。互斥体设计用于共享资源一次只能被一个线程使用的情况。例如，想象一个日志文件被多个进程共享，但同一时间只有一个进程可以向该文件写入。互斥体是处理这种情况的完美同步设备。

互斥体由 System.Threading.Mutex 类支持。它有多个构造函数。两个常用的构造函数如下所示：

```
public Mutex()
public Mutex(bool owned)
```

第一个版本创建初始时未被拥有的互斥体。在第二个版本中，如果 owned 为 true，则互斥体的初始状态由调用线程拥有。否则，它未被拥有。

要获取互斥体，代码将对互斥体调用 WaitOne()。此方法由 Mutex 从 Thread.WaitHandle 类继承。它的最简单形式如下：

```
public bool WaitOne();
```

它会等待直到调用它的互斥体可以被获取。因此，它会阻塞调用线程的执行，直到指定的互斥体可用。它始终返回 true。

当代码不再需要互斥体的所有权时，它通过调用 ReleaseMutex() 来释放它，如下所示：

```
public void ReleaseMutex()
```

这会释放调用它的互斥体，使其他线程能够获取该互斥体。

要使用互斥体同步对共享资源的访问，你将使用 WaitOne() 和 ReleaseMutex()，如下所示：

```
Mutex myMtx = new Mutex();

// ...

myMtx.WaitOne(); // wait to acquire the mutex

// Access the shared resource.

myMtx.ReleaseMutex(); // release the mutex
```

当调用 WaitOne() 时，线程的执行将暂停，直到可以获取互斥体。当调用 ReleaseMutex() 时，互斥体被释放，另一个线程可以获取它。使用这种方法，可以将对共享资源的访问限制为一次一个线程。

以下程序将此框架付诸实践。它创建了两个线程，**IncThread** 和 **DecThread**，它们都访问名为 **SharedRes.Count** 的共享资源。**IncThread** 增加 **SharedRes.Count**，而 **DecThread** 递减它。为了防止两个线程同时访问 **SharedRes.Count**，访问由 **SharedRes** 类的一部分的 **Mtx** 互斥体同步。

```csharp
// Use a Mutex.

using System;
using System.Threading;

// This class contains a shared resource (Count),
// and a mutex (Mtx) to control access to it.
class SharedRes {
    public static int Count = 0;
    public static Mutex Mtx = new Mutex();
}

// This thread increments SharedRes.Count.
class IncThread {
    int num;
    public Thread Thrd;

    public IncThread(string name, int n) {
        Thrd = new Thread(this.Run);
        num = n;
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {

        Console.WriteLine(Thrd.Name + " is waiting for the mutex.");

        // Acquire the Mutex.
        SharedRes.Mtx.WaitOne();

        Console.WriteLine(Thrd.Name + " acquires the mutex.");

        do {
            Thread.Sleep(500);
            SharedRes.Count++;
            Console.WriteLine("In " + Thrd.Name +
                              ", SharedRes.Count is " + SharedRes.Count);
            num--;
        } while(num > 0);

        Console.WriteLine(Thrd.Name + " releases the mutex.");

        // Release the Mutex.
        SharedRes.Mtx.ReleaseMutex();
    }
}
```

```csharp
// This thread decrements SharedRes.Count.
class DecThread {
    int num;
    public Thread Thrd;

    public DecThread(string name, int n) {
        Thrd = new Thread(new ThreadStart(this.Run));
        num = n;
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {

        Console.WriteLine(Thrd.Name + " is waiting for the mutex.");

        // Acquire the Mutex.
        SharedRes.Mtx.WaitOne();

        Console.WriteLine(Thrd.Name + " acquires the mutex.");

        do {
            Thread.Sleep(500);
            SharedRes.Count--;
            Console.WriteLine("In " + Thrd.Name +
                ", SharedRes.Count is " + SharedRes.Count);
            num--;
        } while(num > 0);

        Console.WriteLine(Thrd.Name + " releases the mutex.");

        // Release the Mutex.
        SharedRes.Mtx.ReleaseMutex();
    }
}

class MutexDemo {
    static void Main() {
        // Construct three threads.
        IncThread mt1 = new IncThread("Increment Thread", 5);

        Thread.Sleep(1); // let the Increment thread start

        DecThread mt2 = new DecThread("Decrement Thread", 5);

        mt1.Thrd.Join();
        mt2.Thrd.Join();
    }
}
```

输出如下所示：

Increment Thread is waiting for the mutex.
Increment Thread acquires the mutex.
