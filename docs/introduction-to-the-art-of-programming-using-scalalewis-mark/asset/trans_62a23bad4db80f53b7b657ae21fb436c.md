

is being called on though as that will be the object the monitor is locked on and using the wrong one can lead to incorrect results.

作为第一个示例，让我们看看如何修复银行账户类使其同步化，这样我们就不必担心存款和取款同时发生的情况。

```scala
/**
 * A class that represents a bank account. The balance is stored as an Int
 * representing a number of cents.
 */
class BankAccount(private var bal:Int = 0) {
  def balance:Int = bal
  def deposit(amount:Int) = synchronized {
    assert(amount>=0)
    val oldBalance = balance
    val newBalance = oldBalance+amount
    bal = newBalance
  }
  def withdraw(amount:Int) = synchronized {
    assert(amount>=0 && amount<=bal)
    val oldBalance = balance
    val newBalance = oldBalance-amount
    bal = newBalance
  }
}
```

如你所见，我们所做的只是对 deposit 和 withdraw 的整个方法加上 synchronize 调用。因为我们不再使用返回 Unit 的方法的简写语法，所以添加了一个等号。这就是该示例所需的一切。

你可能会想，为什么同步有效，而我们之前使用 if 检查变量然后自动设置它的代码却无效。其原因在于对监视器上锁的检查和设置是一个原子操作。什么叫做操作是原子的？单词 atom 的希腊词根意思是不可分割。这个名字之所以被赋予粒子，是因为当时认为它们是物质最小的片段且无法分割。虽然在自然界中原子并不真的如此，但对于计算机上的原子操作来说是成立的。在这种另类意义上，当我们说它不能被分割时，我们的意思是它不能被中断。一旦原子操作开始，就不会有其他东西在它完成之前接管。if 后跟 set 的问题在于它不是原子的，并且在该线程读取值、查看它并设置它之间，另一个线程有可能更改变量的值。

那么对于在多个线程中增加计数器的示例呢？根据我们所见，你的第一次尝试可能看起来像这样。

```scala
var cnt = 0
val threads = Array.fill(100) {
  new Thread {
    override def run {
      for (i <- 1 to 1000000) synchronized { cnt += 1 }
    }
  }
}
```

使用这种结构，同步可以在 `ThreadCounting` 对象上完成。如果 `ThreadCounting` 是一个类或一个 trait，你可以执行 `ThreadCounting.this.synchronized`。

此时你可能会想，为什么不将所有内容都同步以避免竞争条件。原因是同步在执行速度上是有成本的。对监视器上锁的检查和设置需要实际时间。此外，它还阻止多个线程同时运行。如果你真的同步所有内容，你很可能会使程序运行非常缓慢，大部分时间只有一个线程处于活动状态，并且有很大的死锁风险。相反，你必须小心如何同步事物。

如果你尝试了本节中的不同程序，你可能会发现通过同步得到正确答案的程序运行得更慢。在为本书测试它们时，发现它们完成所需的时间大约是无同步时的 10 倍。你如何绕过这个问题？尽量不要共享可变状态。在本例中，最好为每个线程设置一个变量进行递增，最后再将所有结果加在一起。以下是这样做的解决方案。

```scala
class CountThread extends Thread {
  var cnt = 0
  override def run {
    for (i <- 1 to 1000000) cnt += 1
  }
}
val threads = Array.fill(100)(new CountThread)
threads.foreach(_.start)
threads.foreach(_.join)
var cnt = threads.view.map(_.cnt).sum
println(cnt)
```

请注意，在这个版本中我们必须定义一个 `Thread` 的子类型的新类。这使我们能够访问 `cnt` 字段。`java.lang.Thread` 类没有名为 `cnt` 的成员，所以我们需要一个具有该成员的新类型。此代码运行速度与之前没有同步的版本几乎相同，并且得到正确答案。

关于此代码的最后一件事是它使用了 `view`。这是一个在第 197 页作为高级主题介绍的话题。这里使用它是因为我们对计时结果感兴趣，并且不让 `map` 创建一个完全新的集合会稍微更高效。

### 21.2.3 Wait/Notify

`synchronized` 方法可以帮助你防止竞争条件，但通常不足以协调不同线程的行为。在基本的线程库中，这是通过 `wait`、`notify`[^5] 和 `notifyAll` 来完成的。更高级的工具已在我们下面将讨论的库中引入，但了解事物在最低层级如何工作是有益的，因此我们将简要讨论这些。

与 `synchronized` 方法一样，`wait`、`notify` 和 `notifyAll` 也是 `AnyRef` 中的方法，可以在该类型的任何对象上调用。`wait` 方法正如其名所示，它会导致当前线程停止执行并等待某事。那件事就是由另一个线程调用 `notify` 或 `notifyAll` 来唤醒它。

所有这些调用都需要当前线程持有对调用该方法对象的监视器的锁。此外，**notify** 和 **notifyAll** 只会唤醒在同一对象上被设置为等待的线程。你通常会在 synchronized 块中看到这些调用。`wait` 的调用会释放该监视器的锁。它将在线程重新唤醒时重新获取。

为了说明它如何工作，请考虑以下示例，其中有多个不同的线程使用 wait 按顺序计数，并且在任何给定时间最多只有一个线程处于活动状态。

```scala
object WaitCounting {
  def main(args: Array[String]) {
    val numThreads = 3
    val threads = Array.tabulate(numThreads)(i => new Thread {
      override def run {
        println("Start " + i)
        for (j <- 1 to 5) {
          WaitCounting.synchronized {
            WaitCounting.wait()
            println(i + " : " + j)
            WaitCounting.notify()
          }
        }
      }
    })
    threads.foreach(_.start)
    Thread.sleep(1000)
    println("First notify.")
    synchronized { notify() }
  }
}
```

每个线程都有一个 **for** 循环，计数到 5。在循环中同步代码所在的对象的代码并调用 **wait**。一旦线程被另一个线程唤醒，它将打印出线程号和循环中的数字，然后通知其他线程。之后它会立即再次进入睡眠，因为下一次循环会导致再次调用 wait。线程构建后，它们被启动，主线程休眠一秒，然后调用 **notify**。

对 **sleep** 的调用确保所有线程都有时间启动并调用 **wait**，然后再进行第一次 **notify** 调用。如果你省略它，第一次 notify 调用可能发生在线程启动之前。更严格的方法是使用一个计数器，在每个线程启动时递增。

每次对 **notify** 的调用都会唤醒一个正在等待 WaitCounting 对象的单个线程，因此这就像多米诺骨牌一样，打印会按 notify 唤醒的顺序在线程中运行。无法预测哪个线程会被唤醒是一个问题。真正的问题在于，在以后的开发中，可能会有其他线程开始等待同一个对象，而该线程可能不遵循打印然后调用 notify 的规则。这可能导致死锁。在本例中，如果你在调用 **notify** 之后在底部简单地添加以下行，你就可以创建死锁。

```scala
synchronized { wait() }
```

这会造成问题，因为现在当其他线程之一调用 **notify** 时，它唤醒的是主线程而不是其中一个打印线程。主线程不会

[^5]: 通常不鼓励使用 `notify`，因为你无法控制它会唤醒哪个线程。这很容易导致死锁。

