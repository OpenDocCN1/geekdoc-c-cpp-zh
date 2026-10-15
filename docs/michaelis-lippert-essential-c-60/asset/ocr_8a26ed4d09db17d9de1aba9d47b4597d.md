```
```csharp
{
    Console.Write(state);
}
}
````
```

The output of Listing 18.2 is similar to Output 18.1—that is, an intermingling of periods and hyphens. If we had a lot of different jobs to perform asynchronously, this pooling technique would provide more efficient execution on single-processor and multiprocessor computers. The efficiency is achieved by reusing threads over and over, rather than reconstructing them for every asynchronous call. Unfortunately, thread pool use is not without its pitfalls: There are still performance and synchronization problems to consider when using a thread pool.

To make efficient use of processors, the thread pool assumes that all the work you schedule on the thread pool will finish in a timely manner so that the thread can be returned to the thread pool and reused by another task. The thread pool also assumes that all the work will be of a relatively short duration (that is, consuming milliseconds or seconds of processor time, not hours or days). By making this assumption, it can ensure that each processor is working full out on a task, and not inefficiently time-slicing multiple tasks, as described in the Beginner Topic on performance. The thread pool attempts to prevent excessive time slicing by ensuring that thread creation is “throttled” so that no one processor is “oversubscribed” with too many threads. Of course, that then means that consuming all threads within the pool can delay execution of queued-up work. If all the threads in the pool are consumed by long-running or I/O bound work, the queued-up work will be delayed.

Unlike Thread and Task, which are objects that you can manipulate directly, the thread pool does not provide a reference to the thread used to execute a given piece of work. This prevents the calling thread from synchronizing with, or controlling, the worker thread via the thread management functions described earlier in the chapter. In Listing 18.2 we use the “poor man’s synchronization” that we earlier discouraged; this would be a bad idea in production code because we do not actually know how long the work will take to complete.

In short, the thread pool does its job well, but that job does not include providing services to deal with long-running jobs or jobs that need to be synchronized with the main thread or with one another. What we really