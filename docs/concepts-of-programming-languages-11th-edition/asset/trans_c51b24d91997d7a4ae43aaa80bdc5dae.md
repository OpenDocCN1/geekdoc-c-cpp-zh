
每个对象都有一个等待列表，其中包含所有曾在该对象上调用 `wait` 的线程。`notify` 方法用于告诉一个正在等待的线程：它可能一直在等待的某个事件已经发生。由 `notify` 唤醒的具体线程无法确定，因为 Java 虚拟机（JVM）会从该线程对象的等待列表中随机选择一个。因此，加之等待线程可能正在等待不同的条件，通常使用 `notifyAll` 方法而不是 `notify`。`notifyAll` 方法通过将对象等待列表上的所有线程放入任务就绪队列来唤醒它们。

`wait`、`notify` 和 `notifyAll` 方法只能从同步方法内部调用，因为它们使用此类方法放在对象上的锁。对 `wait` 的调用总是放在一个由该方法所等待的条件控制的 `while` 循环中。这个 `while` 循环是必要的，因为唤醒线程的 `notify` 或 `notifyAll` 可能是因为另一个条件发生了变化而被调用，而不是该线程所等待的条件。如果调用的是 `notifyAll`，那么所等待的条件现在为真的可能性甚至更小。由于使用了 `notifyAll`，自上次测试以来，其他某个线程可能已经把该条件改成了假。

`wait` 方法可以抛出 `InterruptedException`，它是 `Exception` 的后代。Java 的异常处理在第 14 章讨论。因此，任何调用 `wait` 的代码也必须捕获 `InterruptedException`。假设所等待的条件称为 `theCondition`，使用 `wait` 的常规方式如下：

```java
try {
    while (!theCondition)
        wait();
    // Do whatever is needed after theCondition comes true
}
catch(InterruptedException myProblem) { . . . }
```

下面的程序实现了一个用于存储 `int` 值的循环队列。它同时说明了协作同步和竞争同步。

```java
// Queue
// This class implements a circular queue for storing int
// values. It includes a constructor for allocating and
// initializing the queue to a specified size. It has
// synchronized methods for inserting values into and
// removing values from the queue.

class Queue {
    private int [] que;
    private int nextIn,
                nextOut,
                filled,
                queSize;

    public Queue(int size) {
        que = new int [size];
        filled = 0;
        nextIn = 0;
        nextOut = 0;
        queSize = size;
    } /* end of Queue constructor */

    public synchronized void deposit (int item)
        throws InterruptedException {
        try {
            while (filled == queSize)
                wait();
            que [nextIn] = item;
            nextIn = (nextIn + 1) % queSize;
            filled++;
            notifyAll();
        } /* end of try clause */
        catch(InterruptedException e) {}
    } /* end of deposit method */

    public synchronized int fetch()
        throws InterruptedException {
        int item = 0;
        try {
            while (filled == 0)
                wait();
            item = que [nextOut];
            nextOut = (nextOut + 1) % queSize;
            filled--;
            notifyAll();
        } /* end of try clause */
        catch(InterruptedException e) {}
        return item;
    } /* end of fetch method */
} /* end of Queue class */
```

注意，这里的异常处理器（`catch`）什么也不做。可以如下定义使用 `Queue` 类的生产者对象和消费者对象的类：

```java
class Producer extends Thread {
    private Queue buffer;
    public Producer(Queue que) {
        buffer = que;
    }
    public void run() {
        int new_item;
        while (true) {
            //-- Create a new_item
            buffer.deposit(new_item);
        }
    }
}
```

```java
class Consumer extends Thread {
    private Queue buffer;
    public Consumer(Queue que) {
        buffer = que;
    }
    public void run() {
        int stored_item;
        while (true) {
            stored_item = buffer.fetch();
            //-- Consume the stored_item
        }
    }
}
```

下面的代码创建一个 `Queue` 对象，以及一个 `Producer` 对象和一个 `Consumer` 对象，二者都连接到该 `Queue` 对象，并启动它们的执行：

```java
Queue buff1 = new Queue(100);
Producer producer1 = new Producer(buff1);
Consumer consumer1 = new Consumer(buff1);
producer1.start();
consumer1.start();
```

我们可以将 `Producer` 和 `Consumer` 中的一个或两个定义为 `Runnable` 接口的实现，而不是 `Thread` 的子类。唯一的区别在于第一行，现在会写成如下形式：

```java
class Producer implements Runnable { . . . }
```

要创建并运行这种类的对象，仍然需要创建一个与该对象连接的 `Thread` 对象。下面的代码说明了这一点：

```java
Producer producer1 = new Producer(buff1);
Thread producerThread = new Thread(producer1);
producerThread.start();
```

注意，`buffer` 对象被传递给 `Producer` 构造函数，而 `Producer` 对象被传递给 `Thread` 构造函数。

### 13.7.6 非阻塞同步

Java 包含一些用于控制对某些变量访问的类，这些类不包含阻塞或等待。`java.util.concurrent.atomic` 包定义了允许对 `int`、`long` 和 `boolean` 基本类型变量以及引用和数组进行某些非阻塞同步访问的类。例如，`AtomicInteger` 类定义了 getter 和 setter 方法，以及用于加法、递增和递减操作的方法。这些操作都是原子的；也就是说，它们不能被中断，因此不需要锁来保证多线程程序中受影响变量值的完整性。这是细粒度同步——仅针对单个变量。现在大多数机器都有针对 `int` 和 `long` 类型这些操作的原子指令，因此它们通常很容易实现（不需要隐式锁）。

非阻塞同步的优点在于效率。在无竞争情况下发生的非阻塞访问不会更慢，而且通常比使用 `synchronized` 的访问更快。在竞争情况下发生的非阻塞访问肯定比使用 `synchronized` 的访问更快，因为后者需要挂起和重新调度线程。

### 13.7.7 显式锁

Java 5.0 引入了显式锁，作为提供隐式锁的 `synchronized` 方法和块的替代方案。`Lock` 接口声明了 `lock`、`unlock` 和 `tryLock` 方法。预定义的 `ReentrantLock` 类实现了 `Lock` 接口。要锁定一个代码块，可以使用以下惯用法：

```java
Lock lock = new ReentrantLock();
...
lock.lock();
try {
    // The code that accesses the shared data
} finally {
    lock.unlock();
}
```

这段骨架代码创建一个 `Lock` 对象，并在该 `Lock` 对象上调用 `lock` 方法。然后，它使用 `try` 块包围关键代码。对 `unlock` 的调用放在 `finally` 子句中，以保证无论 `try` 块中发生什么，锁都会被释放。

至少在两种情况下会使用显式锁而不是隐式锁：第一，如果应用程序需要尝试获取锁但不能永远等待它，`Lock` 接口包含一个方法 `tryLock`，它接受一个时间限制参数。如果在时间限制内没有获取到锁，执行将继续到调用 `tryLock` 之后的语句。第二，当锁-解锁对不适合采用块结构时，会使用显式锁。隐式锁总是在锁定它们的复合语句末尾解锁。显式锁可以在代码中的任何位置解锁，无论程序结构如何。

使用显式锁（使用隐式锁时不是这样）的一个危险是遗漏解锁。隐式锁在锁定块的末尾隐式解锁。然而，显式锁会保持锁定，直到被显式解锁，而这有可能永远不发生。

如前所述，每个对象都有一个内在条件队列，用于存储在该对象上等待某个条件的线程。`wait`、`notify` 和 `notifyAll` 方法是内在条件队列的 API。因为每个对象只能有一个条件队列，所以一个队列中可能有线程在等待不同的条件。例如，在我们的缓冲区示例 `Queue` 中，队列可以有线程等待两个条件中的任意一个（`filled == queueSize` 或 `filled == 0`）。这就是缓冲区使用 `notifyAll` 的原因。（如果它使用 `notify`，那么只会唤醒一个线程，而且它可能是在等待与实际变为真的条件不同的条件的线程。）然而，`notifyAll` 的使用代价很高，因为它会唤醒在对象上等待的所有线程，而所有线程都必须检查自己的条件以确定哪一个运行。此外，为了检查条件，它们必须首先获取对象上的锁。

使用内在条件队列的替代方案是 `Condition` 接口，它使用与 `Lock` 对象关联的条件队列。它还声明了 `wait`、`notify` 和 `notifyAll` 的替代方法，分别名为 `await`、`signal` 和 `signalAll`。一个 `Lock` 对象可以有任意数量的 `Condition` 对象。使用 `Condition` 时，可以使用 `signal` 而不是 `signalAll`，这既更容易理解又更高效，部分原因是它导致更少的上下文切换。

### 13.7.8 评估

Java 对并发的支持相对简单但有效。所有 Java 的 `run` 方法都是参与者任务，除了通过共享数据之外，没有通信机制，就像 Ada 任务之间那样。因为它们是重量级线程，Ada 的任务可以很容易地分布到不同的处理器；特别是具有不同内存的不同处理器，这些处理器可能位于不同地点的不同计算机上。这类系统在 Java 线程中是不可能的。

## 13.8 C# 线程

尽管 C# 的线程松散地基于 Java 的线程，但存在显著差异。以下是对 C# 线程的简要概述。
