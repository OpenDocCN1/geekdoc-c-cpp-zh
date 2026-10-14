

当前所选项目的 value。 如果你实现数据绑定以在 ComboBox 控件的下拉列表中显示项目列表，用户选择的值必须是该列表的成员。 在 Customers 应用中，你可以通过设置 SelectedValue 属性，像这样为 title ComboBox 控件的所选值配置数据绑定：

Click here to view code image

```
<ComboBox ... x:Name="title" ... SelectedValue="{Binding Title}" ... />
```

然而，请记住，下拉列表的值列表是硬编码在 XAML 标记中的，像这样：

Click here to view code image

```
<ComboBox ... x:Name="title" ... >
    <ComboBoxItem Content="Mr"/>
    <ComboBoxItem Content="Mrs"/>
    <ComboBoxItem Content="Ms"/>
    <ComboBoxItem Content="Miss"/>
</ComboBox>
```

该标记在控件创建之前不会被应用，因此数据绑定指定的值在列表中找不到，因为在数据绑定构造时列表尚不存在。 结果是该值不会显示。 你可以尝试一下——按刚所示配置 SelectedValue 属性的绑定并运行应用。 title ComboBox 在初始显示时将为空，尽管客户的头衔是 Mr。

这个问题有几种解决方案，但最简单的方法是创建一个包含有效值列表的数据源，然后指定 ComboBox 控件应使用此列表作为其下拉列表的值集。 此外，你需要在为 ComboBox 应用数据绑定之前执行此操作。

## 为 title ComboBox 控件实现数据绑定

- 1. 在 Visual Studio 中，在代码和文本编辑器窗口中显示 MainPage.xaml.cs 文件。
- 2. 将以下以粗体显示的代码添加到 MainPage 构造函数中：

Click here to view code image

```
public MainPage()
{
    this.InitializeComponent();

    List<string> titles = new List<string>
    {
        "Mr", "Mrs", "Ms", "Miss"
    };

```
```
this.title.ItemsSource = titles;
this.cTitle.ItemsSource = titles;

Customer customer = new Customer
{
    ...
};

this.DataContext = customer;
}
```

此代码创建了一个包含客户可以拥有的有效头衔的字符串列表。 然后代码将两个 title ComboBox 控件的 ItemsSource 属性设置为引用此列表（请记住每个视图都有一个 ComboBox 控件）。

### Note

在商业应用中，你很可能会从数据库或其他数据源检索 ComboBox 控件显示的值列表，而不是像本示例中那样使用硬编码列表。

此代码的放置很重要。 它必须在设置 MainPage 表单的 DataContext 属性的语句之前运行，因为在此语句中会发生对表单上控件的数据绑定。

- 3. 在设计视图窗口中显示 MainPage.xaml 文件。
- 4. 修改 title 和 cTitle ComboBox 控件的 XAML 标记，如下所示以粗体显示：

Click here to view code image

```
<Grid x:Name="customersTabularView" ...>
    ...
    <ComboBox Grid.Row="1" Grid.Column="3" x:Name="title" ...
SelectedValue="{Binding Title, Mode=TwoWay}">
        </ComboBox>
    ...
</Grid>
<Grid x:Name="customersColumnarView" ...>
    ...
    <ComboBox Grid.Row="1" Grid.Column="1" x:Name="cTitle" ...
SelectedValue="{Binding Title, Mode=TwoWay}">
        </ComboBox>
    ...
</Grid>
```

请注意，每个控件的 ComboBoxItem 元素列表已被移除，并且 SelectedValue 属性被配置为使用数据绑定与 Customer 对象中的 Title 字段。

- 5. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用程序。
- 6. 验证客户头衔的值是否正确显示（应为 Mr）。 单击 ComboBox 控件的下拉箭头并验证其是否包含值 Mr、Mrs、Ms 和 Miss。
- 7. 调整窗口大小以在窄视图中显示应用并执行相同的检查。 请注意，你可以更改头衔，并且当你切换回宽视图时，新头衔会显示。
- 8. 返回 Visual Studio 并停止调试。

## 创建 ViewModel

你现在已经看到了如何配置数据绑定以将数据源连接到用户界面中的控件，但你使用的数据源非常简单，只包含单个客户。 在现实世界中，数据源可能要复杂得多，由不同类型对象的集合组成。 请记住，在 MVVM 术语中，数据源通常由模型提供，并且 UI（视图）仅通过 ViewModel 对象间接与模型通信。 这种方法的理由是模型和显示模型提供的数据的视图应该是独立的； 如果用户界面被修改，你不应更改模型，也不应在底层模型更改时调整 UI。

ViewModel 在视图和模型之间提供连接，并且还实现了应用的业务逻辑。 同样，此业务逻辑应独立于视图和模型。 ViewModel 通过实现一组命令将业务逻辑公开给视图。 UI 可以根据用户在应用中导航的方式触发这些命令。 在以下练习中，你将通过实现包含 Customer 对象列表的模型并创建提供用户可在视图中在客户之间移动的命令的 ViewModel 来扩展 Customers 应用。

## 创建用于管理客户信息的 ViewModel

- 1. 打开 Customers 项目，该项目位于你的文档文件夹中的 \Microsoft Press\VCSBS\Chapter 26\ViewModel 文件夹中。 该项目包含上一组练习中 Customers 应用的完整版本； 如果你愿意，可以继续使用你自己的项目版本。
- 2. 在 Solution Explorer 中，右键单击 Customers 项目，指向 Add，然后单击 Class。
- 3. 在 Add New Items – Customers 对话框中，在 Name 框中键入 ViewModel.cs，然后单击 Add。

此类提供了一个基本 ViewModel，其中包含 Customer 对象的集合。 用户界面将绑定到此 ViewModel 公开的数据。

4. 在显示 ViewModel.cs 文件的代码和文本编辑器窗口中，将类标记为 public 并将以下示例中以粗体显示的代码添加到 ViewModel 类：

Click here to view code image

```
public class ViewModel
{
    private List<Customer> customers;

    public ViewModel()
    {
        this.customers = new List<Customer>
        {
            new Customer
            {
                CustomerID = 1,
                Title = "Mr",
                FirstName="John",
                LastName="Sharp",
                EmailAddress="john@contoso.com",
                Phone="111-1111"
            },
            new Customer
            {
                CustomerID = 2,
                Title = "Mrs",
                FirstName="Diana",
                LastName="Sharp",
                EmailAddress="diana@contoso.com",
                Phone="111-1112"
            },
            new Customer
            {
                CustomerID = 3,
                Title = "Ms",
                FirstName="Francesca",
                LastName="Sharp",
                EmailAddress="frankie@contoso.com",
                Phone="111-1113"
            }
        };
    }
}
```

ViewModel 类使用 List<Customer> 对象作为其模型，并且构造函数使用一些示例数据填充此列表。 严格来说，这些数据应保存在单独的 Model 类中，但为了本练习的目的，我们将使用此示例数据。

5. 将以下代码中以粗体显示的私有变量 currentCustomer 添加到 ViewModel 类，并在构造函数中将其初始化为零：

Click here to view code image

```
class ViewModel
{
    private List<Customer> customers;
    private int currentCustomer;

    public ViewModel()
    {
        this.currentCustomer = 0;
        this.customers = new List<Customer>
        {
            ...
        }
    }
}
```

ViewModel 类将使用此变量来跟踪视图当前显示的 Customer 对象。

6. 在构造函数之后，将以下以粗体显示的 Current 属性添加到 ViewModel 类：

Click here to view code image

```
class ViewModel
{
    ...

    public ViewModel()
    {
        ...
    }
    public Customer Current
    {
        get { return this.customers.Count > 0 ? this.customers[currentCustomer] : null; }
    }
}
```

Current 属性提供对模型中当前 Customer 对象的访问。 如果没有客户，则返回 null 对象。

