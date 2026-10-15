

```
public string Title
{
    get
    {
        return title;
    }
    set
    {
        title = value;
        RaisePropertyChanged("Title");
    }
}

public string Description
{
    get
    {
        return description;
    }
    set
    {
        description = value;
        RaisePropertyChanged("Description");
    }
}

private void InitializeCommands()
{
    // when someone uses a context menu to delete THIS book,
    // broadcast a message so any affected viewmodels
    // can handle it (e.g the global book list)
    RemoveBookCommand = new RelayCommand(
        () =>
            Messenger.Default.Send<RemoveBookMessage>(
                new RemoveBookMessage(this)));
}
}
```

RelayCommand 是 MVVM Light 框架自带的一个类。该类为在命令执行时将被执行的代码提供了一个包装器。此外，它还为用于确定命令是否可执行而将被执行的代码提供了一个包装器。当你将普通按钮绑定到命令时，它们会运行 RelayCommand 中返回 true 或 false 的自定义代码。当代码返回 false 时，按钮将被禁用。

总而言之，命令提供了一种将 UI 元素以声明方式绑定到代码块的可重用包装器的方式。这些命令可以使用 Blend 或 Visual Studio 2010 的设计器绑定，也可以通过手工输入 XAML 来绑定。再次强调，我喜欢尽可能保持声明性，因此我非常喜欢在可能的情况下使用命令来响应 UI 事件。

WP7 中有一个地方与命令不兼容：应用程序栏。应用程序栏控件不是真正的 Silverlight 控件，尽管人们努力让它们看起来像真正的控件，但它们的行为与 Silverlight 控件的行为不同。这是因为应用程序栏存在于应用程序主框架之外，并且可以根据应用栏的不透明度设置来缩小或扩展应用程序。对于应用程序栏菜单项，你仍然需要响应单击事件。然而，这并不意味着你必须在代码隐藏中直接嵌入代码；你可以将该单击转发给一个命令。在下面的代码中，我将应用栏上的 Add 按钮的单击转发给一个向主视图模型添加书籍的命令：

```
private void addBookButton_Click(object sender, System.EventArgs e)
{
    var vm = DataContext as MainViewModel;
    if (vm != null)
    {
        vm.AddBookCommand.Execute(null);
    }
}
```

最后，在 Listing 16.2 的底部，你可能注意到了 Messenger.Default.Send 代码。巧合的是，这引出了我的下一个主题：消息传递。

## 使用 MVVM Light 发送消息

在尝试保持关注点清晰分离时，最难做到的事情之一就是避免对依赖对象进行直接方法调用。这之所以成为问题，是因为每次你这样做时，你就在应用程序的两层之间串起了一根意大利面条，最终，这根意大利面条变得如此难以解开（而不破坏），以至于维护应用程序的唯一方法就是不断在上面堆放更多的肉丸。

消息传递是保持关注点清晰分离的另一种方式，同时确保 MVVM 应用程序中的所有参与者都遵守脚本。消息传递（也被称为“pub/sub”或许多人所说的“pub sub”）允许应用程序的组件在重要事情发生时进行广告宣传，而无需提前知道需要做出什么响应。这将执行值得注意事件的应用程序部分与响应它们的应用程序部分解耦。

在 Listing 16.2 中，你看到了创建 RemoveBookCommand 对象实例的以下代码：

```
RemoveBookCommand = new RelayCommand(
    () => Messenger.Default.Send<RemoveBookMessage>(
        new RemoveBookMessage(this));
```

在这段代码中，我的意思是每次执行 RemoveBookCommand 时（无论如何或为何执行），当前视图模型（Book）都会向所有订阅者发送一条消息，表明有一本书已被标记为删除。

为什么不确保 Book 视图模型的每个实例都有对 MainView 模型的引用？这样，书就可以直接从列表中删除自己。这种模式的问题在于它违反了 MVVM 开发的“不要向上查找”原则，并且意味着每当我们希望任何其他视图模型对书籍的删除做出响应时，我们都必须将该代码放在 Book 视图模型中，而不是放在适当的视图模型中。

## 不要向上查找

> Jesse Liberty 关于 MVVM 开发有一个非常流行的名言，简单地说就是“不要向上查找”。在构建视图模型时牢记这一点，将有助于指导你构建更好的 MVVM 架构。简而言之，永远不要从视图模型中引用“更高”级别的任何东西。这意味着你的视图模型不应该能够直接引用父视图模型，也不应 ever 对与该视图关联的视图页面（XAML）有直接引用。在我们的例子中，Book 视图模型永远不应该引用 MainViewModel。

与其维护对主视图模型的直接引用并直接操作书籍列表，我们改为发布一条消息（RemoveBookMessage）。无论它在应用程序中的位置如何，订阅该消息的任何视图模型在消息发送时都会被告知此消息。

以下代码来自 MainViewModel 中的构造函数，展示了我们如何订阅书籍删除消息并在不违反两个视图模型之间的分离的情况下执行最终的书籍删除：

```
Messenger.Default.Register<RemoveBookMessage>(this, RemoveBook);
```

然后 RemoveBook 方法的实现执行实际的视图模型操作：

```
public void RemoveBook(RemoveBookMessage removeMessage)
{
    DeleteBookFromList(removeMessage.Book);
}
```

值得在此指出的是，到目前为止我们所操作的东西仅限于视图模型。当我们进入服务提供者主题时，你将看到我们如何干净优雅地将此视图模型连接到一个支持或持久化存储。

## 看，代码隐藏都没有！

使用消息传递可以做的另一件事是将其与属性更改通知结合起来。这允许你自动通知其他视图模型属性何时更改，本质上将标准属性更改通知系统的范围扩展到 MVVM Light 的消息“总线”。

为了向你展示如何做到这一点，我将带你了解一个解决方案，该方案解决了需要在应用程序中保持关注点清晰分离时出现的经典问题：页面之间的转换。对于我们的示例应用程序，当用户点击一本书时，他们将被带到另一个页面。该页面包含一个 pivot 视图，让用户可以翻阅该书的角色、地点、情节、灵感和场景。

当点击项目时应由视图模型处理而不是代码隐藏处理时，你如何从一个页面转换到另一个页面？直接从主页面实例化详情页面并导航到它是否违反了关注点分离？这场争论可能还会持续数百年，但我个人的观点是，如果我能避免页面之间的直接耦合，我就会这样做。

看看我列表框声明的 XAML：

```
<ListBox x:Name="bookListBox"
ItemsSource="{Binding Books}"
ItemTemplate="{StaticResource bookItemTemplate}"
SelectedItem="{Binding Path=SelectedBook, Mode=TwoWay}">
</ListBox>
```

我在这里所做的是将列表框的 SelectedItem 属性绑定到我在视图模型中称为 SelectedBook 的属性。此绑定是双向的，因此我可以通过从代码更改值来影响 UI，或者 UI 可以在用户点击项目时影响我的代码。以下是我的 SelectedBook 属性的定义：

```
public Book SelectedBook
{
    get
    {
        return selectedBook;
    }
    set
    {
        var oldValue = selectedBook;
        if (oldValue == value) return;
        selectedBook = value;
        // broadcast this to all listening viewmodels, not just bound UI
        RaisePropertyChanged("SelectedBook", oldValue, selectedBook, true);
        this.SelectedBook = null;
    }
}
```

