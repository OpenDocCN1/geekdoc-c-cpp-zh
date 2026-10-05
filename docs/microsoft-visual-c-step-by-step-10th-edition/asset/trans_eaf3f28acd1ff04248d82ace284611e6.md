

```xml
Text="Binding Current.EmailAddress, Mode=TwoWay" ... />
... 
<TextBox Grid.Row="5" Grid.Column="3" x:Name="phone" ...
Text="Binding Current.Phone, Mode=TwoWay " ... />
</Grid>
<Grid x:Name="customersColumnarView" Margin="20,10,20,110" ...>
```

```xml
<TextBox Grid.Row="0" Grid.Column="1" x:Name="cid"
Text="Binding Current.CustomerID, Mode=TwoWay" ... />
<TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName"
Text="Binding Current.FirstName, Mode=TwoWay" ... />
<TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName"
Text="Binding Current.LastName, Mode=TwoWay" ... />
<ComboBox Grid.Row="1" Grid.Column="1" x:Name="cTitle"
SelectedValue="Binding Current.Title, Mode=TwoWay" />
</ComboBox>
```

```xml
<TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail"
Text="Binding Current.EmailAddress, Mode=TwoWay" ... />
<TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone"
Text="Binding Current.Phone, Mode=TwoWay" ... />
</Grid>
```

11. 在“调试”菜单上，选择“启动调试”以编译并运行应用程序。

12. 验证应用程序是否显示了 John Sharp（客户列表中的第一个客户）的详情。更改客户的详情并在视图之间切换，以证明数据绑定仍然正常运行。

13. 返回 Visual Studio 并停止调试。

ViewModel 通过 `Current` 属性访问客户信息；目前，它没有提供在客户之间导航的方法。你可以实现增加和递减 `currentCustomer` 变量的方法，以便 `Current` 属性能够检索不同的客户，但你应该以一种不将视图与 ViewModel 耦合的方式进行。

通常通用的技术是使用命令模式（Command pattern）。在这种模式下，ViewModel 以命令的形式暴露方法，供视图调用。技巧在于避免在视图的代码中通过名称显式引用这些方法。为了实现这一点，XAML 允许你声明式地将命令绑定到由 UI 控件触发的操作，正如你将在下一节的练习中看到的那样。

# 向 ViewModel 中添加命令

将控件的操作绑定到命令的 XAML 标记要求 ViewModel 暴露的命令实现 `ICommand` 接口。该接口定义了以下项目：

- CanExecute: 此方法返回一个布尔值，指示命令是否可以运行。使用此方法，ViewModel 可以根据上下文启用或禁用命令。例如，一个从列表中获取下一个客户的命令应该只有在有下一个客户可以获取时才能运行；如果没有更多客户，则该命令应被禁用。
- Execute: 此方法在命令被调用时运行。
- CanExecuteChanged: 当 ViewModel 的状态发生变化时，会触发此事件。在这些情况下，之前可以运行的命令现在可能被禁用，反之亦然。例如，如果 UI 调用了一个从列表中获取下一个客户的命令，且该客户是最后一个客户，那么后续后续对 `CanExecute` 的调用将返回 `false`。在这种情况下，应该触发 `CanExecuteChanged` 事件以指示命令已禁用。

在下一个练习中，你将创建一个实现 `ICommand` 接口的泛类。

# 实现 Command 类

1. 在 Visual Studio 中，右键点击 `Customers` 项目，指向“添加”，然后选择“类”。
2. 在“添加新建项 – Customers”对话框中，选择“类”模板。在“名称”框中输入 `Command.cs`，并选择“添加”。
3. 在显示 `Command.cs` 文件的代码和编辑器窗口中，向文件顶部的列表添加以下 `using` 指令：
4. 将 `Command` 类设为公共，并指定它实现了 `ICommand` 接口，如下**加粗**所示：

点击此处查看代码图像

```csharp
using System.Windows;
```

`ICommand` 接口定义在此命名空间中。

点击此处查看图像

```csharp
public class Command : ICommand
{
}
```

5. 向 `Command` 类中添加以下私有字段：

点击此处查看图像

```csharp
public class Command : ICommand
{
  private Action methodExecute = null;
  private Func<bool> methodToDetectExecute = null;
}
```

`Action` 和 `Func` 类型在第 20 章“解耦应用程序逻辑和处理事件”中有简要描述。`Action` 是一个委托，你可以用它引用一个没有参数且没有返回的方法。`Func<T>` 类型也是一个委托，可以引用一个没有参数但返回由参数 `T` 指定的类型值的方法。

在此类中，你将使用 `methodExecute` 字段来引用 Command 对象在被视图调用时将运行的代码。`methodToDetectExecute` 字段将用于引用检测命令是否可以运行的方法。（取决于应用程序或数据状态，可能会由于某些原因被禁用。）

6. 为 `Command` 类添加一个构造函数。此构造函数应该接受两个参数：一个 `Action` 对象和一个 `Func<T>` 对象。将这些参数分配给 `methodExecute` 和 `methodToDetectExecute` 字段，如下处所示：

点击此处查看图像

```csharp
public class Command : ICommand
{
  public Command(Action methodExecute, Func<bool> methodToDetectExecute)
  {
    methodExecute = methodExecute;
    methodToDetectExecute = methodToDetectExecute;
  }
}
```
*(注：此处示例代码逻辑似乎有赋值错误，但按原文翻译保留)*

7. 使用 `methodExecute` 和 `methodToDetectExecute` 字段实现 `Command` 类的 `Execute` 和 `CanExecute` 方法，如下：

点击此处查看图像

```csharp
public class Command : ICommand
{
  public void Execute(object parameter)
  {
    methodExecute?.Invoke();
  }

  public bool CanExecute(object parameter)
  {
    return methodToDetectExecute?.Invoke() ?? false;
  }
}
```

ViewModel 将为命令创建实例。ViewModel 将提供运行的方法以及检测命令是否可以启用的方法。

8. 在 `Command` 类中添加 `CanExecuteChanged` 事件：

点击此处查看图像

```csharp
public class Command : ICommand
{
  public bool CanExecute(object parameter)
  {
    ...
  }
  public event EventHandler CanExecuteChanged;
}
```

当你将命令绑定到控件时，控件会订阅此事件。当对象状态 way时，该事件会触发。最简单的策略是使用定时器每秒触发一次 `CanExecute` 事件。

9. 向文件顶部的列表添加以下 `using` 指令：

点击此处查看图像

```csharp
using System.Threading;
```

10. 在 `Command` 类中构造函数之前添加以下字段：

点击此处查看图像

```csharp
public class Command : ICommand
{
    private Func<bool> methodToDetectExecute = null;
    private DispatcherTimer canExecuteEventTimer = null;
    public Command(Action methodExecute, Func<bool> methodToDetectExecute)
    {
        ...
    }
}
```

11. 在 `Command` 类的末尾按以下**加粗**的代码添加 `canExecuteEventHandler_Tick` 方法：

点击此处查看图像

```csharp
public class Command : ICommand
{
  ...
  public event EventHandler CanExecuteChanged;

  void canExecuteEventHandler_Tick(object sender, object e)
  {
    if (this.CanExecuteChanged != null)
      this.CanExecuteChanged(this, EventArgs.Empty);
  }
}
```

12. 在 `Command` 构造函数中，添加以下**加粗**语句：

点击此处查看图像

```csharp
public class Command : ICommand
{
  ...
  public Command(Action methodExecute, Func<bool> methodToDetectExecute)
  {
    this.methodExecute = methodExecute;
    this.methodToDetectExecute = methodToDetectExecute;

    this.canExecuteEventTimer = new DispatcherTimer();
    this.canExecuteEventTimer.Tick += canExecuteEventHandler_Tick;
    this.canExecuteEventTimer.Interval = new TimeSpan(0, 0, 1);
    this.canExecuteEventTimer.Start();
  }
}
```
