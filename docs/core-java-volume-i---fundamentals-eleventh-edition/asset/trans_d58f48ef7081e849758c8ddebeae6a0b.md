
如果 `transfer` 方法发现没有足够的资金可用，它会调用

```java
    sufficientFunds.await();
```

当前线程现在被停用并放弃锁。这会让另一个线程进入，我们希望该线程能增加账户余额。

等待获取锁的线程与已调用 `await` 的线程之间存在本质区别。一旦线程调用 `await` 方法，它就会进入该条件的 *等待集*。当锁可用时，该线程*不会*变为可运行状态。相反，它会保持停用，直到另一个线程在同一条件上调用 `signalAll` 方法。

当另一个线程完成转账后，它应该调用

```java
    sufficientFunds.signalAll();
```

这个调用会重新激活所有等待该条件的线程。当这些线程从等待集中移除后，它们再次变为可运行，调度器最终会再次激活它们。届时，它们将尝试重新进入对象。一旦锁可用，其中一个线程将获取锁，并*从上次中断的地方继续*，从 `await` 调用返回。

此时，线程应再次测试条件。不能保证该条件现在已满足——`signalAll` 方法只是向等待线程发出信号，表示该条件此时*可能*已满足，值得再次检查该条件。

> **注意：** 一般来说，对 `await` 的调用应位于如下形式的循环中
>
>     while (!(OK to proceed))
>         condition.await();

至关重要的是，最终必须有*某个*其他线程调用 `signalAll` 方法。当线程调用 `await` 时，它无法自行重新激活。它把希望寄托在其他线程身上。如果其他线程都没有费心重新激活等待线程，那么它永远不会再次运行。这可能导致令人不快的*死锁*情况。如果所有其他线程都被阻塞，而最后一个活动线程调用 `await` 却没有解除其他某个线程的阻塞，那么它也会阻塞。没有线程留下来解除其他线程的阻塞，程序就会挂起。

什么时候应该调用 `signalAll`？经验法则是，只要对象状态以可能对等待中的线程有利的方式发生变化，就应调用 `signalAll`

## 代码清单 12.4  `synch/Bank.java`

```java
package synch;

import java.util.*;
import java.util.concurrent.locks.*;

/**
 * A bank with a number of bank accounts that uses locks for serializing access.
 */
public class Bank
{
    private final double[] accounts;
    private Lock bankLock;
    private Condition sufficientFunds;

    /**
     * Constructs the bank.
     * @param n the number of accounts
     * @param initialBalance the initial balance for each account
     */
    public Bank(int n, double initialBalance)
    {
        accounts = new double[n];
        Arrays.fill(accounts, initialBalance);
        bankLock = new ReentrantLock();
        sufficientFunds = bankLock.newCondition();
    }

    /**
     * Transfers money from one account to another.
     * @param from the account to transfer from
     * @param to the account to transfer to
     * @param amount the amount to transfer
     */
    public void transfer(int from, int to, double amount) throws InterruptedException
    {
        bankLock.lock();
        try
        {
            while (accounts[from] < amount)
                sufficientFunds.await();
            System.out.print(Thread.currentThread());
            accounts[from] -= amount;
            System.out.printf(" %10.2f from %d to %d", amount, from, to);
            accounts[to] += amount;
            System.out.printf(" Total Balance: %10.2f%n", getTotalBalance());
            sufficientFunds.signalAll();
        }
        finally
        {
            bankLock.unlock();
        }
    }

    /**
     * Gets the sum of all account balances.
     * @return the total balance
     */
    public double getTotalBalance()
    {
        bankLock.lock();
        try
        {
            double sum = 0;

            for (double a : accounts)
                sum += a;

            return sum;
        }
        finally
        {
            bankLock.unlock();
        }
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

| java.util.concurrent.locks.Lock | 5 |
| --- | --- |
| • Condition newCondition()<br>返回与此锁关联的条件对象。 | |

| `java.util.concurrent.locks.Condition` | 5 |
|---|---|
| `void await()` | 将此线程放入此条件的等待集。 |
| `void signalAll()` | 解除此条件等待集中所有线程的阻塞。 |
| `void signal()` | 解除此条件等待集中随机选中的一个线程的阻塞。 |

## 12.4.5 synchronized 关键字

在前面的小节中，你了解了如何使用 Lock 和 Condition 对象。在继续之前，让我们总结关于锁和条件的要点：

- 锁保护代码段，一次只允许一个线程执行该代码。
- 锁管理试图进入受保护代码段的线程。
- 一个锁可以有一个或多个关联的条件对象。
- 每个条件对象管理已进入受保护代码段但无法继续执行的线程。

Lock 和 Condition 接口让程序员对锁定有高度的控制权。然而，在大多数情况下，你不需要这种控制——你可以使用内置于 Java 语言中的机制。从 1.0 版开始，Java 中的每个对象都有一个内在锁。如果方法用 synchronized 关键字声明，对象的锁保护整个方法。也就是说，要调用该方法，线程必须获取对象的内在锁。

换句话说，

```java
public synchronized void method()
{
    method body
}
```

等价于

```java
public void method()
{
    this.intrinsicLock.lock();
    try
    {
        method body
    }
    finally
    {
        this.intrinsicLock.unlock();
    }
}
```

例如，我们可以简单地将在 Bank 类的 transfer 方法声明为 synchronized，而不使用显式锁。

对象的内在锁有一个关联条件。wait 方法将线程添加到等待集，而 notifyAll/notify 方法解除等待线程的阻塞。换句话说，调用 wait 或 notifyAll 等价于

```java
intrinsicCondition.await();
intrinsicCondition.signalAll();
```

> **注意。** wait、notifyAll 和 notify 方法是 Object 类的 final 方法。Condition 方法必须命名为 await、signalAll 和 signal，以免与这些方法冲突。

例如，你可以像这样用 Java 实现 Bank 类：

```java
class Bank
{
    private double[] accounts;

    public synchronized void transfer(int from, int to, int amount)
        throws InterruptedException
    {
        while (accounts[from] < amount)
            wait(); // wait on intrinsic object lock's single condition
        accounts[from] -= amount;
        accounts[to] += amount;
        notifyAll(); // notify all threads waiting on the condition
    }

    public synchronized double getTotalBalance() { . . . }
}
```

如你所见，使用 synchronized 关键字会生成简洁得多的代码。当然，要理解这段代码，你必须知道每个对象都有一个内在锁，并且该锁有一个内在条件。锁管理试图进入 synchronized 方法的线程。条件管理已调用 wait 的线程。

> **提示：** synchronized 方法相对简单。然而，初学者常常在条件方面遇到困难。在使用 wait/notifyAll 之前，你应考虑使用第 12.5 节“线程安全集合”（第 781 页）中描述的构造之一。

