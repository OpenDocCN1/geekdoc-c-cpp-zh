

![](img/80ff26f06fc9ab951e1cd4257b867366_392_0.png)

一个常见示例（你可以在本章前面讨论过的 SimpleProgress 代码示例中看到）是 Button 公开其各种事件，包括 Click 事件。在 C# 中，Button 类将此事件公开为：

```
event _dispCommandBarControlEvents_ClickEventHandler Click;
```

其中第二个——很——长——的项是在 .NET 中某处定义的委托。

![](img/80ff26f06fc9ab951e1cd4257b867366_392_1.png)

由于事件的使用非常普遍，.NET 为你定义了两种与事件相关的委托类型：`EventHandler` 和 `EventHandler<TEventArgs>`。你可以将前面代码中的 `NewEditionEventHandler` 改为 `EventHandler`，或改为泛型 `EventHandler<TEventArgs>`，这样就不需要自定义委托类型了。在本章其余部分，我会假使自己使用的是前面提到的内置 `EventHandler<TEventArgs>` 委托类型，而不是 `EventHandler`，也不是我自定义的 `NewEditionEventHandler` 类型。你也应该优先采用这种形式：

```
event EventHandler<NewEditionEventArgs> NewEdition;
```

![](img/80ff26f06fc9ab951e1cd4257b867366_392_2.png)

网站上的 NewspaperEvents 示例演示了如何正确设置事件并在多个订阅者中处理它。（第二个示例程序 `NewspaperEventsNongeneric` 则避开了泛型内容，如果你对代码感到<咳咳>发怵的话。如果是这样，你可以在心里忽略下一节中的 `<eventhandlerargs>` 信息。）

## 订阅者如何订阅事件

要接收特定事件，订阅者需要像这样登记：

```
publisher.EventName +=
    new EventHandler<some EventArgs type here>(some method name here);
```

其中 `publisher` 是发布类的一个实例，`EventName` 是事件名，`EventHandler<TEventArgs>` 是该事件底层的委托。更具体地说，前面示例中的代码可能如下所示：

```
myPublisher.NewEdition += new EventHandler<NewEditionEventArgs>(MyPubHandler);
```

![](img/80ff26f06fc9ab951e1cd4257b867366_392_3.png)

## 如何发布事件

当发布者认定发生了值得向所有订阅者发布的事情时，它就会引发（发送）该事件。这种情况类似于真正的报纸发行周日版。

要发布事件，发布者会在其某个方法中编写类似如下的代码（但请参阅后面的“引发事件的推荐方式”一节）：

```
NewEditionEventArgs e = new NewEditionEventArgs(<args to constructor here>);
NewEdition(this, e); // Raise the event -- 'this' is the publisher object.
```

或者以 Button 为例，尽管这隐藏在 Button 类中：

```
EventArgs e = new EventArgs(); // See next section for more on this topic.
Click(this, e); // Raise the event.
```

在这些示例中，你都要先设置必要的参数——不同事件所需的参数各不相同；有些事件需要传递大量信息。然后你通过“调用”事件名来引发事件（就像调用委托一样！）：

```
eventName(<argumentlist>); // Raising an event (distributing the newspaper)
NewEdition(this, e);
```

![](img/80ff26f06fc9ab951e1cd4257b867366_393_0.png)

事件可以基于具有不同签名、不同参数的委托，如前面的 `NewEditionEventHandler` 示例所示，但为事件提供 `sender` 和 `e` 参数是常规做法。内置的 `EventHandler` 和 `EventHandler<TEventArgs>` 委托类型已经为你定义了这两个参数。

如果事件处理方法需要从事件发送者（引发该事件的对象）获取更多信息，那么传递对该发送者的引用会很有用。因此，一个特定的 Button 对象 `button1` 可以传递对该按钮所属 Form 类的引用。该按钮的 Click 事件处理程序位于 Form 类中，因此发送者就是窗体：你应该传递 `this`。

![](img/80ff26f06fc9ab951e1cd4257b867366_393_1.png)

你可以在发布类的任何方法中“引发”事件。但何时引发呢？只要合适就引发。在下一节之后，我还会对引发事件再多说一些。

## 如何向事件处理程序传递额外信息

事件处理方法中的 `e` 参数是 `System.EventArgs` 类的一个自定义子类。你可以编写自己的 `NewEditionEventArgs` 类来携带你需要传递的任何信息：

```csharp
public class NewEditionEventArgs : EventArgs
{
    public NewEditionEventArgs(DateTime date, string majorHeadline)
    {
        PubDate = date; Head = majorHeadline;
    }
    public DateTime PubDate { get; private set; }  // Compiler creates details.
    public string Head { get; private set; }       //
}
```

如前面的代码示例所示，你应该将该类的成员实现为属性。构造函数使用了属性上的私有 setter 子句。

![](img/80ff26f06fc9ab951e1cd4257b867366_394_0.png)

通常，你的事件不需要额外参数，直接使用 `EventArgs` 基类即可，如下一节所示。

如果你的事件不需要特殊的 EventArgs 派生对象，只需传递：

```csharp
NewEdition(this, EventArgs.Empty);  // Raise the event.
```

## 引发事件的推荐方式

前面的“如何发布事件”一节展示了引发事件的基本骨架。不过，我建议你始终定义一个特殊的“事件引发器”方法，如下所示：

```csharp
protected virtual void OnNewEdition(NewEditionEventArgs e)
{
    EventHandler<NewEditionEventArgs> temp = NewEdition;
    if(temp != null)
    {
        temp(this, e);
    }
}
```

提供此方法可以确保你始终记得完成两个步骤：

1. **将事件存储在临时变量中。**

   这一步可以让事件在多个“线程”同时尝试使用它时更加健壮——线程会将你的程序划分为一个前台任务和一个或多个后台任务，这些任务同时（并发）运行。本书不介绍如何编写多线程程序；只需遵循这条准则即可。

2. **在尝试引发事件之前，先检查事件是否为 null。**

   如果为 null，尝试引发它会导致错误。此外，null 还表示没有其他对象对你的事件感兴趣（没有订阅者），那又何必引发它呢？*务必*检查事件是否为 null，无论你是否编写了这个 `OnSomeEvent` 方法。

![](img/80ff26f06fc9ab951e1cd4257b867366_394_1.png)

第 II 卷 第 9 章 委托那些重要事件

将该方法设为 `protected` 和 `virtual`，可以让子类重写它。这是可选的。

有了这个方法后，它总是采用相同的形式（因而很容易快速编写），你需要在引发事件时调用它：

```csharp
void SomeMethod()
{
    // Do stuff here and then:
    NewEditionEventArgs e =
        new NewEditionEventArgs(DateTime.Today, "Peace Breaks Out!");
    OnNewEdition(e);
}
```

## 观察者如何“处理”事件

订阅对象在订阅时会指定一个*处理方法*的名称——它是构造函数的参数（用粗体表示）：

```csharp
button1.Click += new EventHandler<EventArgs>(button1_click);
```

这行代码大体是在说：“请把我的报纸送到这个地址。”下面是 NewEdition 事件的一个处理程序：

```csharp
myPublisher.NewEdition += new EventHandler<NewEditionEventArgs>(NewEdition);
void NewEdition(object sender, NewEditionEventArgs e)
{
    // Do something in response to the event.
}
```

例如，BankAccount 类可以在 BankAccount 对象中发生任何情况（如存款、取款、转账，甚至错误）时引发自定义的 TransactionAlert 事件。Logger 观察者对象可以订阅这些事件，并将它们记录到文件或数据库中作为审计跟踪。

![](img/80ff26f06fc9ab951e1cd4257b867366_395_0.png)

当你在 Visual Studio 中创建按钮处理程序时（通过双击窗体上的按钮），Visual Studio 会在 Form1.Designer.cs 文件中生成订阅代码。你不应该编辑该订阅，但可以删除它，并在分部窗体类属于你的那一半中编写同样的代码来替代它。此后，窗体设计器就不再知道该订阅了。

在订阅者的处理方法中，你要执行当你的类获知此类事件时应当发生的操作。为了帮助你编写该代码，你可以将 `sender` 参数强制转换为你所知道的类型：

```csharp
Button theButton = (Button)sender;
```

然后按需调用该对象的方法和属性。由于你拥有发送对象的引用，因此可以向订阅者提问。

