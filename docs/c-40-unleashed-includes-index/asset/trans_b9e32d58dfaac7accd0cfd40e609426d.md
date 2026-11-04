
个人而言，我认为如果你能在不知道错误来源的更大上下文的情况下，有意义地从未处理的异常中恢复，那是相当不可能且近乎超人的。如果你认为自己能做到，这个事件可能会对你有用。

## 延续

### 基本概念

虽然听起来很吓人，但延续其实是非常简单的构造。在深入探讨它们与任务结合使用的具体细节之前，让我们先从概念层面来探索它们。考虑以下这段命令式顺序同步代码：

```csharp
int c = Add(a, b);
Console.WriteLine(c);
```

这段代码调用了一个方法 Add，该方法在某个时刻返回 a 和 b 的和，我们接收它并可以继续使用（例如，打印到屏幕上）。让我们检查一下这段代码的几个方面。

首先，注意顺序在代码中扮演的重要角色：Console.WriteLine 方法的调用必须等到 Add 返回后才能进行。像 C# 这样的语言中的分号语法在语法上明确体现了顺序执行的特性。

其次，与前一点相关，这段代码本质上是同步的：在 Add 返回之前，你什么也做不了，只能等待，然后才能进行其他工作。虽然这似乎与顺序的概念相关，但我们仍然可以在不同步的情况下保持顺序。这就是延续发挥作用的地方。

在延续传递风格（CPS）中，前面的代码片段被改写为以下风格，乍一看可能有点奇怪：

```csharp
Add(a, b, c => {
    Console.WriteLine(c);
});
```

现在我们调用方法 Add，它不仅接收两个输入，还接受一个回调参数来接收计算结果。Add 的计算完成后，执行将在此处继续（因此得名延续）。以下是 Add 方法的实现：

```csharp
static void Add(int a, int b, Action<int> continueWith)
{
    continueWith(a + b);
}
```

注意我们仍然有操作的顺序：首先，a 和 b 相加，然后将结果传入延续函数，延续函数在加法完成后运行。这些操作本质上仍然是顺序的。然而，这已不再是我们习惯于 C# 等语言中的分号式顺序。现在加法之后要执行的全部剩余代码都放在一个 lambda 表达式中。

经过这次转换后，一个本质上的差异变得明显：Add 的返回类型发生了变化。现在，Add 方法返回 void。这并不意味着我们丢失了加法的结果；结果将被传递给延续。

到目前为止，从同步的角度来看，我们并没有真正做任何不同的事情。这段代码仍然本质上是同步的：调用 Add 会计算其前两个参数的和，然后调用延续函数。然而，现在我们可以在 Add 方法中轻松引入并发来计算 a 和 b 的和，而不会阻塞 Add 的调用者。一旦该值可用，延续函数就可以被调用，即使是在不同的线程上。在 CPS 的世界里，引入异步变得相当容易：

```csharp
static void Add(int a, int b, Action<int> continueWith)
{
    new Thread(() => continueWith(a + b)).Start();
}
```

### .NET Framework 中的隐藏延续

延续在 .NET Framework 中一直很突出，只是没有被这样称呼。其中最好的例子可能是异步方法调用模式，我们可以使用委托上的 BeginInvoke 和 EndInvoke 来说明：

```csharp
Func<int, int, int> add = (a, b) => a + b;
add.BeginInvoke(3, 4, iar =>
{
    int c = add.EndInvoke(iar);
    Console.WriteLine(c);
}, /* state */ null);

// The main thread can continue asynchronously while the delegate is being
// invoked. At some point the AsyncCallback continuation will be called.
```

如果只有一个延续，如前一节示例所示，通常会使用流畅接口模式，将顺序的延续串联成一条长链：

```csharp
Task<int>.Factory.StartNew(() => 42)
.ContinueWith(t => t.Result / 2)
.ContinueWith(t => t.Result.ToString())
.ContinueWith(t => Console.WriteLine("42 / 2 = " + t.Result));
```

如果你将所有错误处理或取消处理逻辑放在延续函数内部，这种方式效果很好。然而，如果你想针对任务可能完成的不同的状态采取不同的延续操作，就必须使用第一种将任务分配给临时变量的风格来指定多个延续。这两种风格在图 30.5 中进行了对比。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1550_0.png)

图 30.5 顺序与并行延续。

创建新延续时可以指定的一些延续选项标志如下：

- NotOn* 标志会阻止延续在前置任务的指定状态为真时运行。该系列标志的后缀包括 Faulted、Canceled 和 RanToCompletion。
- OnlyOn* 标志针对与上一要点相同的三个状态，仅在前置任务以指定状态完成时才调用延续。
- ExecuteSynchronously 使延续在前置任务完成的线程上同步运行。此选项仅应在延续运行时间很短时使用。

其他延续选项与 TaskCreationOptions 相同，允许指定公平性偏好、长时间运行提示，或将任务附加到其父任务。

以下代码片段展示了一个具有两个延续的任务，一个用于成功，一个用于失败：

```csharp
var answer = Task<int>.Factory.StartNew(() => {
    // Left to the reader: Compute a value "res"; may throw.
    return res;
});

answer.ContinueWith(t => {
    // Will only be called in success cases.
    Console.WriteLine(t.Result);
}, TaskContinuationOptions.OnlyOnRanToCompletion);

answer.ContinueWith(t => {
    // Will only be called in error cases. Handle any exception we can handle.
    t.Exception.Flatten().Handle(ex => {
        // See section "Exploring AggregateException" for more information.
        return false;
    });
}, TaskContinuationOptions.OnlyOnFaulted);
```

## C#（和 Visual Basic）的未来

最有可能出现在 C# 未来版本中的一个特性是对编写看起来像顺序的命令式异步代码的支持。任务上的延续构成了将异步调用链接在一起的底层机制。由于其基于回调的底层特性，代码往往被翻转，变成包含大量错误检查代码的延续 lambda。

C# 5.0 和 VB 11.0 中提出的新 async 特性允许基于名为 await 的新表达式编写看起来像命令式的代码：

```csharp
public async Task<int> CountWords(string url)
{
    string text = await DownloadStringAsync(url);
    return text.Split().Length;
}
```

这里，DownloadStringAsync 方法被假定返回 Task<string>。通过对该任务执行 await 操作，编译器会将方法中剩余的代码转换为该任务上的延续。这只是冰山一角：所有命令式构造，如分支和循环，都可以在异步方法中使用。在内部，编译器生成一个延续的状态机，就像 C# 2.0 及更高版本中的迭代器一样。

有关更多信息，请在网上搜索“Visual Studio Async CTP”

总之，延续用于将异步计算链接在一起。如下一节所述，取消延续也是可能的。鉴于此选项以及处理异常的能力，延续为异步计算链中的顺序点提供了支持。
