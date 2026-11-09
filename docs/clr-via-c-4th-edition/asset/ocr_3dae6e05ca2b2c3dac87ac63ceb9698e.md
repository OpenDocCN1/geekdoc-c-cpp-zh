# The ManualResetEventSlim and SemaphoreSlim Classes

The first two hybrid constructs are System.Threading.ManualResetEventSlim and System.Threading.SemaphoreSlim.² These constructs work exactly like their kernel-mode counterparts, except that both employ spinning in user mode, and they both defer creating the kernel-mode construct until the first time contention occurs. Their Wait methods allow you to pass a timeout and a CancellationToken. Here is what these classes look like (some method overloads are not shown).

```
```csharp
public class ManualResetEventSlim : IDisposable {
   public ManualResetEventSlim(Boolean initialState, Int32 spinCount);
   public void Dispose();
   public void Reset();
   public void Set();
   public Boolean Wait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

   public Boolean IsSet { get; }
   public Int32 SpinCount { get; }
   public WaitHandle WaitHandle { get; }
}
public class SemaphoreSlim : IDisposable {
   public SemaphoreSlim(Int32 initialCount, Int32 maxCount);
   public void Dispose();
   public Int32 Release(Int32 releaseCount);
   public Boolean Wait(Int32 millisecondsTimeout, CancellationToken cancellationToken);

   // Special method for use with async and await (see Chapter 28)
   public Task<Boolean> WaitAsync(Int32 millisecondsTimeout, CancellationToken
      cancellationToken);

   public Int32 CurrentCount { get; }
   public WaitHandle AvailableWaitHandle { get; }
}
```
```

# The Monitor Class and Sync Blocks

Probably the most-used hybrid thread synchronization construct is the Monitor class, which provides a mutual-exclusive lock supporting spinning, thread ownership, and recursion. This is the most-used construct because it has been around the longest, C# has a built-in keyword to support it, the just-in-time (JIT) compiler has built-in knowledge of it, and the common language runtime (CLR) itself uses it on your application’s behalf. However, as you’ll see, there are many problems with this construct, making it easy to produce buggy code. I’ll start by explaining the construct, and then I’ll show the problems and some ways to work around these problems.

Every object on the heap can have a data structure, called a sync block, associated with it. A sync block contains fields similar to that of the AnotherHybridLock class that appeared earlier in this chapter. Specifically, it has fields for a kernel object, the owning thread’s ID, a recursion count, and a waiting threads count. The Monitor class is a static class whose methods accept a reference to

² Although there is no AutoResetEventSlim class, in many situations you can construct a SemaphoreSlim object with a maxCount of 1.