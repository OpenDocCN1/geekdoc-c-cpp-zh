

# 事情在发生 — C# 事件 369

这段代码看起来和我描述的委托实例化相似，区别在于 `=` 之后，你看到的是 `delegate` 关键字、括号中匿名方法的任何参数（如果没有参数则括号为空）以及方法体。这段代码原本是在一个单独的 `DoUpdate()` 方法中——即委托所“指向”的方法——现在它已经移动到了匿名方法内部——不再需要指向了。而且这个方法完全没有意义。

你仍然需要 `UpdateCallback` 委托类型的定义，并且你仍然在调用一个委托实例，在这个例子中命名为 `anon`。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_394_0.png)

不用多说，这段描述并没有涵盖关于匿名方法的所有知识，但它只是一个开始。在“帮助”中查找匿名方法，可以查看网站上 `DelegateExamples` 程序中更多匿名方法的示例。我最后的建议是保持你的方法尽可能简短。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_394_1.png)

# 事情在发生 — C# 事件

在本节中，委托的一个应用值得讨论：C# 事件，它是用委托实现的。事件是回调的一种变体，但它提供了一种更简单的机制，用于每当有重要事件发生时提醒观察者。当有多个“焦急的亲戚”在等待回调时，事件会变得特别有用。事件在 C# 中被广泛使用，特别是用于将用户界面中的对象与使其运行的代码连接起来。本章之前介绍的 `SimpleProgress` 示例中的按钮就说明了这种用法。

# 观察者设计模式

在编程中，运行程序中的各种对象对其他对象上发生的事件产生“感兴趣”是非常常见的。例如，当用户点击按钮时，包含该按钮的表单“想要”知道这件事。事件为 C# 和 .NET 提供了通知任何感兴趣方的的标准机制。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_394_2.png)

事件模式如此常见，以至于它有一个名字：观察者设计模式。它是人们为了供大家在自己的代码中使用发布的许多常见设计模式之一。想要学习其他设计模式，可以参考 Steve Holzner 写的《初学者设计模式》。

观察者模式由一个可观察对象（Observable）——即具有有趣事件的对象（有时称为主题 Subject，这限制了我）——以及任意数量的观察者对象（Observer）组成：即对特定事件感兴趣的对象。观察者以某种方式向可观察对象注册自己，当感兴趣的事件发生时，可观察对象会通知所有注册的观察者。你可以用多种方式实现这种模式而不使用事件（例如回调和接口），但 C# 的做法是使用事件。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_395_0.png)

你可能会遇到观察者的另一种名称是监听器（listeners）。监听器“监听”事件。这并不是最后的替代方案。

# 什么是事件？发布/订阅

事件的一个类比是你的当地报纸。你和其他许多人联系报纸进行订阅，然后报纸向你递送最新新闻，而且完全被雨水渍浸透了。报纸公司是发布者（Publisher），它的客户是订阅者（Subscribers），因此这种观察者的变体通常被称为发布/订阅。这是我在本章中坚持的类比，但请记住观察者模式就是使用不同术语的发布/订阅模式。观察者是订阅者，而可观察对象是发布者。

在 C# 中，当你有一个类产生有趣的事件时，你通过提供一个事件对象（通常是 `public` 的），向任何可能感兴趣了解此类事件的类发布通知的可用性。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_395_1.png)

`event` 一词在 C# 中有两个含义。你可以将 `event` 一词既视为“有趣的发生”，也视为一种特定的 C# 对象。前者是现实世界的概念，后者是你在 C# 中通过 `event` 关键字进行设置的方式。

# 发布者如何宣传其事件

为了吸引订阅者，类会声明一个委托和一个相应的事件，如下所示：

```csharp
public class PublisherEvents
{
    // 作为事件基础的委托类型。
    // 如果所有订阅者都在同一个程序集中，则应声明为 'internal'
    public delegate void NewEventHandler(object sender, EventArgs e);

    // 事件。
    public event NewEventHandler NewEventHandler;
    // ... 其他代码。
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_395_2.png)

委托和事件的定义向世界宣布：“欢迎订阅者！”你可以将事件认为类似于 `EventHandler` 类型的变量。（到目前为止，还没有发送任何事件。这只是它们准备的设施。）

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_395_3.png)

在作为事件基础的委托类型名称后附加 `EventHandler` 被认为是良好的做法。

# 事情在发生 — C# 事件 371

一个常见的例子（你可以在之前讨论的 `SimpleProgress` 代码中看到）是发布者发布其事件，在 C# 中定义如下：

```csharp
event EventHandler Click;
```

这里的 `Click` 事件是在 .NET 中定义的。因为事件被广泛使用，.NET 为你定义了 `EventHandler` 和 `EventHandler<T>`。

在本章的后续部分，`NewEventHandler` 方法展示了这种方式：

```csharp
event NewEventHandler NewEventHandler;
```

发布者通过这种方式发布其事件：

```csharp
event EventHandler NewEventHandler;
```

`PublisherEvents` 示例展示了这种方式。观察者订阅事件的方式：

```csharp
NewEventHandler NewEventHandler; // 观察者订阅
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_396_0.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_396_1.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_396_2.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_396_3.png)

# 事情在发生 — C# 事件 372

在 `SimpleProgress` 程序中，查看 `Form1.Designer.cs` 文件可以了解它是如何注册按钮事件的。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_397_0.png)

# 如何发布事件

当发布者决定有事值得向所有订阅者发布时，它会引发（发送）事件。这种情况类比报纸出版周日刊。为了发布事件，发布者的方法会有如下代码：

```csharp
NewEditionEventArgs e = new NewEditionEventArgs(); // 在构造函数传递参数
NewEdition(this, e); // 引发事件——'this' 是发布者对象。
```

或者对于 `Button` 事件，尽管它是隐藏在 `Button` 类中的：

```csharp
EventArgs e = new EventArgs();
Click(this, e); // 引发事件。
```

在这些每个示例中，你必须设置必要的参数——这些参数因事件而异；某些事件需要传递大量信息。然后你通过“调用”其名称（类似于调用委托）来引发事件：

```csharp
eventName(argumentList); // 引发事件（分发报纸）
NewEdition(this, e);
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_397_1.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_397_2.png)

# 如何向事件处理程序传递额外信息

事件处理程序的 `e` 参数是 `System.EventArgs` 类的一个自定义子类。你可以编写自己的 `NewEditionEventArgs` 类来携带你需要传达的任何信息：

