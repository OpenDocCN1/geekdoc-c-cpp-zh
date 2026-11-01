```
```csharp
using System;
using System.Threading;

namespace Wrox.ProCSharp.Threading
{
    class Program
    {
        static void Main()
        {
            int nWorkerThreads;
            int nCompletionPortThreads;
            ThreadPool.GetMaxThreads(out nWorkerThreads, out nCompletionPortThreads);
            Console.WriteLine('Max worker threads: {0}, ' +
                'I/O completion threads: {1}',
                nWorkerThreads, nCompletionPortThreads);

            for (int i = 0; i < 5; i++)
            {
                ThreadPool.QueueUserWorkItem(JobForAThread);
            }
            Thread.Sleep(3000);
        }

        static void JobForAThread(object state)
        {
            for (int i = 0; i < 3; i++)
            {
                Console.WriteLine('loop {0}, running inside pooled thread {1}',
                    i, Thread.CurrentThread.ManagedThreadId);
                Thread.Sleep(50);
            }
        }
    }
}
```
```

code snippet ThreadPoolSamples/Program.cs

When you run the application, you can see that 50 worker threads are possible with the current settings. The five jobs are processed by just two pooled threads. Your experience may be different, and you can also change the sleep time with the number of jobs to process to get very different results.

```
```
Max worker threads: 1023, I/O completion threads: 1000
loop 0, running inside pooled thread 4
loop 0, running inside pooled thread 3
loop 1, running inside pooled thread 4
loop 1, running inside pooled thread 3
loop 2, running inside pooled thread 4
loop 2, running inside pooled thread 3
loop 0, running inside pooled thread 4
loop 0, running inside pooled thread 3
loop 1, running inside pooled thread 4
loop 1, running inside pooled thread 3
loop 2, running inside pooled thread 4
loop 2, running inside pooled thread 3
loop 0, running inside pooled thread 4
loop 1, running inside pooled thread 4
loop 1, running inside pooled thread 3
loop 2, running inside pooled thread 4
loop 2, running inside pooled thread 3
loop 0, running inside pooled thread 4
loop 1, running inside pooled thread 4
loop 1, running inside pooled thread 3
loop 2, running inside pooled thread 4
loop 2, running inside pooled thread 3
```
```

Thread pools are very easy to use. However, there are some restrictions:

+   - All thread pool threads are background threads. If all foreground threads of a process are finished, all background threads are stopped. You cannot change a pooled thread to a foreground thread.
+   - You cannot set the priority or name of a pooled thread.