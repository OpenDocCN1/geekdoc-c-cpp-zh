
- Twenty bits represent the number of writer threads waiting (WW) to get into the lock. These threads block on the other semaphore object.

Now, because all the information about the lock fits in a single Int32 field, I can manipulate this field by using the methods of the Interlocked class so the lock is incredibly fast and causes a thread to block only when there is contention.

Here's what happens when a thread enters the lock for shared access.

- If the lock is Free: Set state to OwnedByReaders, RR=1, Return.
- If the lock is OwnedByReaders: RR++, Return.
- Else: RW++, Block reader thread. When the thread wakes, loop around and try again.

Here's what happens when a thread that has shared access leaves the lock.

- RR--
- If RR > 0: Return
- If WW > 0: Set state to ReservedForWriter, WW--, Release 1 blocked writer thread, Return
- If RW == 0 && WW == 0: Set state to Free, Return

Here's what happens when a thread enters the lock for exclusive access:

- If the lock is Free: Set state to OwnedByWriter, Return.
- If the lock is ReservedForWriter: Set state to OwnedByWriter, Return.
- If the lock is OwnedByWriter: WW++, Block writer thread. When thread wakes, loop around and try again.
- Else: Set state to OwnedByReadersAndWriterPending, WW++, Block writer thread. When thread wakes, loop around and try again.

Here's what happens when a thread that has exclusive access leaves the lock:

- If WW == 0 && RW == 0: Set state to Free, Return
- If WW > 0: Set state to ReservedForWriter, WW--, Release 1 blocked writer thread, Return
- If WW == 0 && RW > 0: Set state to Free, RW=0, Wake all blocked reader threads, Return

Let's say that there is currently one thread reading from the lock and another thread wants to enter the lock for writing. The writer thread will first check to see if the lock is Free, and because it is not, the thread will advance to perform the next check. However, at this point, the reader thread could leave the lock, and seeing that RR and WW are both 0, the thread could set the lock's state to Free. This is a problem because the writer thread has already performed this test and moved on. Basically what happened is that the reader thread changed the state that the writer thread was accessing behind its back. I needed to solve this problem so that the lock would function correctly. To solve the problem, all of these bit manipulations are performed using the technique I showed in the “The Interlocked Anything Pattern” section from Chapter 29. If you recall, this pattern lets you turn any operation into a thread-safe atomic operation. This is what allows this lock to be so fast and have less state in it than other reader-writer locks. When I run performance tests comparing my OneManyLock against the FCL’s ReaderWriterLockSlim and ReaderWriterLock classes, I get the following results.

| 操作 | 耗时 | 相对性能 |
|---|---|---|
| Incrementing x in OneManyLock | 330 | Fastest |
| Incrementing x in ReaderWriterLockSlim | 554 | ~1.7x slower |
| Incrementing x in ReaderWriterLock | 984 | ~3x slower |

Of course, because all reader-writer locks perform more logic than a mutually exclusive lock, their performance can be slightly worse. However, you have to weigh this against the fact that a reader-writer lock allows multiple readers into the lock simultaneously.

Before leaving this section, I’ll also mention that my Power Threading library (downloadable for free from http://Wintellect.com/PowerThreading.aspx) offers a slightly different version of this lock, called OneManyResourceLock. This lock and others in the library offer many additional features, such as deadlock detection, the ability to turn on lock ownership and recursion (albeit at a performance cost), a unified programming model for all locks, and the ability to observe the run-time behavior of the locks. For observing behavior, you can see the maximum amount of time that a thread ever waited to acquire a lock, and you can see the minimum and maximum amount of time that a lock was held.

### The CountdownEvent Class

The next construct is System.Threading.CountdownEvent. Internally, this construct uses a ManualResetEventSlim object. This construct blocks a thread until its internal counter reaches 0. In a way, this construct’s behavior is the opposite of that of a Semaphore (which blocks threads while its count is 0). Here is what this class looks like (some method overloads are not shown).

```csharp
public class CountdownEvent : IDisposable {
    public CountdownEvent(Int32 initialCount);
    public void Dispose();
    public void Reset(Int32 count);              // Set CurrentCount to count
    public void AddCount(Int32 signalCount);     // Increments CurrentCount by signalCount
    public Boolean TryAddCount(Int32 signalCount); // Increments CurrentCount by signalCount
    public Boolean Signal(Int32 signalCount);    // Decrements CurrentCount by signalCount
    public Boolean Wait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

    public Int32       CurrentCount { get; }
    public Boolean     IsSet        { get; }      // true if CurrentCount is 0
    public WaitHandle  WaitHandle   { get; }
}
```

After a CountdownEvent’s CurrentCount reaches 0, it cannot be changed. The AddCount method throws InvalidOperationException when CurrentCount is 0, whereas the TryAddCount method simply returns false if CurrentCount is 0.

### The Barrier Class

The System.Threading.Barrier construct is designed to solve a very rare problem, so it is unlikely that you will have a use for it. Barrier is used to control a set of threads that are working together in parallel so that they can step through phases of the algorithm together. Perhaps an example is in order: when the CLR is using the server version of its garbage collector (GC), the GC algorithm creates one thread per core. These threads walk up different application threads' stacks, concurrently marking objects in the heap. As each thread completes its portion of the work, it must stop waiting for the other threads to complete their portion of the work. After all threads have marked the objects, then the threads can compact different portions of the heap concurrently. As each thread finishes compacting its portion of the heap, the thread must block waiting for the other threads. After all the threads have finished compacting their portion of the heap, then all the threads walk up the application's threads' stacks, fixing up roots to refer to the new location of the compacted object. Only after all the threads have completed this work is the garbage collector considered complete and the application's threads can be resumed.

This scenario is easily solved using the Barrier class, which looks like this (some method overloads are not shown).

```csharp
public class Barrier : IDisposable {
    public Barrier(Int32 participantCount, Action<Barrier> postPhaseAction);
    public void Dispose();
    public Int64 AddParticipants(Int32 participantCount); // Adds participants
    public void RemoveParticipants(Int32 participantCount); // Subtracts participants
    public Boolean SignalAndWait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

    public Int64 CurrentPhaseNumber    { get; } // Indicates phase in process (starts at 0)
    public Int32 ParticipantCount      { get; } // Number of participants
    public Int32 ParticipantsRemaining { get; } // # of threads needing to call SignalAndWait
}
```

When you construct a Barrier, you tell it how many threads are participating in the work, and you can also pass an Action<Barrier> delegate referring to code that will be invoked whenever all participants complete a phase of the work. You can dynamically add and remove participating threads from the Barrier by calling the AddParticipants and RemoveParticipants methods but, in practice, this is rarely done. As each thread completes its phase of the work, it should call SignalAndWait, which tells the Barrier that the thread is done and the Barrier blocks the thread (using a ManualResetEventSlim). After all participants call SignalAndWait, the Barrier invokes the delegate (using the last thread that called SignalAndWait) and then unblocks all the waiting threads so they can begin the next phase.

### Thread Synchronization Construct Summary

My recommendation always is to avoid writing code that blocks any threads. When performing asynchronous compute or I/O operations, hand the data off from thread to thread in such a way to avoid the chance that multiple threads could access the data simultaneously. If you are unable to fully
