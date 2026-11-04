Actually, you can see the threads executing simultaneously by using the Parallel Stacks window found under the Debug, Windows menu (see Figure 8.27). This feature was added in addition to the Threads window in .NET 4.0, where threads got an additional abstraction level called “tasks.” The Parallel Tasks and Parallel Stacks windows enable users to get a better picture of what task spawned which other tasks and so on.

![](bbox=[0.04, 0.25, 0.7, 0.56])

FIGURE 8.27 Parallel stacks showing simultaneous execution.

# A SIMPLER FIX

Before I continue discussing multithreading and locking techniques, I have to say this particular example is so simple that we can tackle it in a very specific way to yield the correct result. Incrementing and decrementing values are such common operations that atomic variants for it exist, directly supported by the processor hardware. During a single instruction on the hardware level, it's impossible for the OS to perform a context switch, so that takes care of the problem:

```
public void Increment()
{
    Interlocked.Increment(ref _value);
}

public void Decrement()
{
    Interlocked.Decrement(ref _value);
}
```

Notice that the hardware itself has parallelization built in based on the concept of pipelining, but that stretches way beyond our scope of discussion.

# The lock Statement

Since the very first version of the C# language, it was thought important to have language-level support for mutual-exclusion execution of code. The central concept here is that of a lock, which is acquired upon entrance of a block of code and released at the end of it. Lock ownership is an exclusive right; no two blocks of code should be allowed to execute simultaneously. When a lock is already held when another piece of code tries to