
Windows allows a thread to specify a priority when making I/O requests. For more details about I/O priorities, refer to the white paper at http://www.microsoft.com/whdc/driver/priorityio.mspx. Unfortunately, the FCL does not include this functionality yet; hopefully, it will be added in a future version. However, you can still take advantage of this feature by P/Invoking out to native Win32 functions. Here is the P/Invoke code:

```csharp
internal static class ThreadIO {
    public static BackgroundProcessingDisposer BeginBackgroundProcessing(
        Boolean process = false) {

        ChangeBackgroundProcessing(process, true);
        return new BackgroundProcessingDisposer(process);
    }

    public static void EndBackgroundProcessing(Boolean process = false) {
        ChangeBackgroundProcessing(process, false);
    }

    private static void ChangeBackgroundProcessing(Boolean process, Boolean start) {
        Boolean ok = process
            ? SetPriorityClass(GetCurrentWin32ProcessHandle(),
                  start ? ProcessBackgroundMode.Start : ProcessBackgroundMode.End)
            : SetThreadPriority(GetCurrentWin32ThreadHandle(),
                  start ? ThreadBackgroundMode.Start : ThreadBackgroundMode.End);
        if (!ok) throw new Win32Exception();
    }

    // This struct lets C#'s using statement end the background processing mode
    public struct BackgroundProcessingDisposer : IDisposable {
        private readonly Boolean m_process;
        public BackgroundProcessingDisposer(Boolean process) { m_process = process; }
        public void Dispose() { EndBackgroundProcessing(m_process); }
    }


    // See Win32’s THREAD_MODE_BACKGROUND_BEGIN and THREAD_MODE_BACKGROUND_END
    private enum ThreadBackgroundMode { Start = 0x10000, End = 0x20000 }

    // See Win32’s PROCESS_MODE_BACKGROUND_BEGIN and PROCESS_MODE_BACKGROUND_END
    private enum ProcessBackgroundMode { Start = 0x100000, End = 0x200000 }

    [DllImport("Kernel32", EntryPoint = "GetCurrentProcess", ExactSpelling = true)]
    private static extern SafeWaitHandle GetCurrentWin32ProcessHandle();

    [DllImport("Kernel32", ExactSpelling = true, SetLastError = true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern Boolean SetPriorityClass(
        SafeWaitHandle hprocess, ProcessBackgroundMode mode);

    [DllImport("Kernel32", EntryPoint = "GetCurrentThread", ExactSpelling = true)]
    private static extern SafeWaitHandle GetCurrentWin32ThreadHandle();

    [DllImport("Kernel32", ExactSpelling = true, SetLastError = true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern Boolean SetThreadPriority(
        SafeWaitHandle hThread, ThreadBackgroundMode mode);

    // http://msdn.microsoft.com/en-us/library/aa480216.aspx
    [DllImport("Kernel32", SetLastError = true, EntryPoint = "CancelSynchronousIo")]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern Boolean CancelSynchronousIo(SafeWaitHandle hThread);
}
```

And here is code showing how to use it:

```csharp
public static void Main() {
    using (ThreadIO.BeginBackgroundProcessing()) {
        // Issue low-priority I/O requests in here (eg: calls to ReadAsync/WriteAsync)
    }
}
```

You tell Windows that you want your thread to issue low-priority I/O requests by calling ThreadIO's BeginBackgroundProcessing method. Note that this also lowers the CPU scheduling priority of the thread. You can return the thread to making normal-priority I/O requests (and normal CPU scheduling priority) by calling EndBackgroundProcessing or by calling Dispose on the value returned by BeginBackgroundProcessing (as shown above via C#'s using statement). A thread can only affect its own background processing mode; Windows doesn't allow a thread to change the background processing mode of another thread.

If you want all threads in a process to make low-priority I/O requests and have low CPU scheduling, you can call BeginBackgroundProcessing, passing in true for the process parameter. A process can only affect its own background processing mode; Windows doesn't allow a thread to change the background processing mode of another process.

**Important** As a developer, it is your responsibility to use these new background priorities to allow the foreground applications to be more responsive, taking care to avoid priority inversion. In the presence of intense normal-priority I/Os, a thread running at background priority can be delayed for seconds before getting the result of its I/O requests. If a low-priority thread has grabbed a thread synchronization lock for which the normal-priority thread is waiting, the normal-priority threads might end up waiting for the background-priority thread until the low-priority I/O requests are completed. Your background-priority thread does not even have to submit I/Os for the problem to happen. So using shared synchronization objects between normal- and background-priority threads should be minimized (or eliminated if possible) to avoid these priority inversions where normal-priority threads are blocked on locks owned by background-priority threads.

## Chapter 29

### Primitive Thread Synchronization Constructs

In this chapter:

- Class Libraries and Thread Safety — 793
- Primitive User-Mode and Kernel-Mode Constructs — 794
- User-Mode Constructs — 796
- Kernel-Mode Constructs — 813

When a thread pool thread blocks, the thread pool creates additional threads, and the time and memory resources required to create, destroy, and schedule threads is very expensive. When many developers see that they have threads in their program that are not doing anything useful, they tend to create more threads in hopes that the new threads will do something useful. The key to building scalable and responsive applications is to not block the threads you have, so that they can be used and reused to execute other tasks. Chapter 27, “Compute-Bound Asynchronous Operations,” focused on how to use existing threads to perform compute-bound operations, and Chapter 28, “I/O-Bound Asynchronous Operations,” focused on how to use threads when performing I/O-bound operations.

In this chapter, I focus on thread synchronization. Thread synchronization is used to prevent corruption when multiple threads access shared data at the same time. I emphasize at the same time, because thread synchronization is all about timing. If you have some data that is accessed by two threads and those threads cannot possibly touch the data simultaneously, then thread synchronization is not required at all. In Chapter 28, I discussed how different sections of async functions can be executed by different threads. Here we could potentially have two different threads accessing the same variables and data. But async functions are implemented in such a way that it is impossible for two threads to access this same data at the same time. Therefore, no thread synchronization is required when code accesses data contained within the async function.

This is ideal because thread synchronization has many problems associated with it. First, it is tedious and extremely error-prone. In your code, you must identify all data that could potentially be touched by multiple threads at the same time. Then you must surround this code with additional code that acquires and releases a thread synchronization lock. The lock ensures that only one thread at a time can access the resource. If you forget to surround just one block of code with a lock, then the data will become corrupted. Also, there is no way to prove that you have added all your locking code correctly. You just have to run your application, stress-test it a lot, and hope that nothing goes wrong. In fact, you should test your application on a machine that has as many CPUs as possible because the more CPUs you have, the better chance that two or more threads will attempt to access the resource at the same time, making it more likely you’ll detect a problem.

The second problem with locks is that they hurt performance. It takes time to acquire and release a lock because there are additional method calls, and because the CPUs must coordinate with each other to determine which thread will acquire the lock first. Having the CPUs in the machine communicate with each other this way hurts performance. For example, let’s say that you have code that adds a node to the head of a linked list:

```csharp
// This class is used by the LinkedList class
public class Node {
    internal Node m_next;
    // Other members not shown
}
```

```csharp
public sealed class LinkedList {
    private Node m_head;

    public void Add(Node newNode) {
        // The two lines below perform very fast reference assignments
        newNode.m_next = m_head;
        m_head = newNode;
    }
}
```

This Add method simply performs two reference assignments that can execute extremely fast. Now, if we want to make Add thread safe so that multiple threads can call it simultaneously without corrupting the linked list, then we need to have the Add method acquire and release a lock:

```csharp
public sealed class LinkedList {
    private SomeKindOfLock m_lock = new SomeKindOfLock();
    private Node m_head;

    public void Add(Node newNode) {
        m_lock.Enter();
        // The two lines below perform very fast reference assignments
        newNode.m_next = m_head;
        m_head = newNode;
        m_lock.Leave();
    }
}
```

While Add is now thread safe, it has also become substantially slower. How much slower depends on the kind of lock chosen; I will compare the performance of various locks in this chapter and in Chapter
