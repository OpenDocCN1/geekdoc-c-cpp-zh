
- `void notifyAll()` 解除那些在此对象上调用 wait 的线程的阻塞。此方法只能在同步方法或同步块内调用。如果当前线程不是该对象锁的持有者，该方法会抛出 `IllegalMonitorStateException`。
- `void notify()` 在此对象上调用 wait 的线程中随机选择一个线程并解除其阻塞。此方法只能在同步方法或同步块内调用。如果当前线程不是该对象锁的持有者，该方法会抛出 `IllegalMonitorStateException`。
- `void wait()` 使线程等待，直到被通知。此方法只能在同步方法或同步块内调用。如果当前线程不是该对象锁的持有者，它会抛出 `IllegalMonitorStateException`。
- `void wait(long millis)`
- `void wait(long millis, int nanos)` 使线程等待，直到被通知或指定的时间已经过去。这些方法只能在同步方法或同步块内调用。如果当前线程不是该对象锁的持有者，它们会抛出 `IllegalMonitorStateException`。纳秒数不得超过 1,000,000。

### 12.4.6 同步块

正如我们刚刚讨论的，每个 Java 对象都有一个锁。线程可以通过调用同步方法来获取该锁。还有第二种获取锁的机制：进入一个*同步块*。当线程进入如下形式的块时

```java
synchronized (obj) // this is the syntax for a synchronized block
{
    critical section
}
```

那么它就会获取 obj 的锁。

有时你会遇到“临时”锁，例如

```java
public class Bank
{
    private double[] accounts;
    private Object lock = new Object();
    . . .
    public void transfer(int from, int to, int amount)
    {
        synchronized (lock) // an ad-hoc lock
        {
            accounts[from] -= amount;
            accounts[to] += amount;
        }
        System.out.println(. . .);
    }
}
```

这里，创建锁对象只是为了使用每个 Java 对象都拥有的锁。

**注意：**

使用同步块时，要小心锁对象。例如，下面的做法行不通：

```java
private final String lock = "LOCK";
. . .
synchronized (lock) { . . . } // Don't lock on string literal!
```

如果这在同一个程序中出现两次，那么由于字符串字面量是共享的，这些锁就是*同一个对象*。这可能导致死锁。

另外，要避免使用基本类型包装器作为锁：

```java
private final Integer lock = new Integer(42); // Don't lock on wrappers
```

构造函数调用 `new Integer(42)` 已被弃用，而且你不会希望维护程序员将该调用改成 `Integer.valueOf(42)`。如果对相同的魔法数执行两次，锁就会被意外共享。

如果需要修改静态字段，请锁定具体的类，而不是 `getClass()` 返回的值：

```java
synchronized (MyClass.class) { staticCounter++; } // OK
synchronized (getClass()) { staticCounter++; } // Don't
```

如果包含此代码的方法从子类中调用，那么 `getClass()` 会返回一个不同的 `Class` 对象！你不再能保证互斥！

一般来说，如果必须使用 `synchronized` 块，*要清楚你的锁对象是什么！* 你必须对所有受保护的访问路径使用同一个锁，并且其他任何人都不能使用你的锁。

有时，程序员会使用对象的锁来实现额外的原子操作——这种做法称为*客户端加锁*。例如，考虑 `Vector` 类，它是一个方法都同步的列表。现在假设我们将银行余额存储在一个 `Vector<Double>` 中。下面是一个转账方法的朴素实现：

```java
public void transfer(Vector<Double> accounts, int from, int to, int amount) // ERROR
{
    accounts.set(from, accounts.get(from) - amount);
    accounts.set(to, accounts.get(to) + amount);
    System.out.println(. . .);
}
```

`Vector` 类的 `get` 和 `set` 方法是同步的，但这并不能帮助我们。线程完全可能在转账方法中完成第一次 `get` 调用之后被抢占。然后另一个线程可能会将不同的值存储到同一位置。不过，我们可以劫持这个锁：

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

这种方法可行，但它完全依赖于 `Vector` 类对其所有修改器方法都使用内在锁这一事实。然而，这真的是事实吗？`Vector` 类的文档并没有做出这样的承诺。你必须仔细研究源代码，并希望未来的版本不会引入未同步的修改器方法。如你所见，客户端加锁非常脆弱，通常不推荐使用。

**注意：**

Java 虚拟机对同步方法有内置支持。然而，同步块会被编译成一长串字节码来管理内在锁。

### 12.4.7 监视器概念

锁和条件是用来进行线程同步的强大工具，但它们并不太面向对象。多年来，研究人员一直在寻找使多线程安全而又不强迫程序员考虑显式锁的方法。最成功的解决方案之一是由 Per Brinch Hansen 和 Tony Hoare 在 20 世纪 70 年代开创的*监视器*概念。用 Java 的术语来说，监视器具有以下属性：

- 监视器是一个只包含私有字段的类。
- 该类的每个对象都有一个关联的锁。
- 所有方法都由该锁锁定。换句话说，如果客户端调用 `obj.method()`，那么在方法调用开始时就会自动获取 `obj` 的锁，并在方法返回时释放该锁。由于所有字段都是私有的，这种安排确保在一个线程操作字段时，没有其他线程可以访问这些字段。
- 锁可以具有任意数量的关联条件。

早期版本的监视器只有一个条件，其语法相当优雅。你可以直接调用 `await accounts[from] >= amount`，而不需要使用显式的条件变量。然而，研究表明，不加区分地重新测试条件可能效率低下。这个问题通过显式条件变量来解决，每个条件变量管理一组单独的线程。

Java 设计者松散地借鉴了监视器概念。Java 中的*每个对象*都有一个内在锁和一个内在条件。如果一个方法用 `synchronized` 关键字声明，它就像监视器方法一样工作。条件变量通过调用 `wait/notifyAll/notify` 来访问。

然而，Java 对象在三个重要方面与监视器不同，从而损害了线程安全性：

- 字段不要求是私有的。
- 方法不要求是同步的。
- 内在锁可供客户端使用。

这种对安全性的漠视激怒了 Per Brinch Hansen。在对 Java 多线程原语的严厉评论中，他写道：“令我震惊的是，在监视器和 Concurrent Pascal 发明四分之一个世纪之后，编程界竟然认真对待 Java 不安全的并行机制。它毫无价值”[Java’s Insecure Parallelism, *ACM SIGPLAN Notices* 34:38–45, April 1999]。

### 12.4.8 volatile 字段

有时，仅仅为了读取或写入一两个实例字段而付出同步的代价似乎有些过度。毕竟，能出什么问题呢？不幸的是，对于现代处理器和编译器来说，出错的空间很大。

- 具有多个处理器的计算机可以暂时将内存值保存在寄存器或本地内存缓存中。因此，运行在不同处理器上的线程可能会看到同一内存位置的不同值！
- 编译器可以重新排序指令以获得最大吞吐量。编译器不会选择改变代码含义的顺序，但它们假设只有在代码中存在显式指令时内存值才会被更改。然而，内存值可以被另一个线程更改！

如果使用锁来保护可能被多个线程访问的代码，就不会有这些问题。编译器必须尊重锁，必要时刷新本地缓存，并且不进行不恰当的指令重排序。详细信息在 JSR 133 制定的《Java 内存模型与线程规范》中说明（见 www.jcp.org/en/jsr/detail?id=133）。该规范的许多内容高度复杂且技术性强，但文档也包含许多清晰的
