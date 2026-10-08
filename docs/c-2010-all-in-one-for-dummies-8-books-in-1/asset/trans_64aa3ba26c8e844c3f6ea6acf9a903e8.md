

# 604 吸引注意力

列表 4-2: XAML 中的内置命令

```xml
<Menu Grid.Row="0" Grid.Column="0" HorizontalAlignment="Left"
Name="menu">
  <MenuItem Command="ApplicationCommands.Copy"/>
  <MenuItem Command="ApplicationCommands.Paste"/>
</Menu>
<TextBox Grid.Row="1" Grid.Column="0"
HorizontalAlignment="Stretch"/>
<TextBox Grid.Row="2" Grid.Column="0"
HorizontalAlignment="Stretch"/>
```

图 4-1 至 4-3 显示了由列表 4-2 中的 XAML 生成的不同状态下的窗口。当文本框中选中文字时，“复制”菜单将启用。当剪贴板中有可以粘贴到文本框的数据时，“粘贴”菜单将启用。这一切无需编写任何代码即可！

图 4-1: 内置命令（剪贴板为空且无选择）。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_629_0.png)

图 4-2: 内置命令（剪贴板为空且有文字选择）。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_629_1.png)

图 4-3: 内置命令（剪贴板有数据且无文字选择）。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_629_2.png)

# 焦点！

我知道你急于问的问题：如果用户点击了菜单项，该菜单项难道不会获得焦点吗？答案是“不！”。这是因为 WPF 中的菜单通过一些“魔法”操作在点击菜单项之前确定哪个 UElement 拥有焦点。

遗憾的是，这并不适用于标准按钮和其他命令绑定的控件。尽管图 4-4 中的菜单项是启用的，但按钮并没有启用。解决这个问题有两个方法。第一种是在绑定命令的同时，还将将 `CommandTarget` 属性绑定到 `UElement`。不过这只是单个元素的解决方案。要解决所有元素的问题，需要在父容器中将 `FocusManager.IsSharedScope` 属性设置为 `True`。

Practical WPF 第 4 章

图 4-4: 带有按钮的内置控件。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_630_0.png)

# 自定义命令

创建自定义命令需要实例化一个新的 `RoutedUICommand` 或者基于 `ICommand` 接口编写新命令。嗯，你是对的——还有其他方法。最流行的两种就是我在这里讨论的。

# 自定义 UI 命令

创建一个新的 `RoutedUICommand` 是一个简单的实例化，如列表 4-3 所示。

# 列表 4-3: 创建自定义 RoutedUICommand

```csharp
public static RoutedUICommand SaveCommand = 
new RoutedUICommand("Save", "SaveCommand", 
typeof(UIElement));
```

构造函数中的第一个参数填充了 `Text` 属性，第二个参数是命令序列化时使用的名称（我通常会在第一个参数的文本后附加 `Command`），最后一个参数是 `UIParent`。（在本示例中，代码规定任何 `UElement` 都可以作为父级。）另一个构造函数中还有第四个参数（此处未显示），它是 `InputGestures` 列表。

# 606 吸引注意力

自定义的 `RoutedUICommands` 通常创建为静态变量，这样只有一个实例（并且使绑定更简单）。是的，它仍然在代码后台文件中，所以我们还没有实现关注点分离（Separation of Concerns），但我们正在朝着这个目标努力！

# 命令绑定

与内置命令（它们框架的一部分，并自动连接到 `CommandManager` 和绑定系统）不同，自定义命令不是新的。为了支持自定义命令，需要在 XAML 中进行三处更改：

- 添加命名空间声明的命名空间引用。
- 将命令赋值更改为绑定表达式。
- 将命令添加到容器的绑定集合中。

如第 1 章所解释，你可以向 `Window` 添加自定义命名空间声明，以允许自定义类和命名空间。自定义命令的命名空间（如果命令是代码后台的静态变量，则与 `Window` 相同的命名空间）需要添加到 `Window` 中，列表 4-4 显示了一个命名空间声明示例。粗体文本与标准 WPF Window 中的默认命名空间声明相比发生变化的地方。

# 列表 4-4: 更新的自定义 RoutedUI 的 XAML

```xml
<Window x:Class="Chapter4.CommandBindingSample"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:commands="clr-namespace:Chapter4.Commands"
Title="Command Binding" Height="122" Width="261">
```

将消息引入窗口后，必须将其插入到 `Window.CommandBindings` 集合中。需要设置三个正确的属性，如列表 4-5 所示：

- Command: 绑定到命令对象
- CanExecute: 用于测试执行状态的事件处理程序
- Executed: 用于执行命令的事件处理程序

对于内置命令，只需将简单的字符串赋值给 `UIElement` 的命令。对于自定义命令，你必须使用绑定表达式（如第 3 章所述）。静态命令绑定的格式为：

```xml
{x:Static NamespaceReference:Class.CommandVariableName}
```

# 607 吸引注意力

`NamespaceReference` 是分配给 `Window` 标签的别名。有趣的是，`CanExecute` 和 `Executed` 属性被设置为方法的值——不需要任何奇怪的绑定！

第五 卷
第 4 章

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_632_0.png)

# 列表 4-5: Window CommandBindings XAML

```xml
<Window.CommandBindings>
<CommandBinding Command="(x:Static
Commands:CommandBindingSample.SaveCommand)"
CanExecute="Save_CanExecute"
Executed="Save_Executed"/>
</Window.CommandBindings>
```

`CommandBinding` 的 `Command` 属性和 `UIElements` 使用与列表 4-6 所示相同的绑定表达式。当 `UIElement` 绑定了命令时，框架会在 `CommandBindings` 部分查找第一个匹配项。

# 列表 4-6: 赋值给 MenuItem 和 Button 的命令

```xml
<MenuItem Command="x:Static
Commands:CommandBindingSample.SaveCommand"/>
<Button Command="x:Static
Commands:CommandBindingSample.SaveCommand"
Content="Binding RelativeSource
Mode=Self}, Path=Command.Text"/>
```

`RoutedUICommand` 的 `CanExecute` 事件处理程序使用 `CanExecuteRoutedEventArgs` 而不是返回 `True` 或 `False`。将 `Execute` 设置为 `True`（可以运行）或 `False`（不能运行）将启用或禁用命令（或任何关联 UElement）。

如果命令是启用的，当 `UIElement` 触发命令时（例如点击按钮时），将执行 `Executed` 事件处理程序。

# 命令参数

`CanExecuteRoutedEventArgs` 和 `ExecutedRoutedEventArgs` 包含一个 `Parameter` 属性，提供了从 `Window` 将对象传递 `CanExecute` 和 `Executed` 事件处理程序的机制。在图 4-5 的示例中，TextBox 的文本被作为参数传递。如果字符串为空或空，`CanExecute` 事件处理程序中 `CanExecuteRoutedEventArgs` 的 `CanExecute` 属性将设置为 `False`，`Executed` 事件处理程序会在消息框中向用户显示。好吧，这不是一个真实的例子，但这是一个演示！

# 608 吸引注意力

列表 4-7 和 4-8 显示了如何通过 XAML 将参数传递给命令并在 C# 事件实现中使用该参数。

# 列表 4-7: 更新的 XAML 以包含参数

```xml
<Button Command="x:Static
Commands:CommandBindingSample.SaveCommand"
CommandParameter="Binding ElementName=txtField,
Path=Text"
Content="Binding RelativeSource
Mode=Self}, Path=Command.Text"/>
```

# 列表 4-8: 更新的 C# 以显示命令参数

```csharp
private void Save_CanExecute(object sender,
CanExecuteRoutedEventArgs e)
{
    e.Execute = !String.IsNullOrEmpty(e.Parameter as
string);
}
private void Save_Executed(object sender,
ExecutedRoutedEventArgs e)
{
    MessageBox.Show(e.Parameter.ToString());
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_633_0.png)

# 使用 ICommand 的自定义命令

自定义 `RoutedUICommands` 解决了消除所有那些糟糕的 `OnClick` 事件处理程序的问题，将执行代码合并到一个事件处理程序，并带来了 `CanExecute` 事件处理程序的优点，从而实现更动态、直观的用户界面。

为了通过从代码后台移除实现来实现真正的关注点分离，请使用 `ICommand` 接口从头实现命令。`ICommand` 接口包含了 `CanExecute` 和 `Executed` 事件处理程序以及 `CanExecuteChanged` 事件。

