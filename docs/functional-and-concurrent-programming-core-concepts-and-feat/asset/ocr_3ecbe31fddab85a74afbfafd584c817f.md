```
exec.execute(LetterPrinter('A'))
exec.execute(LetterPrinter('B'))
exec.execute(LetterPrinter('C'))

println("END")
```

Listing 21.1: Example concurrency from a thread pool; contrast with Lis. 17.1.

A thread pool is created with four worker threads. Letter-printing tasks are submitted to it using method execute. The output is similar to that of Listing 17.1, except for the names of the threads:

```
main at XX:XX:38.670: START
pool-1-thread-1 at XX:XX:38.694: A
pool-1-thread-2 at XX:XX:38.694: B
main at XX:XX:38.694: END
pool-1-thread-3 at XX:XX:38.694: C
```

A thread that calls execute with a task typically does not run the task but only submits it for execution. Method execute returns immediately, and the task is executed later, asynchronously. The task is actually run when one of the available workers grabs it and starts its execution. If all the workers are busy, the task might be queued or rejected, depending on the thread pool configuration.

Method execute does not return anything useful—it is a void method in Java. Using it leads to a “fire-and-forget” programming style: Submit a task and let in run. You can also use thread pools in more controlled ways by creating handles on running tasks, known as futures. Futures are discussed in Chapter 25.

In the preceding run, notice that the main thread terminates before all the tasks are finished. Earlier examples relied on the thread method join to force the main thread to wait for the other threads to be done before terminating. When using thread pools, you can achieve a similar behavior by waiting for all the worker threads to be done:

```
...
exec.shutdown()
exec.awaitTermination(5, MINUTES)

println("END")
```

Method shutdown is used to indicate to the pool that no new task will be submitted (it disables method execute). Once a pool is shut down, you can wait for its termination.