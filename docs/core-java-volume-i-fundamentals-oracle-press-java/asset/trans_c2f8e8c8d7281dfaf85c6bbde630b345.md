
下面是一个典型的输出：

```text
...
Thread[Thread-11,5,main]    588.48 from 11 to 44 Total Balance:  100000.00
Thread[Thread-12,5,main]    976.11 from 12 to 22 Total Balance:  100000.00
Thread[Thread-14,5,main]    521.51 from 14 to 22 Total Balance:  100000.00
Thread[Thread-13,5,main]    359.89 from 13 to 81 Total Balance:  100000.00
...
Thread[Thread-36,5,main]    401.71 from 36 to 73 Total Balance:  99291.06
Thread[Thread-35,5,main]    691.46 from 35 to 77 Total Balance:  99291.06
Thread[Thread-37,5,main]    78.64 from 37 to 3 Total Balance:  99291.06
Thread[Thread-34,5,main]    197.11 from 34 to 69 Total Balance:  99291.06
Thread[Thread-36,5,main]    85.96 from 36 to 4 Total Balance:  99291.06
...
Thread[Thread-4,5,main]Thread[Thread-33,5,main]    7.31 from 31 to 32 Total Balance:  99979.24
    627.50 from 4 to 5 Total Balance:  99979.24
...
```

如你所见，情况非常不对劲。在前几笔交易中，银行余额保持在 $100,000，这是 100 个账户、每个账户 $1,000 的正确总额。但过了一段时间后，余额会略微变化。运行这个程序时，错误可能很快出现，也可能要过很长时间余额才会被破坏。这种情况无法让人放心，你大概不会愿意把辛苦挣来的钱存入这样的银行。

看看你能否找出 [代码清单 12.3](#) 中的代码以及 [代码清单 12.2](#) 中的 Bank 类的问题。我们将在下一节揭开这个谜团。

### 代码清单 12.3 unsynch/UnsynchBankTest.java

```java
 1 package unsynch;
 2 
 3 /**
 4  * This program shows data corruption when multiple threads access a data structure.
 5  * @version 1.32 2018-04-10
 6  * @author Cay Horstmann
 7  */
 8 public class UnsynchBankTest
 9 {
10     public static final int NACCOUNTS = 100;
11     public static final double INITIAL_BALANCE = 1000;
12     public static final double MAX_AMOUNT = 1000;
13     public static final int DELAY = 10;
14 
15     public static void main(String[] args)
16     {
17         var bank = new Bank(NACCOUNTS, INITIAL_BALANCE);
18         for (int i = 0; i < NACCOUNTS; i++)
19         {
20             int fromAccount = i;
21             Runnable r = () ->
22                 {
23                     try
24                     {
25                         while (true)
26                         {
27                             int toAccount = (int) (bank.size() * Math.random());
28                             double amount = MAX_AMOUNT * Math.random();
29                             bank.transfer(fromAccount, toAccount, amount);
30                             Thread.sleep((int) (DELAY * Math.random()));
31                         }
32                     }
33                     catch (InterruptedException e)
34                     {
35                     }
36                 };
37             var t = new Thread(r);
38             t.start();
39         }
40     }
41 }
```

### 12.4.2 竞态条件解析

上一节中，我们运行了一个程序，其中多个线程更新银行账户余额。过了一段时间后，错误悄悄出现，一些金额要么丢失，要么凭空产生。当两个线程同时尝试更新同一个账户时，就会出现这个问题。假设两个线程同时执行指令

```java
accounts[to] += amount;
```

问题在于，这些操作不是*原子*操作。该指令可能会按如下方式处理：

- 1. 将 `accounts[to]` 加载到寄存器中。
- 2. 加上 `amount`。
- 3. 将结果写回 `accounts[to]`。

现在，假设第一个线程执行了步骤 1 和 2，然后被抢占。假设第二个线程醒来并更新了账户数组中的同一个条目。然后，第一个线程醒来并完成它的步骤 3。

这一操作会抹掉另一个线程所做的修改。结果，总额不再正确（见*图 12.2*）。

反编译 `Bank.class` 文件。例如，代码行

```java
accounts[to] += amount;
```

会被翻译成以下字节码：

```text
aload_0
getfield        #2; //Field accounts:[D
iload_2
dup2
daload
dload_3
dadd
dastore
```

这些代码的含义并不重要。关键在于，递增命令由若干条指令组成，而执行这些指令的线程可能在任意一条指令处被中断。

这种破坏发生的概率有多大？在具有多个核心的现代处理器上，发生破坏的风险相当高。在单核处理器上，我通过将打印语句与更新余额的语句交错执行，提高了观察到该问题的概率。

如果省略打印语句，发生破坏的风险会较低，因为每个线程在再次休眠之前做的工作很少，调度器不太可能在计算过程中抢占它。然而，破坏的风险并不会完全消失。如果你在负载很重的机器上运行大量线程，即使已经删除了打印语句，程序仍然会失败。失败可能需要几分钟、几小时或几天才会发生。坦率地说，程序员生涯中很少有比一个只不定期出现的错误更糟糕的事情。

真正的问题在于，`transfer` 方法的工作可能会在中途被中断。如果我们能确保该方法在线程失去控制之前运行到完成，那么银行账户对象的状态就永远不会被破坏。

### 12.4.3 锁对象

有两种机制可以保护代码块免受并发访问。Java 语言为此提供了 synchronized 关键字，Java 5 还引入了 ReentrantLock 类。synchronized 关键字会自动提供锁以及关联的“条件”，这使得它在大多数需要显式锁定的情况下既强大又方便。不过，我认为在单独了解锁和条件之后，会更容易理解 synchronized 关键字。java.util.concurrent 框架为这些基本机制提供了单独的类，我在这里以及第 772 页的 12.4.4 节“条件对象”中对此进行解释。一旦你理解了这些构建块，我会在第 778 页的 12.4.5 节“synchronized 关键字”中介绍 synchronized 关键字。

使用 ReentrantLock 保护代码块的基本框架如下：

```java
myLock.lock(); // a ReentrantLock object
try
{
    critical section
}
finally
{
    myLock.unlock(); // make sure the lock is unlocked even if an exception is thrown
}
```

这种结构保证一次只有一个线程能进入临界区。一旦某个线程锁定了锁对象，其他线程就无法通过 lock 语句。当其他线程调用 lock 时，它们会被停用，直到第一个线程解锁该锁对象。

**警告：**

将 `unlock` 操作包含在 `finally` 子句中至关重要。如果临界区中的代码抛出异常，必须解锁。否则，其他线程将被永久阻塞。

**注意：**

使用锁时，不能使用 `try-with-resources` 语句。首先，`unlock` 方法并不叫 `close`。但即使它被重命名，`try-with-resources` 语句也无法工作。它的头部期望声明一个新变量。而使用锁时，你希望继续使用线程之间共享的同一个变量。

让我们使用锁来保护 `Bank` 类的 `transfer` 方法。

```java
public class Bank
{
    private Lock bankLock = new ReentrantLock();
    . . .
    public void transfer(int from, int to, int amount)
    {
        bankLock.lock();
        try
        {
            System.out.print(Thread.currentThread());
            accounts[from] -= amount;
            System.out.printf(" %10.2f from %d to %d", amount, from, to);
            accounts[to] += amount;
            System.out.printf(" Total Balance: %10.2f%n", getTotalBalance());
        }
        finally
```
