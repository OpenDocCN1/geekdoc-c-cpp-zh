```
def memo[A, B](f: A => B): A => B =
  val store = TrieMap.empty[A, Future[B]]
  x =>
    val future = store.get(x) match
      case Some(future1) => future1
      case None =>
        val task = FutureTask(() => f(x))
        store.putIfAbsent(x, task) match
          case Some(future2) => future2
          case None =>
            task.run()
            task
    future.get()
```

# Listing 25.7: A thread-safe memoization function, using promises and futures.

Variable store now maps inputs of type A to futures of outputs of type Future[B]. When a thread needs the value f(x), you start by querying the map. If you find a future—future1—you use it, rather than recompute f(x). If x is not in the map, you create a promise/future as an instance of FutureTask named task. You then attempt to add it to the map. If in the meantime—right after the call to method get—some other thread already started a computation of f(x), method putIfAbsent does not add task to the map, but instead returns a future on this other computation—future2. In that case, use it (and forget about task). If method putIfAbsent succeeds in adding task to the store map, the current thread is now in charge of computing f(x). Other threads that need this value will find task in the map and possibly block on it until the computation of f is complete. You then call task.run, which triggers an evaluation of f(x). After this run completes, any subsequent lookup for x in the store map will find a completed future and will retrieve value f(x) from it without invoking f or blocking on method get.

Note that task is referred to as a promise/future. Indeed, it is both. It is completed as a promise by the thread that created it, and it is used as a future by any thread that needs the computed value. Note also that future1 handles the case of a computation started some time before this current call to the memoized function, while future2 handles the case of two threads that call the memoized function on the same input at the same time: Both threads fail to find a key in the store map, both attempt to add a promise to the map, and only one succeeds.