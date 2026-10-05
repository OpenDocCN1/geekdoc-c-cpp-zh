

```
}
...
}
```

此代码初始化了 DispatcherTimer 对象，并在启动计时器之前将计时器事件间隔设置为一秒。

- 13. 在生成（Build）菜单上，选择生成解决方案（Build Solution），并确保你的应用程序无错误生成。

你现在可以使用 `Command` 类向 ViewModel 类添加命令了。在下一个练习中，你将定义命令以使用使用户能够在视图中的不同客户之间移动。

## 向 ViewModel 类中添加 NextCustomer 和 PreviousCustomer 命令

- 1. 在 Visual Studio 中，在代码和文本编辑器窗口打开 `ViewModel.cs` 文件。

- 2. 在文件顶部添加以下 `using` 指令，并修改 ViewModel 类定义以实现 `INotifyChanged` 接口。

点击此处查看代码

```
...
using System.ComponentModel;

namespace Customers
{
    public class ViewModel : INotifyChanged
    {
        ...
    }
}
```

- 3. 在 ViewModel 类的末尾添加 `PropertyChanged` 事件和 `OnPropertyChanged` 方法。这你在 `Customer` 类中包含的相同代码。

点击此处查看代码

```
public class ViewModel : INotifyChanged
{

public event PropertyChangedEventHandler PropertyChanged;
protected virtual void OnPropertyChanged(string propertyName)
{
    if (PropertyChanged is not null)
    {
        PropertyChanged(this,
            new PropertyChangedEventArgs(propertyName));
    }
}
```

记住，视图通过其包含的各种控件的属性绑定表达式中的 `Current` 属性引用数据。当 ViewModel 类移动到不同的客户时，它必须引发 `PropertyChanged` 事件以通知视图要显示的数据已更改。

- 4. 在构造函数之后立即向 ViewModel 类中添加以下字段和属性：

点击此处查看代码

```
public class ViewModel : INotifyPropertyChanged
{
    public ViewModel()
    {
        ...
    }
    private bool _isAtStart;
    public bool IsAtStart
    {
        get => this._isAtStart;
        set{
            this._isAtStart = value;
            this.OnPropertyChanged(nameof(IsAtStart));
        }
    }
    private bool _isAtEnd;
    public bool IsAtEnd
    {
        get => this._isAtEnd;
        set
{
this._isAtEnd = value;
this.OnPropertyChanged(nameof(IsAtEnd));
}
...
}
}
```

你将使用这两个属性来跟踪 ViewModel 的状态。当 ViewModel 中的 `currentCustomer` 字段置于客户集合的开头时，`IsAtStart` 属性将设置为 `true`；当 ViewModel 置于集合的末尾时，`IsAtEnd` 属性将设置为 `true`。

- 5. 修改构造函数以使用 `IsAtStart` 和 `IsAtEnd` 属性，如下所示**加粗**部分所示：

点击此处查看代码图片

```
public ViewModel ( {
this.currentCustomer = 0;
this.IsAtStart = true;
this.IsAtEnd = false;
this.customers = new List<Customer>
...
}
```

- 6. 在 `Current` 属性之后，向 ViewModel 类添加所示**加粗** `Next` 和 `Previous` 私有方法：

点击此处查看代码图片

```
public class ViewModel : INotifyPropertyChanged {
public Customer Current {
...
}
private void Next() {
if (this.customers.Count - 1 > this.currentCustomer) {
}
this.currentCustomer++;
this.OnPropertyChanged(nameof(Current));
this.IsAtStart = false;
this.IsAtEnd = (this.customers.Count - 1 == this.currentCustomer);
}
```

```
private void Previous()
{
    if (this.currentCustomer > 0)
    {
        this.currentCustomer--;
        this.OnPropertyChanged(nameof(Current));
        this.IsAtEnd = false;
        this.IsAtStart = (this.currentCustomer == 0);
    }
    ...
}
```

> 注意
`Count` 属性返回集合中的项目数，但请记住集合中的项是从 0 到 `Count - 1` 编号的。

这些方法更新 `currentCustomer` 变量以指向 `customers` 列表中的下一个（或上一个）客户。注意这些方法维护了 `IsAtStart` 和 `IsAtEnd` 属性的值，并且通过引发 `Current` 属性的 `PropertyChanged` 事件来指示当前客户已更改。这些方法是私有的，因为它们不应从 ViewModel 类的外部访问。外部类将使用命令运行这些方法，你将在后续步骤中添加这些命令。

- 7. 向 ViewModel 类添加 `NextCustomer` 和 `PreviousCustomer` 自动属性，如下所示**加粗**：

点击此处查看代码图片

```
public class ViewModel : INotifyPropertyChanged
{

private List<Customer> customers;
private int currentCustomer;
public Command NextCustomer { get; private set; }
public Command PreviousCustomer { get; private set; }
...
}
```

视图将绑定到这些 `Command` 对象，以便使用户能够在客户之间导航。

- 8. 在 ViewModel 构造函数中，将 `NextCustomer` 和 `PreviousCustomer` 属性指向新的 `Command` 对象，如下：

点击此处查看代码图片

```
public ViewModel()
{
    this.CurrentCustomer = 0;
    this.IsAtStart = true;
    this.IsAtEnd = false;
    this.NextCustomer = new Command(this.Next, () => 
        this.customers.Count > 1 && !this.IsAtEnd);
    this.PreviousCustomer = new Command(this.Previous, () => 
        this.customers.Count > 0 && !this.IsAtStart);
    this.customers = new List<Customer>
}
```

`NextCustomer` 对象将 `this.Next` 方法指定为调用时执行的操作。Lambda 表达式 `() => this.customers.Count > 1 && !this.IsAtEnd` 在客户列表数量大于 1 且不在末尾时返回 `true`。`PreviousCustomer` 对象遵循相同的模式：它指定 `this.Previous` 方法为在执行时从列表中检索上一个客户。`CanExecute` 方法引用 `() => this.customers.Count > 0 && !this.IsAtStart`，当客户数量大于 0 时返回 `true`。

- 9. 在生成（Build）菜单上，选择生成解决方案，验证你的应用程序无错误生成。

现在你已经为 ViewModel 添加了 `NextCustomer` 和 `PreviousCustomer`，可以将它们绑定到视图。

## 在视图上添加 Next 和 Previous 按钮

- 1. 在设计视图中打开 `MainPage.xml` 文件。

- 2. 滚动到 XAML 格底部，在 `</Grid>` 标签之后、`</Page>` 标签之前添加以下标记：

点击此处查看代码

```
</Grid>
<Page.TopAppBar
  <CommandBar>
    <AppBarButton x:Name="previousCustomer" Icon="Previous" Label="Previous" Command="{Binding Path=PreviousCustomer}"/>
    <AppBarButton x:Name="nextCustomer" Icon="Next" Label="Next" Command="{Binding Path=NextCustomer}"/>
  </CommandBar>
</Page.TopAppBar>
</Page>
```

在此代码片段中有几点需要注意：

- 默认情况下，命令栏位于屏幕顶部显示它包含的按钮图标。只有在用户选择时才会显示标签。如果你正在设计一个适用于多个国家或文化的应用程序，你不应为标签提供硬编码值。相反，应将这些标签的文本存储在特定文化的资源文件中，并在运行时动态绑定 Label 属性。

- CommandBar 只能包含一组特定的控件（实现 `CommandBarElement` 接口的控件）。这包括 `AppBarToggleButton` 和 `AppBarSeparator` 控件。这些控件是专门为在命令栏中操作而设计的。如果你尝试向命令栏添加此类控件，你将收到错误消息“指定的值无法赋值给集合”。

- UWP 应用模板包含了各种库存图标（如先前示例代码中的 Previous 和 Next），你可以在 `IconButton` 控件上显示它们。你也可以定义自己的图标和位图。

- 每个按钮都有一个 `Command` 属性，这是你可以将其绑定到实现 `ICommand` 接口对象的属性。在此应用程序中，你已将按钮绑定到 ViewModel 类中的命令。当用户在运行时选择任一按钮时，相应的命令将运行。

- 3. 在调试（Debug）菜单上，选择开始调试。客户应该出现并显示 John Sharp 的详情。命令栏应该显示在表单顶部，并包含 Next 和 Previous 按钮，在图中右上角高亮显示：

