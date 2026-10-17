
```csharp
using System.Threading.Tasks;

public class Program
{
    public static void Main()
    {
        DisplayStatus("Before");
        Task taskA =
            Task.Run(() =>
                DisplayStatus("Starting..."))
            .ContinueWith( antecedent =>
                DisplayStatus("Continuing A..."));

        Task taskB = taskA.ContinueWith( antecedent =>
            DisplayStatus("Continuing B..."));

        Task taskC = taskA.ContinueWith( antecedent =>
            DisplayStatus("Continuing C..."));

        Task.WaitAll(taskB, taskC);
        DisplayStatus("Finished!");
    }

    private static void DisplayStatus(string message)
    {
        string text = string.Format(
            $@"{ Thread.CurrentThread.ManagedThreadId 
              }: { message }");
        Console.WriteLine(text);
    }
}
```

#### 输出 19.8

```
1: Before
3: Starting...
4: Continuing A...
3: Continuing C...
4: Continuing B...
1: Finished!
```

这个输出值得注意的是，线程 ID 有时会改变，有时又会重复。在这种普通的控制台应用程序中，同步上下文（可从 `SynchronizationContext.Current` 访问）为 `null`——默认的同步上下文导致线程池处理线程分配。这解释了为什么线程 ID 在任务之间会改变：有时线程池确定使用新线程更高效，有时它决定最好的行动是重用现有线程。

幸运的是，对于同步上下文至关重要的应用程序类型，它会自动设置。例如，如果创建任务的代码在由 ASP.NET 创建的线程中运行，该线程将有一个类型为 *AspNetSynchronizationContext* 的同步上下文与之关联。相反，如果你的代码在 Windows UI 应用程序（Windows Presentation Foundation [WPF] 或 Windows 窗体）中创建的线程中运行，该线程将有一个 *DispatcherSynchronizationContext* 的实例与之关联。（对于控制台应用程序，默认情况下没有同步上下文。）由于 TPL 咨询同步上下文，且同步上下文会根据执行环境的变化而变化，TPL 能够调度在既高效又安全的环境中执行的延续。

为了修改代码以利用同步上下文，你必须 (1) 设置同步上下文，并且 (2) 使用 *async / await*，以便咨询同步上下文。可以定义自定义同步上下文并与现有同步上下文合作，以提高某些特定场景下的性能。然而，描述如何做到这一点超出了本书的范围。

### 在 Windows UI 中使用 async/await

同步特别重要的一个领域是 UI 和 Web 编程的上下文。例如，在 Windows UI 中，消息泵处理诸如鼠标点击和移动事件等消息。此外，UI 是单线程的，因此与任何 UI 组件（例如文本框）的交互必须始终从单个 UI 线程发生。*async / await* 模式的一个主要优点是，它利用同步上下文来确保延续工作——出现在 *await* 语句之后的工作——始终将在调用 *await* 语句的同一个同步任务上执行。这种方法意义重大

1. 从技术上讲，它是一个可等待类型，如题为“等待非 Task<T> 值”的高级主题中所述。
2. 示例请参阅 *《C# 5.0 之前的多线程模式》* 中的清单 C.8，可在 https://IntelliTect.com/EssentialCSharp 获取。
3. 关于如何设置线程的同步上下文以及如何使用任务调度器将任务调度到该线程的简单示例，请参阅 *《C# 5.0 之前的多线程模式》* 中的清单 C.8，可在 https://IntelliTect.com/EssentialCSharp 获取。

其价值在于，它消除了显式切换回 UI 线程以更新控件的需要。

为了更好地理解这一优势，请考虑 WPF 中按钮点击 UI 事件的示例，如清单 19.23 所示。

## 清单 19.23：WPF 中的同步高延迟调用

```csharp
using System;
private void PingButton_Click(object sender, RoutedEventArgs e)
{
    StatusLabel.Content = "Pinging...";
    UpdateLayout();
    Ping ping = new Ping();
    PingReply pingReply = ping.Send("www.IntelliTect.com");
    StatusLabel.Text = pingReply.Status.ToString();
}
```

已知 `StatusLabel` 是一个 WPF 的 `System.Windows.Controls.TextBlock` 控件，并且我们在 `PingButton_Click()` 事件订阅者中两次更新了 `Content` 属性，因此可以合理假设：首先会显示“Pinging...”，直到 `Ping.Send()` 返回，然后标签会更新为 `Send()` 回复的状态。然而，正如熟悉 Windows UI 框架的人所熟知的那样，实际发生的情况并非如此。相反，一条消息被发布到 Windows 消息泵中，用于将内容更新为“Pinging...”，但由于 UI 线程正忙于执行 `PingButton_Click()` 方法，Windows 消息泵并未得到处理。等到 UI 线程空闲下来查看 Windows 消息泵时，第二个 `Text` 属性更新请求已被排队，因此用户能够观察到的唯一消息是最终的状态。

若要使用 TAP 修复此问题，我们修改了清单 19.24 中高亮的代码。

## 清单 19.24：使用 await 的 WPF 同步高延迟调用

```csharp
using System;
async private void PingButton_Click(object sender, RoutedEventArgs e)
{
    StatusLabel.Content = "Pinging...";
    UpdateLayout();
    Ping ping = new Ping();
    PingReply pingReply = await ping.SendPingAsync("www.IntelliTect.com");
    StatusLabel.Text = pingReply.Status.ToString();
}
```

这一更改带来了两个优势。首先，`ping` 调用的异步特性释放了调用者线程，使其返回到 Windows 消息泵的调用者同步上下文，并处理对 `StatusLabel.Content` 的更新，从而使用户看到“Pinging…”。其次，当等待 `ping.SendTaskAsync()` 完成时，它始终会在与调用者相同的同步上下文中执行。此外，由于同步上下文专门适用于 Windows UI，它是单线程的，因此返回总是回到同一线程——即 UI 线程。换句话说，TAP 不会立即执行延续任务，而是咨询同步上下文，后者将关于延续工作的消息发布到消息泵。接下来，由于 UI 线程监控消息泵，在拾取延续工作消息后，它会调用 `await` 调用之后的代码。（结果是，延续代码的调用发生在处理消息泵的同一线程上，与调用者线程相同。）

TAP 语言模式中内置了一个关键的代码可读性特性。请注意清单 19.24 中，返回 `pingReply.Status` 的调用在 `await` 之后自然地流动，清晰地表明它将在上一行之后立即执行。然而，从头开始编写实际发生的内容会因多种原因而更难理解。

### await 运算符

在一个方法中放置 `await` 的次数没有限制。事实上，这些语句并不限于一个接一个地出现。相反，`await` 语句可以放在循环中并依次连续处理，从而像代码外观那样遵循自然控制流。请考虑清单 19.25 中的示例。

![](img/ef6a8a417630b222bfb3f3b949facff0_880_0.png)

## 清单 19.25：迭代 await 操作

```csharp
async private void PingButton_Click(object sender, RoutedEventArgs e)
{
    List<string> urls = new List<string>()
    {
        "www.habitat-spokane.org",
        "www.partnersinl.org",
        "www.iaassist.org",
        "www.fh.org",
        "www.worldvision.org"
    };
    IPStatus status;
    Func<string, Task<IPStatus>> func = async (localUrl) =>
    {
        Ping ping = new Ping();
        PingReply pingReply = await ping.SendPingAsync(localUrl);
        return pingReply.Status;
    };
    StatusLabel.Content = "Pinging…";
    foreach(string url in urls)
    {
        status = await func(url);
        StatusLabel.Text = $@"{ url }: { status.ToString() } ({ Thread.CurrentThread.ManagedThreadId })";
    }
}
```

无论 `await` 语句是在迭代内发生还是作为独立条目，它们都会串行执行，一个接一个，并且按照从调用线程调用的相同顺序执行。底层实现是将它们在语义上串联起来，类似于 `Task.ContinueWith()`，不同之处在于 `await` 运算符之间的所有代码都将在调用者的同步上下文中执行。

UI 对 TAP 的支持是促使 TAP 创建的关键场景之一。第二个场景发生在服务器端，当客户端请求查询数据库中的一整个表的数据时。由于查询数据可能耗时较长，应该创建一个新的线程，而不是消耗线程池中分配的有限数量的线程。这种方法的缺点在于，查询数据库的工作完全在另一台机器上执行。考虑到线程通常本来就不活跃，没有理由阻塞整个线程。

总之，TAP 的创建旨在解决以下关键问题：

- 需要允许长时间运行的活动发生，而不阻塞 UI 线程。
- 考虑到线程所做的只是等待活动完成，为非 CPU 密集型工作创建新线程（或 `Task`）相对来说是昂贵的。
- 当活动完成时（无论是使用新线程还是通过回调），通常有必要进行线程同步上下文切换，以回到发起活动的原始调用者。
- TAP 提供了一种新的模式，适用于 CPU 密集型和非 CPU 密集型的异步调用——所有 .NET 语言都明确支持这种模式。

![](img/ef6a8a417630b222bfb3f3b949facff0_882_0.png)

顺便一提，在 C# 5.0 和 6.0 中有一个限制，`await` 不能出现在异常处理的 `catch` 或 `finally` 语句中。然而，从 C# 7.0 开始，这一限制已被移除。考虑到你可能会希望在调用堆栈中最外层的异常处理程序中记录异常，而记录日志是一个相对昂贵的操作，因此使用异步 `await` 来执行此操作是有益的，这一改进非常有帮助。

## 并行执行循环迭代

请考虑清单 19.26 中显示的 `for` 循环语句及相关代码，以及对应的输出 19.9。该清单调用了一个用于计算圆周率小数展开部分的方法，其参数是小数位数和起始位数。实际计算内容与讨论无关。这个计算有趣之处在于它非常容易并行化；也就是说，将一个大型任务——比如计算圆周率的 100 万位小数——分割成任意数量的小任务以并行运行，这是 remarkably 容易的。这类计算是最容易通过添加并行性来加速的。

## 清单 19.26：同步分片计算圆周率的 For 循环

```csharp
using System;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;
class Program
{
    const int TotalDigits = 100;
    const int BatchSize = 10;
    static void Main()
    {
        string pi = null;
        const int iterations = TotalDigits / BatchSize;
        for(int i = 0; i < iterations; i++)
        {
            pi += PiCalculator.Calculate(BatchSize, i * BatchSize);
        }
        Console.WriteLine(pi);
    }
}
using System;
class PiCalculator
{
    public static string Calculate(int digits, int startingAt)
    {
        // ...
    }
    // ...
}
```

## 输出 19.9

3.1415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679821480865132823066470938446095505822317253594081284811174502841027019385211055596446229489549303819644288109756659334461284756482337867831652712019091456485669234603486104543266482133936072602491412737548207381687188836920972445941050481623885791367954

`for` 循环同步且顺序地执行每次迭代。然而，由于圆周率计算算法将圆周率计算划分为独立的部分，因此没有必要按顺序计算这些部分。

只要结果按照正确的顺序追加即可。想象一下，如果该循环的所有迭代都能并发运行会发生什么：每个处理器都可以负责单个迭代，并与其他正在执行其他迭代的处理器并行运行。基于迭代的同时执行，我们可以根据处理器数量的增加进一步缩短执行时间。

TPL 提供了一种便捷的方法 `Parallel.For()`，正好可以实现这一目标。列表 19.27 展示了如何修改列表 19.26 中的顺序单线程程序以使用该辅助方法。

### 列表 19.27：并行分块计算圆周率

```csharp
using System;
using System.Threading.Tasks;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;
// ...
class Program
{
    static void Main()
    {
        string pi = null;
        const int iterations = TotalDigits / BatchSize;
        string[] sections = new string[iterations];
        Parallel.For(0, iterations, (i) =>
        {
            sections[i] = PiCalculator.Calculate(BatchSize, i * BatchSize);
        });
        pi = string.Join("", sections);
        Console.WriteLine(pi);
    }
}
```
