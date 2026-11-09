

```
if (temp != null) temp(sender, e);
}
}
```

现在，我们可以将 `OnNewMail` 方法重写如下：

```
protected virtual void OnNewMail(NewMailEventArgs e) {
    e.Raise(this, ref m_NewMail);
}
```

使用 `MailManager` 作为基类型的类可以自由重写 `OnNewMail` 方法。这一能力让派生类能够控制事件的引发。派生类可以按照自己认为合适的任何方式处理新邮件消息。通常，派生类型会调用基类型的 `OnNewMail` 方法，以便已注册的方法收到通知。不过，派生类也可以决定不允许事件被转发。

## 步骤 #4：定义一个将输入转换为所需事件的方法

你的类必须具有某种方法，它接收一些输入并将其转换为事件的引发。在我的 `MailManager` 示例中，调用 `SimulateNewMail` 方法来表示新邮件消息已到达 `MailManager`：

```
internal class MailManager {

    // Step #4: Define a method that translates the
    // input into the desired event
    public void SimulateNewMail(String from, String to, String subject) {

        // Construct an object to hold the information we wish
        // to pass to the receivers of our notification
        NewMailEventArgs e = new NewMailEventArgs(from, to, subject);

        // Call our virtual method notifying our object that the event
        // occurred. If no type overrides this method, our object will
        // notify all the objects that registered interest in the event
        OnNewMail(e);
    }
}
```

`SimulateNewMail` 接收有关消息的信息，并构造一个 `NewMailEventArgs` 对象，将消息信息传递给其构造函数。然后调用 `MailManager` 自己的虚方法 `OnNewMail`，以正式通知 `MailManager` 对象新邮件消息已到达。通常，这会导致事件被引发，从而通知所有已注册的方法。（如前所述，使用 `MailManager` 作为基类的类可以重写此行为。）

## 编译器如何实现事件

现在你已经知道如何定义提供事件成员的类，让我们更仔细地看看事件到底是什么以及它是如何工作的。在 `MailManager` 类中，有一行代码定义了事件成员本身。

```
public event EventHandler<NewMailEventArgs> NewMail;
```

当 C# 编译器编译上面这一行时，它会将这一行源代码转换为以下三个构造：

```
/// 1. A PRIVATE delegate field that is initialized to null
private EventHandler<NewMailEventArgs> NewMail = null;

// 2. A PUBLIC add_XXX method (where Xxx is the Event name)
// Allows methods to register interest in the event.
public void add_NewMail(EventHandler<NewMailEventArgs> value) {
    // The loop and the call to CompareExchange is all just a fancy way
    // of adding a delegate to the event in a thread-safe way
    EventHandler<NewMailEventArgs> prevHandler;
    EventHandler<NewMailEventArgs> newMail = this.NewMail;
    do {
        prevHandler = newMail;
        EventHandler<NewMailEventArgs> newHandler =
            (EventHandler<NewMailEventArgs>) Delegate.Combine(prevHandler, value);
        newMail = Interlocked.CompareExchange<EventHandler<NewMailEventArgs>>(
            ref this.NewMail, newHandler, prevHandler);
    } while (newMail != prevHandler);
}
```

```
// 3. A PUBLIC remove_XXX method (where Xxx is the Event name)
// Allows methods to unregister interest in the event.
public void remove_NewMail(EventHandler<NewMailEventArgs> value) {
    // The loop and the call to CompareExchange is all just a fancy way
    // of removing a delegate from the event in a thread-safe way
    EventHandler<NewMailEventArgs> prevHandler;
    EventHandler<NewMailEventArgs> newMail = this.NewMail;
    do {
        prevHandler = newMail;
        EventHandler<NewMailEventArgs> newHandler =
            (EventHandler<NewMailEventArgs>) Delegate.Remove(prevHandler, value);
        newMail = Interlocked.CompareExchange<EventHandler<NewMailEventArgs>>(
            ref this.NewMail, newHandler, prevHandler);
    } while (newMail != prevHandler);
}
```

第一个构造只是相应委托类型的一个字段。该字段是对委托列表头部的引用，当事件发生时，这些委托将被通知。该字段初始化为 `null`，表示没有监听者注册对该事件的兴趣。当某个方法注册对事件的兴趣时，该字段引用一个 `EventHandler<NewMailEventArgs>` 委托实例，该实例可能还引用其他 `EventHandler<NewMailEventArgs>` 委托。当监听者注册对事件的兴趣时，监听者实际上只是将该委托类型的一个实例添加到列表中。显然，取消注册意味着从列表中移除该委托。

你会注意到，委托字段（本例中的 `NewMail`）始终是 private 的，即使原始源代码行将事件定义为 public。将委托字段设为 private 的原因是为了防止定义类之外的代码不正当地操作它。如果该字段是 public 的，任何代码都可以更改该字段的值，并可能清除所有已注册对该事件感兴趣的委托。

C# 编译器生成的第二个构造是一个方法，允许其他对象注册对事件的兴趣。C# 编译器自动通过在事件名称（`NewMail`）前加上 `add_` 来命名此函数。C# 编译器自动生成此方法内部的代码。该代码总是调用 `System.Delegate` 的静态 `Combine` 方法，该方法将委托实例添加到委托列表中，并返回列表的新头部，然后将其保存回字段中。

C# 编译器生成的第三个构造是一个方法，允许对象注销对事件的兴趣。同样，C# 编译器自动通过在事件名称（`NewMail`）前加上 `remove_` 来命名此函数。此方法内部的代码总是调用 `Delegate` 的静态 `Remove` 方法，该方法从委托列表中移除委托实例，并返回列表的新头部，然后将其保存回字段中。

**警告** 如果你尝试移除一个从未添加过的方法，那么 `Delegate` 的 `Remove` 方法在内部不会执行任何操作。也就是说，你不会得到任何类型的异常或警告；事件的方法集合保持不变。

**注意** `add` 和 `remove` 方法使用一种众所周知的模式以线程安全的方式更新值。这一模式在第 29 章的“The Interlocked Anything Pattern”一节中讨论。

在本例中，`add` 和 `remove` 方法是 public 的。它们之所以是 public 的，是因为原始源代码行将事件声明为 public。如果事件被声明为 protected，编译器生成的 `add` 和 `remove` 方法也将被声明为 protected。因此，当你在类型中定义事件时，事件的可访问性决定了哪些代码可以注册和注销对该事件的兴趣，但只有类型本身才能直接访问委托字段。事件成员还可以声明为 static 或 virtual，在这种情况下，编译器生成的 `add` 和 `remove` 方法将分别是 static 或 virtual。

除了生成上述三个构造之外，编译器还会在托管程序集的元数据中生成一个事件定义条目。该条目包含一些标志和底层委托类型，并引用 `add` 和 `remove` 访问器方法。该信息的存在只是为了在“事件”的抽象概念与其访问器方法之间建立关联。编译器和其他工具可以使用该元数据，并且也可以通过使用 `System.Reflection.EventInfo` 类来获取该信息。然而，CLR 本身不使用该元数据信息，在运行时只需要访问器方法。

## 设计一个监听事件的类型

到目前为止，艰巨的工作肯定已经完成了。在本节中，我将向你展示如何定义一个使用其他类型提供的事件的类型。让我们先检查 `Fax` 类型的代码：

```
internal sealed class Fax {
    // Pass the MailManager object to the constructor
    public Fax(MailManager mm) {

        // Construct an instance of the EventHandler<NewMailEventArgs>
        // delegate that refers to our FaxMsg callback method.
        // Register our callback with MailManager's NewMail event
        mm.NewMail += FaxMsg;
    }

    // This is the method the MailManager will call
    // when a new email message arrives
    private void FaxMsg(Object sender, NewMailEventArgs e) {

        // 'sender' identifies the MailManager object in case
        // we want to communicate back to it.

        // 'e' identifies the additional event information
        // the MailManager wants to give us.

        // Normally, the code here would fax the email message.
        // This test implementation displays the info in the console
        Console.WriteLine("Faxing an email message:");
        Console.WriteLine("  From={0}, To={1}, Subject={2}",
            e.From, e.To, e.Subject);
    }

    // This method could be executed to have the Fax object unregister
    // itself when the NewMail event so that it no longer receives
    // notifications
    public void Unregister(MailManager mm) {

        // Unregister with MailManager's NewMail event
        mm.NewMail -= FaxMsg;
    }
}
```

当电子邮件应用程序初始化时，它首先会构造一个 `MailManager` 对象，并将对该对象的引用保存在一个变量中。然后，应用程序会构造一个 `Fax` 对象，并将 `MailManager` 对象的引用作为参数传递。在 `Fax` 构造函数中，`Fax` 对象使用 C# 的 `+=` 运算符注册它对 `MailManager` 的 `NewMail` 事件的兴趣：

```
mm.NewMail += FaxMsg;
```

