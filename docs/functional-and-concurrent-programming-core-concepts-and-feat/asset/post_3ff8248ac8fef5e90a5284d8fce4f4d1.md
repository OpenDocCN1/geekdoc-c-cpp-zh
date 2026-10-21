
and receiving messages are operations that modify the state of a channel, and that can be blocking if a channel is full or empty. Synchronization of non-thread entities, such as actors and coroutines, and the use of messages are briefly discussed in Chapter 27.

Locks are primarily used for non-interference, but other synchronizers are better suited to cooperation. Chapter 23 gives an overview of the most common synchronizers. For now, let’s solve the list-sharing problem with a simple but useful synchronizer: the countdown latch. It is implemented in the java.util.concurrent library as a CountDownLatch:

```
val shared = SafeStringList()
val latch  = CountDownLatch(2)

def addStrings(n: Int, str: String): Unit =
    n times shared.add(str)
    latch.countDown()

exec.execute(() => addStrings(5, "T1"))
exec.execute(() => addStrings(5, "T2"))

latch.await()

assert(shared.size == 10)
```

### Listing 22.2: Waiting for task completion using a countdown latch synchronizer.

The state of a countdown latch is a counter. Method countDown decrements this counter if it is positive, and method await blocks any calling thread until the latch’s counter is 0. In this example, a latch is created with a state equal to 2. The main thread waits for the latch state to be 0 before querying the size of the list. The other two threads each decrement the state by 1 as they finish, thus bringing it to 0 when they are both done. By calling latch.await, you avoid the drawbacks of sleeping or busy-waiting: The main thread is blocked efficiently and does not use CPU time while waiting, and it is notified to resume execution as soon as the latch opens, without additional sleeping delay.

## 22.3 Deadlocks

When a program uses synchronizers, threads are blocked until the synchronizer reaches a desired state. Synchronization carries a danger—namely, it makes threads wait for a condition that may never be satisfied. Some errors are easy to catch. For instance, a thread calls await on a latch, but nowhere is countDown ever called in the code. Other mistakes can be trickier, such as waiting for more countdowns than can possibly happen in a program.²

²Though not the focus of this section, waiting for fewer countdowns is also a synchronization mistake, resulting in a thread that uses data too early.

Deadlocks are a rather common situation in which threads end up waiting for a condition that is never established. In a deadlock, multiple threads wait for each other in a cycle. As an illustration, consider the following implementation of a thread-safe box:

```
Scala
class SafeBox[A]:
  private var contents = Option.empty[A]
  private val filled   = CountDownLatch(1)

  // DON'T DO THIS!
  def get: A = synchronized {
    filled.await()
    contents.get
  }

  def set(value: A): Boolean = synchronized {
    if contents.nonEmpty then false
    else
      contents = Some(value)
      filled.countDown()
      true
  }
```

### Listing 22.3: Deadlock-prone implementation of a box; fixed in Listing 22.4.

A box is created empty, and can be filled only once, using method set. Further attempts to invoke set simply return false. A latch is open when the box is filled. Threads that need access to the contents of a box are blocked on this latch until set is called. A box is designed so that set and get can be called by different threads concurrently. All accesses to variable contents go through a lock, the box itself.³

This all sounds very reasonable, but the implementation of get is incorrect. It starts by locking the box. Then, if the box is still empty, the calling thread is blocked on the latch. This thread, however, still owns the lock on the box, making it impossible for any other thread to run set to fill the box. This is a deadlock situation, as shown in Figure 22.1. Thread T1 owns the lock on the box and waits for T2 to fill the box. Thread T2 waits for T1 to release the lock so T2 can set the contents of the box. The two threads are waiting for each other, permanently.

³Such a box is typically made available in concurrency libraries as a future or a promise and does not need to be reimplemented. Futures and promises are discussed in Chapter 25.

### Figure 22.1 Possible deadlock of the incorrect box implementation in Listing 22.3.

This problem is easy to fix. There is no need for a thread inside method get to access the contents of the box until the latch is open. Therefore, the thread should wait on the latch first. (As a synchronizer, a latch is obviously thread-safe and can be accessed without locking.) Then, after the latch is open, the thread can lock the box to access its contents:

```
Scala
class SafeBox[A]:
  private var contents = Option.empty[A]
  private val filled   = CountDownLatch(1)

  def get: A =
    filled.await()
    synchronized(contents.get)

  def set(value: A): Boolean = synchronized {
    if contents.nonEmpty then false
    else
      contents = Some(value)
      filled.countDown()
      true
  }
```

### Listing 22.4: Thread-safe box with a latch; fixed from Listing 22.3; see also Listing 27.2.

The implementation of set is left unchanged. Since countDown is a fast, non-blocking operation, you can call it while holding the lock.

Developers who are new to concurrent programming might think it strange, but you can also implement method set in this way:

## Chapter 22 Synchronization

```
```scala
def set(value: A): Boolean = synchronized {
 if contents.nonEmpty then false
 else
  filled.countDown()
  contents = Some(value)
 true
}
```
```

This variant opens the latch before variable contents is set, while the box is still empty. It might seem like a mistake, but thanks to locking, this latch opening is harmless: A thread inside get might go through the latch at this point, but it will still be blocked by the lock until the box contents are actually set. If you want to access the latch outside the locked section, as in get, you can write the set method slightly differently:

```
```scala
def set(value: A): Boolean = {
  val setter = synchronized {
    if contents.nonEmpty then false
    else
      contents = Some(value)
    true
  }
  if setter then filled.countDown()
  setter
}
```
```

In this variant, you first lock the box to check that it is still empty. If so, the box contents are set, and setter is true. You can then release the lock before opening the latch. Releasing the lock is harmless: It simply lets another thread call set and find the box already filled.

Programming with synchronizers is error-prone, and deadlocks are a common problem. Deadlocks can be devastating—threads hang and the system halts—but they are not the worst kind of concurrency bug. What makes deadlocks somewhat easier to investigate compared to other situations is the fact that the threads involved in a waiting cycle are not running, and you can examine them at your leisure.

A Java virtual machine (JVM) can usually provide information on its threads, typically in the form of a thread dump. How you trigger a thread dump depends on the JVM—the HotSpot JVM used in this book reacts to a SIGQUIT signal—and the exact format of the output may vary.

As an illustration, you can cause the incorrect box implementation from Listing 22.3 to deadlock by using the following two-thread program:

```
val exec = Executors.newCachedThreadPool()
val box  = SafeBox[Int]()
exec.execute(() => box.set(0))
println(box.get)
```

A secondary thread attempts to set a box with zero while the main thread invokes get. On some runs, this program terminates properly. On others, it gets stuck. A thread dump reveals the following information (slightly edited for clarity):

```
"pool-1-thread-1" #15 prio=5 os_prio=31 cpu=3.79ms elapsed=121.29s
  java.lang.Thread.State: BLOCKED (on object monitor)
    at chap22.Box1$SafeBox.set
  - waiting to lock <0x000000061f1f6a68> (a chap22.Box1$SafeBox)

"main" #1 prio=5 os_prio=31 cpu=223.28ms elapsed=121.51s
  java.lang.Thread.State: WAITING (parking)
    at jdk.internal.misc.Unsafe.park
  - parking to wait for <0x000000061f99e8>
    (a java.util.concurrent.CountDownLatch$Sync)
  at java.util.concurrent.locks.LockSupport.park
  at java.util.concurrent.locks.AbstractQueuedSynchronizer.acquire
  at java.util.concurrent.CountDownLatch.await
  at chap22.Box1$SafeBox.get
    - locked <0x000000061f1f6a68> (a chap22.Box1$SafeBox)
```

(The dump includes many more threads not displayed here. These are internal to the JVM and are used for just-in-time compilation, garbage collection, and other operations.)

The output shows that the two threads of interest are not running. The worker thread from the pool, pool-1-thread-1, is blocked on an object monitor—JVM's terminology for its intrinsic locks—at the beginning of method set. It is trying to lock object 0x000000061f1f6a68, an instance of SafeBox. Meanwhile, the main thread is blocked on method await from CountDownLatch. (All the synchronizers in java.util.concurrent are implemented in terms of an AbstractQueuedSynchronizer class and use a low-level operation park to suspend threads.) You can see on the last line that the main thread owns the lock on the same SafeBox instance that the worker thread is waiting for, object 0x000000061f1f6a68. The deadlock state is exactly that shown in Figure 22.1 (main is T1 and pool-1-thread-1 is T2).
