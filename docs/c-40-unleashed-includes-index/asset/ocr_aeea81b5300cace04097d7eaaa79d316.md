Close, or by means of the using statement. Internally, it simply calls the helper Dispose method with a Boolean argument to perform the cleanup. Here we centralize all logic for both the IDisposable case and the finalizer case. The disposing parameter is used to differentiate both cases in case cleanup logic needs to be a bit different depending on the use. In addition to calling the cleanup code, Dispose also tells the garbage collector it doesn't need to bother calling the finalizer method because the user has already done the disposal explicitly.

To wrap up this preliminary discussion about disposal patterns, note that generally you'll be at the consuming side where the proper use of the using statement can save you lots of headaches. If you forget to dispose of a resource properly, issues may pop up when you least expect them, so make sure to check whether a type implements IDisposable. If so, take the appropriate action to ensure the object gets disposed at a reasonable time.

Along those lines, try to avoid having a using statement's code block exceed the time the acquired resource is needed. This keeps the resource alive for an unnecessarily long period and can lead to all sorts of contention (lock duration, pool exhaustion, and so forth) on whatever system maintains that resource. Remember, you're probably not the only one who relies on the resource or the system maintaining it.

```
/*ab*/using (resource)
{
    // Lots of resource-agnostic fluff here.

    /* Really using the resource here. */

    // And more fluff that doesn't rely on the resource.
}
```

# (In)appropriate Use of IDisposable

One danger of telling people the implementation of the using statement is that they start to retrofit the pattern for purposes other than deterministic resource cleanup. In its true essence, the using statement is a try-finally statement in disguise with some method call happening nearly at the very end of the associated block. The following is a sample use of IDisposable is to implement a code execution timing facility:

```
using (new ExecutionTimer(Console.Out /* to log to */))
    // Code to be benchmarked goes here.
```

Here, the constructor of ExecutionTimer would start the timer and the Dispose method would stop it, printing the elapsed time since the constructor was called to the specified logger. Although this can be handy at times, the using statement was never intended to be a general-purpose code block decoration facility. When browsing code, seeing a using statement is meant to trigger “aha, the developer is dealing with some resource that