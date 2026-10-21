# 24.6 Bounded Thread Pool

In Listing 24.3, you can place a bound on the number of tasks that run concurrently, which can be beneficial in some circumstances. This feature is lost in Listing 24.4 because you have no control over the number of worker threads in the shared pool.

A best-of-both-worlds implementation would rely on a shared thread pool and implement an additional constraint on how many tasks may run concurrently inside the pool. You can achieve this with a semaphore, created with as many permits as the desired level of parallelism:

```
class Runner[A](exec: Executor, bound: Int)(comp: A => Unit):
    def run(inputs: Seq[A]): Unit =
        val canStart = Semaphore(bound)

        for input <- inputs do
            val task: Runnable = () =>
                try comp(input)
                finally canStart.release()

            canStart.acquire()
            exec.execute(task)
        end for

        canStart.acquire(bound)
```

Listing 24.5: Parallel execution: shared thread pool with a bound.

The thread that invokes method run acquires a permit from the semaphore before submitting each task for execution. When a task finishes, it releases the permit so another task can be submitted. This guarantees that the maximum number of tasks running at any point in time is bounded by the initial number of permits in the semaphore. After all tasks have been submitted, canStart.acquire(bound) is used to wait for task completion: Once all the permits are back inside the semaphore, you know that all the tasks are finished. No additional countdown latch is needed.

A runner created as Runner(exec, 2)(sleepTask) where exec is an unlimited thread pool may produce the following output:

```
main at XX:XX:04.870: START
pool-1-thread-1 at XX:XX:04.901: begin 2
pool-1-thread-2 at XX:XX:04.901: begin 1
pool-1-thread-2 at XX:XX:05.901: end 1
pool-1-thread-3 at XX:XX:05.902: begin 3
pool-1-thread-1 at XX:XX:06.901: end 2
pool-1-thread-3 at XX:XX:08.902: end 3
main at XX:XX:08.903: END
```