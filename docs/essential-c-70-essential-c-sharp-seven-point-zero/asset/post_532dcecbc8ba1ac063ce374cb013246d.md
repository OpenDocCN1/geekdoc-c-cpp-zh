
public static void DoWork()
{
    Console.WriteLine("DoWork() started....");
    DoWorkSignaledResetEvent.Set();
    MainSignaledResetEvent.Wait();
    Console.WriteLine("DoWork() ending....");
}

public static void Main()
{
    using (MainSignaledResetEvent = new ManualResetEventSlim())
    using (DoWorkSignaledResetEvent = new ManualResetEventSlim())
    {
        Console.WriteLine("Application started....");
        Console.WriteLine("Starting task....");
        // Use Task.Factory.StartNew for .NET 4.0
        Task task = Task.Run(() => DoWork());
        // Block until DoWork() has started
        DoWorkSignaledResetEvent.Wait();
        Console.WriteLine("Waiting while thread executes...");
        MainSignaledResetEvent.Set();
        task.Wait();
        Console.WriteLine("Thread completed");
        Console.WriteLine("Application shutting down....");
    }
}

**OUTPUT 20.6**

Application started....
Starting thread....
DoWork() started....
Waiting while thread executes...
DoWork() ending....
Thread completed
Application shutting down....

Listing 20.10 begins by instantiating and starting a new Task. Table 20.3 shows the execution path in which each column represents a thread. In cases where code appears on the same row, it is indeterminate which side executes first.

## TABLE 20.3: Execution Path with ManualResetEvent Synchronization

| Main() | DoWork() |
| :--- | :--- |
| `...` | |
| `Console.WriteLine(` | |
| `"Application started....");` | |
| `Task task = new Task(DoWork);` | |
| `Console.WriteLine(` | |
| `"Starting thread....");` | |
| `task.Start();` | |
| `DoWorkSignaledResetEvent.Wait();` | `Console.WriteLine(` |
| | `"DoWork() started....");` |
| | `DoWorkSignaledResetEvent.Set();` |
| `Console.WriteLine(` | `MainSignaledResetEvent.Wait();` |
| `"Thread executing...");` | |
| `MainSignaledResetEvent.Set();` | |
| `task.Wait();` | `Console.WriteLine(` |
| | `"DoWork() ending....");` |
| `Console.WriteLine(` | |
| `"Thread completed");` | |
| `Console.WriteLine(` | |
| `"Application exiting...");` | |

Calling a reset event's `Wait()` method (for a `ManualResetEvent`, it is called `WaitOne()`) blocks the calling thread until another thread signals and allows the blocked thread to continue. Instead of blocking indefinitely, `Wait()`/`WaitOne()` overrides include a parameter, either in milliseconds or as a `TimeSpan` object, for the maximum amount of time to block. When specifying a timeout period, the return from `WaitOne()` will be `false` if the timeout occurs before the reset event is signaled. `ManualResetEvent.Wait()` also includes a version that takes a cancellation token, allowing for cancellation requests as discussed in Chapter 19.

The difference between `ManualResetEventSlim` and `ManualResetEvent` is that the latter uses kernel synchronization by default whereas the former is optimized to avoid trips to the kernel except as a last resort. Thus, `ManualResetEventSlim` is more performant even though it could possibly use more CPU cycles. For this reason, you should use `ManualResetEventSlim` in general unless waiting on multiple events or across processes is required.

Notice that reset events implement `IDisposable`, so they should be disposed when they are no longer needed. In Listing 20.10, we do this via a `using` statement. (`CancellationTokenSource` contains a `ManualResetEvent`, which is why it, too, implements `IDisposable`.)

Although not exactly the same, `System.Threading.Monitor`'s `Wait()` and `Pulse()` methods provide similar functionality to reset events in some circumstances.

## ADVANCED TOPIC

### Favor `ManualResetEvent` and Semaphores over `AutoResetEvent`

There is a third reset event, `System.Threading.AutoResetEvent`, that, like `ManualResetEvent`, allows one thread to signal (with a call to `Set()`) another thread that this first thread has reached a certain location in the code. The difference is that the `AutoResetEvent` unblocks only one thread's `Wait()` call: After the first thread passes through the auto-reset gate, it goes back to locked. With the auto-reset event, it is all too easy to mistakenly code the producer thread with more iterations than the consumer thread. Therefore, use of `Monitor`'s `Wait()`/`Pulse()` pattern or use a semaphore (if fewer than *n* threads can participate in a particular block) is generally preferred.

In contrast to an `AutoResetEvent`, the `ManualResetEvent` won't return to the unsignaled state until `Reset()` is called explicitly.

### Semaphore/SemaphoreSlim and CountdownEvent

`Semaphore` and `SemaphoreSlim` have the same performance differences as `ManualResetEvent` and `ManualResetEventSlim`. Unlike `ManualResetEvent`/`ManualResetEventSlim`, which provide a lock (like a gate) that is either open or closed, semaphores restrict only *N* calls to pass within a critical section simultaneously. The semaphore essentially keeps a count of the pool of resources. When this count reaches zero, it blocks any further access to the pool until one of the resources is returned, making it available for the next blocked request that is queued.

CountdownEvent is much like a semaphore, except it achieves the opposite synchronization. That is, rather than protecting further access to a pool of resources that are all used up, the CountdownEvent allows access only once the count reaches zero. Consider, for example, a parallel operation that downloads a multitude of stock quotes. Only when all of the quotes are downloaded can a particular search algorithm execute. The CountdownEvent may be used for synchronizing the search algorithm, decrementing the count as each stock is downloading, and then releasing the search to start once the count reaches zero.

Notice that SemaphoreSlim and CountdownEvent were introduced with Microsoft .NET Framework 4. In .NET 4.5, the former includes a SemaphoreSlim.WaitAsync() method so that the Task-based Asynchronous Pattern (TAP) can be used when waiting to enter the semaphore.

### Concurrent Collection Classes

Another series of classes introduced with Microsoft .NET Framework 4 is the concurrent collection classes. These classes are especially designed to include built-in synchronization code so that they can support simultaneous access by multiple threads without concern for race conditions. A list of the concurrent collection classes appears in Table 20.4.

| Collection Class | Description |
| :--- | :--- |
| BlockingCollection<T> | Provides a blocking collection that enables producer/consumer scenarios in which producers write data into the collection while consumers read the data. This class provides a generic collection type that synchronizes add and remove operations without concern for the back-end storage (whether a queue, stack, list, or something else). BlockingCollection<T> provides blocking and bounding support for collections that implement the IProducerConsumerCollection<T> interface. |
| ConcurrentBag<T>* | A thread-safe unordered collection of T type objects. |
| ConcurrentDictionary<TKey, TValue> | A thread-safe dictionary; a collection of keys and values. |
| ConcurrentQueue<T>* | A thread-safe queue supporting first in, first out (FIFO) semantics on objects of type T. |
| ConcurrentStack<T>* | A thread-safe stack supporting first in, last out (FILO) semantics on objects of type T. |

* Collection classes that implement IProducerConsumerCollection<T>.

A common pattern enabled by concurrent collections is support for thread-safe access by producers and consumers. Classes that implement `IProducerConsumerCollection<T>` (identified by * in Table 20.4) are specifically designed to provide such support. This enables one or more classes to be pumping data into the collection while a different set reads it out, removing it. The order in which data is added and removed is determined by the individual collection classes that implement the `IProducerConsumerCollection<T>` interface.

Although it is not built into the out-of-the-box .NET/.NET Core Frameworks, an additional immutable collection library is available as a NuGet package reference, called `System.Collections.Immutable`. The advantage of the immutable collection is that it can be passed freely between threads without concern for either deadlocks or interim updates. As immutable collections cannot be modified, interim updates won't occur; thus such collections are automatically thread-safe (so there is no need to lock access). For more information, see http://itl.tc/SystemCollectionsImmutable.

# Thread Local Storage

In some cases, using synchronization locks can lead to unacceptable performance and scalability restrictions. In other instances, providing synchronization around a particular data element may be too complex, especially when it is added after the original coding.

One alternative solution to synchronization is isolation, and one method for implementing isolation is **thread local storage**. With thread local storage, each thread has its own dedicated instance of a variable.
