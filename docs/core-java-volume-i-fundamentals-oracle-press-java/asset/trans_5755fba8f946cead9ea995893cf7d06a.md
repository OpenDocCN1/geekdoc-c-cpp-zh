
```java
{
    bankLock.unlock();
  }
}
}
}
```

假设一个线程调用 `transfer`，并在完成之前被抢占。假设第二个线程也调用 `transfer`。第二个线程无法获取锁，并在调用 `lock` 方法时被阻塞。它被停用，必须等待第一个线程执行完 `transfer` 方法。当第一个线程解锁后，第二个线程才能继续执行（见图 12.3）。

试试看。将锁定代码添加到 `transfer` 方法中，然后再次运行程序。你可以一直运行它，银行余额也不会被破坏。

注意，每个 Bank 对象都有自己的 ReentrantLock 对象。如果两个线程尝试访问同一个 Bank 对象，那么该锁用于将访问串行化。然而，如果两个线程访问不同的 Bank 对象，每个线程会获取不同的锁，并且两个线程都不会被阻塞。这是应该的，因为当线程操作不同的银行实例时，它们无法相互干扰。

该锁被称为*可重入*锁，因为一个线程可以重复获取它已经拥有的锁。该锁有一个*持有计数*，用于跟踪对 lock 方法的嵌套调用。线程必须为每一次 `lock` 调用都调用 `unlock`，才能释放锁。由于这一特性，受锁保护的代码可以调用另一个使用同一把锁的方法。

例如，`transfer` 方法调用 `getTotalBalance` 方法，后者也会锁定 `bankLock` 对象，此时该对象的持有计数为 2。当 `getTotalBalance` 方法退出时，持有计数回到 1。当 `transfer` 方法退出时，持有计数为 0，线程释放该锁。

![](img/0e7b74ef51a065c077b42cd87b362288_1076_0.png)

**图 12.3** 未同步线程与同步线程的比较

通常，你会希望保护那些更新或检查共享对象的代码块，这样就能确保这些操作在另一个线程使用同一对象之前运行完成。

**注意：**

务必小心确保临界区中的代码不会因为抛出异常而被绕过。如果在临界区结束之前抛出异常，finally 子句会释放锁，但对象可能处于受损状态。

### java.util.concurrent.locks.Lock⁵

- `void lock()` — 获取此锁；如果该锁当前由另一个线程拥有，则阻塞。
- `void unlock()` — 释放此锁。

### java.util.concurrent.locks.ReentrantLock⁵

- `ReentrantLock()` — 构造一个可重入锁，可用于保护临界区。
- `ReentrantLock(boolean fair)` — 构造一个具有给定公平策略的锁。公平锁偏向等待时间最长的线程。然而，这种公平性保证可能会显著拖累性能。因此，默认情况下，锁不要求是公平的。

![](img/0e7b74ef51a065c077b42cd87b362288_1077_0.png)

**注意：**

公平听起来不错，但公平锁比普通锁*慢得多*。只有当你真正了解自己在做什么，并且有特定理由认为公平性对你的程序至关重要时，才应启用公平锁。

即使使用公平锁，也不能保证线程调度器是公平的。如果线程调度器选择忽略一个已经等待锁很长时间的线程，该线程就没有机会被锁公平对待。

## 12.4.4 条件对象

通常，线程进入临界区后才发现，直到某个条件得到满足，它才能继续执行。使用*条件对象*来管理那些已经获取锁但无法做有用工作的线程。本节介绍 Java 库中条件对象的实现。（由于历史原因，条件对象通常被称为*条件变量*。）

让我们改进银行模拟。我们不希望从一个没有足够资金完成转账的账户中转出资金。注意，我们不能使用如下代码

```java
if (bank.getBalance(from) >= amount)
    bank.transfer(from, to, amount);
```

当前线程完全可能在测试成功之后、调用 `transfer` 之前被停用。

```java
if (bank.getBalance(from) >= amount)
    // thread might be deactivated at this point
    bank.transfer(from, to, amount);
```

当线程再次运行时，账户余额可能已经低于取款金额。必须确保在测试和转账操作之间没有其他线程能修改余额。为此，用锁同时保护测试和转账操作：

```java
public void transfer(int from, int to, int amount)
{
    bankLock.lock();
    try
    {
        while (accounts[from] < amount)
        {
            // wait
            . . .
        }
        // transfer funds
        . . .
    }
    finally
    {
        bankLock.unlock();
    }
}
```

那么，当账户中没有足够的钱时，我们该怎么办？我们等待其他线程存入资金。但这个线程刚刚获得了对 bankLock 的独占访问权，因此其他线程没有机会存款。条件对象正是在这里发挥作用。

一个锁对象可以有一个或多个关联的条件对象。通过 `newCondition` 方法获得条件对象。习惯上给每个条件对象起一个能体现它所表示条件的名称。例如，这里我们建立一个条件对象来表示“资金充足”条件。

```java
class Bank
{
    private Condition sufficientFunds;
    . . .
    public Bank()
    {
        . . .
        sufficientFunds = bankLock.newCondition();
    }
}
```

如果 `transfer` 方法发现没有足够的资金可用，它会调用

```java
sufficientFunds.await();
```

当前线程现在被停用并放弃锁。这会让另一个线程进入，我们希望该线程能增加账户余额。

等待获取锁的线程与已经调用 `await` 的线程之间存在本质区别。一旦线程调用 `await` 方法，它就会进入该条件的一个*等待集*。当锁可用时，该线程*不会*变为可运行状态。相反，它会保持停用状态，直到另一个线程在同一个条件上调用 `signalAll` 方法。

当另一个线程完成转账后，它应该调用

```java
sufficientFunds.signalAll();
```

这个调用会重新激活所有等待该条件的线程。当这些线程从等待集中移除后，它们再次变为可运行状态，调度器最终会再次激活它们。届时，它们将尝试重新进入该对象。一旦锁可用，其中一个线程将获取锁，*并从上次离开的地方继续执行*，从 `await` 调用处返回。

此时，线程应再次测试该条件。不能保证条件现在已满足——`signalAll` 方法只是向等待线程发出信号，表示此时条件*可能*已满足，值得再次检查该条件。

**注意：**

通常，对 `await` 的调用应位于如下形式的循环中

```java
while (!(OK to proceed))
    condition.await();
```

若无法继续执行，它就会再次阻塞。如果没有其他线程再次调用 signal，系统就会死锁。

**注意：**

只有线程拥有某个条件的锁时，才能在该条件上调用 `await`、`signalAll` 或 `signal`。

如果运行代码清单 12.4 中的示例程序，你会注意到永远不会出错。总余额永远保持在 $100,000。任何账户都不会出现负余额。（再次按 Ctrl+C 终止程序。）你可能还会注意到程序运行得稍慢一些——这是同步机制中额外簿记工作带来的代价。

在实践中，正确使用条件可能相当具有挑战性。在开始实现自己的条件对象之前，应考虑使用第 12.5 节“线程安全集合”（第 797 页）中描述的构造之一。

**代码清单 12.4** synch/Bank.java

```java
package synch;

import java.util.*;
import java.util.concurrent.locks.*;

/**
 * A bank with a number of bank accounts that uses locks for serializing access.
 */
public class Bank {
    private final double[] accounts;
    private Lock bankLock;
    private Condition sufficientFunds;
}
```
