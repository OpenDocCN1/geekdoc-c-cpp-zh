
### 23. 返回 MainPage.xaml 文件
在 XAML 格中，修改 `customersTabularView` 控件中每个标签的 `TextBlock` 控件标记。删除 `HorizontalAlignment`、`TextWrapping`、`VerticalAlignment` 和 `FontSize` 属性，并引用 `LabelStyle` 样式，此处**加粗**所示：

点击此处查看代码图片

```xml
<Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Visible">
  ....
  <Grid Grid.Row="2">
    ....
    <TextBlock Grid.Row="0" Column="1" Style="{StaticResource LabelStyle}" Text="ID"/>
    <TextBlock Grid.Row="0" Column="3" Style="{StaticResource LabelStyle}" Text="Title"/>
    <TextBlock Grid.Row="0" Column="5" Style="{StaticResource LabelStyle}" Text="First Name"/>
    <TextBlock Grid.Row="0" Column="7" Style="{StaticResource LabelStyle}" Text="Last Name"/>
    
    <TextBlock Grid.Row="3" Column="1" Style="{StaticResource LabelStyle}" Text="Email"/>
    ....
    <TextBlock Grid.Row="5" Column="1" Style="{StaticResource LabelStyle}" Text="Phone"/>
  </Grid>
</Grid x:Name="customersColumnar" Margin="10,20,10,20" Visibility="Collapsed">
  ....
  <Grid Grid.Row="1">
    ....
    <TextBlock Grid.Row="0" Column="0" Style="{StaticResource LabelStyle}" Text="ID"/>
    <TextBlock Grid.Row="1" Column="0" Style="{StaticResource LabelStyle}" Text="Title"/>
    <TextBlock Grid.Row="2" Column="0" Style="{StaticResource LabelStyle}" Text="First Name"/>
    <TextBlock Grid.Row="3" Column="0" Style="{StaticResource LabelStyle}" Text="Email"/>
    <TextBlock Grid.Row="4" Column="0" Style="{StaticResource LabelStyle}" Text="Last Name"/>
    <TextBlock Grid.Row="5" Column="0" Style="{StaticResource LabelStyle}" Text="Phone"/>
  </Grid>
</Grid>
```

`customersColumnGrid` 上的标签应该改变并看起来像这个 30 字体大小：`img/4fc1423ece9eb794a4edb8b1746d_113_0.png`

### 24. 在调试菜单上，选择调试以生成并运行应用程序
`Customers` 表单应该出现，并且其样式与它在设计视图中 `TextBox` 控件显示的方式相同。

> **注意**尽管 `Segoe Print` 字体适用于标签和标题，但不建议将其作为数据输入字段的字体，因为某些字符很难区分。例如，小写字母 l 与数字 1 非常相似，大写字母 o 与数字 0 无法区分。出于此原因，继续使用 `TextBox` 控件的默认字体是合理的。

### 25. 调整窗口大小使其变窄，并验证样式已应用到 `customersColumnGrid` 中的控件上
表单看起来应该像下面的图片：`img/4fc1423ece9eb794a4edb8b1746d_115_0.png`

### 26. 返回 Visual Studio 并停止调试

- 如果您想继续下一节，请保持 `Visual Studio 2022` 运行并转到第 26 节。
- 如果您现在想退出 `Visual Studio 2022`，在“文件”菜单上选择“退出”。如果看到“保存”对话框，选择“是”并保存项目。

## 快速参考

| 目标 | 执行此操作 |
|---|---|
| 创建新的 UWP 应用 | 使用 `Visual Studio 2022` 中的 UWP 模板之一，例如“空白应用”模板。 |
| 实现可缩放到不同设备形状和方向的用户界面 | 使用 `Grid` 控件。将 `Grid` 划分为行和列，并将控件放在这些行和列中，而不是相对于 `Grid` 边缘指定绝对位置。 |
| 实现可适应不同显示宽的用户界面 | 为每个视图创建不同的布局，以适当的方式显示控件。使用视觉状态管理器（Visual State Manager）在视觉状态更改时选择要显示的布局。 |
| 创建自定义样式 | 为应用添加资源字典。在字典字典中使用中使用 `<Style>` 元素定义样式，并指定每个样式更改的属性。例如： |
| 对控件应用自定义样式 | 设置控件的 `Style` 属性并通过名称引用样式。例如： |

点击此处查看代码图像

```
<Style x:Key="PageStyle" TargetType="Page">
  <Setter Property="Background" Value="StaticResource WoodBrush"/>
</Style>
```

点击此处查看代码图像

```
<Grid Style="{StaticResource PageStyle}">
```

# 在通用 Windows 平台应用中显示和搜索数据

在完成本节后，你将能够：

- 解释如何使用模型-视图-视图模型（MVVM）模式来实现通用 Windows 应用程序的逻辑。
- 使用数据绑定在视图中显示和修改数据。
- 创建一个 ViewModel，视图可以通过它与模型进行交互。

第 25 节“为通用 Windows 应用程序实现用户界面”演示了如何设计用户界面 (UI)，以适应用户运行你的程序时可能采用的各种设备形状、方向和视图。本节开发的示例应用是一个简单的程序，设计用于显示和编辑客户的详细信息。

在本节中，你将看到如何在 UI 中显示数据，并学习 Windows 11 中用于在应用程序中搜索数据的功能。在执行这些任务时，你还将学习构建通用 Windows 平台 (UWP) 应用程序的最佳方法。本节涵盖了大量内容。特别是你将将如何使用数据绑定将 UI 与其显示的数据连接起来，以及如何创建一个 ViewModel 将用户界面逻辑与应用程序的数据模型和业务逻辑分离。

# 实现模型-视图-视图模型模式

结构良好的图形应用程序会将 UI 设计与应用程序使用的数据以及构成应用程序功能的业务逻辑分离开。这种分离有助于消除各个组件之间的依赖关系，能够在不需要更改业务逻辑或底层数据模型的情况下，允许数据有不同的呈现形式。这种方法还为具有相应专业专长的人员设计和实现不同元素扫清了道路。例如，图形艺术家可以专注于设计具有吸引力且直观的 UI，数据库专家可以专注于实现一组用于存储和访问数据的优化数据结构，而 C# 开发者可以将她的精力放在实现应用程序的业务逻辑上。这种共同目标是许多开发方法的目标——在过去的几年里，已经设计出许多技术来帮助以此方式构建应用程序。

可以说，最流行的方法是遵循模型-视图-视图模型 (MVVM) 设计模式。在这种设计模式中，模型（Model）提供应用程序使用的数据，视图（View）代表数据在 UI 中的显示方式。视图模型（ViewModel）包含连接这两者的逻辑，将用户输入转换为在模型上执行业务操作的命令，并以视图期望的方式格式化数据。

下面的图显示了 MVVM 应用元素之间简化的关系。请注意，应用程序可能为相同的数据提供多个视图。例如，在 UWP 应用中，你可能实现不同的视图状态，这些状态可以通过不同的布局来呈现信息。ViewModel 的工作之一是确保来自相同模型的数据可以被许多不同的视图显示和操作。在 UWP 应用中，视图可以使用数据绑定连接到 ViewModel 呈现的数据。此外，视图可以通过调用 ViewModel 实现的命令来请求 ViewModel 更新数据或执行业务任务。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1019_0.png)

# 使用数据绑定显示数据

在开始为“客户”应用实现 ViewModel 之前，稍微了解一下数据绑定以及如何将其应用于在 UI 中显示数据是有帮助的。使用数据绑定可以将控件的属性链接到对象的属性上；那么，如果对象的指定属性值发生变化，链接到对象的控件中的属性也会发生变化。

此外，数据绑定可以是双向的。如果控件中使用数据绑定的属性值发生变化，修改将传播到控件链接到的对象上。下面的练习提供了如何使用数据绑定显示数据的简要介绍。它基于第 25 节中的“客户”应用。

# 使用数据绑定显示客户信息

1. 启动 `Visual Studio 2022`，如果它尚未运行。
2. 打开 `Customers` 解决方案，它位于文档文件夹中的 `\Microsoft Press\VCSBS\Chapter 26\DataBinding` 文件夹。这是第 25 节开发的“客户”应用程序版本，但 UI 布局经过微调；控件显示在蓝色背景上，这使得它们更加突出。

> 注意
> 蓝色背景是通过使用 `Rectangle` 控件创建的，该控件跨越了显示标题和数据的 `TextBlock` 和 `TextBox` 控件相同的行和列。矩形使用 `LinearGradientBrush` 填充，该画刷逐渐将矩形的颜色从顶部的蓝色变为底部的深蓝色。`customersTabView` `Grid` 中显示的 `Rectangle` 控件的 XAML 标记所示。（`customersLayerView` `Grid` 的 XAML 标记包含一个类似的 `Rectangle` 控件，跨越了该布局使用的行和列。）

点击此处查看代码图像

```
<Grid Grid.Rows="6" Grid.Column="1">
<Rectangle ColumnSpan="7">
  <LinearGradientBrush EndPoint="0.5,1" StartPoint="0.5,0">
    <GradientStop Color="#FF0E3895"/>
    <GradientStop Color="#FF141415" Offset="0.929"/>
  </LinearGradientBrush>
</Rectangle>
</Grid>
```

3. 在解决方案管理器中，右键点击 `Customers` 项目，指向“添加”，然后选择“类”。
4. 在“添加新建项 - Customers”对话框中，确保选择了“类”模板。在“名称”框中输入 `Customer.cs`。然后选择“添加”。

你需要实现...

5. 在显示 `Customer.cs` 文件的代码文本编辑器窗口中，将 `Customer` 类设为公共并添加此处所示的私有字段和公共属性：

点击此处查看代码图像

```
public class Customer
{
    private int _customerID;
    public int CustomerID
    {
        get => this._customerID;
        set {
            this._customerID = value;
        }
    }
    private string _title;
    public string Title
    {
        get => this._title;
        set {
            this._title = value;
        }
    }
    private string _firstName;
    public string FirstName
    {
        get => this._firstName;
```

```csharp
set
{
    this._firstName = value;
}
private string _lastName;
public string LastName
{
    get => this._lastName;
    set {
        this._lastName = value;
    }
}
private string _emailAddress;
public string EmailAddress
{
    get => this._emailAddress;
    set {
        this._emailAddress = value;
    }
}
private string _phone;
public string Phone
{
    get => this._phone;
    set {
        this._phone = value;
    }
}
```

你可能在想，为什么该类没有定义自动属性，或者为什么属性设置器没有实现为表达式体成员（expression-bodied members），考虑到它们所做的只是在私有字段中赋值。这两个问题的答案都是，你将在稍后的练习中为这些属性添加代码。

6. 在解决方案资源管理器中，进入 `Customers` 项目，双击 `MainPage.xaml` 文件，以在设计视图窗口中显示应用程序的用户界面。
7. 在 XAML 格中，找到名为 `id` `TextBox` 控件的标记。如**加粗**所示，修改设置该控件 `Text` 属性的 XAML 标记。

点击此处查看代码图像

```xml
<TextBox Grid.Row="1" Grid.Column="1" x:Name="id" ...
Text="{Binding CustomerID}" .../>
```

`syntax="Binding Path"` 语法指定 `Text` 属性的值将在运行时由 `Path` 表达式的值提供。在这种情况下，`Path` 被 `CustomerID`，因此 `CustomerID` 表达式保存的值将由此控件显示。然而，你需要提供更多信息来指示 `CustomerID` 实际上是 `Customer` 对象的属性。为了实现这一点，你需要设置控件的 `DataContext` 属性，你稍后会执行。

8. 为表上的其他每个文本控件添加以下绑定表达式。如后续代码**加粗**所示，对 `customersTableView` 和 `customersColumnarGridView` 控件中的 `TextBox` 控件应用数据绑定。（`ComboBox` 控件需要不同的处理，你将在在本章后后的“与 ComboBox 控件使用数据绑定”部分中解决。）

点击此处查看代码图像

```xml
<Grid x:Name="customersTableView" ...>

  <TextBox Grid.Row="1" Grid.Column="5" x:Name="firstName"
Text="{Binding FirstName}" .../>
  <TextBox Grid.Row="1" Grid.Column="7" x:Name="lastName"
Text="{Binding LastName}" .../>

  <TextBox Grid.Row="3" Grid.Column="3" Grid.ColumnSpan="5"
x:Name="email" ... Text="{Binding EmailAddress}" .../>
  ...
  <TextBox Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3"
x:Name="phone" ... Text="{Binding Phone}" .../>
</Grid>
<Grid x:Name="customersColumnarGridView" Margin="10,20,10,20"
Visibility="Collapsed">

  <TextBox Grid.Row="0" Grid.Column="1" x:Name="cId" 
Text="{Binding CustomerID}" .../>
  ...
```

```xml
<TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName" ...
Text="{Binding FirstName}" />
<TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName" ...
Text="{Binding LastName}" />
<TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail" ...
Text="{Binding EmailAddress}" />
<TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone" ...
Text="{Binding Phone}" />
</Grid>
```

注意绑定表达式如何可以用于多个控件。例如，表达式 `(Binding CustomerID)` 被 `id` 和 `cid` `TextBox` 引用，这导致两个控件都显示相同的数据。
