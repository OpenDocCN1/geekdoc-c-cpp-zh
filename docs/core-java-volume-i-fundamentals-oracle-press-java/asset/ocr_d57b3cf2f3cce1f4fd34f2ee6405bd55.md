The type parameter is the type of the returned value. For example, a `Callable<Integer>` represents an asynchronous computation that eventually returns an `Integer` object.

A `Future` holds the *result* of an asynchronous computation. You start a computation, give someone the `Future` object, and forget about it. The owner of the `Future` object can obtain the result when it is ready.

The `Future<V>` interface has the following methods:

```
```java
V get()
V get(long timeout, TimeUnit unit)
void cancel(boolean mayInterruptIfRunning)
boolean isCancelled()
boolean isDone()
```
```

A call to the first `get` method blocks until the computation is finished. The second `get` method also blocks, but it throws a `TimeoutException` if the call timed out before the computation finished. If the thread running the computation is interrupted, both methods throw an `InterruptedException`. If the computation has already finished, `get` returns immediately.

The `isDone` method returns `false` if the computation is still in progress, `true` if it is finished.

You can cancel the computation with the `cancel` method. If the computation has not yet started, it is canceled and will never start. If the computation is currently in progress, it is interrupted if the `mayInterrupt` parameter is `true`.

![](bbox=[0.137, 0.726, 0.183, 0.759])

> > **CAUTION:**
> >
> > Canceling a task involves two steps. The underlying thread must be located and interrupted. And the task implementation (in the `call` method) must sense the interruption and abandon its work. If a `Future` object does not know on which thread the task is executed, or if the task does not monitor