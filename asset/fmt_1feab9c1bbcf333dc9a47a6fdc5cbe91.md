
```csharp
public void addtext2(string s)
{
    if (this.textBox1.InvokeRequired)
    {
      Delegate_addtext d = new Delegate_addtext(addtext2);
      this.Invoke(d, new object[] { s });
    }
    else
    {
      this.textBox1.Text += s + Environment.NewLine;
    }
}
```

每个线程的 `for` 循环现在只需调用 `addtext2`，而无需担心 `invoke` 或 UI 线程：

```
addtext2(i.ToString());
```

也就是说，新的 `addtext2` 方法会判断它应该是被调用还是被 `invoke`，如果需要被 `invoke`，它会将自己封装为委托，并使用 `invoke` 在 UI 线程上运行自身。

如果你想给 UI 线程留出处理事件的时间，在更新文本框后添加：

`Application.DoEvents();` 是一个好主意，但仅适用于 Windows Forms，因为 WPF 使用的是完全不同的调度系统，且不支持类似于 `DoEvents` 的方法。

## 异步调用 (Asynchronous calls)

在创建控件的线程上运行委托的 `BeginInvoke/EndInvoke` 方法也适用于从线程池线程中运行任何委托。

你所做的仅仅是将方法封装在委托中，并使用委托类实现的 `BeginInvoke/EndInvoke` 即可。

例如，我们可以构造两个委托，执行与之前定义的线程 `T1` 和 `T2` 相同的任务：

```csharp
delegate void AsyncTask();
AsyncTask T1 = delegate()
{
    for (int i = 0; i < 999; i++)
    addText2(i.ToString());
}
```

```csharp
AsyncTask T2 = delegate()
{
    for (int i = 999; i > 0; i--)
    addText2(i.ToString());
}
```

其中 `addText2` 在之前定义，并使用 `Invoke` 在 UI 线程上运行内容。

我们可以使用委托的 `Invoke` 方法来同步运行它们，即在它们创建的同一个线程（即 UI 线程）上运行。

- `T1.Invoke();`
- `T2.Invoke();`

在这种情况下，`T1` 在 `T2` 开始之前就会完成。若要在单独线程上运行它们（即异步运行），我们将 `Invoke` 更改为 `BeginInvoke`：

- `IAsyncResult R1 = T1.BeginInvoke(null, null);`
- `IAsyncResult R2 = T2.BeginInvoke(null, null);`
- `T1.EndInvoke(R1);`
- `T2.EndInvoke(R2);`

`EndInvoke` 方法仅仅是等待委托完成。

如果你尝试这样做，你会发现它不起作用。所发生的情况是整个程序在第一个 `EndInvoke` 处挂起——尝试在继续阅读之前弄清楚为什么。

原因是，当线程调用 `addText2` 时，执行会切换到 UI 线程，但 UI 被阻塞等待任务结束，并且没有处理该委托！

这是一个典型的死锁示例——两个线程（UI 和 `T1` 或 `T2` 中的任一）都在等待对方执行被对方所阻塞的操作。解决方案很简单——不要阻塞 UI 线程。不幸的是，不阻塞 UI 线程的最简单方法是使用回调方法在线程完成后进行清理，而这并不总是简单的。

例如，一个可以清理两个线程的合适回调委托：

```csharp
AsyncCallback C = delegate(IAsyncResult ar)
{
    AsyncTask T = (AsyncTask)ar.AsyncState;
    T.EndInvoke(ar);
};
```

为了使此生效，我们需要调用异步委托，并将回调和委托本身作为 `ar` 参数传递：

```
IAsyncResult R1 = T1.BeginInvoke(C, T1)
IAsyncResult R2 = T2.BeginInvoke(C, T2);
```

经过此更改后，一切运行如如所示。

## Invoke 模式 (The Invoke Pattern)

你可能会疑惑为什么使用 `Invoke` 在 UI 线程上运行 UI 对象。为什么不简单使用一个线程来同步对每个控件的访问，以便每次只有一个线程更新控件？只要每个线程在下一个线程开始之前完成，就不会有让控件处于奇怪的半完成状态的危险。

采用 `invoke` 方法的原因仅仅是，UI 线程会在需要时访问控件，而且它不会遵守你创建的任何线程的规则，这意味着你无法通过锁将控件的访问限制在单个线程上，UI 线程会直接忽略它们。要让锁工作，所有尝试访问资源的线程必须遵守锁定机制。任何不遵守规则的线程都会破坏整个大局。

然而，`Invoke` 可以被实现为强制线程在访问对象时表现良好。对象可以测试是哪个线程在访问，并可以强制其使用 UI 线程。这种 `Invoke` 模式足够实用，让我们知道如何使用它。

你可以看到 `AutoResetEvent` 允许一组线程等待信号（即被调用），并且每次只有一个线程启动。

点构造函数必须创建一个委托（在此情况下称为 `doInvoke`），它可以在自己的线程上运行该委托，以便让被调用的方法在线程 T 上运行：

```csharp
public Point()
{
    ThreadStart.WaitInvoke = delegate ()
    {
        do {
            autoEvent.WaitOne();
            d.DynamicInvoke(null);
        } while (true);
    };
}
```

注意，`doInvoke` 设计为在线程 T 上运行，而不是当前线程。在 `doInvoke` 中发生的情况是线程被立即挂起，等待另一个线程设置 `AutoResetEvent` 对象来唤醒。也就是说，将用于 `Invoke` 方法的线程被挂起，以等待方法运行。当这种情况发生时，我们假设 `_d` 中存储了一个已准备好被调用的委托。我们必须使用 `DynamicInvoke`，因为我们不知道该委托的实际形式是什么，因此它必须被绑定。`DynamicInvoke` 方法简单地在当前线程上运行该委托，也就是说它类似于对委托封装的方法进行动态调用。构造函数的其余部分创建了处于未设置状态 `AutoResetEvent`，然后创建并启动线程 T，将其交给 `doInvoke` 委托以运行：

```csharp
autoEvent = new AutoResetEvent(false);
T = new Thread(doInvoke);
T.Start();
```

你现在可以看到这一切是如何运作的，但它们如何结合在一起是非常复杂的。我们启动了一个运行我们的 `doInvoke` 的新线程，它只是在等待 `AutoResetEvent` 设置之前运行 `_d` 中的委托。`doInvoke` 委托只会在线程 T 上运行，在大多数时间内它处于挂起并等待被唤醒。当它被唤醒时，它运行在 `_d` 中找到的任何委托，然后再次睡眠。

缺失的是负责设置委托和唤醒线程的 `invoke` 方法：

```csharp
public void invoke(Delegate d)
{
    d = d;
    autoEvent.Set();
    do
    {
        Application.DoEvents();
    } while (T.ThreadState == ThreadState.Running);
}
```

`invoke` 方法简单地存储要调用的委托，并使用 `autoEvent` 信号线程 T 开始运行。由于 `invoke` 是阻塞的，它随后进入循环以等待被调用的委托完成，线程 T 再次挂起。

你可以看到，要将 `BeginInvoke` 实现为非阻塞的 `invoke`，你所做的只是立即返回。

这就是 `Point` 类中 `invoke` 实现的全部内容。我们现在只需要一些代码来尝试它，这非常简单。首先，我们创建一个点 实例：

```csharp
point p = new Point();
```

我们还需要一个要调用的委托：

```csharp
asyncTask update = delegate()
{
    p.x = 10;
    p.y = 20;
}
```

最后我们调用它：

```
p.invoke(update);
```

当 `invoke` 返回时，`Point` 对象的 `x` 和 `y` 属性被设置为 10 和 20 —— 这是通过 T 运行 `update` 委托完成的。

将这些想法扩展到传递参数的委托容易得多——只需像标准 `Invoke` 那样使用对象数组即可。到非阻塞 `invoke` 的扩展更为复杂，因为你必须考虑到可能会有多个委托被队列等待执行。是的，你需要一个队列来存储所有待处理的委托。这增加了复杂性，因为你必须控制对队列的访问，并安排线程 T 在每次被唤醒时清空队列。细节上更复杂，但原理是相同的。

正确掌握 `invoke` 模式和异步 `invoke` 模式可能是困难的，但如果你试图提供供他人使用的对象，那么这是非常值得的。

# 结语

`invoke` 模式是一种管理其他线程与 UI 交互的非常简单的方法。它减少了其他线程操作 UI 事件的需求，从而将它们与其他所有交互置于同一水平。

# 第 17 章

## 异步等待

.NET 中的 `async/await` 异步编程设施解决了其长期以来存在的问题之一——如何编写一个正确使用 UI 的优雅应用程序。但为了避免问题，你仍然需要理解问题和解决方案。

正如我们在上一章中看到的，任何 Windows Forms、WPF 或 MAUI 程序员面临的最大问题之一是，你不能使用 UI 线程完成大量工作。如果你这样做，结果就是应用程序无响应。正确的解决方案是使用新线程来完成所有繁重计算，并将 UI 线程空出来处理它应该处理的事情，即用户事件。然而，计算通常必须提供证据证明它已经完成了某些工作，这意味着它必须与 UI 组件交互。

众所周知，UI 组件不是线程安全的——因此有了规则：创建组件的线程可以访问它。你可以选择性关闭此规则并允许工作线程访问 UI，但这不是一个好主意。正如上一章描述的，允许工作线程访问 UI 的正确方法是在工作线程中使用 `Invoke` 方法，请求 UI 线程运行一个委托，该委托使用工作线程提供的数据进行更新。这可能是正确的方法，但它会导致代码非常混乱，鉴于这是一个常见需求，我们可以用更简单的方法来实现两个或多个线程与 UI 协作，而 `async` 和 `await` 正是发挥作用的地方。`Invoke` 方法允许工作线程在 UI 上运行代码。这种方法的处是允许工作线程在有需要时与 UI 交互。问题是正如代码所示它会保持 UI 线程忙碌直到它完成。那就是：

```csharp
void DoWork()
{
    for (int i = 0; i < 10; i++)
    {
        Thread.Sleep(500);
    }
}
```

让 UI 线程忙碌 5 秒并且要使用 `Thread.Sleep` 你还需要添加：

```
System.Threading;
```

没有 `async/await`，唯一的选择是阻塞 UI 线程让工作线程执行，或者提供一个回调让 UI 线程处理结果。这就是“当你准备好了我就回来找你”机制。

### 动手示例

启动一个新的 Windows Forms 项目并放置两个文本框和一个按钮——按钮将启动该过程，文本框将记录其进度。给出的示例在 WPF 中也可以完美运行，只需更改控件和名称。

首先，让我们看看我们试图解决的问题。按钮的点击事件处理程序调用了一个执行工作的方法：

```csharp
private void button1_Click(object sender, EventArgs e)
{
    textBox.Text = "Click Started";
    DoWork();
    textBox2.Text = "Click Finished";
}
```

你可以看到前两个文本框被更改以显示正在发生的情况。对于本示例而言，`DoWork` 可以由一个不断循环并占用线程的例程来模拟。对于结果相同，`DoWork` 可以简单地等待 I/O 操作完成——重要的点是，正如代码所示，它会保持 UI 线程的关注直到它完成。这让 UI 线程忙碌 5 秒。你认为当你运行此程序时会看到什么？如果不熟悉单线程 UI 配合分发器（dispatcher）工作的方式，你可能会认为你看到 `Click Started` 出现，然后在5 秒后出现 `Click Finished`。实际上发生的是，你看到两条消息在5 秒后同时出现。

几秒钟过去了，期间 UI 冻结状态。这种行为的原因仅仅是因为从 `DoWork` 方法被调用的一刻起 UI 就冻结了，而通常发生在“Click Started”文本渲染到显示器之前。这正是为什么你不希望在 UI 线程上进行任何密集计算的原因——你根本不想在 UI 线程上进行任何计算！理想的 UI 线程大部分时间应该是空闲的，准备好响应用户的输入。

### Async 和 Await

现在我们可以看看如何使用 `async` 和 `await` 来实现此属性。首先要明确，任何在你前面加上 `async` 的方法都是异步方法，这意味着它可以被启动和停止，而不是仅仅从第一条指令运行到最后一条。我们可以创建一个新方法并将其标记为异步，但为了保持示例与上述的同步方法尽可能相似，我们可以直接将点击事件处理器改为异步方法：
