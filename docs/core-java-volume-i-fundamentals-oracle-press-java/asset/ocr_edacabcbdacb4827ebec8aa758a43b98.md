you can measure how much slower your application runs without the benefit of concurrency.

![](bbox=[0.128, 0.177, 0.181, 0.219])

# NOTE:

> > Java EE provides a `ManagedExecutorService` subclass that is suitable for concurrent tasks in a Java EE environment. Similarly, web frameworks such as Play provide executor services that are intended for tasks within the framework.

You can submit a `Runnable` or `Callable` to an `ExecutorService` with one of the following methods:

```
```java
Future<T> submit(Callable<T> task)
Future<?> submit(Runnable task)
Future<T> submit(Runnable task, T result)
```
```

The pool will run the submitted task at its earliest convenience. When you call `submit`, you get back a `Future` object that you can use to get the result or cancel the task.

The second submit method returns an odd-looking `Future<?>`. You can use such an object to call `isDone`, `cancel`, or `isCancelled`, but the get method simply returns null upon completion.

The third version of submit yields a `Future` whose get method returns the given result object upon completion.

When you are done with a thread pool, call `shutdown`. This method initiates the shutdown sequence for the pool. An executor that is shut down accepts no new tasks. When all tasks are finished, the threads in the pool die. Alternatively, you can call `shutdownNow`. The pool then cancels all tasks that have not yet begun.

Here, in summary, is what you do to use a thread pool: