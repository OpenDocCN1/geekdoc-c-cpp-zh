```
for i <- 1 to N do
  exec.execute { () =>
    startEnd.await()
    5 times shared.add(i.toString)
    startEnd.await()
  }

startEnd.await()
val time1 = System.nanoTime()
startEnd.await()
val time2 = System.nanoTime()

exec.shutdown()

assert(shared.size == 5 * N)
assert((1 to N).forall(i => shared.getAll.count(_ == i.toString) == 5))
assert((time2 - time1) / 1E9 <= 0.01)
```

Listing 23.4: Replace two latches from Lis. 23.3 with a single barrier.

In this variant of the test, all the threads reach the barrier a first time, at which point the pool threads start adding to the list and the main thread starts keeping track of time. After all the add operations are completed, all the threads reach the barrier again, and the main thread records the finish time. Cyclic barriers are often used in the implementation of iterative algorithms.

# 23.3 Semaphores

A semaphore is a synchronizer that maintains a count of virtual permits as its state. Threads can acquire and release permits, and when no permit is available, the acquiring method becomes blocking.

Semaphores are very versatile, but rather low-level synchronizers. You can implement many other synchronizers using semaphores. (Concurrency libraries typically rely on more efficient, non-semaphore-based implementations.) For instance, you can write a simple, exclusive, non-reentrant lock using a semaphore:

```
class SimpleLock:
  private val semaphore = Semaphore(1)
  @volatile private var owner = Option.empty[Thread]

  def lock(): Unit =
    semaphore.acquire()
    owner = Some(Thread.currentThread)
```