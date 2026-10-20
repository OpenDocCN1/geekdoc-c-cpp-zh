
生产者必须先执行；如果消费者上次消费之后生产者尚未生产，则消费者必须等待；如果消费者尚未消费生产者最近产生的值，则生产者必须等待。多次执行此程序，以确认每个产生的整数都恰好被消费一次。在示例输出中，请注意突出显示的行，这些行指示生产者和消费者何时必须等待以执行各自的任务。

```
// Fig. 26.21: SharedBufferTest2.java
// Two threads manipulating a synchronized buffer.
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class SharedBufferTest2
{
    public static void main( String[] args )
    {
        // create new thread pool with two threads
        ExecutorService application = Executors.newCachedThreadPool();

        // create SynchronizedBuffer to store ints
        Buffer sharedLocation = new SynchronizedBuffer();

        System.out.printf( "%-40s%\t%s%\n%-40s%\n\n", "Operation", "Buffer", "Occupied", "----------", "------\t------" );

        // execute the Producer and Consumer tasks
        application.execute( new Producer( sharedLocation ) );
        application.execute( new Consumer( sharedLocation ) );

        application.shutdown();
    } // end main
} // end class SharedBufferTest2
```

| 操作 | 缓冲区 | 已占用 |
| ---------- | ------ | -------- |
| 生产者写入 1 | 1 | true |
| 生产者尝试写入。缓冲区已满，生产者等待。 | 1 | true |
| 消费者读取 1 | 1 | false |
| 生产者写入 2 | 2 | true |
| 生产者尝试写入。缓冲区已满，生产者等待。 | 2 | true |
| 消费者读取 2 | 2 | false |
| 生产者写入 3 | 3 | true |
| 消费者读取 3 | 3 | false |

图 26.21 | 两个线程操作同步缓冲区。（第 1 部分，共 2 部分）

|  |  |  |
|---|---|---|
| 生产者写入 4 | 4 | true |
| 消费者读取 4 | 4 | false |
| 消费者尝试读取。缓冲区为空，消费者等待。 | 4 | false |
| 生产者写入 5 | 5 | true |
| 消费者读取 5 | 5 | false |
| 消费者尝试读取。缓冲区为空，消费者等待。 | 5 | false |
| 生产者写入 6 | 6 | true |
| 消费者读取 6 | 6 | false |
| 生产者写入 7 | 7 | true |
| 消费者读取 7 | 7 | false |
| 生产者写入 8 | 8 | true |
| 消费者读取 8 | 8 | false |
| 生产者写入 9 | 9 | true |
| 消费者读取 9 | 9 | false |
| 生产者写入 10 | 10 | true |
| 生产者完成生产，终止生产者 消费者读取 10 | 10 | false |
| 消费者读取的值总计为 55，终止消费者 |  |  |

图 26.21 | 两个线程操作同步缓冲区。（第 2 部分，共 2 部分）

## 26.10 并发集合概述

在第 20 章中，我们介绍了 Java Collections API 中的多种集合。我们还提到，您可以获得这些集合的同步版本，以允许每次只有一个线程访问可能被多个线程共享的集合。java.util.concurrent 包中的集合是专门设计和优化的，用于在多个线程之间共享集合的程序中。

图 26.22 列出了 java.util.concurrent 包中的许多并发集合。有关这些集合的更多信息，请访问

```
download.oracle.com/javase/6/docs/api/java/util/concurrent/
package-summary.html
```

有关 Java SE 7 中新增的并发集合的信息，请访问

```
download.java.net/jdk7/docs/api/java/util/concurrent/package-summary.html
```

| 集合 | 描述 |
|---|---|
| ArrayBlockingQueue | 一个固定大小的队列，支持生产者/消费者关系——可能涉及多个生产者和消费者。 |
| ConcurrentHashMap | 一种基于哈希的映射，允许任意数量的读取线程和有限数量的写入线程。 |
| ConcurrentLinkedQueue | 队列的并发链表实现，可以动态增长。 |
| ConcurrentSkipListMap | 一种按键排序的并发映射。 |
| ConcurrentSkipListSet | 一个有序的并发集合。 |
| CopyOnWriteArrayList | 一个线程安全的 ArrayList。每次修改集合的操作都会先创建内容的新副本。当集合遍历的频率远高于内容修改频率时使用。 |
| CopyOnWriteArraySet | 使用 CopyOnWriteArrayList 实现的集合。 |
| DelayQueue | 一个包含 Delayed 对象的可变大小队列。只有在其延迟到期后才能移除对象。 |
| LinkedBlockingDeque | 一个双端阻塞队列，以链表形式实现，可选择固定大小。 |
| LinkedBlockingQueue | 一个阻塞队列，以链表形式实现，可选择固定大小。 |
| PriorityBlockingQueue | 一个可变长度的基于优先级的阻塞队列（类似于 PriorityQueue）。 |
| SynchronousQueue | 一个没有内部容量的阻塞队列实现。一个线程的每次插入操作都必须等待另一个线程的移除操作，反之亦然。 |
| Java SE 7 中新增的并发集合 | |
| ConcurrentLinkedDeque | 双端队列的并发链表实现。 |
| LinkedTransferQueue | TransferQueue 接口的链表实现。每个生产者可以选择等待消费者取走正在插入的元素（通过 transfer 方法），或者简单地将元素放入队列（通过 put 方法）。还提供了重载的 tryTransfer 方法，可以立即将元素转移给正在等待的消费者，或者在指定的超时时间内完成转移。如果无法完成转移，则不会将元素放入队列。通常用于在线程之间传递消息的应用程序。 |

## 26.11 使用 GUI 的多线程

Swing 应用程序为多线程编程带来了一系列独特的挑战。所有 Swing 应用程序都有一个称为事件分发线程的单一线程，用于处理与应用程序 GUI 组件的交互。典型的交互包括*更新 GUI 组件*或*处理用户操作*，例如鼠标单击。所有需要与应用程序 GUI 交互的任务都被放置在*事件队列*中，并由事件分发线程按顺序执行。

*Swing GUI 组件不是线程安全的*——它们不能由多个线程操作，否则会有产生错误结果的风险。与本章介绍的其他示例不同，GUI 应用程序中的线程安全不是通过同步线程操作来实现的，而是通过*确保 Swing 组件仅从单个线程（即事件分发线程）访问*来实现的。这种技术称为**线程封闭**。只允许一个线程访问非线程安全的对象，消除了多个线程并发访问这些对象而导致损坏的可能性。

通常，在事件分发线程上按顺序执行简单计算与 GUI 组件操作就足够了。如果应用程序必须响应用户界面交互而执行长时间计算，那么事件分发线程在该计算期间无法处理事件队列中的其他任务。这会导致 GUI 组件无响应。最好在单独的线程中处理长时间运行的计算，从而释放事件分发线程以继续管理其他 GUI 交互。当然，要根据计算结果更新 GUI，您必须从事件分发线程（而不是执行计算的辅助线程）更新 GUI。

### SwingWorker 类

类 **SwingWorker**（位于 javax.swing 包中）在辅助线程中执行长时间运行的计算，并根据计算结果从事件分发线程更新 Swing 组件。SwingWorker 实现了 Runnable 接口，这意味着 *SwingWorker 对象可以安排在单独的线程中执行*。SwingWorker 类提供了几种方法，以简化在辅助线程中执行计算并使结果可用于在 GUI 中显示。图 26.23 描述了一些常用的 SwingWorker 方法。

| 方法 | 描述 |
|---|---|
| `doInBackground` | 定义一个长时间计算，并在辅助线程中调用。 |
| `done` | 当 `doInBackground` 返回时，在事件分发线程上执行。 |
| `execute` | 调度 SwingWorker 对象在辅助线程中执行。 |
| `get` | 等待计算完成，然后返回计算结果（即 `doInBackground` 的返回值）。 |
| `publish` | 将中间结果从 `doInBackground` 方法发送到 `process` 方法，以便在事件分发线程上处理。 |

**图 26.23** | 常用的 SwingWorker 方法。（第 1 部分，共 2 部分）
