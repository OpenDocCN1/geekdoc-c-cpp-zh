

# 发生了 — C# 事件 373

```csharp
public class NewEditionEventArgs : EventArgs
{
    public NewEditionEventArgs(DateTime date, string majorHeadline)
    { Date = date; Head = majorHeadline; }
    public DateTime Date { get; private set; } // 编译器创建详细信息。
    public string Head { get; private set; } //n
}
```
```

你应该像上一个代码示例那样，将此类的成员实现为属性。构造函数使用了属性上的私有设置器语句（private setter clauses）。

通常，你的事件不需要任何额外的参数，你可以直接退而使用 `EventArgs` 基类，如下一节所示。

如果你的事件不需要特殊的 `EventArgs` 派生对象，只需传递：

```csharp
NewEdition(this, EventArgs.Empty); // 触发事件。
```

## 触发你的事件的推荐方法

早些章节“如何发布事件”展示了触发事件的骨架。然而，我建议你始终定义一个特殊的“事件触发”方法，如下所示：

```csharp
protected void OnNewEdition(NewEditionEventArgs e)
{
    EventHandler<NewEditionEventArgs> temp = NewEdition;
    if (temp == null)
    {
        temp(this, e);
    }
}
```

提供此方法可以确保你始终记得完成两个步骤：

- 1. **将事件存储在临时变量中。**

这一步使得你的事件在多个“线程”尝试同时使用它的情况下更具可用性——线程将你的程序分为前台任务和多个后台任务，它们是同时运行（并发）的。我在这里不会介绍如何编写多线程程序；只需遵循此指南即可。

- 2. **在触发事件之前检查事件是否为空。**

如果它是 null，尝试触发它会导致错误。此外，null 意味着没有其他对象对你的事件表现出兴趣（没有订阅者）；无论你是否写了这个 `OnSomeEvent` 方法，务都要检查事件是否为 null。

![](img/36596fb11aa4233d5cab0d6ddd1d82e_398_0.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e_398_1.png)

# 374 发生了 — C# 事件

将方法设为 `protected` 和 `virtual` 允许子类重写方法。这是可选的。

在你拥有该方法后（它始终具有相同的形式，便于快速编写），你需要在需要触发事件时调用该方法：

```csharp
void SomeMethod()
{
    // 在此处执行一些操作，然后：
    NewEditionEventArgs args = 
        new NewEditionEventArgs(DateTime.Today, "战争爆发!");
    OnNewEdition(args);
}
```

## 观察者如何“处理”事件

订阅对象在订阅时指定处理程序方法的名称——它是构造函数的参数（**粗体**）：

```csharp
button1.Click += new EventHandler<NewEditionEventArgs>(button1_Click);
```

这行代码的意思是：“请将我发送到这个地址。”这里是 `NewEdition` 事件的处理程序：

```csharp
myPublisher.NewEdition += new EventHandler<NewEditionEventArgs>(NewHandler);
void NewHandler(object sender, NewEditionEventArgs args)
{
    // 响应事件执行某些操作。
}
```

例如，`BankAccount` 类可以在 `BankAccount` 对象中发生存款、取款、转账或错误时触发一个自定义的 `TransactionAlert` 事件。一个 `Logger` 观察者对象可以订阅并将这些事件记录到文件中或作为审计跟踪。

![](img/36596fb11aa4233d5cab0d6ddd1d82e_399_0.png)

## 何时使用委托，何时使用事件，何时使用 lambda

**事件 (Events)**：当你有多个订阅者，或者与使用你类类的客户端软件通信时，使用事件。

**Lambda**：这本书的配套网站上有一篇关于 lambda 的文章。Lambda 表达式本质上只是指定传递给委托的方法的简短方式。你可以使用 lambda 代替匿名方法。

**委托 (Delegates)**：当你需要回调或需要随机化操作时，使用委托或匿名方法。

![](img/36596fb11aa4233d5cab0d6ddd1d82e_400_0.png)

当你在 Visual Studio 中创建按钮处理程序时（通过双击表单上的按钮），Visual Studio 会在 `Form.Designer.cs` 文件中生成订阅代码。你不应该编辑订阅代码，但可以将其删除并在你的部分表单类（partial form class）的另一部分编写相同的代码。之后，表单设计器对此一无所知。

在你的订阅者处理方法中，你可以编写当类感知此类事件时应该发生的任何操作。为了帮助你编写该代码，你可以将 `sender` 参数转换为你已知的类型：

```csharp
Button btn = (Button)sender;
```

然后根据需要使用该对象的所有方法和属性。因为你拥有发送对象的引用，如果需要，你可以向订阅者提问并对其执行操作——就像送报纸的人敲门收取月费一样。而且，你也可以相同的方式通过获取 `e` 参数的属性从 `e` 参数中提取信息：

```csharp
Console.WriteLine(e.Date);
```

