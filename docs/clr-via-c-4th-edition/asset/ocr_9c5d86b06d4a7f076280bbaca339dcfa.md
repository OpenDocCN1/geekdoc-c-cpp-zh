To solve the problem, all of these bit manipulations are performed using the technique I showed in the “The Interlocked Anything Pattern” section from Chapter 29. If you recall, this pattern lets you turn any operation into a thread-safe atomic operation. This is what allows this lock to be so fast and have less state in it than other reader-writer locks. When I run performance tests comparing my OneManyLock against the FCL’s ReaderWriterLockSlim and ReaderWriterLock classes, I get the following results.

+   - Incrementing x in OneManyLock: 330 — Fastest
+   - Incrementing x in ReaderWriterLockSlim: 554 — ~1.7x slower
+   - Incrementing x in ReaderWriterLock: 984 — ~3x slower

Of course, because all reader-writer locks perform more logic than a mutually exclusive lock, their performance can be slightly worse. However, you have to weigh this against the fact that a reader-writer lock allows multiple readers into the lock simultaneously.

Before leaving this section, I’ll also mention that my Power Threading library (downloadable for free from http://Wintellect.com/PowerThreading.aspx) offers a slightly different version of this lock, called OneManyResourceLock. This lock and others in the library offer many additional features, such as deadlock detection, the ability to turn on lock ownership and recursion (albeit at a performance cost), a unified programming model for all locks, and the ability to observe the run-time behavior of the locks. For observing behavior, you can see the maximum amount of time that a thread ever waited to acquire a lock, and you can see the minimum and maximum amount of time that a lock was held.

# # The CountdownEvent Class

The next construct is System.Threading.CountdownEvent. Internally, this construct uses a ManualResetEventSlim object. This construct blocks a thread until its internal counter reaches 0. In a way, this construct’s behavior is the opposite of that of a Semaphore (which blocks threads while its count is 0). Here is what this class looks like (some method overloads are not shown).

```
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
```

After a CountdownEvent’s CurrentCount reaches 0, it cannot be changed. The AddCount method throws InvalidOperationException when CurrentCount is 0, whereas the TryAddCount method simply returns false if CurrentCount is 0.