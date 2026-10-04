

# 关注注意力

## 列表 4-3: 创建自定义的 RoutedUICommand

```csharp
public static RoutedUICommand SaveCommand = new RoutedUICommand("Save", typeof(UIElement));
```

构造函数中的第一个参数用于填充 `Text` 属性，第二个参数是命令在序列化时使用的名称（我通常会在第一个参数的文本后附加 `Command`），最后一个参数是 `UIElement`（在本示例中，代码规定任何 `UIElement` 都可以作为父元素）。构造函数中还有第四个参数（此处未显示），是一个 `InputGestures` 列表。

自定义的 `RoutedUICommands` 通常作为静态变量创建，这样就只有一个实例（并且使绑定更简单）。它仍然在后台代码文件（code-behind）中，因此你还没有实现关注点分离，但你正在朝着目标迈进！

## 命令绑定

与内置命令（它们是框架的一部分，并自动连接到 `CommandManager` 和绑定系统）不同，自定义命令并不是内置。你需要在 XAML 中进行三个更改来支持自定义命令：

- 在命名空间声明中添加命令的命名空间。
- 将命令赋值更改为绑定表达式。
- 将命令添加到容器的绑定集合中。

正如我解释的那样，你可以为 `Window` 添加自定义命名空间声明，以允许 XAML 访问自定义类和命名空间。自定义命令的命名空间（如果命令是静态变量，则与后台代码的命名空间相同）需要添加到 `Window` 标签中。列表 4-4 显示了命名空间声明的示例。粗体文本与标准 WPF `Window` 中的默认命名空间声明相比的变化。

## 列表 4-4: 更新后的自定义 RoutedUICommand 的 XAML

```xml
<Window Class="Chapter4.Commands.CommandBindingSample" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:Commands="clr-namespace:Chapter4.Commands" Title="Command Binding" Height="122" Width="261">
```

将命名空间引入 `Window` 后，必须将命令插入 `Window.CommandBindings` 集合中。你需要设置三个主要属性，如列表 4-5 所示：

- Command: 绑定到命令对象的绑定
- CanExecute: 用于测试执行状态的事件处理器
- Executed: 执行命令的事件处理器

对于内置命令，只需将一个简单的字符串分配给 `UIElement`。对于自定义命令，你必须使用绑定表达式（如第 3 章中讨论的）。静态命令的格式为：

```xaml
{x:Static NamespaceReference:Class.CommandVariableName}
```

`NamespaceReference` 是分配给 `Window` 标签的名称。有趣的是，`CanExecute` 和 `Executed` 属性被直接设置为方法——不需要任何复杂的绑定！

## 列表 4-5: Window CommandBindings XAML

```xml
<Window.CommandBindings>
    <CommandBinding Command="{x:Static:CommandBindingSample.SaveCommand}"
                    CanExecute="Save,SaveExecute"
                    Executed="Save,Executed"/>
</Window.CommandBindings>
```

`CommandBinding` 的 `Command` 属性和 `UIElements` 使用与列表 4-6 所示相同的绑定表达式。当 `UIElement` 绑定了命令时，框架会沿着元素树向上查找 `CommandBindings` 部分的第一个匹配项。当找到项后，`UIElement` 将使用分配的事件处理器 `CanExecute` 和 `Execute`。

## 列表 4-6: 为 MenuItem 和 Button 分配命令

```xml
<MenuItem Command="{x:Static Commands:CommandBindingSample.SaveCommand}"/>
<Button Command="{x:Static Commands:CommandBindingSample.SaveCommand}"
        Content="{Binding Source={RelativeSource Mode=Self}, Path=Command.Text}"/>
```

`RoutedUICommand` 的 `CanExecute` 事件处理器使用 `CanExecuteRoutedEventArgs` 对象而不是返回 `True` 或 `False`。

将 `e.CanExecute` 设置为 `True`（可以运行）或 `False`（不可运行）将启用或禁用命令（以及任何关联 UIElement）。

如果命令已启用，当 `UIElement` 触发命令时（例如点击按钮时），将执行 `Executed` 事件。

## 命令参数

`CanExecuteRoutedArgs` 和 `ExecutedRoutedArgs` 包含一个属性，提供了从 `Window` 将对象传递到 `CanExecute` 和 `Executed` 处理器的机制。在示例 4-5 中，`TextBox` 的文本作为参数传递。在 `CanExecute` 事件处理器中，如果字符串为空，`CanExecuteRoutedArgs` 的 `CanExecute` 属性被设置为 `False`，而 `Executed` 事件处理器会在消息框中向用户显示。好吧，这不是一个现实的示例，但这是一个演示！

列表 4-7 和 4-8 显示了如何通过 XAML 向命令传递参数，然后在 C# 事件实现中使用该参数。

## 列表 4-7: 命令参数的更新 XAML

```xaml
<Button Command=
```

## 列表 4-8: 更新后的 C# 以向用户显示参数

```csharp
private void Save_CanExecute(object sender, ExecutedRoutedEventArgs e)
{
    e.CanExecute = !string.IsNullOrEmpty(e.Parameter as string);
}
private void Save_Executed(object sender, ExecutedRoutedEventArgs e)
{
    MessageBox.Show(e.Parameter.ToString());
}
```

![Commanding Attention](img/6df7bb88e9302e98442acc219cfbd7fc_656_0.png)

# 实战 WPF: 使用 ICommand 的自定义命令

`RoutedCommands` 解决了从显示机制（在本例中为 WPF）获取的问题。为了通过将逻辑从 UI 中移动来实现关注点分离，命令使用了 `ICommand` 接口。

- 签名中没有 `sender` 和 `ExecutedRoutedEventArgs` 参数。
- `CanExecute` 事件处理器返回 `bool`。
- `CanExecuteChanged` 事件挂钩到 `CommandManager`。
- `Command` 接口没有 `Text` 属性；只有在绑定 `MenuItem` 和 `Button` 时才需要它。

## 列表 4-9: CustomSaveCommand

```csharp
public class CustomSaveCommand : ICommand
{
    public string Text { get; set; }
    public CustomSaveCommand(string text)
    {
        Text = text;
    }

    public void Execute(object parameter)
    {
        //在此处插入保存代码
        //向用户显示反馈
        MessageBox.Show(parameter.ToString());
    }

    public bool CanExecute(object parameter)
    {
        return !string.IsNullOrEmpty(parameter as string);
    }

    public event EventHandler CanExecuteChanged
    {
        add { CommandManager.RequerySuggested += value; }
        remove { CommandManager.RequerySuggested -= value; }
    }
}
```

在示例中，自定义命令通过后台代码实例化，方式与之前示例中的自定义 `RoutedUICommand` 相同。下一节详细介绍了将命令暴露给 XAML 的更好方法。

