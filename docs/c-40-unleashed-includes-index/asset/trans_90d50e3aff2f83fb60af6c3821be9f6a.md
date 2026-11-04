
## 使用 IntelliTrace 进行历史调试的插曲

当我们身处托管代码应用程序调试的奇妙世界时，应该看看 Visual Studio 2010 新增的一项功能：IntelliTrace。在上一节的示例中，我们处理的是一个在程序开始失败之前很久就被不恰当地吞掉的异常。如果能将程序的执行回溯到过去，以调查当前调用堆栈范围之外的程序状态，岂不是非常方便？这正是 IntelliTrace 所能实现的。

要体验这个令人兴奋的新功能，我们首先需要通过“工具”->“选项”对话框进行配置，在树视图中的 IntelliTrace 节点下。有两种模式可用；后一种称为“诊断事件和调用信息”，是最强大的。图 23.10 显示了下一个实验所需的设置。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1212_0.png)

图 23.10 配置新的 IntelliTrace 功能。

暂时禁用首次异常，我们将在正确配置历史调试功能的情况下执行同一个程序。在因 NullReference 异常而崩溃的位置，通过“调试”->“IntelliTrace”->“调试历史调用”菜单使 IntelliTrace 窗口可见（如果尚未可见）。这将显示图 23.11 所示的视图。

在这里观察几点。此时，IntelliTrace 显示的信息与你在“调用堆栈”窗口中看到的信息大致相同：调试器在方法 A 中的异常处停止，Main 方法位于堆栈更上方。然而，从这个视图中，我们可以开始进行时间旅行。使用代码编辑器边距中的按钮，可以返回到历史调试器记录的上一个事件。到目前为止，还没有什么太令人兴奋的；这只会让我们回到 Main 方法对 A 的调用。

神奇之处在于，当我们回到 Main 方法对 B 的调用时；现在我们可以根据已收集的 IntelliTrace 信息步入 B。不仅如此，该技术还使我们能够通过重放已收集的事件来调试对 B 的调用。图 23.12 显示了在调用 B 处代码编辑器边距中的不同选项。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1213_0.png)

图 23.11 崩溃点处的调试历史。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1213_1.png)

图 23.12 我们不仅可以沿调用堆栈向上走，还可以步入其他路径。

在调试应用程序时，当你完全不知道无效的程序状态源自何处，这项新功能非常方便。

## 为什么日志记录很重要

使用 IntelliTrace 不应成为在代码中省略有用的跟踪和诊断的理由（例如，将程序执行期间的重要事件写入日志文件），因为总有一天你会遇到未启用 IntelliTrace 的实时崩溃。

## 何时捕获以及捕获什么

正确处理异常是框架和应用程序开发人员的巨大责任。仅凭这一点，给出关于何时捕获以及捕获什么的指导就很重要。

让我们从后一个问题开始：捕获哪些异常。你首先想知道所使用的 API 可能抛出哪些异常；对于这类信息，文档非常宝贵。例如，考虑 System.IO.File.OpenRead API，其中记录了以下异常：

- ArgumentException——路径是零长度字符串、仅包含空白，或包含一个或多个 InvalidPathChars 定义无效字符。
- ArgumentNullException——路径为 null。
- PathTooLongException——指定的路径、文件名或两者都超过系统定义的最大长度。例如，在基于 Windows 的平台上，路径必须少于 248 个字符，文件名必须少于 260 个字符。
- DirectoryNotFoundException——指定的路径无效（例如，它位于未映射的驱动器上）。
- UnauthorizedAccessException——路径指定了目录，或调用方没有所需的权限。
- FileNotFoundException——在路径中指定的文件未找到。
- NotSupportedException——路径格式无效。

下一步是根据各种标准对异常进行分类。一类包含由代码中的 bug 或调用堆栈更高层的不正确输入验证导致的异常。例如，ArgumentNullException 是可以通过确保 null 引用永远不会被传入相关参数来避免的。如果这些参数的数据来自外部，那么在接收数据的位置进行正确的输入验证就是正确的做法。执行根本不应到达这一步。

还有一些异常，你无法提供任何有意义的恢复。在前面的示例中，你不太可能从未经授权的访问异常中恢复，因为涉及文件系统级别的设置。根据对 OpenRead 方法的调用所在的位置，你可能希望让此异常继续传播、向用户显示错误对话框，或执行诊断日志记录。

另一类包括你可以尝试阻止但永远无法完全消除的异常。一个很好的例子是 FileNotFoundException，外部世界会影响调用的结果。你可能会自发地想到这样的缓解措施：

```
if (!File.Exists(file)) {
    // Preventing the FileNotFoundException by proper action here?
}

var fs = File.OpenRead(file);
```

无论你检查文件是否存在多少次，上述代码中仍然存在竞态条件。如果文件在检查时间与尝试打开文件时间之间消失，你仍然会得到 FileNotFoundException。如果你处于处理该异常的良好位置（例如，通过通知用户），或者你已经想好了在另一个位置查找文件的回退方案，那就这么做；否则，让异常冒泡到调用方，并记录这种情况。

另一类异常与无论你多么努力都无法处理的情况有关。系统可能内存不足；调用堆栈可能溢出（这可能表明递归算法中存在 bug）；或者如果情况真的很糟，执行引擎可能出了问题。在任何情况下都不应处理这些异常。

### 不可捕获！

CLR 包含一个异常类型列表，将其归类为不可捕获，意味着用户无法处理它们。示例包括 OutOfMemoryException 和 StackOverflowException 类型。

最后，一些设计不良的 API 要求用户即使在常规使用中也要处理异常。幸运的是，这类 API 很少见，并且通常已被更好的成员替换或补充。一个很好的例子是 .NET 1.x 中的 int.Parse：

```
int age = -1;
bool ageValid;

try {
    age = int.Parse(userAge);
    ageValid = true;
} catch (FormatException) {
    ageValid = false;
}

if (!ageValid) {
    // Take appropriate action; e.g. ask for input again.
}
```

API 设计者很快认识到，这不是检查有效输入的好方法，因此引入了一个名为 TryParse 的姊妹方法：

```
int age;
if (int.TryParse(userAge, out age)) {
    // Take appropriate action; e.g. ask for input again.
}
```

绝不要设计要求用户在常规情况下捕获异常的 API；这样做不仅会导致代码更加繁琐，还会降低性能，并在启用首次异常时妨碍调试。

## 不要捕获所有异常（再次强调）

基于上一节的讨论，你应该已经被劝阻不要捕获所有异常。有些异常根本无法捕获，而另一些则应传播给调用方以采取有意义的行动（如果可能）。此规则的例外很少，我不会在这里尝试定义这样的例外。

## 超出你的控制

使用 try 语句捕获异常只有在你的代码位于调用堆栈更高层某处时才有效。毕竟，受保护的块只保护在其内部运行的代码。你并不拥有神奇的能力，可以将异常处理程序扩展到不属于你的代码、系统某个不相关角落的代码周围。

这类实际问题的典型来源是 UI 编程，其中调度器用于代表用户在正确的线程上以指定的正确优先级运行工作。调度已安排工作项的代码超出你的控制。例如，在 Windows Presentation Foundation (WPF) 中，是应用程序的 Run 方法启动调度器。在更详细地介绍 WPF 时，我们会更多地讨论调度器的作用。现在，只需关注下面这个小例子：

```
private void crash_Click(object sender, RoutedEventArgs e) {
    Dispatcher.BeginInvoke(new Action(() => {
        throw new Exception("Oops!"); })
    );
}
```

这里我们通过调度器安排后台工作，使 crash 按钮的事件处理程序立即返回。在未来的某个时刻，这个工作项将被调度器拾取，从而导致委托被调用。崩溃时的调用堆栈大致如下：

```
WpfApplication1.exe!WpfApplication1.MainWindow.crash_Click.AnonymousMethod__0
...
WindowsBase.dll!System.Windows.Threading.Dispatcher.Run
...
PresentationFramework.dll!System.Windows.Application.Run
WpfApplication1.exe!WpfApplication1.App.Main
```

在顶部，我们看到包含传递给 BeginInvoke 的代码的匿名方法。这是由调度器以某种方式调用的，经过了隐藏在应用程序的 Main 方法所进行的 Application.Run 调用背后的所有机制。显然没有地方可以处理这样的异常。我们能做的一件事是确保通过 BeginInvoke 发布的委托不会因为可避免的原因而崩溃。这是迄今为止最好的解决方案。然而，在某些情况下，这会使得
