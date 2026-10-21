

发送和接收消息是修改通道状态的操作，如果通道已满或为空则可能阻塞。对非线程实体（如 actors 和 coroutines）的同步以及消息的使用在第 27 章中简要讨论。

锁主要用于非干扰，但其他同步器更适合合作。第 23 章概述了最常见的同步器。现在，让我们用一个简单但有用的同步器——倒计时闩锁——来解决列表共享问题。它在 java.util.concurrent 库中实现为 CountDownLatch：

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

倒计时闩锁的状态是一个计数器。方法 countDown 如果计数器为正则递减该计数器，而方法 await 会阻塞调用线程，直到闩锁的计数器为 0。在此示例中，闩锁的初始状态为 2。主线程在查询列表大小之前等待闩锁状态变为 0。其他两个线程在各自完成时各递减状态 1，从而在它们都完成后将其降为 0。通过调用 latch.await，你避免了休眠或忙等待的缺点：主线程被高效地阻塞，在等待期间不使用 CPU 时间，并且在闩锁打开后立即被通知恢复执行，而不会有额外的休眠延迟。

## 22.3 Deadlocks

当程序使用同步器时，线程会被阻塞，直到同步器达到期望状态。同步存在危险——即线程会等待可能永远无法满足的条件。有些错误很容易发现。例如，线程在闩锁上调用 await，但代码中根本没有调用 countDown。其他错误可能更棘手，例如等待的倒计时次数比程序中可能发生的还要多。²

²尽管本节不以此为重点，但等待的倒计时次数过少也是同步错误，会导致线程过早使用数据。

死锁是线程最终等待永远无法建立的条件的一种相当常见的情况。在死锁中，多个线程在循环中相互等待。作为说明，请考虑以下线程安全盒的实现：

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

盒子初始为空，只能使用 set 方法填充一次。进一步调用 set 仅返回 false。闩锁在盒子被填充时打开。需要访问盒子内容的线程在此闩锁上被阻塞，直到调用 set。盒子设计为 set 和 get 可以由不同线程并发调用。对变量 contents 的所有访问都通过锁，即盒子本身进行。³

这一切听起来都很合理，但 get 的实现是错误的。它首先锁定盒子。然后，如果盒子仍为空，调用线程会在闩锁上被阻塞。然而，该线程仍然拥有盒子的锁，使得任何其他线程都无法运行 set 来填充盒子。这就是死锁情况，如图 22.1 所示。线程 T1 拥有盒子的锁并等待 T2 填充盒子。线程 T2 等待 T1 释放锁，以便 T2 设置盒子的内容。两个线程在永久地相互等待。

³这样的盒子通常在并发库中作为 future 或 promise 提供，无需重新实现。Futures 和 promises 在第 25 章中讨论。

### Figure 22.1 Possible deadlock of the incorrect box implementation in Listing 22.3.

这个问题很容易修复。get 方法中的线程在闩锁打开之前无需访问盒子的内容。因此，线程应先等待闩锁。（作为同步器，闩锁显然是线程安全的，可以在不加锁的情况下访问。）然后，在闩锁打开后，线程可以锁定盒子以访问其内容：

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

set 的实现保持不变。由于 countDown 是一个快速的非阻塞操作，你可以在持有锁时调用它。

对并发编程新手来说可能觉得奇怪，但你也可以这样实现 set 方法：

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

此变体在变量 contents 设置之前打开闩锁，此时盒子仍为空。乍一看似乎是错误，但由于加锁，此闩锁的打开是无害的：get 中的线程可能在此点通过闩锁，但它仍会被锁阻塞，直到盒子内容实际被设置。如果你想在锁定的部分之外访问闩锁，如在 get 中，你可以稍作不同地编写 set 方法：

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

在此变体中，你首先锁定盒子以检查它是否仍为空。如果是，则设置盒子内容，且 setter 为 true。然后你可以在打开闩锁之前释放锁。释放锁是无害的：它只是让另一个线程调用 set 并发现盒子已被填充。

使用同步器进行编程容易出错，死锁是常见问题。死锁可能非常严重——线程挂起，系统停滞——但它们并不是最糟糕的并发错误。死锁相比其他情况更容易调查的原因在于，参与等待循环的线程并未运行，你可以随意检查它们。

Java 虚拟机通常可以提供其线程的信息，通常以线程转储的形式。如何触发线程转储取决于 JVM——本书使用的 HotSpot JVM 对 SIGQUIT 信号做出反应——而输出的确切格式可能有所不同。

作为说明，你可以通过以下双线程程序使 Listing 22.3 中的错误盒子实现发生死锁：

```
val exec = Executors.newCachedThreadPool()
val box  = SafeBox[Int]()
exec.execute(() => box.set(0))
println(box.get)
```

一个辅助线程尝试用零设置盒子，而主线程调用 get。在某些运行中，此程序会正常终止。在其他情况下，它会卡住。线程转储揭示了以下信息（为清晰起见略有编辑）：

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

（转储中包含此处未显示的许多其他线程。这些是 JVM 内部的，用于即时编译、垃圾回收和其他操作。）

输出显示了两个感兴趣的线程并未运行。线程池的工作线程 pool-1-thread-1 在 set 方法开始处被阻塞在对象监视器上——JVM 对其内部锁的术语——它正尝试锁定对象 0x000000061f1f6a68，即 SafeBox 的一个实例。与此同时，主线程在 CountDownLatch 的 await 方法上被阻塞。（java.util.concurrent 中的所有同步器都是基于 AbstractQueuedSynchronizer 类实现的，并使用低级操作 park 来挂起线程。）你可以在最后一行看到，主线程拥有工作线程正在等待的同一个 SafeBox 实例的锁，即对象 0x000000061f1f6a68。死锁状态正是图 22.1 所示的状态（main 为 T1，pool-1-thread-1 为 T2）。

