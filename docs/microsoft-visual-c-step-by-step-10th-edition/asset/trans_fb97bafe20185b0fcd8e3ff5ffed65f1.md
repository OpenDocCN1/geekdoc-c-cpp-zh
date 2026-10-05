

```cs
}
else
{
    this.LastError = response.ReasonPhrase;
}
catch (Exception e)
{
    this.LastError = e.Message;
}
finally
{
    this.OnPropertyChanged(nameof(CustomerListCount));
    this.IsBusy = false;
}
```

此代码的关键点如下：

- ViewModel 类的状态被设置为 Busy。此操作将导致页面显示 ProgressRing 控件。
- 客户端对象的 `GetAsync` 方法向网络服务发送 HTTP GET 请求。请求被发送到 `api/customers` 端点。请求中的 `offset` 和 `count` 参数使用提供给 `GetAsync` 方法的值进行填充。
- 如果客户端对象的 `GetAsync` 方法执行成功，网络服务返回的数据将从 JSON 字符串反序列化为 `Customer` 对象集合。
- 如果 `customers` 集合当前为 `null`，则将其为此 `Customer` 对象集合；否则，将此集合中的数据追加到 `customers` 集合中。
- 如果发生错误，错误消息将赋值给 `LastError` 属性，该属性将在页面上显示。
- 在 `finally` 块中，重置 Busy 状态（ProgressRing 控件将消失），并更新记录计数以便在页面底部的应用栏中显示。

- 10. 在代码和文本编辑器窗口中打开 `MainPage.xaml.cs` 文件。

- 11. 在 `MainPage` 类旁边添加所示的 `BatchSize` 常量。此值将用于指示每次从网络服务检索多少行数据。

点击此处查看代码图像

```cs
public sealed partial class MainPage : Page
{
    internal const int BatchSize = 100;
    ...
}
```

- 12. 在 `MainPage` 构造函数中，通过调用 `GetDataAsync` 方法填充 ViewModel 对象。将 `offset` 参数设置为 0（从开始开始），并将 `count` 参数设置为 `BatchSize`：
点击此处查看代码图像

```cs
public MainPage()
{
    ViewModel viewModel = new ViewModel();
    await viewModel.GetDataAsync(0, BatchSize);
    this.DataContext = viewModel;
}
```

- 13. 在“调试”菜单上，选择“启动调试”以编译并运行应用程序。当应用程序启动时，在检索数据期间，你应该能短暂看到 ProgressRing 控件，然后第一个客户将出现。

- 14. 选择顶部应用栏中的按钮在客户之间移动。注意底部应用栏中的计数指示了你当前位于哪行。

| ID | Title | First Name | Last Name |
|---|---|---|---|
| 16 | Mr. | Christopher | Beck |
| Email | christopher1@adventure-works.com | | |
| Phone | | 1 (11) 500 555-0132 | | |

- 15. 完成数据浏览后，关闭应用程序并返回 Visual Studio。

“Customers”应用程序获取并显示前 100 个客户，但如果你想看更多怎么办？在下一次练习中，你将为应用程序添加此功能。你可以使用 `GetDataAsync` 方法来实现此操作，并提供适当的 `offset` 来获取下一块客户。你还需要更新 UI 并添加一个“更多”（More）按钮。

# 以显示更多客户并添加“更多”按钮

- 1. 在代码和文本编辑器窗口中打开 `ViewModel.cs` 文件。

- 2. 在 ViewModel 类的列表中添加后续所示**加粗**的 `MoreCustomers` 和 `Reset` 命令：

点击此处查看代码图像

```cs
public class ViewModel : INotifyPropertyChanged
{
    public Command LastCustomer { get; private set; }
    public Command MoreCustomers { get; private set; }
    public Command Reset { get; private set; }
}
```

- 3. 在 ViewModel 类中、在 `Last` 方法之后添加所示的 `More` 方法。该方法使用 `GetDataAsync` 方法从当前块记录的末尾获取计数记录。代码更新了 ViewModel 对象的状态，以确保导航按钮继续正常运行：

点击此处查看代码图像

```cs
private async Task More(int offset, int count)
{
    await this.GetDataAsync(this.currentCustomer = this.customers.Count > offset ? offset : this.customers.Count - 1);
    this.OnPropertyChanged(nameof(CurrentCustomer));
    this.IsAtStart = (this.currentCustomer == 0);
    this.IsAtEnd = (this.customers.Count == 0 || this.customers.Count - 1 == this.currentCustomer);
}
```

- 4. 在 ViewModel 构造函数中，初始化 `MoreCustomers` 命令以运行 `More` 方法。只有当有有效的 `HttpClient` 对象可以检索数据时才启用该命令。

点击此处查看代码图像

```cs
public ViewModel()
{
    this.LastCustomer = new Command(this.Last, ...);
    this.MoreCustomers = new Command(async () => await this.More(...), () => this.client is not null);
}
```

- 5. 同样，初始化 `Reset` 命令以丢弃 `Customers` 集合中的现有数据并重新获取第一块客户：

点击此处查看代码图像

```cs
public ViewModel()
{
    this.MoreCustomers = new Command(...);
    this.Reset = new Command(async () => {
        this.customers = null;
        await this.GetDataAsync(0, MainPage.BatchSize);
    }, () => this.client is not null);
}
```

- 6. 在设计视图中打开 `MainPage.xaml` 文件。然后在 `TopAppBar` 控件的末尾添加以下 `AppBarSeparator` 和 `AppButton` 控件。用户可以点击这些按钮来获取下一块客户或将页面重置为原始状态。`AppBarSeparator` 用于分组应用栏头中的控件。

点击此处查看代码

```xml
<Page.TopAppBar>
    <Command>
        <AppButton x:Name="lastCustomer" .../>
        <AppBarSeparator/>
        <AppButton x:Name="more" Icon="More" Label="More"
            Command="Binding Path=MoreCustomers"/>
        <AppButton x:Name="reset" Icon="Rotate" Label="Reset"
            Command="Binding Path=Reset"/>
    </Command>
</Page.TopAppBar>
```

- 7. 在调试模式下生成并运行应用程序。

顶部现在应包含“更多”和“重置”按钮。每次选择“更多”，都会获取额外的数据。如果选择“重置”，将删除列表并重新获取第一块客户。

- 8. 返回 Visual Studio 并停止调试。

# 在 Customers 应用程序中搜索数据

“Customers”应用程序允许你浏览记录，但有时你可能更精确的筛选：查找特定客户或一组客户的能力。为了解决这个问题，你将实现通过表单查询（QBF）的功能。使用 QBF，你在页面字段中输入搜索条件。当用户完成输入搜索条件后，应用程序可以调用 `api/customers/find` 端点来检索匹配的客户列表。

最初，应用程序用于浏览；我将其称为浏览模式。然而，QBF 需要你将程序处于另一种模式，我称为搜索模式。在这种模式下，页面将被清空，并要求用户输入条件。例如，用户可以在 `FirstName` 字段中输入一个名字。

