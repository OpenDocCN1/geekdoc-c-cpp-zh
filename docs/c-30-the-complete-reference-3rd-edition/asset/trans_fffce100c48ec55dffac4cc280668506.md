
下面是 Pulse() 和 PulseAll() 的一般形式：

```
public static void Pulse(object waitOb)
public static void PulseAll(object waitOb)
```

其中，waitOb 是正在被释放的对象。

如果从不在同步代码（例如 lock 块）内的代码中调用 Wait()、Pulse() 或 PulseAll()，则将抛出 SynchronizationLockException。

## 使用 Wait() 和 Pulse() 的示例

为了理解 Wait() 和 Pulse() 的必要性及其应用，我们将创建一个程序，通过在屏幕上显示单词“Tick”和“Tock”来模拟时钟的滴答声。为此，我们将创建一个名为 TickTock 的类，其中包含两个方法：Tick() 和 Tock()。Tick() 方法显示单词“Tick”，Tock() 显示“Tock”。为了运行这个时钟，需要创建两个线程，一个调用 Tick()，另一个调用 Tock()。目标是让这两个线程以某种方式执行，使程序的输出显示出一致的“Tick Tock”——也就是一个“Tick”后跟一个“Tock”的重复模式。

```
// Use Wait() and Pulse() to create a ticking clock.
using System;
using System.Threading;

class TickTock {
    object lockOn = new object();

    public void Tick(bool running) {
        lock(lockOn) {
            if(!running) { // stop the clock
                Monitor.Pulse(lockOn); // notify any waiting threads
                return;
            }

            Console.Write("Tick ");
            Monitor.Pulse(lockOn); // let Tock() run
            Monitor.Wait(lockOn); // wait for Tock() to complete
        }
    }
    public void Tock(bool running) {
        lock(lockOn) {
            if(!running) { // stop the clock
                Monitor.Pulse(lockOn); // notify any waiting threads
                return;
            }

            Console.WriteLine("Tock");
            Monitor.Pulse(lockOn); // let Tick() run
            Monitor.Wait(lockOn); // wait for Tick() to complete
        }
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
        if(Thrd.Name == "Tick") {
            for(int i=0; i<5; i++) ttOb.Tick(true);
            ttOb.Tick(false);
        }
        else {
            for(int i=0; i<5; i++) ttOb.Tock(true);
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

下面是该程序产生的输出：

```
Tick Tock
Tick Tock
Tick Tock
Tick Tock
Tick Tock
Clock Stopped
```

让我们仔细看看这个程序。在 Main() 中，创建了一个名为 tt 的 TickTock 对象，并使用该对象启动两个执行线程。在 MyThread 的 Run() 方法内部，如果线程名是“Tick”，就调用 Tick()。如果线程名是“Tock”，就调用 Tock() 方法。每个方法都会被调用五次，并传入 true 作为参数。只要传入 true，时钟就会运行。最后分别向每个方法传入 false 进行调用，从而停止时钟。

这个程序最重要的部分在 Tick() 和 Tock() 方法中。我们先从 Tick() 方法开始；为方便起见，这里再次列出它：

```csharp
public void Tick(bool running) {
    lock(lockOn) {
        if(!running) { // stop the clock
            Monitor.Pulse(lockOn); // notify any waiting threads
            return;
        }

        Console.Write("Tick ");
        Monitor.Pulse(lockOn); // let Tock() run

        Monitor.Wait(lockOn); // wait for Tock() to complete
    }
}
```

首先，注意 Tick() 中的代码位于一个 lock 块内。回顾一下，Wait() 和 Pulse() 只能在同步块内使用。该方法首先检查 running 参数的值。这个参数用于干净地关闭时钟。如果它为 false，则表示时钟已经停止。在这种情况下，会调用 Pulse()，以使任何正在等待的线程能够运行。我们稍后会回到这一点。假设 Tick() 执行时时钟正在运行，那么会显示单词“Tick”，然后调用 Pulse()，接着调用 Wait()。调用 Pulse() 允许一个在同一对象上等待的线程运行。调用 Wait() 会使 Tick() 挂起，直到另一个线程调用 Pulse()。因此，当调用 Tick() 时，它显示一个“Tick”，让另一个线程运行，然后挂起。

Tock() 方法是 Tick() 的完全副本，只是它显示“Tock”。因此，当进入该方法时，它显示“Tock”，调用 Pulse()，然后等待。将这两个方法成对来看，对 Tick() 的调用后面只能跟着对 Tock() 的调用，而对 Tock() 的调用后面只能跟着对 Tick() 的调用，依此类推。因此，这两个方法是相互同步的。

当时钟停止时调用 Pulse() 的原因，是为了让最后一次对 Wait() 的调用能够成功。请记住，Tick() 和 Tock() 都会在显示消息后执行对 Wait() 的调用。问题在于，当时钟停止时，其中一个方法仍将处于等待状态。因此，需要最后调用一次 Pulse()，以便让正在等待的方法运行。作为实验，请尝试删除这次对 Pulse() 的调用，看看会发生什么。你会看到，程序会“挂起”，你需要按 CTRL+C 才能退出。原因是，当最后一次调用 Tock() 调用 Wait() 时，没有相应的 Pulse() 调用来让 Tock() 结束。因此，Tock() 就停在那里，永远等待下去。

在继续之前，如果你怀疑 Wait() 和 Pulse() 的调用是否真的需要让“时钟”正确运行，请将下面这个版本的 TickTock 替换到前面的程序中。这个版本移除了所有对 Wait() 和 Pulse() 的调用。

```csharp
// A nonfunctional version of TickTock.
class TickTock {
    object lockOn = new object();

    public void Tick(bool running) {
        lock(lockOn) {
            if(!running) { // stop the clock
                return;
            }
        }
        Console.Write("Tick ");
    }
    public void Tock(bool running) {
        lock(lockOn) {
            if(!running) { // stop the clock
                return;
            }
        }
        Console.WriteLine("Tock");
    }
}
```

替换之后，程序产生的输出将如下所示：

```
Tick Tick Tick Tick Tick Tock
Tock
Tock
Tock
Tock
Clock Stopped
```

显然，Tick() 和 Tock() 方法不再同步了！

## 死锁与竞态条件

在开发多线程程序时，必须小心避免死锁和竞态条件。顾名思义，死锁是一种情况：一个线程在等待另一个线程做某事，但另一个线程却在等待第一个线程。于是，两个线程都被挂起，互相等待，谁也无法执行。这种情况类似于两个过分客气的人都坚持让对方先过门！

避免死锁看起来很容易，但实际上并不容易。例如，死锁可能以迂回的方式发生。考虑 TickTock 类。如前所述，如果 Tick() 或 Tock() 没有执行最后的 Pulse()，那么其中一个就会无限期等待，程序就会死锁。死锁的原因通常不能仅仅通过查看程序的源代码就轻易理解，因为并发执行的线程在运行时可能以复杂的方式交互。要避免死锁，需要仔细编程和充分测试。一般来说，如果多线程程序偶尔“挂起”，死锁很可能就是原因。

竞态条件发生在两个（或更多）线程在没有适当同步的情况下同时尝试访问共享资源时。例如，一个线程可能正在向变量写入新值，而另一个线程正在递增该变量的当前值。如果没有同步，结果将取决于线程执行的顺序。（第二个线程递增的是原始值，还是第一个线程写入的新值？）在这种情况下，可以说这两个线程在“相互竞争”，最终结果取决于哪个线程先完成。与死锁一样，竞态条件也可能以难以发现的方式发生。解决办法是预防：通过仔细编程，正确同步对共享资源的访问。
