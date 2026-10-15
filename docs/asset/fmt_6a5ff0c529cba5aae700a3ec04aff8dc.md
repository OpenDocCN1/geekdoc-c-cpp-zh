
Listing 19.10 begins by instantiating and starting a new `Task`. Table 19.3 on the next page shows the execution path in which each column represents a thread. In cases where code appears on the same row, it is indeterminate which side executes first.

Calling a reset event’s `Wait()` method (for a `ManualResetEvent`, it is called `WaitOne()`) blocks the calling thread until another thread signals and allows the blocked thread to continue. Instead of blocking indefinitely, `Wait()`/`WaitOne()` overrides include a parameter, either in milliseconds or as a `TimeSpan` object, for the maximum amount of time to block. When specifying a timeout period, the return from `WaitOne()` will be `false` if the timeout occurs before the reset event is signaled. `ManualResetEvent.Wait()`

## TABLE 19.3: Execution Path with `ManualResetEvent` Synchronization

| `Main()` | `DoWork()` |
| --- | --- |
| `...` | |
| `Console.WriteLine( "Application started...");` | |
| `Task task = new Task(DoWork);` | |
| `Console.WriteLine( "Starting thread...");` | |
| `task.Start();` | |
| `DoWorkSignaledResetEvent.Wait();` | `Console.WriteLine( "DoWork() started...");` |
| | `DoWorkSignaledResetEvent.Set();` |
| `Console.WriteLine( "Thread executing...");` | `MainSignaledResetEvent.Wait();` |
| `MainSignaledResetEvent.Set();` | |
| `task.Wait();` | `Console.WriteLine( "DoWork() ending...");` |
| `Console.WriteLine( "Thread completed");` | |
| `Console.WriteLine( "Application exiting...");` | |

It also includes a version that takes a cancellation token, allowing for cancellation requests as discussed in Chapter 18.

The difference between `ManualResetEventSlim` and `ManualResetEvent` is the fact that the latter uses kernel synchronization by default whereas the former is optimized to avoid trips to the kernel except as a last resort. Thus, `ManualResetEventSlim` is more performant even though it could possibly use more CPU cycles. For this reason, you should use `ManualResetEventSlim` in general unless waiting on multiple events or across processes is required.

Notice that reset events implement `IDisposable`, so they should be disposed when they are no longer needed. In Listing 19.10, we do this via a `using` statement. (`CancellationTokenSource` contains a `ManualResetEvent`, which is why it, too, implements `IDisposable`.)

虽然不完全相同，但在某些情况下，`System.Threading.Monitor` 的 `Wait()` 和 `Pulse()` 方法提供了与重置事件类似的功能。

## ADVANCED TOPIC

### 优先使用 `ManualResetEvent` 和信号量而非 `AutoResetEvent`

还有第三种重置事件 `System.Threading.AutoResetEvent`，它与 `ManualResetEvent` 类似，允许一个线程通过调用 `Set()` 向另一个线程发出信号，表明该线程已到达代码中的某个位置。不同之处在于 `AutoResetEvent` 只解除阻塞一个线程的 `Wait()` 调用：在第一个线程通过自动重置门之后，它会重新变为锁定状态。使用自动重置事件时，很容易错误地将生产者线程编码为比消费者线程迭代次数更多。因此，通常更推荐使用 `Monitor` 的 `Wait()`/`Pulse()` 模式，或使用信号量（如果少于 `n` 个线程可以参与特定代码块）。

与 `AutoResetEvent` 相比，`ManualResetEvent` 在显式调用 `Reset()` 之前不会返回到未发出信号状态。

## `Semaphore`/`SemaphoreSlim` 和 `CountdownEvent`

`Semaphore` 和 `SemaphoreSlim` 与 `ManualResetEvent` 和 `ManualResetEventSlim` 具有相同的性能差异。与 `ManualResetEvent`/`ManualResetEventSlim` 不同，后者提供一个类似闸门的锁，要么打开要么关闭，信号量仅限制同时在临界区内通过的 `N` 次调用。信号量本质上维护着资源池的计数。当此计数达到零时，它会阻止对池的任何进一步访问，直到其中一个资源被归还，使其可供下一个排队的被阻塞请求使用。

`CountdownEvent` 与信号量非常相似，只是实现了相反的同步。也就是说，与保护对已用完的资源池的进一步访问不同，`CountdownEvent` 仅在计数达到零时才允许访问。例如，考虑一个并行操作，该操作下载大量股票报价。只有在所有报价都下载完成后，才能执行特定的搜索算法。`CountdownEvent` 可用于同步搜索算法，在每个股票下载时递减计数，然后在计数达到零时释放搜索开始。

请注意，`SemaphoreSlim` 和 `CountdownEvent` 是在 .NET Framework 4 中引入的。在 .NET 4.5 中，前者包含 `SemaphoreSlim.WaitAsync()` 方法，以便在等待进入信号量时可以使用 TAP。

## Concurrent Collection Classes

.NET Framework 4 中引入的另一系列类是并发集合类。这些类特别设计为包含内置同步代码，以便它们可以在多线程同时访问时无需担心竞争条件。并发集合类的列表出现在表 19.4 中。

并发集合启用的一种常见模式是对生产者和消费者提供线程安全访问。实现 `IProducerConsumerCollection<T>` 的类（在表 19.4 中用 `*` 标识）专门设计为提供此类支持。这使得一个或多个类可以将数据泵入集合，而不同的类则读取并移除数据。数据添加和移除的顺序由实现 `IProducerConsumerCollection<T>` 接口的各个集合类决定。

### TABLE 19.4: Concurrent Collection Classes

| Collection Class | Description |
| --- | --- |
| `BlockingCollection<T>` | 提供一个阻塞集合，使生产者/消费者场景成为可能，在此场景中生产者将数据写入集合，而消费者读取数据。此类提供一种通用集合类型，可在不考虑后端存储的情况下同步添加和移除操作（无论是队列、堆栈、列表等）。`BlockingCollection<T>` 为实现 `IProducerConsumerCollection<T>` 接口的集合提供阻塞和有界支持。 |
| `*ConcurrentBag<T>` | `T` 类型对象的线程安全无序集合。 |
| `ConcurrentDictionary<TKey, TValue>` | 线程安全的字典；键值对集合。 |
| `*ConcurrentQueue<T>` | 支持对 `T` 类型对象进行先进先出（FIFO）语义的线程安全队列。 |
| `*ConcurrentStack<T>` | 支持对 `T` 类型对象进行先进后出（FILO）语义的线程安全堆栈。 |

`*` 实现 `IProducerConsumerCollection<T>` 的集合类。

虽然它不是开箱即用的 .NET Framework 的内置组件，但还有一个额外的不可变集合库可用，称为 `System.Collections.Immutable`。不可变集合的优点是它可以在线程之间自由传递，而无需担心死锁或中间更新。由于不可变集合无法修改，因此不会发生中间更新；因此此类集合自动是线程安全的（因此无需锁定访问）。有关更多信息，请参阅 `http://bit.ly/SystemCollectionsImmutable`。

## Thread Local Storage

在某些情况下，使用同步锁可能导致不可接受的性能和可扩展性限制。在其他情况下，对特定数据元素提供同步可能过于复杂，尤其是在原始编码之后添加时。

同步的一种替代解决方案是隔离，实现隔离的一种方法是线程本地存储。使用线程本地存储时，每个线程都有自己专用的变量实例。因此无需同步，因为在单个线程上下文中出现的数据无需同步。线程本地存储实现的两个示例是 `ThreadLocal<T>` 和 `ThreadStaticAttribute`。

### `ThreadLocal<T>`

在 .NET Framework 4 中使用线程本地存储涉及声明一个类型为 `ThreadLocal<T>` 的字段（或在编译器闭包的情况下为变量）。结果是每个线程都有该字段的不同实例，如清单 19.11 和输出 19.7 所示。请注意，即使该字段是静态的，也存在不同的实例。

#### LISTING 19.11: Using `ThreadLocal<T>` for Thread Local Storage

```
using System;
using System.Threading;

public class Program
{
    static ThreadLocal<double> _Count =
        new ThreadLocal<double>(() => 0.01134);

    public static double Count
    {
        get { return _Count.Value; }
        set { _Count.Value = value; }
    }

    public static void Main()
    {
        Thread thread = new Thread(Decrement);
        thread.Start();

        // Increment
        for(double i = 0; i < short.MaxValue; i++)
        {
            Count++;
        }

        thread.Join();
        Console.WriteLine("Main Count = {0}", Count);
    }

    static void Decrement()
    {
        Count = -Count;
        for (double i = 0; i < short.MaxValue; i++)
        {
            Count--;
        }
        Console.WriteLine(
            "Decrement Count = {0}", Count);
    }
}
```

#### OUTPUT 19.7

```
Decrement Count = -32767.01134
Main Count = 32767.01134
```

正如输出 19.7 所演示的那样，执行 `Main()` 的线程的 `Count` 值永远不会被执行 `Decrement()` 的线程递减。对于 `Main()` 的线程，初始值为 0.01134，最终值为 32767.01134。`Decrement()` 的值类似，只是为负值。由于 `Count` 基于类型为 `ThreadLocal<T>` 的静态字段，运行 `Main()` 的线程和运行 `Decrement()` 的线程在 `_Count.Value` 中存储有独立的值。

### Thread Local Storage with `ThreadStaticAttribute`

如清单 19.12 所示，用 `ThreadStaticAttribute` 装饰静态字段是指定静态变量为每个线程一个实例的第二种方法。与 `ThreadLocal<T>` 相比，此技术有一些注意事项，但它也有在 .NET Framework 4 之前可用的优势。（此外，由于 `ThreadLocal<T>` 基于 `ThreadStaticAttribute`，因此在足够频繁重复的小迭代中，它会消耗更少的内存并带来轻微的性能优势。）

#### LISTING 19.12: Using `ThreadStaticAttribute` for Thread Local Storage

```
using System;
using System.Threading;

public class Program
{
    [ThreadStatic]
    static double _Count = 0.01134;
    public static double Count
    {
        get { return Program._Count; }
        set { Program._Count = value; }
    }

    public static void Main()
    {
        Thread thread = new Thread(Decrement);
        thread.Start();

        // Increment
        for(int i = 0; i < short.MaxValue; i++)
        {
            Count++;
        }

        thread.Join();
        Console.WriteLine("Main Count = {0}", Count);
    }

    static void Decrement()
    {
        for(int i = 0; i < short.MaxValue; i++)
        {
            Count--;
        }
        Console.WriteLine("Decrement Count = {0}", Count);
    }
}
```

The results of Listing 19.12 appear in Output 19.8.

#### Output 19.8

```text
Decrement Count = -32767
Main Count = 32767.01134
```

Unlike with Listing 19.11, the value of `Count` for the thread executing `Main()` is never decremented by the thread executing `Decrement()`. For `Decrement()`’s thread, the initial value is 0 (`default(double)`) and the final value is -32767. In other words, with `ThreadStaticAttribute` the value of `Count` for each thread is specific to the thread and not accessible across threads.
