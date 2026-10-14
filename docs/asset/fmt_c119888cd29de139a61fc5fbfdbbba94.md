
`customers` 列表包含应用显示的客户；它之前使用你已删除的 `DataSource.cs` 文件中的数据填充。

`*client*` 变量使用将发送请求的 Web 服务器的地址进行初始化。REST Web 服务可以接收以多种格式发送请求和响应，但 Customers 应用将使用 JSON。前面代码中的最后一句将 `*client*` 变量配置为以此格式提交请求。

11. 在 Solution Explorer 中，展开 Customers 项目的根文件夹，双击 `Customer.cs` 文件以在代码和文本编辑器窗口中显示它。

12. 在 `*Phone*` 属性之后，立即向 `*Customer*` 类添加以下以粗体显示的公共属性：

Click here to view code image

```
public class Customer : INotifyPropertyChanged
{
    ...
    public string Phone
    {
        ...
    }
    public System.Guid rowguid { get; set; }
    public System.DateTime ModifiedDate { get; set; }
    ...
}
```

Web 服务从数据库检索这些字段，Customers 应用必须准备好处理它们；否则，如果用户决定修改客户的详细信息，这些字段将会丢失。（你将在本章后面为 Customers 应用添加此功能。）

13. 返回到 `*ViewModel*` 类。在构造函数之后，添加此处所示的公共 `*GetDataAsync*` 方法：

Click here to view code image

```
public async Task GetDataAsync()
{
    try
    {
        var response = await this.client.GetAsync("api/customers");
        if (response.IsSuccessStatusCode)
        {
            var customerData =
                await response.Content.ReadAsStringAsync();
            this.customers =
                JsonConvert.DeserializeObject<List<Customer>>
                (customerData);
            this.currentCustomer = 0;
            this.OnPropertyChanged(nameof(Current));
            this.IsAtStart = true;
            this.IsAtEnd = (this.customers.Count == 0);
        }
        else
        {
            // TODO: Handle GET failure
        }
    }
    catch (Exception e)
    {
        // TODO: Handle exceptions
    }
}
```

此方法为异步；它使用 `HttpClient` 对象的 `GetAsync` 方法调用 Web 服务中的 `api/customers` 操作。此操作从 AdventureWorks 数据库获取客户的详细信息。`GetAsync` 方法本身也是异步的，并返回包装在 `Task` 中的 `HttpResponseMessage` 对象。`HttpResponseMessage` 对象包含指示请求是否成功的状态代码，如果成功，应用将使用 `HttpResponseMessage` 对象的 `Content` 属性的 `ReadAsStringAsync` 方法实际检索 Web 服务返回的数据。此数据由包含每个客户详细信息的 JSON 格式字符串组成，因此它使用 `JsonConvert` 类的静态 `DeserializeObject` 方法转换为 `Customer` 对象列表并分配给 `customers` 集合（`JsonConvert` 类是 Json.NET 包的一部分）。然后 ViewModel 的 `currentCustomer` 属性设置为指向此集合中的第一个客户，并且 `IsAtStart` 和 `IsAtEnd` 属性被初始化以指示 ViewModel 的状态。

### Note

ASP.NET Web API 客户端库假定所有 Web 服务请求都可能需要不确定的时间来运行。因此，像 `HttpClient` 和 `HttpResponseMessage` 这样的类被设计为支持异步操作，以防止应用在等待响应时被阻塞。事实上，这些类仅支持异步操作；`GetAsync` 或 `ReadAsStringAsync` 没有同步版本。

请注意，目前 `GetDataAsync` 方法不会处理任何异常或失败，只是静默地消耗它们。你将在本章后面看到在 UWP 应用中报告异常的技术。

### Note

在生产应用中，你不应不必要地通过网络获取数据。相反，你应该选择性地检索数据。然而，在此应用中，AdventureWorks 数据库仅包含几百个客户，因此它们全部被检索并缓存在 `customers` 列表中。

14. 修改 `Current` 属性的 get 访问器，如下所示：

Click here to view code image

```
public Customer Current
{
    get
    {
        if (this.customers != null)
        {
            return this.customers[currentCustomer];
        }
        else
        {
            return null;
        }
    }
}
```

`GetDataAsync` 方法是异步的，因此 MainPage 表单上的控件可能在 `customers` 集合未填充时尝试绑定到客户。在这种情况下，此修改可防止数据绑定在访问 `customers` 集合时生成空引用异常。

15. 在 `ViewModel` 构造函数中，更新使每个命令可运行的条件，如以下代码中以粗体所示：

Click here to view code image

```
public ViewModel()
{
    ...
    this.NextCustomer = new Command(this.Next,
        () => { return this.customers != null &&
                this.customers.Count > 1 && !this.IsAtEnd; });
    this.PreviousCustomer = new Command(this.Previous,
        () => { return this.customers != null &&
                this.customers.Count > 0 && !this.IsAtStart; });
    this.FirstCustomer = new Command(this.First,
        () => { return this.customers != null &&
                this.customers.Count > 0 && !this.IsAtStart; });
    this.LastCustomer = new Command(this.Last,
    () => { return this.customers != null &&
        this.customers.Count > 1 && !this.IsAtEnd; });
}
```

这些更改可确保命令栏上的按钮在有数据可显示之前不会被启用。

16. 在 Solution Explorer 中，展开 `MainPage.xaml` 并双击 `MainPage.xaml.cs` 以在代码和文本编辑器窗口中打开它。

17. 将以下以粗体显示的语句添加到 `MainPage` 构造函数中：

Click here to view code image

```
public MainPage()
{
    ...
    ViewModel viewModel = new ViewModel();
    viewModel.GetDataAsync();
    this.DataContext = viewModel;
}
```

此语句填充 ViewModel。

18. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用。

表单最初会显示为空白，而 `GetDataAsync` 方法正在运行，但几秒钟后，第一个客户 Orlando Gee 的详细信息应显示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_849_0.png)

# Adventure Works Customers

19. 使用命令栏中的导航按钮在客户列表中移动，以验证表单按预期工作。

20. 返回 Visual Studio 并停止调试。

作为本节的最后润色，让用户在表单最初显示时知道，尽管表单看起来为空，但应用实际上正在获取数据会很有帮助。在 UWP 应用中，你可以使用 `ProgressRing` 控件提供此反馈。此控件应在 ViewModel 忙于与 Web 服务通信时显示，否则应处于非活动状态。

## Add a busy indicator to the Customers form

1. 在代码和文本编辑器窗口中打开 `ViewModel.cs` 文件。在 `GetDataAsync` 方法之后，向 `ViewModel` 类添加私有 `_isBusy` 字段和公共 `IsBusy` 属性，如下所示：

Click here to view code image

```
private bool _isBusy;
public bool IsBusy
{
    get { return this._isBusy; }
    set
    {
        this._isBusy = value;
        this.OnPropertyChanged(nameof(IsBusy));
    }
}
```

2. 在 `GetDataAsync` 方法中，添加以下以粗体显示的语句：

Click here to view code image
```
public async Task GetDataAsync()
{
    try
    {
        this.IsBusy = true;
        var response = await
        this.client.GetAsync("api/customers");
        ...
    }
    catch (Exception e)
    {
        // TODO: Handle exceptions
    }
    finally
    {
        this.IsBusy = false;
    }
}
```

`GetData` 方法在运行查询以获取客户信息之前将 `IsBusy` 属性设置为 true。`finally` 块可确保即使发生异常，`IsBusy` 属性也会被设置回 false。

3. 在 Design View 窗口中打开 `MainPage.xaml` 文件。

4. 在 XAML 窗格中，将以下代码中以粗体显示的 `ProgressRing` 控件添加为顶层 `Grid` 控件中的第一个项：

Click here to view code image
```
<Grid Style="{StaticResource GridStyle}">
    <ProgressRing HorizontalAlignment="Center"
VerticalAlignment="Center" Foreground="AntiqueWhite"
Height="100" Width="100" IsActive="{Binding IsBusy}"
Canvas.ZIndex="1"/>
    <Grid x:Name="customersTabularView" Margin="40,104,0,0" ...>
    ...
```

将 `Canvas.ZIndex` 属性设置为 "1" 可确保 `ProgressRing` 显示在 `Grid` 控件显示的其他控件前面。

5. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用。

请注意，当应用启动时，在显示第一个客户之前进度环会短暂出现。如果发现第一个客户出现得太快，可以在 `GetDataAsync` 方法中引入一个小的延迟，以确认进度环正在工作。添加以下语句，该语句将方法暂停五秒钟：

Click here to view code image
```
public async Task GetDataAsync()
{
    try
    {
        this.IsBusy = true;
        await Task.Delay(5000);
        var response = await this.client.GetAsync(...);
        ...
    }
    ...
}
```

在完成进度环的测试后，请务必删除此语句。

6. 返回 Visual Studio 并停止调试。

## 通过 REST Web 服务插入、更新和删除数据

除了让用户能够查询和显示数据之外，许多应用还需要让用户插入、更新和删除信息。ASP.NET Web API 实现了一个模型，通过使用 HTTP PUT、POST 和 DELETE 请求来支持这些操作。按照惯例，PUT 请求修改 Web 服务中的现有资源，而 POST 请求创建资源的新实例。DELETE 请求删除资源。ASP.NET Web API 模板中 Add Scaffold 向导生成的代码遵循这些约定。

### REST Web 服务中的幂等性

在 REST Web 服务中，PUT 请求应该是幂等的，这意味着如果您重复执行相同的更新，结果始终应该是相同的。以 AdventureWorksService 示例为例，如果您修改一个客户并将电话号码设置为“888-888-8888”，则无论您执行此操作多少次，其效果都是相同的。这可能看起来很明显，但您应该在设计 REST Web 服务时考虑到这一要求。通过这种设计方法，Web 服务在面对并发请求时可以保持健壮，甚至在网络故障的情况下也能保持健壮（如果客户端应用与 Web 服务的连接丢失，它可以简单地尝试重新连接并再次执行相同的请求，而无需担心之前的请求是否成功）。因此，您应该将 REST Web 服务视为存储和检索数据的一种手段，而不应尝试实现业务特定的操作。

例如，如果您正在构建一个银行系统，您可能会想提供一个 `CreditAccount` 方法，将金额添加到客户账户的余额中，并将其作为 PUT 操作公开。但是，每次调用此操作时，结果都是对账户的增量贷记。因此，有必要跟踪对该操作的调用是否成功。如果应用认为之前的调用失败或超时而重复调用此操作，则可能会导致对同一账户进行多次重复贷记。

有关在云应用中管理数据一致性的更多信息，请参阅 https://msdn.microsoft.com/library/dn589800.aspx 上的“Data Consistency Primer”。

在下一个练习中，您将扩展 Customers 应用并添加功能，让用户可以添加新客户并修改现有客户的详细信息。应用将构造适当的 REST 请求并将其发送到 `AdventureWorksService` Web 服务。您将不提供删除客户的功能。此限制可确保您拥有与 Adventure Works 组织有过业务往来的所有客户的记录，这可能出于审计目的而必需。此外，即使客户很长时间没有活跃，将来也可能下订单。

### Note

对于业务应用而言，越来越常见的做法是永远不删除数据，而是简单地执行更新，将数据标记为以某种方式“已删除”并防止其显示。这主要是由于需要保留完整的数据记录，通常是为了满足监管要求。

## 在 ViewModel 类中实现添加和编辑功能

1. 返回 Visual Studio。

2. 在 Customers 项目中，删除 `ViewModel.cs` 文件以将其从项目中移除。允许 Visual Studio 永久删除此文件。

3. 右键单击 Customers 项目，指向 Add，然后单击 Existing Item。选择位于“我的文档”文件夹中 `\Microsoft Press\VCSBS\Chapter 27` 文件夹中的 `ViewModel.cs` 文件，然后单击 Add。

`ViewModel.cs` 文件中的代码变得相当冗长，因此已重新组织为区域以便于管理。`ViewModel` 类还已扩展了以下布尔属性，以指示 ViewModel 正在运行的模式：Browsing、Adding 或 Editing。这些属性在名为 `Properties For Managing The Edit Mode` 的区域中定义：

- **IsBrowsing** 此属性指示 ViewModel 是否处于浏览模式。当 ViewModel 处于浏览模式时，`FirstCustomer`、`LastCustomer`、`PreviousCustomer` 和 `NextCustomer` 命令处于启用状态，并且视图可以调用这些命令来浏览数据。
