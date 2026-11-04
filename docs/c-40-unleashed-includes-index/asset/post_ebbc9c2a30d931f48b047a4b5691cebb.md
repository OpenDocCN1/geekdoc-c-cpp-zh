
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

## (In)appropriate Use of IDisposable

One danger of telling people the implementation of the using statement is that they start to retrofit the pattern for purposes other than deterministic resource cleanup. In its true essence, the using statement is a try-finally statement in disguise with some method call happening nearly at the very end of the associated block. The following is a sample use of IDisposable to implement a code execution timing facility:

```
using (new ExecutionTimer(Console.Out /* to log to */))
    // Code to be benchmarked goes here.
```

Here, the constructor of ExecutionTimer would start the timer and the Dispose method would stop it, printing the elapsed time since the constructor was called to the specified logger. Although this can be handy at times, the using statement was never intended to be a general-purpose code block decoration facility. When browsing code, seeing a using statement is meant to trigger “aha, the developer is dealing with some resource that requires cleanup” (IDisposable semantics) and not “aha, the developer is sneaking in some code at the end of the block to do whatever he sees fit.”

In the preceding example, things are even a bit more subtle because the constructor hides essential logic, too. Refactoring the code to construct the object higher up and feed it in a local variable expression in the resource-acquisition part of the using statement would have very different semantics because you would be measuring a bigger code block's execution time.

What we would really need to make such scenarios of associating pieces of code with leaving and entering of a block is some kind of first-class treatment of blocks by the language. Action delegates turn out to be such a thing in disguise but still suffer from some syntactical noise:

```
ExecutionTimer.Measure(() => // using lambda expression syntax here
{
    // Code to be benchmarked goes here.
});
```

In the preceding example, the Measure method would start a timer first, then call the delegate that's passed in, and finally stop the timer and report the elapsed time at the end. Obviously, the destination logger could be fed in to the method as a parameter, too.

You could think of a way to allow this syntax to be made easier if (and this is all hand-waving amateur language design) some delegate appears as the last parameter on a method, so that “juxtaposition” of a method and a block means the same as feeding the block in to the method as a delegate:

```
ExecutionTimer.Measure(Console.Out) // The block becomes a second parameter.
{
    // Code to be benchmarked goes here.
}
```

Another concern is the fact that calling through the delegate has an additional cost that becomes truly hidden now to the user of the method. It's not clear first-class block treatment based on delegates (or any such feature at all) will hit the top of feature prioritization lists for the language in the foreseeable future.

## Locking on Objects

Lots of real-world software doesn't have a single thread of execution. To execute multiple tasks at a time, threads or abstractions thereof (such as tasks in .NET 4.0) are used. It's the responsibility of the underlying operating system scheduler or a runtime facility to let units of execution get a turn at making progress. Concepts such as context switches, thread pool management, and so on directly relate to this.

What's of more interest to us in this context is the problem of different threads accessing the same resource simultaneously. This gives rise to potential issues with regard to consistency of state. To avoid going too abstract here, let's make things very concrete by presenting a Counter class that maintains a single integer value and has two operations, Increment and Decrement:

```
class Counter
{
    private int _value;

    public void Increment()
    {
        _value++;
    }

    public void Decrement()
    {
        _value--;
    }

    public int Value { get { return _value; } }
}
```

Dissecting this code, we start by observing a field called _value that stores the counter's value. The property at the end of the class definition provides a read-only means to read out the value of the counter. The Increment and Decrement methods are trivial to understand and operate on the underlying field.

Based on this, you can certainly predict the behavior of the following code:

```
const int N = 10000000;

var count = new Counter();

for (int i = 0; i < N; i++) count.Increment();
for (int i = 0; i < N; i++) count.Decrement();

Console.WriteLine(count.Value);
```

If that doesn't produce zero, things have gone really wrong. But what if the incrementing and decrementing loops are operating in parallel? To illustrate this, we could use plain old threads, but let's go for .NET 4.0's new facilities and use the Parallel class to declare our parallel invocation desire:

```
const int N = 10000000;

var count = new Counter();

Parallel.Invoke(
    () => { for (int i = 0; i < N; i++) count.Increment(); },
    () => { for (int i = 0; i < N; i++) count.Decrement(); });

Console.WriteLine(count.Value);
```

Parallel.Invoke simply takes in a series of delegates that we want to execute in parallel. The most natural way (starting from C# 3.0) to pass in such delegates is by means of lambda expression syntax: () => { /*code*/ } stands for "no arguments, (), goes to, =>, /*code*/." The result? Faster code, but truly nondeterministic (see Figure 8.23).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_478_0.png)

FIGURE 8.23 Parallel execution nondeterminism.

## Under the Hood

You might, and actually should, wonder where this nondeterminism comes from. To understand this, we need to delve a little deeper. The crux of the problem lies in the fact Increment and Decrement are not atomic operations:

```
public void Increment()
{
    _value++;
}
```

The use of the post-increment expression (used as a statement here) really decomposes in three distinct operations that are carried out sequentially: First the value is read, then it gets incremented, and finally it gets assigned back to the field. Figure 8.24 shows the IL code corresponding to a post-increment expression.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_479_0.png)

## FIGURE 8.24 Non-atomic post-increment on a field.

It's worth the effort to try to understand this code fully. And how better than to show it with an evaluation stack transition diagram, as we've done before on various occasions (see Figure 8.25)? You'll get the hang of it soon, believe me.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_479_1.png)

## FIGURE 8.25 An "innocent" post-increment operation on a field.

The first two instructions are really setting up plumbing for what's coming afterward: ldarg.0 loads the very first argument on the method, which is a reference to the object instance itself in case of an instance method (the this reference). Instructions such as ldfld and stfld (load and store field) require the instance on the top of the stack. They'll pop the instance reference from the stack and subsequently load or store from or to the field in question. Because we need to carry out both operations in the same method body, the loaded this reference is duplicated by the dup instruction. This prevents having to use ldarg.0 twice, in favor of the dup instruction, which merely copies a few bytes holding the object reference to be duplicated on the evaluation stack. Where the trouble in multithreaded execution comes in is with the last four instructions. Assume any number of other threads are executing operations on the same field (for example, to decrement). Any number of interleaving schemes is possible because the
