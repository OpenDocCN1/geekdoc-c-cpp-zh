
![](img/a16f85e62ce9bdc527f4b09dbfe26092_1510_0.png)

FIGURE 29.23 Railway semaphores synchronize access to a railway.

From a managed code point of view, semaphores are exposed through the Semaphore class, which is constructed with two integer values, one for an initial count and one for the maximum count. The idea is this: The maximum count indicates the number of concurrent entries that are possible to code protected by the semaphore. Using the railway semaphore as an analogy, this count would be two because two trains can be on the railway segment at the same time (one of which has to proceed with caution):

```csharp
var railwaySemaphore = new Semaphore(2, 2);
```

The first parameter for initial count indicates how many parties are initially allowed to “run with” the semaphore. In the preceding, we set this number to 2, which means the railway semaphore was erected when no trains were on the segment that the device is about to protect. In other words, two trains are allowed to pass the semaphore right after it's taken in use by the railway company.

Two key operations exist on a semaphore (ignoring overloads), as shown here. The Release methods are used to decrement the value of the semaphore, either by one or by the specified count. The WaitOne methods are inherited from a WaitHandle base class (which is discussed in the “Signaling with Events” section) and increment the semaphore's value. If the semaphore has reached its maximum count, the WaitOne method blocks until the value gets decreased by Release calls:

```csharp
public int Release();
public int Release(int releaseCount);

public virtual bool WaitOne();
// More WaitOne method overloads...
```

Multiple threads can be waiting on the semaphore at the same time. Which thread will get a chance to run after the WaitOne operation succeeds is unpredictable and depends on the operating system scheduler's mood. Unless the release count is more than one, no two threads will be able to return from the WaitOne operation. After all, primitives such as semaphores provide firm guarantees about their protection facilities. In case of a semaphore, it should never be possible to have more than the specified maximum uses of the semaphore at the same time.

An example with trains is shown here. Obviously, this simple example doesn't protect a shared resource for real (just an imaginary railway segment). True use of semaphores includes protecting a shared resource pool with an upper bound on the number of uses that are permitted simultaneously. Such an example is shown on MSDN.

```csharp
var rnd = new Random();

var railwaySemaphore = new Semaphore(2, 2);
for (int i = 0; i < 10; i++)
{
    new Thread(() =>
    {
        // Time to leave the railway station.
        Thread.Sleep(rnd.Next(500, 8000));
        Console.WriteLine(Thread.CurrentThread.Name + " departing.");

        // Time to reach the semaphore next to the track.
        Thread.Sleep(rnd.Next(100, 5000));
        Console.WriteLine(Thread.CurrentThread.Name + " at signal.");

        // Waiting for the first signal.
        // The train is allowed to pass if no two trains are in the segment.
        railwaySemaphore.WaitOne();
        Console.WriteLine(Thread.CurrentThread.Name + " passed signal.");

        // Time to reach the end of the protected railway segment.
        Thread.Sleep(rnd.Next(2000, 4000));
        Console.WriteLine(Thread.CurrentThread.Name + " exited segment.");
        railwaySemaphore.Release();
    }) { Name = "Train " + i }.Start();
}
```

If the semaphore works correctly (it does), you shouldn't see more than two messages about a train passing the signal without a train exiting the segment first. It's left as an exercise for UI-savvy readers to implement a graphical visualization of the track, the signal, and the different trains driving over the railway.

Just like mutexes, semaphores are a built-in operating system primitives exposed to managed code. In the code shown here, we've been using a local semaphore without a name. However, constructor overloads exist, as well as a static OpenExisting method, to work with named semaphores. Such semaphore objects can be used across several processes to coordinate use of a shared resource pool, for instance.

Because of their impact on the scheduling of operating system threads (putting them in a waiting blocked state while acquiring the semaphore through WaitOne), you need to account for a certain overhead. To reduce this overhead in particular scenarios, a new type has been introduced in .NET 4 called SemaphoreSlim. This one doesn't rely on the operating system-level concept of a semaphore and is less expensive. It's especially well suited when only a single process needs protection for a shared resource because this class supports only local unnamed semaphores. In other words, it's a feature that sits at the common language runtime level without the operating system's knowledge of it.

One API-level difference is the Wait method rather than the WaitOne method. In fact, WaitOne is an inheritance (literally) from the WaitHandle base class used for various operating system-level synchronization primitive wrappers. The SemaphoreSlim not being such a primitive, it doesn't derive from this class. However, if a wait operation using a WaitHandle is desirable, the AvailableWaitHandle property can be used. We don't elaborate on the concept of wait handles just yet; they're discussed in more detail during our discussion in the “Signaling with Events” section.

Finally, where the Semaphore class doesn't expose the current count of the semaphore, the SemaphoreSlim class does through a CurrentCount property.

## More Advanced Locks

Added in .NET 3.5 and .NET 4, respectively, the ReaderWriterLockSlim and SpinLock primitives are often useful, too. Their use is fairly specialized, so we'll limit ourselves to a basic discussion.

## ReaderWriterLock(Slim)

The essential problem of various concurrency and synchronization problems boils down to simultaneous reader and writer accesses on a shared resource. Often, the presence of multiple readers is allowed, while writers should be protected from one another to prevent harm. Therefore, the classic monitor-based lock is often too coarse-grained because it can't differentiate from reader and writer accesses.

ReaderWriterLock and ReaderWriterLockSlim accommodate for such scenarios. The latter was introduced in .NET 3.5 and is recommended. Use of reader/writer locks is restricted to the current process only, and the lock doesn't wrap functionality provided by the operating system. In such a case, the slogan “the slimmer, the better” definitely holds, hence the advice to use ReaderWriterLockSlim nowadays. We only talk about this class to give you an idea about the lock's use.

In its very essence, ReaderWriterLockSlim exposes pairs of Enter and Exit methods for different kinds of accesses, as follows:

- **Read mode:** Any number of threads can be reading at the same time; in other words, sharing is allowed.
- **Write mode:** Only one thread can have this exclusive write access. Being in this mode prevents others from entering the lock due to its exclusive nature.
- **Upgradeable mode is a special read mode:** At some point in the future, the reader thread may decide to upgrade the lock to gain writer access.

The precise behavior of attempts to acquire the lock depends on the current state the lock is in. This is detailed in a table on MSDN. In short, the idea is to allow for many readers and to prevent writers from messing up state. To do so, writers block everyone else who attempts to access the lock in any mode. Readers, on the other hand, permit more readers to enter, unless a writer is waiting to gain access. An attempt to gain write access blocks until everyone else has left the lock.

It should be mentioned that two families of enter methods exist. One set of methods is of the form Enter followed by the desired access level. Those methods block until the requested access is permitted. The TryEnter set of methods returns a Boolean value to indicate whether the request (with an optional timeout) to enter the lock succeeded.

A trivial example of reader/writer locks is shown in the following code fragment:

```csharp
var @lock = new ReaderWriterLockSlim();

int counter = 0;
new Thread(() =>
{
    while (true)
    {
        @lock.EnterWriteLock();
        counter++;
        counter--;
        @lock.ExitWriteLock();
    }
}).Start();

while (true)
{
    Thread.Sleep(100);

    @lock.EnterReadLock();
    Console.WriteLine(counter);
    @lock.ExitReadLock();
}
```

The main thread here acts as a monitor of some counter. Many such monitors could be observing the counter value simultaneously without doing any harm. However, some background thread is updating the counter constantly. Such updates should never be observable in an intermediate nonatomic state. Because of this, we need locks.

Try taking out any of the locks to see the counter invariant being broken. In particular, the counter should never read a value other than zero because the increment and decrement operations should remain balanced. You're also encouraged to add more reader and writer threads to the mix to show the reader/writer lock properly protects read and write accesses to the counter. Messing up the access level associated with a piece of code (for
