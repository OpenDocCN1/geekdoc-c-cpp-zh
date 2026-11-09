
回顾 `incrementValue` 方法，这是一个只有一行的 Java 方法，没有循环或分支：

```java
public class IdGenerator {
    int lastIdUsed;

    public int incrementValue() {
        return ++lastIdUsed;
    }
}
```

忽略整数溢出，并假设只有一个线程可以访问 `IdGenerator` 的单个实例。在这种情况下，只有一条执行路径，结果也唯一确定：

- 返回的值等于 `lastIdUsed` 的值，两者都比调用方法前大 1。

如果我们使用两个线程且不修改方法，会发生什么？如果每个线程各调用一次 `incrementValue`，可能的结果有哪些？可能的执行路径有多少条？首先看结果（假设 `lastIdUsed` 的初始值为 93）：

- 线程 1 得到值 94，线程 2 得到值 95，`lastIdUsed` 现在是 95。
- 线程 1 得到值 95，线程 2 得到值 94，`lastIdUsed` 现在是 95。
- 线程 1 得到值 94，线程 2 得到值 94，`lastIdUsed` 现在是 94。

最终结果虽然令人惊讶，但确实是可能的。要理解这些不同结果为何会出现，我们需要了解可能的执行路径数量，以及 Java 虚拟机如何执行这些路径。

## 路径数量

要计算可能的执行路径数量，我们从生成的字节码开始。这一行 Java 代码（`return ++lastIdUsed;`）变成了 8 条字节码指令。两个线程可以像荷官洗牌时交错牌面那样交错执行这 8 条指令。² 即使每只手只有 8 张牌，洗牌后的结果数量也非常可观。

对于这种简单情况：*N* 条指令按顺序执行，没有循环或条件分支，*T* 个线程，总可能的执行路径数量等于

$$\frac{(NT)!}{N!^T}$$

## 计算可能的顺序

这来自 Uncle Bob 写给 Brett 的一封邮件：

有 *N* 个步骤和 *T* 个线程时，总步骤数为 *T* × *N*。在每个步骤之前，都有一个上下文切换，在 *T* 个线程之间进行选择。因此，每条路径都可以表示为表示上下文切换的数字字符串。给定步骤 A 和 B 以及线程 1 和 2，六条可能的路径是 1122、1212、1221、2112、2121 和 2211。或者，用步骤表示就是 A1B1A2B2、A1A2B1B2、A1A2B2B1、A2A1B1B2、A2A1B2B1 和 A2B2A1B1。对于三个线程，序列是 112233、112323、113223、113232、121233、121323、121332、123132、123123、……。

这些字符串的一个特征是，每个 *T* 必须始终出现 *N* 次。因此字符串 111111 是无效的，因为它有 6 个 1，而 2 和 3 各有 0 个。

所以我们想要的是 *N* 个 1、*N* 个 2、……、*N* 个 *T* 的排列。这实际上就是从 *N* × *T* 个元素中取 *N* × *T* 个元素的排列，即 (*N* × *T*)!，但要移除所有重复项。诀窍在于计算重复项的数量，并从 (*N* × *T*)! 中减去它。

给定两个步骤和两个线程，有多少个重复项？每个四位字符串都有两个 1 和两个 2。每一对都可以交换而不改变字符串的含义。你可以交换两个 1、两个 2、两者都交换，或者都不交换。所以每个字符串有四个同构体，这意味着有三个重复项。因此，四个选项中三个是重复的；或者说，四个排列中有一个不是重复的。4! * .25 = 6。所以这个推理似乎成立。

```java
04:    public void resetId() {
05:        value = 0;
06:    }
07:
08:    public int getNextId() {
09:        ++value;
10:    }
11:}
```

如果我们把 `value` 的类型从 int 改为 long，会发生什么？第 5 行仍然是原子操作吗？根据 JVM 规范，不是。在特定的处理器上它可能是原子的，但根据 JVM 规范，对任何 64 位值的赋值都需要两次 32 位赋值。这意味着在第一次 32 位赋值和第二次 32 位赋值之间，另一个线程可能偷偷介入并改变其中一个值。

第 9 行的前置递增运算符 ++ 呢？前置递增运算符可能被中断，因此它不是原子的。为了理解这一点，让我们详细检查这两个方法的字节码。

在继续之前，这里有三个重要的定义：

- **帧（Frame）——** 每个方法调用都需要一个帧。帧包括返回地址、传递给方法的参数以及方法中定义的局部变量。这是定义调用栈的标准技术，现代语言用它来实现基本的函数/方法调用，并支持递归调用。
- **局部变量（Local variable）——** 在方法作用域内定义的任何变量。所有非静态方法至少有一个变量 `this`，它代表当前对象，即（在当前线程中）收到最近消息、从而引起方法调用的那个对象。
- **操作数栈（Operand stack）——** Java 虚拟机中的许多指令都接受参数。操作数栈就是放置这些参数的地方。该栈是标准的后进先出（LIFO）数据结构。

以下是 `resetId()` 生成的字节码：

人们普遍误认为 ++（前置或后置递增）运算符是原子的，但它显然不是。这意味着你需要知道：

- 哪些地方有共享对象/值
- 哪些代码可能导致并发的读/写问题
- 如何防范这些并发问题的发生

## 了解你的类库

### Executor 框架

正如第 [321](#) 页的 `ExecutorClientScheduler.java` 所示，Java 5 中引入的 Executor 框架允许使用线程池进行复杂的执行。这是 `java.util.concurrent` 包中的一个类。

如果你正在创建线程却没有使用线程池，或者使用了手写的线程池，你应该考虑使用 Executor。它会让你的代码更干净、更易读、更精简。

`Executor` 框架会池化线程、自动调整大小，并在必要时重新创建线程。它还支持 *future*，这是一种常见的并发编程结构。`Executor` 框架既适用于实现 `Runnable` 的类，也适用于实现 `Callable` 接口的类。`Callable` 看起来像 `Runnable`，但它可以返回结果，这在多线程解决方案中是常见的需求。

当代码需要执行多个独立的操作并等待它们全部完成时，*future* 非常有用：

```java
public String processRequest(String message) throws Exception {
    Callable<String> makeExternalCall = new Callable<String>() {

        public String call() throws Exception {
            String result = "";
            // make external request
            return result;
        }
    };
    Future<String> result = executorService.submit(makeExternalCall);
    String partialResult = doSomeLocalProcessing();
    return result.get() + partialResult;
}
```

在这个例子中，方法开始执行 `makeExternalCall` 对象，然后继续其他处理。最后一行调用 `result.get()`，该方法会阻塞直到 future 完成。

### 非阻塞解决方案

Java 5 虚拟机利用了现代处理器设计，支持可靠的非阻塞更新。例如，考虑一个使用同步（因此是阻塞）来提供线程安全值更新的类：

```java
public class ObjectWithValue {
    private int value;
    public synchronized void incrementValue() { ++value; }
    public int getValue() { return value; }
}
```

Java 5 为这类情况提供了一系列新类：`AtomicBoolean`、`AtomicInteger` 和 `AtomicReference` 是其中三个例子；还有更多。我们可以用非阻塞方式重写上述代码：

```java
public class ObjectWithValue {
    private AtomicInteger value = new AtomicInteger(0);

    public void incrementValue() {
        value.incrementAndGet();
    }
    public int getValue() {
        return value.get();
    }
}
```

即使这使用了对象而不是原始类型，并且发送的是 `incrementAndGet()` 之类的消息而不是 ++，这个类的性能也几乎总是会超过之前的版本。在某些情况下，它只会

