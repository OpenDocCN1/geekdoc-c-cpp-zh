

依赖于类型为 A => Future[B] 的计算而不是 A => B 的额外好处是，future 还可以携带失败——在 Scala 中，你可以将 Future 视为异步的 Try。例如，你可以通过确保即使找不到用户时也始终产生一个 future 来改进 getAccount 函数：

```
def getAccount(user: User): Future[Account] = Future.fromTry(Try(allAccounts(user)))
```

这样，类似 getAccount(user).onComplete(...) 的表达式仍然会执行回调动作，而如果 getAccount 抛出异常则不成立。失败的 future 可以以函数式的方式处理，使用 Scala 中的 recover 等专用函数，或 Java 中的 exceptionally。

为简单起见，来自清单 26.8 的连接处理函数并未处理错误。你可以使用标准的 future 函数为服务器增加健壮性。例如，创建页面失败可以通过转换 pageF future 来处理：

```
val safePageF: Future[Page] = pageF.recover { case ex: PageException => errorPage(ex) }
```

或通过添加失败回调：

```
pageF.failed.foreach { ex =>
  connection.write(errorPage(ex))
  connection.close()
}
```

使用 pageF.foreach 或使用 pageF.failed.foreach 指定的回调动作中，只会运行其中一种，而不会同时运行两种。

## 非阻塞“Join”模式

在服务器示例中，pageF 是通过使用 flatMap 组合两个 future dataF 和 adF 创建的。你可以使用相同的方法组合三个或更多 future：

```
val f1: Future[Int] = ...
val f2: Future[String] = ...
val f3: Future[Double] = ...

val f: Future[(Int, String, Double)] =
  f1.flatMap(n => f2.flatMap(s => f3.map(d => (n, s, d))))
```

不过这无法扩展到更大数量的 future。一种有趣且并不罕见的情况是将 N 个相同类型的 future 组合成一个单一的 future，N 为任意数。在服务器示例中，客户端可能从 *N* 个数据库查询中获取数据，这些查询并行执行：

```
```scala
def queryDB(requests: List[Request]): Future[Page] =
  val futures: List[Future[Data]] = requests.map(request => Future(dbLookup(request)))
  val dataListF: Future[List[Data]] = Future.sequence(futures)
  dataListF.map(makeBigPage)
```
```

第一行使用 `map` 为每个请求创建一个数据库查询任务。这些并行运行的任务形成一个 future 列表。`queryDB` 中的关键步骤是对 `Future.sequence` 的调用。此函数使用类型为 `List[Future[A]]` 的输入来产生类型为 `Future[List[A]]` 的输出。它返回的 future 在所有输入 future 完成后完成，并包含它们的所有值作为一个列表（假设没有错误）。调用 `Future.sequence` 起到的作用与 fork-join 模式中的“join”部分相同，但不会阻塞。最后一步使用从 `List[Data]` 到 `Page` 的函数 `makeBigPage` 来构建最终页面。

截至本文撰写时，`CompletableFuture` 没有标准的 sequence 函数，但你可以使用 `thenCompose`（相当于 `flatMap`）和 `thenApply`（相当于 `map`）自行实现：

```
```scala
def sequence[A](futures: List[CompletableFuture[A]]): CompletableFuture[List[A]] =
  futures match
    case Nil => CompletableFuture.completedFuture(List.empty)
    case future :: more =>
      future.thenCompose(first => sequence(more).thenApply(others => first :: others))
```
```

清单 26.10：不阻塞地将一个 CompletableFuture 列表合并为一个。

此函数使用递归来嵌套调用 `thenCompose`（`flatMap`）。在递归分支中，`sequence(more)` 是一个 future，它将包含除第一个之外的所有输入 future 的值。然后使用 `thenCompose` 和 `thenApply`（`flatMap` 和 `map`）将此 future 与第一个输入 future 组合起来，其模式与之前合并两个 future 时使用的模式相同（如清单 26.5、26.7 和 26.8 所示）。

## 非阻塞“Fork-Join”模式

函数 `queryDB` 使用一种 fork-join 模式，其中 `sequence` 在不阻塞的情况下实现了“join”部分。fork-join 是一种足够常见的模式，以至于 Scala 定义了函数 `traverse` 来实现计算的“fork”和“join”两部分。你可以使用它来实现 `queryDB` 的更简洁版本：

```
```scala
def queryDB(requests: List[Request]): Future[Page] =
  Future.traverse(requests)(request => Future(dbLookup(request))).map(makeBigPage)
```
```

## 第 27 章

## 最小化线程阻塞

第 26 章提倡以函数式的方式使用 future 的编程风格，从而最小化线程阻塞。多年来，人们花费了大量精力试图避免不必要的线程阻塞，通常出于性能原因。¹ 本章快速概述了一些流行的技术，这些技术力求不阻塞线程，并且通常避免使用锁和其他同步器。

### 27.1 原子操作

作为第一个示例，考虑类 java.util.concurrent.AtomicInteger 的情况，它在一些早期的示例中使用过。在 Java² 中使用锁实现线程安全的可变整数是相当直接的：

// THIS IS NOT java.util.concurrent.AtomicInteger!
private int value = 0;

public synchronized int get() {
    return value;
}

public synchronized int incrementAndGet() {
    value += 1;
    return value;
}
```

此代码是正确且线程安全的，但不一定高效。如果两个线程共享这样的整数，并且同时调用 incrementAndGet，一个线程成功获取对象的内部锁，而另一个线程被阻塞。这是不理想的，因为将该线程挂起和恢复所需的时间远多于另一个线程执行 value += 1 所需的时间。当锁不可用时，让线程浪费一些 CPU 周期进行自旋，而不是阻塞，直到另一个线程完成整数的递增会更好。

实际的类 `AtomicInteger` 并未使用锁。从概念上讲，它实现如下：

```
```java
public class AtomicInteger {

    private static final AtomicIntegerFieldUpdater<AtomicInteger> updater
        = newUpdater(AtomicInteger.class, "value");

    private volatile int value;

    public int get() {
        return value;
    }

    public int incrementAndGet() {
        while (true) {
            int current = value;
            int next = current + 1;
            if (updater.compareAndSet(this, current, next))
                return next;
        }
    }
    ...
}
```
```

清单 27.1：Java 中类 `AtomicInteger` 的概念实现。

没有任何方法被同步，并且实现不依赖任何锁定机制。相反，变量 value 是 volatile 且无需锁定即可访问。

读取整数不是问题：方法 `get` 只是读取并返回 value。然而，方法 `incrementAndGet` 存在原子性挑战。你需要避免两个并发进入该方法的线程相互覆盖对方的更新的场景（参见第 18.1 节的讨论）。

实现依赖于 compare-and-set（CAS）操作：

```
`compare-and-set(target, expectedValue, newValue)`
```

此表达式仅在目标等于预期值时才将目标设置为新值。如果目标与预期值不同，CAS 操作不会修改它。在语义上，这等同于 if (target == expected) target = newValue，只是检查后再执行的操作是原子执行的。CAS 在目标成功更新时返回 true，否则返回 false。

> 出于这个原因，现代 JVM 实现在锁不可用时通常不会立即挂起线程，而是先自旋一段时间，以防锁很快变得可用。
> 
> Compare-and-set 有时也称为 *compare-and-swap*。区别在于 compare-and-swap 返回交换前变量的值，而 compare-and-set 返回布尔值。

