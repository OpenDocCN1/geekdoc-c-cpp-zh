the interrupted status of the thread on which it executes, cancellation will have no effect.

One way to execute a Callable is to use a FutureTask, which implements both the Future and Runnable interfaces, so that you can construct a thread for running it:

```
```java
Callable<Integer> task = . . .;
var futureTask = new FutureTask<Integer>(task);
var t = new Thread(futureTask); // it's a Runnable t.start();
. . .
Integer result = futureTask.get(); // it's a Future
```
```

More commonly, you will pass a callable to an executor. That is the topic of the next section.

**java.util.concurrent.Callable<V> 5**

+   - `V call()`
+     runs a task that yields a result.

**java.util.concurrent.Future<V> 5**

+   - `V get()`
+   - `V get(long time, TimeUnit unit)`
+     gets the result, blocking until it is available or the given time has elapsed. The second method throws a `TimeoutException` if it was unsuccessful.
+   - `boolean cancel(boolean mayInterrupt)`