
声明静态方法为 synchronized 也是合法的。如果调用这样的方法，它会获取关联类对象的内在锁。例如，如果 Bank 类有一个静态同步方法，那么调用它时会锁定 Bank.class 对象的锁。因此，其他线程无法调用此方法或同一类的任何其他同步静态方法。

内在锁和条件有一些限制。其中包括：

- 你无法中断正在尝试获取锁的线程。
- 尝试获取锁时无法指定超时。
- 每个锁只有一个条件可能效率低下。

在代码中应该使用什么——Lock 和 Condition 对象还是同步方法？以下是我们的建议：

- 最好既不使用 Lock/Condition 也不使用 synchronized 关键字。在许多情况下，你可以使用 java.util.concurrent 包中的某种机制，它会为你完成所有锁定。例如，在第 781 页的 12.5.1 节“阻塞队列”中，你将看到如何使用阻塞队列来同步处理共同任务的线程。你还应该探索并行流——参见第二卷第一章。
- 如果 synchronized 关键字适合你的情况，务必使用它。你会编写更少的代码，并且出错的空间更小。清单 12.5 展示了使用同步方法实现的银行示例。
- 如果你确实需要这些构造提供的额外能力，请使用 Lock/Condition。

## 清单 12.5 synch2/Bank.java

```java
package synch2;

import java.util.*;

/**
 * A bank with a number of bank accounts that uses synchronization primitives.
 */
public class Bank
{
   private final double[] accounts;

   /**
    * Constructs the bank.
    * @param n the number of accounts
    * @param initialBalance the initial balance for each account
    */
public Bank(int n, double initialBalance)
{
    accounts = new double[n];
    Arrays.fill(accounts, initialBalance);
}

/**
 * Transfers money from one account to another.
 * @param from the account to transfer from
 * @param to the account to transfer to
 * @param amount the amount to transfer
 */
public synchronized void transfer(int from, int to, double amount)
    throws InterruptedException
{
    while (accounts[from] < amount)
        wait();
    System.out.print(Thread.currentThread());
    accounts[from] -= amount;
    System.out.printf(" %10.2f from %d to %d", amount, from, to);
    accounts[to] += amount;
    System.out.printf(" Total Balance: %10.2f%n", getTotalBalance());
    notifyAll();
}

/**
 * Gets the sum of all account balances.
 * @return the total balance
 */
public synchronized double getTotalBalance()
{
    double sum = 0;

    for (double a : accounts)
        sum += a;

    return sum;
}

/**
 * Gets the number of accounts in the bank.
 * @return the number of accounts
 */
public int size()
{
    return accounts.length;
}
}
```

### `java.lang.Object` 1.0

- `void notifyAll()`  
  解除在此对象上调用 wait 的线程的阻塞。此方法只能在同步方法或同步块内调用。如果当前线程不是对象锁的所有者，则该方法抛出 `IllegalMonitorStateException`。

- `void notify()`  
  从此对象上调用 wait 的线程中随机选择一个线程解除阻塞。此方法只能在同步方法或同步块内调用。如果当前线程不是对象锁的所有者，则该方法抛出 `IllegalMonitorStateException`。

- `void wait()`  
  使线程等待，直到被通知。此方法只能在同步方法或同步块内调用。如果当前线程不是对象锁的所有者，则抛出 `IllegalMonitorStateException`。

- `void wait(long millis)`
- `void wait(long millis, int nanos)`  
  使线程等待，直到被通知或经过指定时间。这些方法只能在同步方法或同步块内调用。如果当前线程不是对象锁的所有者，则它们抛出 `IllegalMonitorStateException`。纳秒数不得超过 1,000,000。

## 12.4.6 同步块

正如我们刚刚讨论的，每个 Java 对象都有一个锁。线程可以通过调用同步方法来获取锁。还有第二种获取锁的机制：进入同步块。当线程进入以下形式的块时

```java
synchronized (obj) // this is the syntax for a synchronized block
{
    critical section
}
```

那么它获取 obj 的锁。

你有时会发现“临时”锁，例如

```java
public class Bank
{
    private double[] accounts;
    private Object lock = new Object();
}
```

```java
public void transfer(int from, int to, int amount)
{
   synchronized (lock) // an ad-hoc lock
   {
      accounts[from] -= amount;
      accounts[to] += amount;
   }
   System.out.println(. . .);
}
```

这里，创建锁对象只是为了使用每个 Java 对象都拥有的锁。

有时，程序员使用对象的锁来实现额外的原子操作——这种做法称为*客户端锁定*。例如，考虑 `Vector` 类，它是一个方法已同步的列表。现在假设我们将银行余额存储在一个 `Vector<Double>` 中。以下是 transfer 方法的一个简单实现：

```java
public void transfer(Vector<Double> accounts, int from, int to, int amount) // ERROR
{
   accounts.set(from, accounts.get(from) - amount);
   accounts.set(to, accounts.get(to) + amount);
   System.out.println(. . .);
}
```

`Vector` 类的 get 和 set 方法是同步的，但这并不能帮助我们。线程完全可能在 transfer 方法中完成第一次 get 调用后被抢占。另一个线程随后可能将不同的值存储到同一位置。但是，我们可以劫持锁：

```java
public void transfer(Vector<Double> accounts, int from, int to, int amount)
{
   synchronized (accounts)
   {
      accounts.set(from, accounts.get(from) - amount);
      accounts.set(to, accounts.get(to) + amount);
   }
   System.out.println(. . .);
}
```

这种方法可行，但它完全依赖于 `Vector` 类对其所有修改器方法使用内在锁这一事实。然而，这真的是事实吗？`Vector` 类的文档没有做出这样的承诺。你必须仔细研究源代码，并希望未来的版本不会引入未同步的修改器。如你所见，客户端锁定非常脆弱，通常不建议使用。

> **注意：** Java 虚拟机内置支持同步方法。但是，同步块会被编译成一长串字节码来管理内在锁。

## 12.4.7 监视器概念

锁和条件是线程同步的强大工具，但它们不是很面向对象。多年来，研究人员一直在寻找使多线程安全而不迫使程序员考虑显式锁的方法。最成功的解决方案之一是 20 世纪 70 年代由 Per Brinch Hansen 和 Tony Hoare 开创的监视器概念。用 Java 的术语来说，监视器具有以下属性：

- 监视器是一个只有私有字段的类。
- 该类的每个对象都有一个关联的锁。
- 所有方法都被该锁锁定。换句话说，如果客户端调用 `obj.method()`，那么在方法调用开始时自动获取 `obj` 的锁，并在方法返回时释放。由于所有字段都是私有的，这种安排确保当一个线程操作字段时，没有其他线程可以访问这些字段。
- 锁可以具有任意数量的关联条件。

早期版本的监视器有一个条件，语法相当优雅。你可以直接调用 await accounts[from] >= amount，而不使用显式的条件变量。然而，研究表明，不加区分地重新测试条件可能效率低下。这个问题通过显式条件变量来解决，每个条件变量管理一组单独的线程。

Java 设计者松散地改编了监视器概念。Java 中的每个对象都有一个内在锁和一个内在条件。如果方法使用 `synchronized` 关键字声明，则它就像一个监视器方法。通过调用 `wait/notifyAll/notify` 来访问条件变量。

然而，Java 对象在三个重要方面与监视器不同，这损害了线程安全：

- 字段不要求是私有的。
- 方法不要求是同步的。
- 内在锁对客户端可用。

