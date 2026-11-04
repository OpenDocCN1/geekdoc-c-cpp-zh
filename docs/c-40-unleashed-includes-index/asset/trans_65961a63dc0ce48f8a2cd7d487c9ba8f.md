
多播委托。为我们的 Finished 事件生成的代码大致如下：

```csharp
private Action _finished;

public void add_Finished(Action value) {
    _finished = (Action)Delegate.Combine(_finished, value);
}

public void remove_Finished(Action value) {
    _finished = (Action)Delegate.Remove(_finished, value);
}
```

## 多线程的微妙之处

上一段中的“大致”一词至关重要。实际上，由于多线程方面的考量，生成的代码会稍微复杂一些。如果多个线程同时添加或移除事件处理程序，就会引发各种问题。

要理解为什么会这样，请注意调用 Combine 后紧跟一个赋值操作（Remove 调用也类似）。当线程切换发生在 Combine 调用和赋值之间时，另一个线程也可能对多播委托进行干扰。当切换回原始线程并执行赋值后，被中断线程所造成的影响会被覆盖：这就产生了竞争条件。

作为语言的使用者，你不必担心这一点，但了解一下这种保护机制已经存在是件好事。

## 引发事件的正确方式

在之前的 CountDown 示例中，你已经看到了如何使用以下模式来引发事件：

```csharp
if (MyEvent != null)
    MyEvent(/* args */);
```

看起来很正确，对吧？如果没有人监听该事件，MyEvent 就是 null，我们不应该尝试调用该委托，因为那会导致运行时用不友好的 NullReferenceException 对我们发出警告。

## 为什么偏偏用 null？

空的事件处理程序竟然用 null 引用来表示，这可能有点令人意外。这实际上是由于 Delegate 上 Combine 和 Remove 方法的实现方式所致，但这只是把问题进一步推开：为什么不直接返回一个带有空调用列表的 MulticastDelegate 呢？

如果那样做，编译器就需要确保每个事件在生命周期开始时都有一个空的 MulticastDelegate。换句话说，所有字段都需要用一个带有空调用列表的委托来赋值。这本身不是问题，但要想想这会占用多少内存，尤其是在充满事件的框架中。一个很好的例子是 Windows Forms，最简单的 Button 类型也有不下 68 个事件。带有空调用列表的多播委托会占用可观的内存，这可能会成为问题。尤其因为通常只有一小部分事件会被实际处理。

不幸的是，面对多线程时，前面这段代码并不完全正确，因为 null 检查和调用并不是原子操作。例如，假设一个线程在另一个线程执行 null 检查和调用之间移除了一个事件处理程序。两个线程的交互顺序如表 18.1 所示。

**表 18.1 与事件的多线程交互**

|  | 线程 1 | 线程 2 | MyEvent 目标 |
|---|---|---|---|
| 1 | `if (MyEvent != null)` |  | `A` |
| 2 |  | `MyEvent -= A;` | `A or null` |
| 3 | `MyEvent(/* args */);` |  | `null` |

在最后一行，程序会崩溃，因为线程 2 的穿插执行导致线程 1 观察到了一个 null 的 MyEvent 委托。为了避免这个问题，可以先把事件赋值给一个局部变量作为中间步骤：

```csharp
var evt = MyEvent;
if (evt != null)
    evt(/* args */);
```

回想一下，添加或移除事件处理程序并不是简单地就地调整多播委托的调用列表；相反，对 Combine 或 Remove 的调用会返回一个新的委托实例，其中包含新的调用列表。因此，通过将当前委托的引用缓存在局部变量中，我们就有了可以依赖的稳定对象。图 18.9 更详细地展示了这一点。严格来说，这意味着我们可能会在事件处理程序的调用上稍微滞后一点：采用这种修复后，即使第二个线程已经取消挂钩，第一个线程的最后一行仍会调用 A。这通常不是什么大问题。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_876_0.png)

**图 18.9 安全的多线程事件处理程序交互。**

如果你想亲眼看看这个图示的问题，用一点点多线程代码就可以很容易地复现：

```csharp
static event Action MyEvent;

static void Main() {
    // Thread mimicking a client attaching and detaching handlers.
    new Thread(() => {
        while (true) {
            Action a = () => Console.WriteLine("Hi!");
            MyEvent += a;
            MyEvent -= a;
        }
    }).Start();

    // Main thread raises the event with too little protection.
    while (true) {
        if (MyEvent != null)
            MyEvent();
    }
}
```

取决于你的运气，屏幕上打印的“Hi!”消息数量会有所不同。但迟早，前面的代码会在主线程上因 null 引用而崩溃。正如我们讨论过的，修复方法是在本地复制 MyEvent 引用。

## add 和 remove 访问器

事件基于指向两个方法的元数据，因此 C# 提供了一种定制这些方法的途径（如果你想要这么做的话），这完全不足为奇。

在事件（和属性）的上下文中，我们称这些方法为访问器。对于事件而言，有两个访问器，分别叫 add 和 remove。语法是可以预见的，与属性的 get 和 set 类似：

```csharp
public event Action Finished {
  add {
    // Called when doing +=.
  }
  remove {
    // Called when doing -=.
  }
}
```

在这些访问器内部，可以通过 `value` 关键字访问 `+=` 和 `-=` 运算符的右侧值。这与属性 setter 访问被赋给它的值的方式类似。

一旦我们实现了 add 和 remove 访问器，编译器就不再为多播委托生成字段，所有实现细节都留给开发者。你可以将其与自动实现属性（它会为你创建后台存储字段）和手动实现 getter/setter 的对比联系起来，如图 18.10 所示。令人惊讶的是，我们竟然要等到 C# 3.0 才迎来自动实现属性，而事件从该语言最初发布起就同时拥有“自动实现”和“手工实现”（使用显式访问器）两种变体。

| 自动实现属性 | 无访问器的事件 |
|---|---|
| `public int Foo { get; set; } =`<br>`private int _foo;`<br>`public int Foo {`<br>`  get {`<br>`    return _foo;`<br>`  }`<br>`  set {`<br>`    _foo = value;`<br>`  }`<br>`}` | `public event Action Foo;`<br>`= (ignoring multithreading)`<br>`private Action _foo;`<br>`public event Action Foo {`<br>`  add {`<br>`    _foo += value;`<br>`  }`<br>`  remove {`<br>`    _foo -= value;`<br>`  }`<br>`}` |

**图 18.10 属性与事件之间的对称性。**

这个特性派上用场的一个例子是实现一个更节省内存的事件系统时。在上一节的边栏中，我提到对没有目标方法的多播委托使用 null 的一个原因，是为了避免为每个空事件进行堆分配。这在另一个方面也有影响：事件的多播委托对象所需要的字段。例如，在 99.99% 的情况下，开发者只会处理按钮控件的 Click 事件。对于 Windows Forms 的 Button 来说，这是该控件 68 个事件中的 1 个，这会导致 67 个 null 引用被白白浪费内存。自己手动实现 add 和 remove 访问器就能解决这个问题。

在继续之前，请注意，这种手动实现 add 和 remove 访问器的做法很少会用到，除非你打算设计事件数量非常庞大、内存占用变得非常显著的系统。为了让你对我们所讨论的框架规模有所了解，请注意，据我所知，这种思路的两个具体实现是 Windows Forms 和 Windows Presentation Foundation（WPF）。

那我们就来试一试，设计一个精简高效的事件管理系统。我们不再为每个多播委托保留存储字段，而是将一个对象的事件处理程序存储在字典中。每个可用事件都由一个唯一键表示。与该键关联的值决定了事件处理程序，而字典中不存在对应条目则表示该事件没有处理程序。为了便于讨论，我们保持一定的抽象，假设我们有这样一个类：

```csharp
class Bar {
    public event Action A1, A2, A3, A4, A5, A6, A7, A8;
}
```

Bar 的每个实例都有八个编译器生成的、用于存放 Action 委托的存储字段，用来保存 A1 到 A8 的处理程序。当没有附加任何事件处理程序时，就浪费了八个引用。如果有 10 个 Bar 实例，总共就是 80 个。

使用字典后，我们会得到如下情形：

```csharp
class Bar {
    static readonly object s_keyA1 = new object();
    // ...
    static readonly object s_keyA8 = new object();

    private Dictionary<object, Delegate> _handlers = /* TODO */;

    public event Action A1 {
        add { /* TODO */ }
        remove { /* TODO */ }
    }
    // ...
    public event Action A8 {
        add { /* TODO */ }
        remove { /* TODO */ }
    }
}
```
