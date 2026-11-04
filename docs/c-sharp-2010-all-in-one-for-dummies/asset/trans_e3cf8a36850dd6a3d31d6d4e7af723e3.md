
PerformStep() 随后会用绿色填充进度条的另外 10% 增量，其数额由其 Step 属性决定，初始设置为 10。仔细观察最后一步——它只是一个闪烁。

- 6. 最后，控制权返回到 DoSomethingLengthy()，它继续循环。当循环运行完毕时，DoSomethingLengthy() 退出，将控制权返回给 button1_Click() 方法。该方法随后通过将 Value 属性设置为 0 来清除 ProgressBar。应用程序随后安静下来，等待用户再次点击其中一个按钮（或其关闭按钮）。

就是这样。通过使用委托来实现回调，程序保持其进度条为最新状态。有关委托用法的列表，请参阅章节“我把示例委托给了伊戈尔”。更多委托示例，请参阅网站上的 DelegateExamples 程序。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_393_0.png)

当你需要为委托类型参数定义一个类型以实现回调时，编写一个自定义委托。使用预定义的委托用于事件以及集合类的 Find() 和 ForEach() 方法。

## 嘘！保持安静——匿名方法

在你掌握了使用委托的要点后，花点时间快速了解一下微软在几年前对 C# 2.0 中简化委托的首次尝试。

为了减少一些委托的繁琐，你可以使用匿名方法。匿名方法只是以更传统的记法编写。虽然语法和一些细节有所不同，但无论使用“原始”委托、匿名方法还是 lambda 表达式，其效果本质上是相同的。你可以在本书的配套网站上了解更多关于 lambda 表达式的信息。

匿名方法在同一时间创建委托实例和它所“指向”的方法——就地、即时、马上。以下是 DoSomethingLengthy() 方法的核心内容，再次呈现，这次重写为使用匿名方法（以粗体显示）：

```csharp
private void DoSomethingLengthy() // No arguments needed this time.
{
    ...
    for (int i = 0; i < duration; i++)
    {
        if ((i % updateInterval) == 0)
        {
            UpdateProgressCallback anon = delegate() // Create delegate instance.
            {
                progressBar1.PerformStep();        // Method 'pointed' to
            };
            if (anon != null) anon();           // Invoke the delegate.
        }
    }
}
```

这段代码看起来与我所描述的委托实例化类似，只是等号 = 之后，你会看到 delegate 关键字、匿名方法的参数（如果没有参数则为空括号）以及方法体。过去放在单独的 DoUpdate() 方法中的代码——即委托所“指向”的方法——已移入匿名方法内部——不再需要指向。而这个方法完全没有名字。

你仍然需要 UpdateProgressCallback 委托类型的定义，并且你仍然在调用一个委托实例，在本例中命名为 anon。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_394_0.png)

不用说，这段描述并没有涵盖关于匿名方法需要知道的一切，但这是一个开始。在帮助中查找“匿名方法”一词，以在网站上的 DelegateExamples 程序中查看更多匿名方法示例。我的临别建议是保持你的匿名方法简短。

## 事情发生了——C# 事件

委托的又一个应用值得在本节中讨论：C# 事件，它是用委托实现的。事件是回调的一种变体，但提供了一种更简单的机制，用于在重要事件发生时提醒“感兴趣的观察者”。当有多个焦急的“亲戚”在等待回调时，事件尤其有用。事件在 C# 中被广泛使用，尤其用于将用户界面中的对象连接到使其工作的代码。本章前面介绍的 SimpleProgress 示例中的按钮就说明了这种用法。

### 观察者设计模式

在编程中，运行程序中的各种对象——我提到的那些焦急的“亲戚”——对其他对象上发生的事件“感兴趣”是非常常见的。例如，当用户点击一个按钮时，包含该按钮的窗体“希望”知道这件事。事件提供了 C# 和 .NET 中通知任何感兴趣方重要操作的标准机制。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_394_1.png)

事件模式如此常见，以至于它有一个名字：观察者设计模式。它是人们为任何人在自己的代码中使用而发表的众多常见 *设计模式* 之一。要开始学习其他设计 *模式*，你可以参考 Steve Holzner 所著的 *设计模式傻瓜书*。

观察者模式由一个可观察对象组成——具有有趣事件的对象（有时称为主题 Subject，不过这让我感到困惑）——以及任意数量的观察者对象：对特定事件感兴趣的对象。观察者以某种方式向可观察对象注册自己，而当感兴趣的事件发生时，可观察对象会通知所有已注册的观察者。你可以通过多种方式在没有事件的情况下实现此模式（如回调和接口），但 C# 的做法是使用事件。

你可能会遇到的观察者的另一种名称是侦听器。侦听器“监听”事件。而这并不是最后的替代名称。

### 什么是事件？发布/订阅

事件的一个类比是你的本地报纸。你和许多其他人联系报社订阅，然后报社向你投递最新的报纸，通常还被雨水坑弄湿。报社是发布者，客户是订阅者，因此这种观察者的变体通常称为发布/订阅。我在本章中坚持使用这个类比，但请记住，观察者模式就是使用不同术语的发布/订阅模式。观察者是订阅者，他们所观察的可观察对象是发布者。

在 C# 中，当你有一个类在其上会发生有趣的事件时，你可以通过提供一个事件对象（通常是公共的）来向可能对了解此类事件感兴趣的任何类宣传通知的可用性。

event 这个词在 C# 中有两个含义。你可以认为 event 这个词既表示“一个有趣的发生”，也表示一种特定的 C# 对象。前者是现实世界的概念，后者是它在 C# 中使用 event 关键字设置的方式。

### 发布者如何宣传其事件

为了招揽订阅者，一个类声明一个委托和相应的事件，像这样：

```csharp
public class PublisherOfInterestingEvents
{
    // A delegate type on which to base the event.
    // Should be declared 'internal' if all subscribers are in the same assembly.
    public delegate void NewEditionEventHandler(object sender,
                                                NewEditionEventArgs e);
    // The event:
    public event NewEditionEventHandler NewEdition;
    // ... other code.
}
```

委托和事件的定义向世界宣布：“欢迎订阅！”你可以将 NewEdition 事件视为 NewEditionEventHandler 委托类型的一个变量类似。（到目前为止，还没有发送任何事件。这只是它们的基础设施。）

将 EventHandler 附加到作为事件基础的委托类型的名称上被认为是一种良好的做法。

**在网上**

一个常见的例子，你可以在本章前面讨论的 SimpleProgress 代码示例中看到，就是 Button 宣传其各种事件，包括 Click 事件。在 C# 中，Button 类将此事件公开为

```csharp
event _dispCommandBarControlEvents_ClickEventHandler Click;
```

其中第二个、长长的项是在 .NET 中的某个地方定义的委托。

由于事件被如此广泛使用，.NET 为你定义了两种与事件相关的委托类型，名为 EventHandler 和 `EventHandler<TEventArgs>`。你可以将前面的代码中的 NewEditionEventHandler 改为 EventHandler 或泛型的 `EventHandler<TEventArgs>`，并且不需要自己的委托类型。在本章的其余部分，我假装我使用了前面提到的内置 `EventHandler<TEventArgs>` 委托类型，而不是 EventHandler 或我的自定义类型 NewEditionEventHandler。你也应该更喜欢这种形式：

```csharp
event EventHandler<NewEditionEventArgs> NewEdition;
```

**请记住**

Book II  
Chapter 9

Delegating Those Important Events

网站上的 NewspaperEvents 示例演示了如何正确设置你的事件并在各种订阅者中处理它。（第二个示例程序 NewspaperEventsNongeneric 如果你对泛型感到 `<ahem>` 害怕，则避免了泛型内容。如果是这样，你可以在以下部分中在脑海中省略 `<eventhandler-args>` 信息。）

**在网上**

### 订阅者如何订阅事件

要接收特定事件，订阅者会像这样注册：

```csharp
publisher.EventName +=
    new EventHandler<some EventArgs type here>(some method name here);
```

其中 publisher 是发布者类的一个实例，EventName 是事件名称，而 `EventHandler<TEventArgs>` 是事件下面的委托。更具体地说，前一个示例中的代码可能是：

```csharp
myPublisher.NewEdition += new EventHandler<NewEditionEventArgs>(MyPubHandler);
```

因为事件对象在其小小的引擎盖下是一个委托，所以 += 语法是将一个方法添加到委托在调用时会调用的方法列表中。

**提示**

任意数量的对象都可以这样订阅（并且委托将保存所有已订阅的“处理程序”方法的列表）——甚至在该事件上定义的对象的对象也可以订阅，如果你愿意的话。（而且是的，这个示例表明一个委托可以“指向”多个方法。）
