
# TABLE 10-5 (continued)

| TYPE NAME | DESCRIPTION |
| --- | --- |
| ConcurrentBag<T> | This class represents a thread-safe, unordered collection of objects. You can use ConcurrentBag<T> where the thread will be both producing and consuming data stored in the bag, because ConcurrentBag<T> performance is optimized for these scenarios. |
| ConcurrentDictionary<TKey, TValue> | This class represents a thread-safe collection of key-value pairs that can be accessed by multiple threads concurrently. You can use the Dictionary<TKey, TValue> easily, because it implements the same semantics. The internal implementation of this class provides a much better scaling for multiple threads in both small and large dictionaries than you can achieve with Dictionary<TKey, TValue>. |
| ConcurrentQueue<T> | This class represents a thread-safe First-In-First-Out (FIFO) collection. |
| ConcurrentStack<T> | This class represents a thread-safe Last-In-First-Out (LIFO) collection. |

Except ConcurrentDictionary<TKey, TValue>, all other classes implement the IProducerConsumerCollection<T> interface, which represents a collection that allows for thread-safe adding and removing of data.

# Synchronization Primitives

The System.Threading namespace contains new types that avoid expensive locking mechanisms in legacy multithreading code. Most of these types are lightweight, and enable fine-grained concurrency and faster performance than predecessors in the .NET Framework.

Table 10-6 lists these synchronization primitives.

# TABLE 10-6: Synchronization Primitives

| TYPE NAME | DESCRIPTION |
| --- | --- |
| Barrier | This class is new, and it does not have a predecessor in the previous .NET Framework versions. Barrier enables multiple tasks to cooperatively work on an algorithm in parallel through multiple phases. You can use this class to manage a group of tasks to cooperate by moving through a series of phases, where each in the group signals it has arrived at the Barrier in a given phase, and implicitly waits for others to arrive. |
| | A real-life example is when company cars are driven across the U.S. from Seattle to Miami. The drivers do not drive in a convoy, but agree on several points (let's say Denver and Houston) where they wait for each other. When everyone arrives at these barriers, they start the next section of the route. The same Barrier instance can be used for multiple phases. |
| CountdownEvent | This class represents a synchronization primitive that is signaled when its count reaches zero. You can use this in fork-and-join scenarios, because it provides an easy rendezvous mechanism. CountdownEvent allows to wait until one or more threads finish some other operation. An instance of this class is initialized with an integral count, typically greater than 0. Threads block waiting on the event until the count reaches 0, at which the count is decremented by CountdownEvent's Decrement method, which is typically called by a worker thread completing a unit of work being tracked by the event. |
| ManualResetEventSlim | This type is a slimmed down and lightweight version of its predecessor, ManualResetEvent, and can be used to notify one or more waiting threads that an event has occurred. The price of slimming is that you can use an instance of ManualResetEventSlim only for intra-process communication. |
| SemaphoreSlim | This lightweight class can be used to limit the number of threads that can access a resource or pool of resources. It has a predecessor Semaphore introduced by .NET 2.0. However, while Semaphore leverages on Windows kernel semaphores, SemaphoreSlim does not. |
| SpinLock, SpinWait | These synchronization primitives enable a thread to wait. They improve performance when the wait time is expected to be short, by avoiding expensive switching and blocking operations. SpinLock is a mutual-exclusion lock that causes the thread that is acquiring the lock to wait in a loop (or spin) for a period of time before yielding its quantum. SpinLock is a value type, that for performance reasons, so you need to pass a SpinLock instance around, it should be passed by reference, rather than by value. SpinWait is a small, lightweight type that will spin for a specified time and eventually put the thread into a wait state if the count is exceeded. SpinWait is a value type; its members are not thread-safe. If multiple threads spin, each should use its own instance of SpinWait. |

These synchronization primitives play an important role in TPL implementation. They are heavily used, and significantly contribute to the great performance of TPL.

# Lazy Initialization Classes

Postponing initialization of type members until they are needed is a frequently used programming pattern. It is especially useful when initialization is expensive by means of consumed CPU cycles, memory, or other resources. Lazy initialization classes listed in Table 10-7 help you in these scenarios.

**TABLE 10-7:** Lazy Initialization Types

| TYPE NAME | DESCRIPTION |
| --- | --- |
| System.Lazy<T> | This class provides support for lazy initialization of a T instance. When you create an instance of Lazy<T>, it does not instantiate T. You can access the instance behind Lazy<T> using its Value property. Lazy initialization occurs the first time the Lazy<T>.Value property is accessed, or the Lazy<T>.ToString method is called. |
| System.Threading.LazyInitializer | This static class provides lazy initialization routines. .NET Framework 4.0, you can use a few overloads of the EnsureInitialized method. In the future, the class may be extended with more helper methods. In scenarios where you might lazy-initialize a number of objects, you might decide that wrapping each object in a Lazy<T> requires too much memory, or too many computing resources. Or, you might have stringent requirements about how lazy initialization is exposed. In such cases, you can use the static EnsureInitialized methods to lazy-initialize without wrapping it in an instance of Lazy<T>. |
| System.Threading.ThreadLocal<T> | This class provides thread-local storage of data type T. Although this class lazy initialization in its implementation, "laziness" isn't its main functionality. By providing an instance of ThreadLocal<T>, you can be sure that the T instance accessed through Value property is shared within the thread it created. Its role is similar to the ThreadStatic attribute used to decorate static fields. However, ThreadLocal<T> provides better performance. |

# Cancellation Primitives

If you know how complex it could be. TPL provides a few types that simplify the complexity of cancellation. The primitives listed in Table 10-8 can be used in your parallel applications using tasks, PLINQ expression, and Parallel loops.

# TABLE 10-8: Cancellation Primitives

| TYPE NAME | DESCRIPTION |
| --- | --- |
| CancellationToken | This structure propagates notification that operations should be cancelled. You can pass an instance of CancellationToken to blocking calls such as BlockingCollection.Add(..), BlockingCollection.Take(..), ManualResetEventSlim.Wait(..), Task.Wait(...), and Task.WaitAll(...). These methods have overloads that accept a CancellationToken instance, and finish when a cancellation occurs. |
| CancellationTokenSource | This class signals to a Cancellation that should be cancelled. You can use this as a conductor in cooperative cancellation scenarios. You can pass the Token of a CancellationTokenSource to methods accepting it. When the Cancel method is called, all instances belonging to this CancellationTokenSource instance will be notified. |

# CODE CONTRACTS

Modern software architecture uses layers and components with exact boundaries and well-defined responsibilities. Without this kind of approach, it is difficult to writeable software with good quality. The cooperation among these components is generally defined by contracts. For many developers, contracts are the definitions of interfaces (interface classes) and related data objects or entities the components use to define the communication surface. For example, let's assume that you develop warehouse management software where one of the interfaces is WarehouseService and a related entity is:

```
public class WarehouseService
{
    public void QueueOrder(Order order)
    {
        // ...
    }
}
```

public class Order
```
