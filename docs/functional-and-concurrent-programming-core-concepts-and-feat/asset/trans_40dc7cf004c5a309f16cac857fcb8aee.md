

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

## 23.3 Semaphores

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

acquired by some threads may be released by other threads (semaphore permits are virtual), hence my choice of the word “created” instead of “released.” This implementation of a bounded queue suffers from the fact that operations on a non-empty and non-full queue—which are non-blocking—still need to go through two semaphore operations. This inefficiency is avoided in a better bounded queue implementation in Listing 23.8.

## 23.4 Conditions

Conditions are another low-level synchronizer that you can use to implement other synchronizers. Conceptually, a condition maintains a set of waiting threads, which are blocked. A condition defines methods for the thread to notify another thread that it can continue, or to add itself to the set. Notification has no effect if no thread is currently waiting.

Conditions have been available on the JVM since the beginning: Every Java object is a condition, in the same way that every Java object is a lock. Conditions and locks work hand-in-hand: You typically need to lock a shared state to decide whether waiting is needed. If a thread needs to wait, it must release this lock before waiting so that other threads can lock and modify the shared state. Note that an object needs to maintain two separate sets of waiting threads: those waiting to acquire the lock and those waiting to be notified from the condition.

Before the advent of java.util.concurrent in Java 5, you had to write all your synchronizers in terms of these basic Java conditions. As an illustration, the blocking queue from Section 23.3 could be reimplemented using a condition:

```
```scala
class BoundedQueue[A](capacity: Int):
  private val queue = mutable.Queue.empty[A]

def take(): A synchronized {
    while (queue.isEmpty) do wait()
    notifyAll()
    queue.dequeue()
  }

def put(element: A): Unit = synchronized {
    while (queue.length == capacity) do wait()
    notifyAll()
    queue.enqueue(element)
  }
```
```

> Listing 23.7: Bounded queue with a single condition; see also Lis. 23.8.

The bounded queue itself is used as the lock and condition—all calls to methods synchronized, wait, and notifyAll are made on this. In take, you make the calling

thread wait on the condition if the queue is empty; in put, you make it wait if the queue is full. After any successful element insertion or removal, you notify the entire set of waiting threads that the state of the queue has changed.

This code has a few peculiarities that deserve to be discussed in detail:

- The blocking method wait is called within the synchronized block of code, even though I stated earlier that you should never invoke a blocking method while holding a lock because it results in deadlocks. First, let’s understand why this is necessary. The issue is a non-atomic check-then-act: In take, for instance, a thread could see that a queue is empty and release the lock in anticipation to calling wait. But before this thread reaches wait and is actually added to the set of waiting threads, another thread invokes put and calls notifyAll. By the time the taking thread reaches the waiting set, notifyAll has already happened, and the thread gets stuck, even though the queue is now non-empty. (Listing 23.6 does not suffer from this problem because a semaphore permit can always be safely created, whether a thread is waiting for it or not.) Calling method wait within the synchronized block avoids this problem, but what about the deadlock issue? Things work correctly only because wait internally releases the lock after a thread is added to the waiting set (and it is invalid for a thread to invoke wait on an object that is not locked by the thread). So, the first rule to remember is simple: Code should always use X.wait inside an X.synchronized block on the same object X.
- In both take and put, the check that a queue is not empty or not full is performed inside a loop. This is essential, and it is a consequence of the locking issues discussed earlier. When a thread calls wait, it owns a lock that is automatically released. This lock needs to be reacquired after the thread is notified for the thread to continue executing the synchronized block. Several threads—notified from the set of waiting threads, or initiating new calls to method take or put—compete for this lock, and any thread that ends up acquiring the lock can modify the state of the queue. A taking thread, for instance, could be notified that a queue is non-empty, but the queue could become empty again by the time the thread manages to reacquire the lock. So, once the lock has been reacquired, a thread needs to test the state of the queue again and go back to waiting again if the state is not suitable. The second rule is as simple as the first: Always invoke wait in a loop that reevaluates the condition you are waiting for.
- All the waiting threads are notified—using notifyAll—after a queue element is added or removed. This is wasteful: If you are adding one element in an empty queue, why notify ten threads to come and get it? However, method notify, which notifies only one of the waiting threads, cannot be used in this example. When multiple threads are waiting, method notify does not specify which thread is

```
def put(element: A): Unit =
    lock.lock()
    try
        while queue.length == capacity do canPut.await()
        canTake.signal()
        queue.enqueue(element)
    finally lock.unlock()
```

Listing 23.8: Bounded queue based on two conditions.

Methods await, signal, and signalAll correspond to methods wait, notify, and notifyAll on intrinsic conditions. This implementation has better performance than Listing 23.7 because inserting or removing an element triggers the notification of at most one thread—using signal, not signalAll. Standard blocking queues from java.util.concurrent rely on a similar strategy—an instance of ReentrantLock and two conditions.

## Aside on Verification by Model Checking

Footnote 1 mentioned that using notify instead of notifyAll in Listing 23.7 could lead to a deadlock situation. This deadlock is not as systematic as it was in Listing 22.3—most runs proceed correctly to completion—and the steps it takes to make it happen are not entirely obvious. As an illustration of techniques that can be used to complement runtime testing, this aside applies model checking to the incorrect queue implementation—notifyAll replaced with notify—to discover the deadlock.

The formalism used here is TLA⁺, the Temporal Logic of Actions. It is a mathematical notation based on set theory, with some temporal logic elements added. A model of method put from a blocking queue can be written in TLA⁺ as follows:

Put(t, m) ≜ IF Len(queue) < Capacity
    THEN queue' = Append(queue, m) ∧ Notify
    ELSE Wait(t) ∧ UNCHANGED queue

The details are not essential, but it can be seen that the model uses the same strategy as in Listing 23.7, except that notify is used instead of notifyAll.ᵃ In particular, if the queue is not full, an element is added and method notify is called; otherwise, the thread calls method wait and the queue is unchanged. Method take is modeled similarly.

ᵃThe models uses IF instead of while because of an implicit loop in the TLA⁺ model, but the condition is being rechecked as in Listing 23.7.

