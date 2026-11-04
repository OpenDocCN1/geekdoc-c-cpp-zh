However, ThreadLocal<T> can be used without any problem. As the use of lambda expressions (and hence closures) becomes more common, this is a great gift brought to us in .NET 4. In Chapter 30, you see uses of other .NET 4 constructs, such as Parallel.For, where the use of lambdas is very convenient. The introduction of those made the need for a ThreadLocal<T> construct more pressing. The following code shows how to make the counter variable thread local, just as we did before for the similar example with the ThreadStatic attribute. Recall this changes the behavior of the code, causing the reader to print its own private copy of the i, always set zero:

```
static void Main()
{
    var i = new ThreadLocal<int>();
    new Thread(() =>
    {
        while (true)
            i.Value++;
    }).Start();

    while (true)
    {
        Thread.Sleep(1000);
        Console.WriteLine(i.Value);
    }
}
```

# A WORD ON THREAD SAFETY

Thus far, we haven't mentioned thread safety (something we discuss more fully as we cover synchronization primitives later in this chapter). In particular, we avoided a discussion about thread safety in the context of both our counter examples by having only one writer thread. However, if multiple parties were to attempt to write to a shared (that is, nonthread-local) counter, we'd need to stand still and think about ensuring thread safety. In the last counter example using ThreadLocal<T>, a pretty clear multithreading issue exists if there would be multiple writers. Take a look at the following line of code:

i.Value++;

This seemingly innocent line of code does quite a lot of things, things that cause the increment operation not to be atomic. First, the Value property is read using a getter call. Then the local copy of the retrieved value is incremented. Finally, the incremented value is assigned by using the Value setter. This is far from thread safe if multiple writers are updating the counter. More on this in a moment.

# Thread-Local Storage

We've kept the "most native" way of establishing thread-local state for last because ThreadStatic and ThreadLocal<T> are the recommended ways to achieve this effect. Nonetheless, there is a third way to do thread-local storage.