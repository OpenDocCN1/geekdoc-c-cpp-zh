
在这个示例中，两个事件被用来向演出中的多个演出方发出信号。所有小提琴手都在等待它们的事件，而所有小号手也在等待它们的事件。当指挥在他希望他们开始的时候设置该事件时，他们就可以继续自己的工作。

懂音乐的读者会注意到这里缺少了一些东西。指挥如何知道所有演奏者都准备好接收该事件？最有可能的情况是，当事件被设置时，所有演奏者都已经准备好了，因为他们各自的线程已经启动了一段时间。然而，正确的同步需要更精心的设计，我们稍后将讨论这一点。

## CountDownEvent（倒计时事件）

倒计时事件是在 .NET 4 中引入的，它允许多个参与方根据一个计数来相互同步。也就是说，只有当总计数达到零时，事件才会被设置。每次调用 Signal 都会将计数值减 1 或减一个指定的量。在构造时可以设置初始计数。当计数达到零时，等待该事件的线程可以从其 Wait 调用处继续执行。

就我们的乐队而言，这种机制可以用作最初的握手。为了限制代码清单的篇幅，我们做了一点简化，只展示握手部分，即指挥等待所有演奏者发出“已准备好”的信号：

```
var start = new CountdownEvent(8);
var conductorSignalsViolins = new ManualResetEvent(false);
var conductorSignalsTrumpetists = new ManualResetEvent(false);

for (int i = 0; i < 5; i++)
{
    new Thread(() =>
    {
        Console.WriteLine(Thread.CurrentThread.Name + " takes a seat.");
        start.Signal();
        conductorSignalsViolins.WaitOne();
        // Code to play my part...
    }) { Name = "V" + i }.Start();
}

for (int i = 0; i < 3; i++)
{
    new Thread(() =>
    {
        Console.WriteLine(Thread.CurrentThread.Name + " takes a seat.");
        start.Signal();
        conductorSignalsTrumpetists.WaitOne();
        // Code to play my part...
    }) { Name = "T" + i }.Start();
}
```

同样有趣的是两组静态方法的存在，分别名为 WaitAny 和 WaitAll。它们的作用是为涉及多个等待句柄的同步提供支持。在我们的乐队示例中，所有演奏者都在等待唯一的指挥告诉他们开始演奏。但是，想象一下如果指挥从不给他们发开始演奏的信号会怎样？他们将永远卡住。这种情况可能会在剧院火警响起时出现。显然，你不想让演奏者卡住。

我们如何解决前面段落描述的问题呢？这里我们要做的是等待两个事件中的任意一个发生：一个是乐队指挥，另一个是紧急的“逃命吧”情况。在一个更与编程相关的示例中，这种技术可以用来等待一个事件或一个取消信号。应该清楚的是，根据是哪个等待句柄使等待操作成功，应该采取不同的行动。让我们聚焦于一个小提琴手的代码，展示如何执行 WaitAny：

```csharp
var conductorSignalsViolins = new ManualResetEvent(false);
var emergencyAlarm = new ManualResetEvent(false);

for (int i = 0; i < 5; i++)
{
    new Thread(() =>
    {
        int res = WaitHandle.WaitAny(new[] { conductorSignalsViolins,
            emergencyAlarm });
        if (res == 0)
            // Code to play my part...
        else
            // Just quitting from the thread would suffice, but let's be
            // a bit more illustrative here...
            Environment.FailFast("Run for your life!");
    }) { Name = "V" + i }.Start();
}
```

// 乐队指挥可以发出开始演奏的信号——或者——
// 有人可以触发火警。

WaitAny 方法返回导致等待操作成功的等待句柄在数组中的索引。基于这个值，可以执行不同的代码。

我们在对等待句柄的探讨中省略了 WaitAll 方法，但其操作是类似的：传入一个句柄数组，但这一次只有所有句柄都已被发出信号时，等待才会成功。当多个参与方必须先发出就绪信号，另一个参与方才能继续其工作时，这就很有用了。

在幕后，这些方法使用 Win32 [Msg]WaitForMultipleObjects[Ex] 函数。这解释了为什么执行这些高级等待操作需要操作系统句柄；操作系统只知道这些。某些精简变体仍然能够通过将对象“升级”为具有 Win32 句柄来获取 WaitHandle。然而，这样做会失去其一部分“精简”特性。

## Interlocked 辅助方法

回顾我们之前的计数器示例，回想一下使得必须进行同步才能产生正确结果的核心问题。一些基本操作，例如整数值的递增和递减，并不是原子的，这可能会让许多读者感到惊讶。为什么这些简单的操作会造成巨大的麻烦？答案在于它们从 C# 语言角度来看的定义。

特别是，i++ 只是 i += 1 的简写，而后者又是 i = i + 1 的简写语法。注意我们忽略了这种自增表达式作为表达式来使用的能力。但基本事实仍然是，这些表达式是序列变更（mutation）操作的简写语法。正是在这里，运行时和操作系统获得了灵活性，它们可以在不希望的地方交错执行不同的线程，从而导致我们讨论过的问题。

### 递增与递减

但是，像“加一”这样的基本操作就一定要是非原子的吗？事实证明答案是否定的，这要归功于代码运行所在平台（或者更确切地说，JIT 编译到的平台）的指令集。这些指令通过 Interlocked 类暴露给托管代码开发人员。使用 Interlocked 上的静态方法，我们可以将计数器示例重写如下：

```csharp
static void Main()
{
    int n = 0;

    var up = new Thread(() =>
    {
        for (int i = 0; i < 1000000; i++)
            Interlocked.Increment(ref n);
    });

    up.Start();

    for (int i = 0; i < 1000000; i++)
        Interlocked.Decrement(ref n);

    up.Join();
    Console.WriteLine(n);
}
```

Increment 和 Decrement 方法通过 ref 参数接收要变更的值。这些方法提供的保证是操作以原子方式完成，因此其他线程无法观察到中间状态。这里给出的计数器同步问题解决方案是迄今为止最高效的。

从某种意义上说，这是多线程上执行的代码的互斥（mutual exclusion）的一个病态案例，我们非常幸运这些操作能够以互锁（interlocked）方式完成。如果不是这种情况，就必须使用锁（lock）或互斥量（mutex）。其他一些简单操作也有对应的互锁版本，例如通过 Add 方法暴露的加（或减）一个值。然而，以互斥方式从不同线程调用整个方法则需要使用锁。

### （比较并）交换

大量对性能要求极高的多线程代码（例如操作系统内核等中的代码）可以利用一些专门的互锁操作。一种常见的操作是以原子方式交换两个内存位置的内容，可以附带条件，也可以不带条件。

我们先来看两者中较简单的一个：通过 Interlocked.Exchange 方法重载公开的“互锁交换”操作。下面显示了用于 32 位整数值的重载：

```
public static int Exchange(ref int location1, int value);
```

这里，location1 参数引用的是要变更的值，通过将第二个参数中指定的值赋给它来实现变更。该方法返回从 location1 读取的原始值：

```
int value = 24;
Console.WriteLine(value); // Prints 24
Console.WriteLine(Interlocked.Exchange(ref value, 42)); // Prints 24
Console.WriteLine(value); // Now prints 42
```

这种原始操作在各种情况下都会派上用场。在 MSDN 文档中，展示了一个使用 Exchange 方法实现的简单锁。有关更多信息，请参阅该文档。

一个相关的操作称为“比较并交换”，它所做的工作比我们刚才看到的交换操作略多一些。下面显示了用于整数值的一个重载：

```
public static int CompareExchange(ref int location1, int value, int comparand);
```

其思想是这样的：在将 location1 中的值与第二个参数中指定的值交换之前，先将 location1 中的原始值与 comparand 进行比较。如果两者相等，则执行交换操作；如果不相等，则什么都不做。无论哪种情况，该方法都会返回从 location1 读取的原始值。

当我们希望在状态符合预期时执行值交换时，这个方法就很有用。其思想是，当另一个线程有机会在我们线程执行交换之前改变状态时，我们希望以原子方式执行检查和交换操作。使用 if 语句不会

