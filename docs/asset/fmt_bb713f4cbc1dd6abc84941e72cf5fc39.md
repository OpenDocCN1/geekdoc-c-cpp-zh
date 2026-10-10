
```csharp
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

### 5. 修改构造函数以使用 `IsAtStart` 和 `IsAtEnd` 属性，如下所示**加粗**部分所示：

点击此处查看代码图片

```csharp
public ViewModel ( {
this.currentCustomer = 0;
this.IsAtStart = true;
this.IsAtEnd = false;
this.customers = new List<Customer>
...
}
}
```

### 6. 在 `Current` 属性之后，向 ViewModel 类添加所示**加粗** `Next` 和 `Previous` 私有方法：

点击此处查看代码图片

```csharp
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

```csharp
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

### 7. 向 ViewModel 类添加 `NextCustomer` 和 `PreviousCustomer` 自动属性，如下所示**加粗**：

点击此处查看代码图片

```csharp
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

### 8. 在 ViewModel 构造函数中，将 `NextCustomer` 和 `PreviousCustomer` 属性指向新的 `Command` 对象，如下：

点击此处查看代码图片

```csharp
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

### 9. 在生成（Build）菜单上，选择生成解决方案，验证你的应用程序无错误生成。

现在你已经为 ViewModel 添加了 `NextCustomer` 和 `PreviousCustomer`，可以将它们绑定到视图。

## 在视图上添加 Next 和 Previous 按钮

1. 在设计视图中打开 `MainPage.xml` 文件。

2. 滚动到 XAML 格底部，在 `</Grid>` 标签之后、`</Page>` 标签之前添加以下标记：

点击此处查看代码

```xml
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

3. 在调试（Debug）菜单上，选择开始调试。客户应该出现并显示 John Sharp 的详情。命令栏应该显示在表单顶部，并包含 Next 和 Previous 按钮，在图中右上角高亮显示：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1055_0.png)

注意，“上一个”按钮不可用。这是因为 ViewModel 的 `IsAtStart` 属性为 `true`，而“上一个”按钮引 Command 对象的 `CanExecute` 方法指示命令无法运行。

4. 选择命令栏上的省略号按钮。按钮标签将会出现。这些标签将一直显示直到你选择命令栏上的其中一个按钮。

5. 在命令栏上，选择**Next**（下一步）。
客户 2 Diana Sharp 的详情应当出现，在短暂的延迟（长达一秒）后，“上一个”按钮将变为可用。`IsAtStart` 属性不再为 `true`，因此命令的 `CanExecute` 方法返回 `true`。然而，在命令中的计时器对象过期并触发 `CanExecuteChanged` 事件之前，按钮不会收到此状态变化的通知，这可能需要一秒钟才会发生。

> 注意
> 如果你对命令状态的变化有更即时的响应，可以安排 Command 类中的计时器更频繁地过期。然而，避免过度减少时间；过于频繁地触发 `CanExecuteChanged` 事件会影响 UI 的性能。

6. 在命令栏上，再次选择 Next。
7. 客户 3 Francesca Sharp 的详情应当出现，在有一到两秒的短暂延迟后，“下一步”按钮将不再可用。这次，ViewModel 的 `IsEnd` 属性为 `true`，因此“下一步”按钮对应的 Command对象的 `CanExecute` 方法返回 `false`，该命令被禁用。
8. 调整窗口大小以在窄视图显示应用程序，并验证应用程序继续正常运行。“下一步”和“上一个”按钮应该能够在客户列表中前后回移动。
9. 返回到 Visual Studio 并停止调试。

## 总结

在本章中，你学习了如何在表单上显示数据，如何为表单设置数据上下文，以及如何通过实现 `INotifyPropertyChanged` 接口创建支持数据绑定的数据源。你还学习了如何使用模型-视图-ViewModel（MVVM）模式创建 UWP 应用程序，并看到了如何创建一个 ViewModel 以及一个通过命令与数据源进行交互的视图。

## 快速参考

| 目的 | 操作 |
|---|---|
| 将控件的属性绑定到对象的属性 | 在控件的 XAML 标记中使用数据绑定表达式。例如：[点击此处查看代码图像](#) |

```xml
<TextBox ... Text="Binding FirstName" ...//>
```

### 允许对象向绑定发送数据值更改的通知

在定义对象的类中实现 `INotifyPropertyChanged` 接口，并在每次属性值更改时抛出 `PropertyChanged` 事件。例如：

点击此处查看代码图像

```csharp
class Customer : INotifyPropertyChanged
{
    ...
    public event PropertyChangedEventHandler PropertyChanged;
    protected virtual void OnPropertyChanged(string propertyName)
    {
        if (PropertyChanged is not null)
        {
            PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

### 允许使用数据绑定的控件更新其所绑定的属性值

将数据绑定配置为双向绑定。例如：

点击此处查看代码图像

```xml
<TextBox ... Text="Binding FirstName, Mode=TwoWay" .../>
```

### 当用户从包含 Button 控件的界面中选择 Button 控件时，分离运行的业务逻辑

使用提供通过 `ICommand` 接口实现的命令的 ViewModel，并将 Button 控件绑定到这些命令中的一个。例如：

点击此处查看代码图像

```xml
<Button xName="nextCustomer" ... Command="{Binding Path=NextCustomer}"/>
```
