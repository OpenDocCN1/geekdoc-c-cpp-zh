case of raw use of thread objects, we allocate as many threads as we can cope with, each of which will be blocked for the sleep duration. Literally thousands of threads can be sleeping at the same time. When using the thread pool, we're merely blocking the threads from the pool, which are limited in their number. In other words, not all work items get a chance to start sleeping at the same time.

# Performance Characteristics

This brings us to another important point: Use of the thread pool reduces the stress put on the operating system, but in doing so the degree of parallelism is reduced. In the example discussed here, quite a difference exists in behavior between use of the thread pool versus use of plain threads. When using the thread pool for our thousand parallel sleeping actions, they are not overlapped because only a limited number of work items is assigned to a physical thread at the same time. As a result, sleeping for 100 milliseconds in parallel will take much longer than 100 milliseconds in total. However, when using plain threads, the thousand sleeps can be going on at the same time, depending on the mood of the operating system scheduler.

Using the CountdownEvent synchronization primitive introduced in .NET 4, we can illustrate this behavior. We discuss such primitives later in the “Synchronization Primitives” section.

```
static void Main()
{
    const int N = 1000;
    var evt = new CountdownEvent(N);

    Console.WriteLine(\"Scheduling work...\");

    var sw = new Stopwatch();
    sw.Start();

    for (int i = 0; i < N; i++)
    {
        new Thread(_ =>
        {
            Thread.Sleep(100);
            evt.Signal();
        }).Start();
    }

    evt.Wait();
    sw.Stop();

    Console.WriteLine(sw.ElapsedMilliseconds);
}
```