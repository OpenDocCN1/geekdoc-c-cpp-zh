

```
Decrement Thread is waiting for the mutex.
In Increment Thread, SharedRes.Count is 1
In Increment Thread, SharedRes.Count is 2
In Increment Thread, SharedRes.Count is 3
In Increment Thread, SharedRes.Count is 4
In Increment Thread, SharedRes.Count is 5
Increment Thread releases the mutex.
Decrement Thread acquires the mutex.
In Decrement Thread, SharedRes.Count is 4
In Decrement Thread, SharedRes.Count is 3
In Decrement Thread, SharedRes.Count is 2
In Decrement Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
Decrement Thread releases the mutex.
```

如输出所示，对 SharedRes.Count 的访问是同步的，一次只有一个线程能够更改其值。

为了证明生成前面的输出需要 Mutex，请尝试注释掉前面程序中对 WaitOne() 和 ReleaseMutex() 的调用。运行程序时，你将看到以下序列（你实际看到的输出可能有所不同）：

```
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
```

如该输出所示，没有互斥量时，对 SharedRes.Count 的递增和递减是交错进行的，而不是按顺序进行的。

上一个示例创建的互斥量仅对创建它的进程可见。然而，可以创建在整个系统范围内已知的互斥量。为此，必须使用以下构造函数之一创建命名互斥量：

```
public Mutex(bool owned, string name)
public Mutex(bool owned, string name, out bool whatHappened)
```

在两种形式中，互斥量的名称通过 name 传入。在第一种形式中，如果 owned 为 true，则请求获得该互斥量的所有权。然而，由于系统范围内的互斥量可能已被另一个进程拥有，因此最好为此参数指定 false。在第二种形式中，返回时，如果请求并获得了所有权，则 whatHappened 将为 true。如果所有权被拒绝，则它将为 false。（Mutex 构造函数还有第三种形式，允许指定控制访问的 MutexSecurity 对象。）使用命名互斥量可以管理进程间同步。

另一点：已获得互斥量的线程在调用 ReleaseMutex() 之前，可以合法地再调用一次或多次 WaitOne()，并且这些额外调用会成功。也就是说，冗余的 WaitOne() 调用不会阻塞已经拥有该互斥量的线程。但是，在释放互斥量之前，WaitOne() 的调用次数必须由相同次数的 ReleaseMutex() 调用抵消。

## 信号量

信号量类似于互斥量，不同之处在于它可以同时授予多个线程访问共享资源的权限。因此，当要同步一组资源时，信号量很有用。信号量通过使用计数器来控制对共享资源的访问。如果计数器大于零，则允许访问。如果为零，则拒绝访问。计数器计数的是许可。因此，要访问资源，线程必须从信号量获得许可。

一般来说，要使用信号量，希望访问共享资源的线程会尝试获取许可。如果信号量的计数器大于零，线程便获得一个许可，这会使信号量的计数递减。否则，线程将阻塞，直到能够获得许可。当线程不再需要访问共享资源时，它会释放许可，这会使信号量的计数递增。如果有另一个线程正在等待许可，那么该线程将在此时获得许可。允许的同时访问数量在创建信号量时指定。如果创建的信号量只允许一次访问，那么信号量的作用就与互斥量完全相同。

当共享资源由一组或一个池组成时，信号量特别有用。例如，一组网络连接（其中任何一个都可用于通信）就是一个资源池。需要网络连接的线程并不关心获得哪一个连接。在这种情况下，信号量提供了一种方便的机制来管理对这些连接的访问。

信号量由 System.Threading.Semaphore 实现。它有几个构造函数。最简单形式如下所示：

```csharp
public Semaphore(int initial, int max)
```

这里，initial 指定信号量许可计数器的初始值，即可用许可的数量。计数器的最大值通过 max 传入。因此，max 表示信号量可以授予的最大许可数。initial 中的值指定这些许可最初有多少个可用。

使用信号量类似于使用前面所述的互斥量。要获得访问权限，代码将调用信号量的 WaitOne()。此方法由 Semaphore 从 WaitHandle 类继承。WaitOne() 会一直等待，直到可以获取调用它的信号量。因此，它会阻塞调用线程的执行，直到指定的信号量可以授予许可。

当代码不再需要信号量的所有权时，它通过调用 Release() 来释放信号量，如下所示：

```csharp
public int Release()
public int Release(int num)
```

第一种形式释放一个许可。第二种形式释放由 num 指定的许可数。两者都返回释放前存在的许可计数。

线程可以在调用 Release() 之前多次调用 WaitOne()。但是，在释放许可之前，WaitOne() 的调用次数必须由相同次数的 Release() 调用抵消。或者，可以调用 Release(int) 形式，传入一个等于 WaitOne() 调用次数的数字。

下面是一个说明信号量的示例。在该程序中，类 MyThread 使用一个信号量，以便在任何时候只允许执行两个 MyThread 线程。因此，被共享的资源是 CPU。

```csharp
// Use a Semaphore.
using System;
using System.Threading;

// This thread allows only two instances of itself
// to run at any one time.
class MyThread {
    public Thread Thrd;

    // This creates a semaphore that allows up to two
    // permits to be granted and that initially has
    // two permits available.
    static Semaphore sem = new Semaphore(2, 2);

    public MyThread(string name) {
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {

        Console.WriteLine(Thrd.Name + " is waiting for a permit.");

        sem.WaitOne();

        Console.WriteLine(Thrd.Name + " acquires a permit.");

        for(char ch='A'; ch < 'D'; ch++) {
            Console.WriteLine(Thrd.Name + ": " + ch + " ");
            Thread.Sleep(500);
        }

        Console.WriteLine(Thrd.Name + " releases a permit.");

        // Release the semaphore.
        sem.Release();
    }
}

class SemaphoreDemo {
    static void Main() {

        // Construct three threads.
        MyThread mt1 = new MyThread("Thread #1");
        MyThread mt2 = new MyThread("Thread #2");
        MyThread mt3 = new MyThread("Thread #3");

        mt1.Thrd.Join();
        mt2.Thrd.Join();
        mt3.Thrd.Join();
    }
}
```

MyThread 声明了信号量 sem，如下所示：

```
static Semaphore sem = new Semaphore(2, 2);
```

这会创建一个最多可授予两个许可、并且最初两个许可都可用的信号量。

在 MyThread.Run() 中，注意在信号量 sem 授予许可之前，执行无法继续。如果没有可用许可，则该线程的执行会挂起。当确实有许可可用时，执行会恢复，线程可以运行。在 Main() 中，创建了三个 MyThread 线程。然而，只有前两个能够执行。第三个必须等待，直到其他线程之一终止。下面显示的输出验证了这一点。（你实际看到的输出可能略有不同。）

```
Thread #1 is waiting for a permit.
Thread #1 acquires a permit.
Thread #1 : A
Thread #2 is waiting for a permit.
Thread #2 acquires a permit.
Thread #2 : A
Thread #3 is waiting for a permit.
Thread #1 : B
Thread #2 : B
Thread #1 : C
Thread #2 : C
Thread #1 releases a permit.
Thread #3 acquires a permit.
Thread #3 : A
Thread #3 releases a permit.
Thread #3 : B
Thread #3 : C
Thread #3 releases a permit.
```

上一个示例创建的信号量仅对创建它的进程可见。然而，可以创建在整个系统范围内已知的信号量。为此，必须创建命名信号量。要这样做，请使用以下构造函数之一：

```
public Semaphore(int initial, int max, string name)
public Semaphore(int initial, int max, string name, out bool whatHappened)
```

在两种形式中，信号量的名称通过 name 传入。在第一种形式中，如果指定名称的信号量尚不存在，则使用 initial 和 max 的值创建它。如果它已经存在，则忽略 initial 和 max 的值。在第二种形式中，返回时，如果信号量已创建，则 whatHappened 将为 true。在这种情况下，将使用 initial 和 max 的值来创建信号量。如果 whatHappened 为 false，那么

