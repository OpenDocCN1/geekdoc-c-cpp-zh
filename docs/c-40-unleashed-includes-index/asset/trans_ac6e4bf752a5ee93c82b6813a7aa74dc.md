
因为你需要对 handlers 的引用来引用其 OnShutDown 方法，所以只有在存在对 handlers 的引用时才能这样做。移除事件处理程序的那一行创建了一个新的委托实例，该实例引用 handlers 上的 OnShutDown，并且该实例由 Delegate.Remove 方法在多播委托的调用列表中定位。简而言之，不要忘记取消挂钩你的事件处理程序。

如果这一切吓得你魂飞魄散，也不用太担心。虽然这个问题确实存在（我们的示例已证明），但它并不常见。所描述问题的核心在于，我们在另一个不拥有引发事件的对象上处理事件。在我们的例子中，我们甚至使用静态事件来构造一个糟糕的场景。为什么事件源的“所有权”很重要？好吧，考虑下面所示的 Windows Forms 窗体的情况：

```csharp
class LoginForm : Form {
    private Button login;

    public LoginForm() {
        login = new Button { Text = "Log in" };
        login.Click += login_Click;
    }

    private void login_Click(object sender, EventArgs e) { /* TODO */ }
}
```

这里，窗体实例拥有登录按钮对象。窗体为按钮的 Click 事件附加了一个事件处理程序，而该处理程序位于窗体实例本身上。实际上，构造函数的第三行可以读作如下：

```csharp
login.Click += this.login_Click;
```

因此，带有事件处理程序的“事件接收器”（窗体）与事件源（按钮）的所有者相同。一旦窗体对象变得无法访问，其所有控件及其事件处理程序也随之无法访问。如图 18.12 所示，这使得可以回收窗体及其控件。另一方面，前面示例（显示在图 18.12 底部）会造成问题，如前所述。

## 使用 SOS 追踪泄漏

.NET Framework 附带了一个名为 SOS（即 "Son of Strike"）的低级调试器扩展，可在 Visual Studio 中加载以进行高级调试。它能帮助的众多事情之一就是定位内存泄漏的来源。

调试我们内存泄漏的一个示例会话显示在图 18.13 中。在第一行，SOS 扩展从 .NET Framework 所在的文件夹加载。

假设我们已经知道某个 Handlers 实例正在泄漏，我们发出 !dumpheap 命令在托管堆中搜索指定类型的对象。我们恰好找到该类型的一个实例，并想知道是什么让它保持存活。给出其报告的地址，!GCRoot 就能解决问题。

GCRoot 命令追踪保持对象存活的引用路径（即证明代码如何仍能访问它）。对于我们怀疑的 Handlers 对象，追踪看起来像 System.Action -> Handlers。（将箭头读作“引用”。）

由此，我们清楚地看到一个 Action 委托仍引用着 Handlers 对象。在某些情况下，这已足以作为线索，开始查找本应移除但未移除事件处理程序的地方。如果需要更多信息，你可以转储 Action 委托以查看其目标方法等等。

在网上搜索术语 GCRoot、SOS 和 event，以了解更多关于使用 SOS 调试此处所示的此类对象泄漏的信息。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_885_0.png)

## 图 18.12 拥有事件源对象对事件处理程序的使用很有帮助。

由于这个问题已被认为是 .NET 应用程序内存问题的主要来源之一，WPF 添加了“弱事件”模式。我们在此不展开说明，但在使用 WPF 时，你可能希望在 MSDN 上更深入地研究这个问题。

取消挂钩事件处理程序看起来相当直接，只需使用 -= 运算符即可。虽然这是事实，但由于 C# 2.0 中引入匿名函数表达式以及 C# 3.0 中引入 lambda 表达式，存在一个需要注意的地方。之前我们见过这样的代码：

![](img/a16f85e62ce9bdc527f4b09dbfe26092_886_0.png)

## 图 18.13 使用 SOS 分析内存泄漏。

```csharp
var countDown = new CountDown(5);

// Hook up event handlers, using lambda expressions
countDown.Tick += currentSecond => Console.WriteLine(currentSecond);
countDown.Finished += () => Console.Beep();

countDown.Start();
```

鉴于我们关于事件处理程序的讨论，出于遵循最佳实践的考虑，我们可能希望取消挂钩 Tick 和 Finished 事件处理程序。首先要问的问题是何时适合这样做。显然，在事件仍可能被引发时不应取消挂钩，但我们知道在 Finished 事件被引发后不会再有进一步的事件（尽管这种“协议”应由 CountDown 类型的提供者真正记录下来）。这使得 Finished 事件处理程序内部的代码成为取消挂钩 Tick 事件处理程序以及其自身的合适位置。现在更紧迫的问题是如何实现这一点。

要准确回答这个问题，让我们先退一步。因为我们知道事件不过是伪装的多播委托，我们可以使用一个普通的多播委托作为实验的培养皿。看看下面的代码片段，我们在其中使用方便的 lambda 表达式语法使事情更简洁：

```
Action evt = null;
evt += () => Console.WriteLine("Hello");
if (evt != null)
    evt();
evt -= () => Console.WriteLine("Hello");
if (evt != null)
    evt();
```

小测验：它会打印多少次 Hello？如果你说一次，再想想；答案是两次。虽然看起来我们在第二行和第四行添加和移除的是同一个事件处理程序，但它们并不是同一个对象。回想一下匿名函数在底层编译成什么：包含匿名函数表达式中指定代码的编译器生成方法：

```
Action evt = null;
evt += new Action(__AnonymousMethod1);
if (evt != null)
    evt();
evt -= new Action(__AnonymousMethod2);
if (evt != null)
    evt();
```

两个匿名函数表达式会导致编译器生成两个不同的方法，即使它们内部的代码相同。编译器本可以更聪明一些，检测“语义相同”的匿名函数表达式并为它们共享同一个对象。然而，这实现起来相当棘手，编译器编写者认为还有更重要的事情需要处理。

因为我们在添加和移除委托时使用了两个不同的方法，所以 += 和 -= 操作不会相互抵消。解决此问题的方法是使用中间变量：

```
Action evt = null;
Action handler = () => Console.WriteLine("Hello");
evt += handler;
if (evt != null)
    evt();
evt -= handler;
if (evt != null)
    evt();
```

为了能够取消挂钩我们的 CountDown 事件处理程序，我们必须将它们提升为局部变量，如刚才所示：

```csharp
var countDown = new CountDown(5);

// Hook up event handlers
Action<uint> tickHandler = currentSecond => Console.WriteLine(currentSecond);
Action finishedHandler = () => {
    Console.Beep();

    // Finished has been called: we can unhook both Tick and Finished now.
    countDown.Tick -= tickHandler;
    countDown.Finished -= finishedHandler;
};

countDown.Tick += tickHandler;
countDown.Finished += finishedHandler;

countDown.Start();
```

前面的代码几乎正确；只是还不能编译。概念上，一切看起来都是正确的：我们首先创建类型为 Action 的处理程序委托，然后使用常规 += 语法稍后挂钩它们。在 Finished 事件处理程序内部，我们可以根据对 CountDown 事件协议的了解再次取消挂钩它们。

剩余的问题（阻止我们编译前述代码）相当微妙。仔细看看 finishedHandler lambda 表达式。在定义它的同时，我们在最后一行在其自己的主体内部使用它。用更技术性的术语来说，我们正在定义一个递归 lambda 表达式，而语言在此语法形式下不允许这样做，如图 18.14 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_888_0.png)

## 图 18.14 递归 lambda 表达式让编译器不满意。
