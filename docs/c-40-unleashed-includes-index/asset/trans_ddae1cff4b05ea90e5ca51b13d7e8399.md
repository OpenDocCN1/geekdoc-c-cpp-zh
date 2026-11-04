

![](img/a16f85e62ce9bdc527f4b09dbfe26092_853_0.png)

图17.26 Windows 中挂起应用程序的“白雪公主效应”。

这个应用程序编写得很糟糕，因为它在执行开销很大的计算时阻塞了 UI 线程，从而阻止了应用程序的消息循环（在 UI 线程上运行）处理窗口消息。窗口消息被用作一种将工作分派给应用程序的方式（例如，处理键盘或鼠标输入）、恢复焦点，甚至将自身重绘到屏幕上。

在图17.26中，当窗口管理器要求窗口重绘自身时，窗口已无法响应 WM_PAINT 消息，因为它被阻塞，正在等待斐波那契数计算返回。Windows 会检测应用程序不再响应窗口消息的情况，并通过在标题栏中添加臭名昭著的“未响应”提示来表示该状态。从 Windows Vista 开始，它还会在窗口客户区覆盖一层雾状云，以直观地表示应用程序已挂起。

稍后你将看到在 Windows Forms 和 WPF 等 UI 开发框架的上下文中如何处理长时间运行的操作。现在，只需注意进行阻塞调用可能引发的问题。

## 合并委托

为了准备第18章关于事件的讨论，我还想再提一件关于委托的事：它们能够在“多播场景”中使用。前面你已经看到，C# 中的委托类型如何派生自一个名为 MulticastDelegate 的基类。在 Visual Studio 中查看该类型的信息，你会看到该类型本身如何派生自 Delegate：

```csharp
namespace System
{
    public abstract class MulticastDelegate : Delegate
    {
        ...
```

再进一步查看 MulticastDelegate 类型的成员，你会注意到其中一个成员揭示了它真正的核心目标：允许在委托的调用过程中调用多个目标方法。图17.27 对此有所暗示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_854_0.png)

图17.27 MulticastDelegate 对象内部保留一个 Delegate 对象列表。

如果一个 Delegate 对象可以引用一个方法，而一个 MulticastDelegate 包含一个 Delegate 对象数组（称为*调用列表*），那么显然一个 MulticastDelegate 可以引用多个方法。因此，调用这样的委托会将传入的参数多播到调用列表中的所有方法。

到目前为止，我们创建的委托始终一次只指向一个方法。例如，下面基于 lambda 表达式定义了三个 Action<string> 委托：

```csharp
Action<string> sayHiEnglish = name => Console.WriteLine("Hello " + name);
Action<string> sayHiDutch   = name => Console.WriteLine("Hallo " + name);
Action<string> sayHiFrench  = name => Console.WriteLine("Allo " + name);
```

如果给定一个名字，并且想调用上述所有委托，用多种语言向到来的用户问候，该怎么办？存在不同的方法。显然，我们可以逐个调用这三个委托：

```csharp
sayHiEnglish(name);
sayHiDutch(name);
sayHiFrench(name);
```

如果随后要求我们再加入另一种语言，就需要重新修改这些委托的调用位置，代码会开始变得臃肿。此外，甚至可能出现这样的情况：我们为问候系统的用户提供了一种方式，让他们为我们没有预料到的不同语言接入其他委托。现在，我们代码中的委托调用次数不再固定。

让我们走支持未知数量目标方法的路线：用一个手工构造的调用列表自己完成底层连接：

```csharp
var greetings = new List<Action<string>> {
    name => Console.WriteLine("Hello " + name),
    name => Console.WriteLine("Hallo " + name),
    name => Console.WriteLine("Allo " + name)
};
```

现在我们可以为用户提供某种能力，将问候委托添加到此列表中（显然要运用面向对象编程中学到的所有最佳实践，不直接暴露该列表），并通过循环调用它们全部：

```csharp
void SendGreetings(string name) {
    foreach (var greeting in greetings) {
        greeting(name); // invokes the delegate
    }
}
```

忽略这个用循环实现的简单方法，看看生成的方法签名：它接收一个 string，不返回任何内容。换句话说，它符合 Action<string> 目标方法的签名。我们在这里实际上是以一种相当迂回的方式将一系列委托合并成了一个。为什么说迂回？MulticastDelegate 正是通过一个名为 Combine 的静态方法开箱即用地提供了这一功能，如图17.28 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_855_0.png)

图17.28 通过 Delegate API 合并委托。

请注意，Combine 方法实际上定义在基类型 Delegate 上，因此我们本来也可以在 Delegate 上调用它。将 Combine 应用于一组 Delegate 对象的结果本身就是一个 Delegate。你可能已经猜到，System.Delegate 是所有委托对象的基类型。为了让前面的代码尽可能具有强类型，我们可以对结果进行强制转换：

```csharp
Action<string> sayHiEnglish = name => Console.WriteLine("Hello " + name);
Action<string> sayHiDutch   = name => Console.WriteLine("Hallo " + name);
Action<string> sayHiFrench  = name => Console.WriteLine("Allo "  + name);

var sendGreetings = (Action<string>)Delegate.Combine(sayHiEnglish, sayHiDutch,
    sayHiFrench);

sendGreetings("Bart");
```

调用生成的 sendGreetings 委托的结果如你所料：三条问候消息会按照它们在 Combine 调用中指定的顺序打印到屏幕上。

尽管前面的做法可行，但由于需要方法调用以及为了回到更强类型的世界而必须进行强制转换，它看起来有些不太舒服。此外，无法基于 Combine 的签名和强制转换进行编译时检查：

```csharp
Action<string> sayHiEnglish = name => Console.WriteLine("Hello " + name);
Func<int, int> twiceAsNice = x => x * 2;
ThreadStart t = (ThreadStart)Delegate.Combine(sayHiEnglish, twiceAsNice);
t();
```

尽管这段代码可以正常编译，但它完全不合理，因为这里要合并的委托彼此不兼容。事实上，Delegate 调用会在运行时失败，因为运行时会检测到这种不兼容性。而且，即使我们用两个兼容的委托（例如 sayHiEnglish 和 sayHiDutch）正确处理了这一部分，如果目标类型（示例中的 ThreadStart）与生成的委托不兼容，强制转换也可能失败。

幸运的是，C# 使用非常熟悉的 + 运算符在语言层面提供了对合并委托的支持。sendGreetings 委托可以这样构造：

```csharp
Action<string> sayHiEnglish = name => Console.WriteLine("Hello " + name);
Action<string> sayHiDutch   = name => Console.WriteLine("Hallo " + name);
Action<string> sayHiFrench  = name => Console.WriteLine("Allo " + name);

var sendGreetings = sayHiEnglish + sayHiDutch + sayHiFrench;
sendGreetings("Bart");
```

这样做的结果是静态类型的，因此 sendGreetings 会被正确推断为 Action<string> 类型，就像组成它的所有委托一样。

既然能够使用 + 运算符，那么使用 += 的复合赋值呢？这同样可行：

```csharp
var sendGreetings = sayHiEnglish + sayHiDutch;
sendGreetings += sayHiFrench;
```

### 为什么这种语法很重要

在第18章关于事件的讨论中，你将看到这种复合赋值如何用于将事件处理程序附加到事件（不过，如你所见，这一功能实际上定义在委托上，而不仅仅是用于事件）。

因为编译器拥有关于被“加在一起”的委托对象的所有类型信息，所以它可以防止我们写出无效的组合。图17.29 展示了这样一种失误触发的编译时错误。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_857_0.png)

图17.29 委托组合的编译时检查。

使用 + 和 += 运算符实现委托组合根本不是什么黑魔法。我们只是在底层依赖 Delegate.Combine 方法，然后强制转换为目标类型。由于对委托兼容性进行了编译时检查，所有生成的代码在静态上都能保证成功。

将委托与 null 引用组合会怎样？事实证明，Combine 只是允许使用 null 引用，而不会使调用失败。那些 null 引用根本不会进入调用列表，而是会被过滤掉：

```csharp
var sendGreetings = sayHiEnglish + sayHiForeign; // assume sayHiForeign is null
sendGreetings("Bart"); // we still get here and this simply prints "Hello Bart"
```

为什么 null 情况如此重要？嗯，多播委托上不仅有加法操作（我们称之为组合）：也存在移除操作。下面的示例说明了这一点：

```csharp
Action<string> sendGreetings = null;

sendGreetings += sayHiEnglish;
sendGreetings += sayHiDutch;
sendGreetings("Bart"); // Prints "Hello Bart" and "Hallo Bart"

sendGreetings -= sayHiEnglish;
sendGreetings += sayHiFrench;
sendGreetings("John"); // Prints "Hallo John" and "Allo John"
```

在底层，使用二元运算符或复合 -= 赋值移除委托都是通过调用 Delegate.Remove 实现的。

在事件上下文中，从调用列表中添加和移除委托非常重要，你很快就会看到。在这种情况下，通常会从一个空的

