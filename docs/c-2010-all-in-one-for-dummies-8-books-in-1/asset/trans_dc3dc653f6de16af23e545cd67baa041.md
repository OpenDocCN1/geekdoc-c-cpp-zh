

# 深入了解 WPF 数据绑定 599

WPF 提供了许多项控件（ItemsControls）控件，允许你将对象集合绑定到它们上。ItemsControl 的示例包括 ListBox 和 ComboBox（以及其他）。集合通过 `ItemsSource` 属性绑定到 ItemsControl。可以通过 `ItemTemplate` 属性为通过 ItemsControl 绑定的每个对象应用数据模板。

第 V 卷
第 3 章

通过属性继承，ListBox 的 `ItemsSource` 默认设置为 Window 的 `DataContext`。空的 `[Binding]` 元素简单地表明它将使用其父级元素的当前绑定，该绑定会沿着元素树向上递归，直到到达设置了绑定的地方。记住，由于我们将 DataContext 绑定到 Servers 列表并应用于 Window 身，ListBox 将继承该绑定作为自身的 `ItemsSource`。

## WPF 中的数据绑定

在资源中定义的描述 `ServerStatus` 对象的数据模板将用于渲染每个绑定的对象。你可以通过 `ItemTemplate` 属性看到这一点，它使用了指向在资源中定义的 `ServerTemplate` 的 `StaticResource`。

现在，当你运行应用程序时，你将以一种美观的方式呈现 `ServerStatus` 数据！（请参见图 3-6。）

图 3-6：
使用值转换器和数据模板渲染数据集合。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_624_0.png)

# 深入了解 WPF 数据绑定

本章并非涵盖 WPF 数据绑定支持的所有功能。WPF 数据模板的其他方面也值得关注这些概念：

- *DataTemplateSelector*：这是一个基类，允许你根据某些逻辑条件渲染数据模板。
-   使用数据模板作为一种手段，为用户提供数据添加/编辑功能。
-   根据用户的偏好在运行时切换数据模板。这允许用户随意切换数据模板。例如，在列表中，你可能只显示摘要信息；但是，你可以在数据模板中提供一个按钮，允许用户根据需要切换在摘要模板和更详细的模板之间切换。

# 第 4 章：实战 WPF

### 本章内容

-   吸引注意力
-   让你的 ViewModel 运行起来

尽管 WPF 仍然支持直接的事件处理程序连接（针对 `OnClick` 事件），但 WPF 引入了一种得多的机制来响应用户事件。它显著减少了你需要编写的代码量，并为你的应用程序增加了可测试性。传统的事件处理全部包含在表单的后台代码（code-behind）中，这极难以自动方式进行测试。

软件模式已经存在很久了，并以经典的《设计模式：可重用面向对象软件的元素》（由 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vissides 编写，通常被称为“四人帮”）为引领。软件一直在演进，多年来开发了许多新模式。为 WPF 开发的最有效的用户界面模式之一是 Model-View-ViewModel 模式（通常称为 ViewModel）。在应用程序中使用 ViewModel 模式将提高重用性、可测试性、可读性、可维护性以及大多数其他“属性”。

# 吸引注意力

命令模式（Command Pattern）自很久以来就一直存在，而且你很可能每天都在使用它。复制和粘贴命令是 Windows 和 Windows 应用程序内置模式的示例实现。WPF 提供了大量的内置命令，还允许完全自定义的命令！

传统的用户事件处理（在 WPF 中仍然支持）是通过事件处理程序。当按钮被点击时，事件处理程序（必须在后台代码处理程序中）将执行。将此代码放在用户界面代码中，会混合关注点。事实上，框架中没有任何东西强制将代码写在后台代码中，它只是总是最终落到那里。

当向 Window 添加了需要执行代码的额外 UIElements 时，情况会变得更加复杂。这种情况的常见解决方法是将原始事件处理程序中的代码重构到一个单独的方法，并让相关 UIElements 的事件处理程序调用该方法。

# 602 吸引注意力

新方法甚至可以移动到业务层，分离关注点并允许进行测试。

另一个问题是用户体验问题。通常，菜单和按钮需要根据 Window 中数据状态（或某些条件/用户操作）积极启用或禁用。如果用户有选择权，他们倾向于反复点击“激活”项目，疑惑为什么没有发生事情。毕竟，他们从生就被训练要寻找你应用程序中的漏洞。

在 WPF 中实现的命令模式干净且方便地解决了这些问题。

# ICommand

ICommand（此处使用的所有命令的基接口）定义了两个处理器和一个事件。请参见列表 4-1。

# 列表 4-1：ICommand 接口

```
bool CanExecute(object parameter);
void Execute(object parameter);
event EventHandler CanExecuteChanged
```

或许 WPF 命令最强大的功能是能够在运行时确定控件是否绑定了执行（详细讨论见下一节）。`CanExecute` 由 `SqlCommand` 在每次焦点更改时运行，当属性更改时，或者按需要执行。如果 `CanExecute` 返回 false，所有绑定的元素将禁用。

`CanExecuteChanged` 事件提供了一种机制，通过 `INotifyCollectionChanged` 和 `INotifyPropertyChanged` 事件来触发命令。

# 路由命令

ICommand 接口并不提供路由。`RoutedCommand` 类（及其第一个生类 `RoutedUI`）利用事件路由（Routing）来提供功能。`PreviewExecute` 事件在 `Execute` 事件发生之前触发。这些事件会向上冒泡，直到找到正确命令的元素。

# RoutedCommand 与 UICommand

`RoutedCommand` 和 `UICommand` 的唯一区别在于 `RoutedUI` 添加了一个用于装饰内容的 `Text` 属性。MenuItems 会自动获取此属性并将其赋值给 `Header` 属性。

```
Content={Binding Source={RelativeSource=Self},Path=Text}}
```

实战 WPF
第 4 章

路由命令还暴露了一组输入手势（InputGestures）——触发 `Execute` 事件的按键或其他手势。这允许为命令分配热键，例如大多数 Windows 应用程序中的 Control+S。

# 内置命令

WPF 提供了许多内置命令，你可以使用很少甚至不需要代码来使用。业务开发人员常用的集合封装在 `ApplicationCommands` 库中。使用内置命令的优势是所有的底层工作都为你完成了。例如，`CanExecute` 和 `Execute` 事件处理程序已经实现。你只需要通过 XAML 将它们绑定到 UI元素即可。

内置命令的完整列表可以访问 http://msdn.microsoft.com/en-us/library/system.windows.input.aspx。

列表 4-2 和 4-1 中的示例使用了 `ApplicationCommand.Copy` 和 `ApplicationCommand.Paste` 命令来方便应用程序中的剪贴板操作。当焦点的 UIElement 支持粘贴操作且剪贴板中有焦点元素支持的数据时，任何绑定到粘贴命令的元素都会启用；当有可以复制到剪贴板的元素被选中时，任何绑定到复制命令的元素都会启用。作为顺带说明，WPF 允许通过删除容器名称（ApplicationCommands）来简化内置命令，因此 Copy 和 Paste 是 ApplicationCommands.Copy 和 ApplicationCommands.Paste 命令的合法缩写。为了可读性，我倾向于使用全限定名称。

命令示例的完整代码位于 Chapter4 解决方案中的 Chapter4Commands 和 Chapter4CommandsTests 项目。

