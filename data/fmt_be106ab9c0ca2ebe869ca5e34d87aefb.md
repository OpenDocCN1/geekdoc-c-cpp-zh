
注意，每个控件的 `ComboBoxItem` 元素列表已被移除，且 `SelectedValue` 属性已配置为与 `Customer` 对象中的 `Title` 字段进行数据绑定。

- 5. 在“调试”菜单上，点击“启动调试”以生成并运行应用程序。
- 6. 验证客户头衔的值是否正确显示（应为 Mr）。点击 `ComboBox` 控件的下拉箭头，验证它是否包含 Mr、Mrs、Ms 和 Miss 这些值。
- 7. 调整窗口大小以窄视图视图显示应用程序，并执行相同的检查。注意你可以更改标题，当切换回宽视图视图时，新标题将会显示。
- 8. 返回 Visual Studio 并停止调试。

## 创建 ViewModel

你已经了解了如何创建一个包含客户可能拥有的有效衔的字符串列表，然后指定 `ComboBox` 控件应使用其作为其下拉列表的值集。此外，你需要在应用 `ComboBox` 的数据绑定之前执行此操作。你已经看到了如何创建一个包含客户可能拥有的有效衔的字符串列表。代码随后设置了两个标题 `ComboBox` 控件的 `ItemsSource` 属性以引用此列表（记住每个视图都有一个 `ComboBox` 控件）。

> 注意：在商业应用程序中，你很可能会从数据库或其他数据源中检索由 `ComboBox` 控件显示的值列表，而不是像本示例中这样使用硬编码的列表。

这段代码的位置非常重要。它必须在设置 `MainPage` 表单 `DataContext` 属性的语句之前运行，因为该语句是表单上控件数据绑定发生的地方。

## 为标题 ComboBox 控件实现数据绑定

- 1. 在 Visual Studio 中，在代码和文本编辑器中显示 `MainPage.xaml.cs` 文件。
- 2. 在 `MainPage` 构造函数中添加以下**粗体**的代码：

```
public void MainPage()
{
    this.InitializeComponent();
    List<string> titles = new List<string>
    {
        "Mr", "Mrs", "Ms", "Miss"
    };
    this.title.ItemsSource = titles;
    this.cTitle.ItemsSource = titles;
    Customer customer = new Customer
    {
    ..\};
    this.DataContext = customer;
}
```

此代码创建了一个包含客户可能拥有的有效衔的字符串列表。然后，代码将两个标题 `ComboBox` 控件的 `ItemsSource` 属性设置为引用此列表（记住每个视图都有一个 `ComboBox` 控件）。

> 注意：在商业应用程序中，你很可能会从数据库或其他数据源中检索由 `ComboBox` 控件显示的值列表，而不是像本示例中这样使用硬编码的列表。

这段代码的位置非常重要。它必须在设置 `MainPage` 表单 `DataContext` 属性的语句之前运行，因为该语句是表单上控件数据绑定发生的地方。

- 3. 在设计视图中显示 `MainPage.xml` 文件。
- 4. 修改 `title` 和 `cTitle` `ComboBox` 控件的 XAML 标记，此处**粗体**所示：

```
<Grid x:Name="customersTabularView" ...>
<ComboBox Grid.Row="1" Grid.Column="3" x:Name="title" ...
SelectedValue="Binding Title, Mode=TwoWay"}
</ComboBox>
<Grid x:Name="customersColumnarView" ...>
<ComboBox Grid.Row="1" x:Name="cTitle" ...
SelectedValue="Binding Title, Mode=TwoWay"}
</ComboBox>
</Grid>
```

注意，每个控件的 `ComboBoxItem` 元素列表已被移除，且 `SelectedValue` 属性已配置为与 `Customer` 对象中的 `Title` 字段进行数据绑定。

## 为客户信息创建 ViewModel

结果是该值没有显示。如果你愿意，可以尝试此操作——如上所示为 `SelectedValue` 属性配置绑定并运行应用程序。当 `title` ComboBox 初始显示时它是空的，尽管客户拥有“Mr”头衔。

```
<Grid x:Name="customersTabularView" ... >
  <TextBox Grid.Row="1" Grid.Column="1" x:Name="id" ...
    Text="{Binding Current.CustomerID, Mode=TwoWay}" />
  <TextBox Grid.Row="1" Grid.Column="5" x:Name="firstName" ...
    Text="{Binding Current.FirstName, Mode=TwoWay}" />
  <TextBox Grid.Row="1" Grid.Column="7" x:Name="lastName" ...
    Text="{Binding Current.LastName, Mode=TwoWay}" />
  <ComboBox Grid.Row="1" Grid.Column="3" x:Name="title" ...
    SelectedValue="{Binding Current.Title, Mode=TwoWay}" />
  <TextBox Grid.Row="3" Grid.Column="3" x:Name="email" ...
    Text="{Binding Current.EmailAddress, Mode=TwoWay}" />
  <TextBox Grid.Row="5" Grid.Column="3" x:Name="phone" ...
    Text="{Binding Current.Phone, Mode=TwoWay}" />
</Grid>

<Grid x:Name="customersColumnView" Margin="20, 10, 20, 110" ...>
  <TextBox Grid.Row="0" Grid.Column="1" x:Name="Cid" ...
    Text="{Binding Current.CustomerID, Mode=TwoWay}" />
  <TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName" ...
    Text="{Binding Current.FirstName, Mode=TwoWay}" />
  <TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName" ...
    Text="{Binding Current.LastName, Mode=TwoWay}" />
  <ComboBox Grid.Row="3" Grid.Column="1" x:Name="cTitle" ...
    SelectedValue="{Binding Current.Title, Mode=TwoWay}" />
  <TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail" ...
    Text="{Binding Current.EmailAddress, Mode=TwoWay}" />
  <TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone" ...
    Text="{Binding Current.Phone, Mode=TwoWay}" />
</Grid>
```

- 11. 在“调试”菜单上，点击“开始调试”以生成并运行应用程序。
- 12. 验证应用程序是否显示了 John Sharp（客户列表中的第一个客户）的详情。更改客户详情并在视图之间切换，以证明数据绑定仍在正常工作。
- 13. 返回 Visual Studio 并停止调试。

ViewModel 通过 `Current` 属性访问客户信息，目前它尚未提供一种在客户之间进行导航的方法。你可以实现增加和递减 `currentCustomer` 变量的方法，以便 `Current` 属性能够检索不同的客户，但你应该以一种不将视图与 ViewModel 耦合的方式来这样做。最广泛接受的技术是使用命令模式（Command pattern）。在这一模式中，ViewModel 以命令的形式暴露方法，视图可以调用这些方法。技巧在于避免在视图的代码中显式地通过名称引用这些方法。为了实现这一点，XAML 允许你以声明的方式将命令绑定到由 UI 控件触发的操作上，正如你将在下一节的练习中看到的那样。

## 向 ViewModel 中添加命令

将控件的操作绑定到命令的 XAML 标记要求 ViewModel 暴露的命令必须实现 `ICommand` 接口。该接口定义了以下项目：

- CanExecute: 此方法返回一个布尔值，指示命令是否可以运行。使用此方法，ViewModel 可以根据上下文启用或禁用命令。例如，从列表中获取下一个客户的命令应该只在有下一个客户可以获取时才运行；如果没有更多客户，则该命令应被禁用。
- Execute: 此方法在命令被调用时运行。
- ExecuteChanged: 当 ViewModel 的状态发生变化时会触发此事件。在这种情况下，之前可以运行的命令可能会被禁用，反之亦然。例如，如果 UI 调用了一个一个从列表中获取下一个客户的命令，而该客户是最后一个客户，则对 `CanExecute` 的后续调用应返回 `false`。在这种情况下，应该触发 `ExecuteChanged` 事件以指示命令已禁用。

在下一个练习中，你将创建一个实现 `ICommand` 接口的泛型类。

## 实现 Command 类

- 1. 在 Visual Studio 中，右键点击 Customers 项目，指向“添加”，然后点击“类”。
- 2. 在“添加新建项 - Customers”对话框中，选择“类”模板。在名称框中，输入 `Command.cs`，然后点击“添加”。
- 3. 在显示 `Command.cs` 文件的代码文本编辑器窗口中，在文件顶列表中添加以下 `using` 指令：

```csharp
using System.Windows.Input;
```

`ICommand` 接口定义在此命名空间中。

- 4. 将 Command 类设为公共，并指定它实现了 Command 接口，如下加粗部分所示：

```csharp
public class Command : ICommand
{
}
```

- 5. 为 Command 类添加以下私有字段：

```csharp
public class Command : ICommand
{
    private Action methodExecute = null;
    private Func<bool> methodToDetectCanExecute = null;
}
```

`Action` 和 `Func` 类型将在第 20 章“解耦应用程序逻辑”中简要描述。`Action` 类型是一个委托，用于引用要执行的方法；而 `Func<bool>` 类型是一个不接受参数但返回一个值的委托，用于检测是否应该启用命令。ViewModel 将提供要执行的方法以及检测命令是否可以运行的方法。

- 6. 为 Command 类添加构造函数。该构造函数应接受两个参数：一个 `Action` 对象和一个 `Func<bool>` 对象。将这些参数赋值给 `methodExecute` 和 `methodToDetectCanExecute` 字段，如下：

```csharp
public class Command : ICommand
{
    ...
}
```

```csharp
public Command(Action methodExecute, Func<bool> methodToDetectCanExecute)
{
    this.methodExecute = methodExecute;
    this.methodToDetectCanExecute = methodToDetectCanExecute;
}
```

- 7. 使用 `methodExecute` 和 `methodToDetectCanExecute` 字段实现 Command 类的 `Execute` 和 `CanExecute` 方法如下：

```csharp
public class Command : ICommand
{
    public Command(Action methodExecute, Func<bool> methodToDetectCanExecute)
    {
    }
}
```

```csharp
public void Execute(object parameter)
{
    this.methodExecute();
}
```

```csharp
public bool CanExecute(object parameter)
{
    if (this.methodToDetectCanExecute == null)
    {
        return true;
    }
    else
    {
        return this.methodToDetectCanExecute();
    }
}
```
