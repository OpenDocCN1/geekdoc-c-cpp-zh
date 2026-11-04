
有趣的属性。像 co- 和 *逆变* 这样吓人的词再次出现，但不用害怕；它比听起来容易。假设你想为不同类型的事件挂接同一个事件处理程序。例如，让我们处理按钮上的两个事件：KeyDown 和 MouseMove。（想象一下你想对发送到按钮的任何输入做出反应，无论是通过鼠标交互还是键盘。）首先，来看一下这两个事件的声明：

~~~csharp
public event KeyEventHandler KeyDown;
public event MouseEventHandler MouseMove;
~~~

如果我们要挂接两个独立的事件处理程序但想共享它们的逻辑，情况会是这样：

~~~csharp
static void Main() {
    Button sayHello = new Button { Text = "Greet me!" };
    sayHello.MouseMove += new MouseEventHandler(sayHello_MouseMove);
    sayHello.KeyDown += new KeyEventHandler(sayHello_KeyDown);
}

static void sayHello_MouseMove(object sender, MouseEventArgs e) {
    sayHello_KeyDownOrClick(sender, e);
}

static void sayHello_KeyDown(object sender, KeyEventArgs e) {
    sayHello_KeyDownOrClick(sender, e);
}

static void sayHello_KeyDownOrClick(object sender, EventArgs e) {
    // Common logic goes here, for example, using (Button)sender
}
~~~

看到我们是如何将 MouseMove 或 KeyDown 的事件处理程序调用转发到单个方法了吗？肯定是方法调用，但还有一个更微妙的事情正在发生：我们将 sayHello_KeyDownOrClick 的最后一个参数类型设为 MouseEventArgs 和 KeyEventArgs 的共同超类型。这是一个大家都理解的关于常规方法调用的自然规则：给定某种类型的对象，你始终可以将它作为参数传递给类型较不具体（即超类型）的方法。

但我们可以做得更好。得益于委托参数类型的 *逆变*，我们可以改写成如下形式：

~~~csharp
static void Main() {
    Button sayHello = new Button { Text = "Greet me!" };
    sayHello.MouseMove += sayHello_KeyDownOrClick;
    sayHello.KeyDown += sayHello_KeyDownOrClick;
}
~~~

```csharp
static void sayHello_KeyDownOrClick(object sender, EventArgs e) {
    // Common logic goes here, for example, using (Button)sender
}
```

这里我们使用与方法组转换相关的规则，该规则考虑了逆变。这一切意味着可以创建一个委托（此处用作事件处理程序），它引用的是参数类型比预期类型派生程度更低的方法。例如，虽然 MouseMove 期望一个委托指向第二个参数类型为 MouseEventArgs 的方法，但传递一个在参数位置接受 EventArgs 的方法的委托也是可以的。要理解为什么这样是可以的，只需想想当事件源调用委托并传入一个 MouseEventArgs 时会发生什么。通过委托它会被传递给接受参数为 EventArgs 对象的事件处理程序方法，这没问题，因为每个 MouseEventArgs 都是一个 EventArgs。

在参数类型上应用逆变的地方，协变适用于返回类型，但在事件处理程序的上下文中很少使用（因为它们通常具有 void 返回类型）。委托返回类型和参数类型的协变和逆变在图 18.18 中有所描述。在查看图表时，记住前缀 co（顺流）和 contra（逆流）的源自拉丁语的含义会有所帮助。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_895_0.png)

图 18.18 · 委托类型的协变和逆变。

## EventHandler<T>

![](img/a16f85e62ce9bdc527f4b09dbfe26092_896_0.png)

要求（或强烈建议，出于一致性考虑）开发者创建自己的 EventArgs 派生类型对他们来说已经是足够的负担，但在 .NET 的早期阶段甚至这还不够。必须创建一个自定义的 EventHandler 委托，使用典型的 object sender 和 MyEventArgs e 签名。

自从 .NET 2.0 引入泛型以来，通过引入 EventHandler<T>，这一过程变得稍微简化：

```
public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e)
where TEventArgs : EventArgs;
```

放在 TEventArgs 类型参数上的泛型约束强制执行事件处理程序模式的正确使用。通过要求第二个参数为派生自 EventArgs 的类型，委托类型的逆变和方法组转换在所有事件中继续有效。

作为示例，让我们按照前面概述的事件模式重构我们的 CountDown 示例。首先，我们为 Tick 事件定义一个 EventArgs 子类型，因为我们希望向用户提供有关已用时间的信息：

```
class TickEventArgs : EventArgs {
    public TickEventArgs(uint seconds) {
        this.Seconds = seconds;
    }

    public uint Seconds { get; private set; }
}
```

对于 Finished 事件，我们可以简单地使用 EventArgs 基类，因为我们不会传达任何事件特定的信息。

借助我们专门的 EventArgs 类型，剩下的就是更改 CountDown 类以使用事件的适当 EventHandler 类型。图 18.19 显示了在 IDE 中执行此操作时的场景，说明了通用 EventHandler<TEventArgs> 委托类型的使用，IntelliSense 显示了约束。

新的事件声明如下所示：

```
public event EventHandler<TickEventArgs> Tick;
public event EventHandler Finished;
```

引发事件的方式必须更改，因为委托的签名已更改。对于 sender 参数，我们只需传递 this。EventArgs 参数方面情况略有不同，但显然在 Tick 情况下我们会使用 TickEventArgs 的实例。为了减少在 Finished 事件上使用的普通空 EventArgs 的内存使用，我们可以使用静态只读 EventArgs.Empty 字段。总的来说，对包含嵌入式后台线程过程的 Start 方法所做的更改相当小：

```
public void Start() {
    new Thread(() => {
        uint n = _seconds;
        while (n > 0u) {
            var tick = Tick;
            if (tick != null) {
                tick(this, new TickEventArgs(n));
            }
            Thread.Sleep(1000);
            n--;
        }

        var finished = Finished;
        if (finished != null) {
            finished(this, EventArgs.Empty);
        }
    }).Start();
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_897_0.png)

图 18.19 使用 EventHandler<T>。

正如你现在所预期的那样，对于静态事件，应使用 null 值作为 sender 参数。

显然，使用位置也需要更改，以便使用事件处理程序方法的正确签名。在 Tick 事件处理程序中，我们使用事件参数获取已用秒数：

```
static void TickHandler(object sender, TickEventArgs e) {
    Console.WriteLine(e.Seconds);
}
```

```
static void FinishedHandler(object sender, EventArgs e) {
    Console.Beep();

    // Finished has been called; we can unhook both Tick and Finished now.
    s_countDown.Tick -= TickHandler;
    s_countDown.Finished -= FinishedHandler;
}
```

## FXCop 关于命名

FxCop 将触发警告，如果未遵循事件处理程序参数的命名。作为风格问题，将第一个参数命名为 sender，第二个命名为 e。事实上，这是一个极少数官方推荐使用单字母标识符的地方。

## 为派生类使用而设计事件

那我们 CountDown 类型的扩展者呢？假设我们设计的倒计时机制使其核心功能可以被重写（例如，通过将 Start 标记为 virtual）或我们只是没有密封该类。子类型可能希望在扩展的一部分中引发我们的任何事件。例如，具有 EmergencyStop 功能的 CountDown 可能希望在计时器达到零之前调用 Finished。我邀请你思考更多示例。

关键问题是子类型是否可以引发在其基类型上声明的事件。一些推理可以帮助在不 yet 涉及编译器的情况下回答这个问题。你已经看到事件声明如何导致创建包含多播委托的私有字段，该委托跟踪事件的已添加事件处理程序。要引发事件，该私有字段会被获取，然后进行委托调用。所有这些观察都导致我们得出结论：子类型将无法引发其基类上定义的事件，因为使用了私有字段。

作为确认，尝试编译以下代码会在尝试获取 Finished 事件的委托对象的行上惨败：

```
class FancyCountDown : CountDown {
    public void EmergencyStop() {
        // Cause a stop somehow; requires more extensibility
        // provided by the base class.

        var finished = Finished; // this line fails to compile!
        if (finished != null) {
            finished(this, EventArgs.Empty);
        }
    }
}
```
