
### 代码示例

```
private void Previous()
{
    if (this.currentCustomer > 0)
    {
        this.currentCustomer--;
        this.OnPropertyChanged(nameof(Current));
        this.OnPropertyChanged(nameof(CurrentCustomerIndex));
    }
}
```

```
private void First()
{
    this.currentCustomer = 0;
    this.OnPropertyChanged(nameof(Current));
    this.OnPropertyChanged(nameof(CurrentCustomerIndex));
}
```

```
private void Last()
{
    this.currentCustomer = this.customers.Count - 1;
    this.OnPropertyChanged(nameof(Current));
    this.OnPropertyChanged(nameof(CurrentCustomerIndex));
    ...
}
```

### UI 布局

- 5. 在设计视图（Design View）窗口中打开 `MainPage.xml` 文件。

- 6. 在顶层 `Grid` 控件旁边添加所示 `ProgressRing` 控件：

点击此处查看代码图像

```
<Page
Style="{StaticResource PageStyle}"
<Grid>
  <ProgressRing HorizontalAlignment="Center"
               VerticalAlignment="Center"
               Foreground="AntiqueWhite" Height="100" Width="100"
               IsActive="Binding IsBusy}" Canvas.ZIndex="1"/>
  <Grid x:Name="customersTabularView" Margin="10,20,10,20"
        Visibility="Visible">
  ...
</Grid>
```

`ProgressRing` 控件控制你在应用程序忙碌时可能会看到的旋转活动环。该控件向用户显示正在进行活动——换句话说，应用程序没有冻结。只有当 `ViewModel` 的 `IsBusy` 属性为 `true` 时，该控件才处于激活状态。将 `Canvas.ZIndex` 属性设置为 `1`，可以确保进度环在激活时位于页面上所有其他控件的前方。

- 7. 在显示客户电话的控件之后，添加 `TextBlock` `customersTabularView` `Grid` 控件。该控件将显示 `ViewModel` 中 `LastError` 属性的消息。

点击此处查看代码图像

```
<Grid x:Name="customersTabularView" Margin="40,54,0,0"
      Visibility="Visible">
  ...
  <Grid.Row="2">
    <TextBlock Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3"
               x:Name="phone" />
    <TextBlock Grid.Row="6" Grid.Column="1"
               Grid.ColumnSpan="7"
               Style="{StaticResource ErrorStyle}" Text="{Binding LastError}"/>
  </Grid>
</Grid>
..
```

- 8. 找到 `customersColumnar` `Grid` 控件。在 `customersColumnar` `Grid` 内部的 `Grid` 控件中添加第六个 `RowDefinition` 控件，如下：

点击此处查看代码图像

```
...
<Grid x:Name="customersColumnarView" Margin="10,20,10,20"
Visibility="Collapsed">
  <Grid.Row="1">
    <Grid.RowDefinitions>
      <RowDefinition />
      <RowDefinition />
      <RowDefinition />
      <RowDefinition />
      <RowDefinition />
      <RowDefinition />
    </Grid.RowDefinitions>
  
...
```

- 9. 在嵌套 `Grid` 控件的末尾，添加 `TextBlock` 控件以显示 `ViewModel` 类中 `LastError` 属性的消息：

点击此处查看代码图像

```
<TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone" .../>
<TextBlock Grid.Row="6" Grid.Column="0" Grid.ColumnSpan="2"
Style="StaticResource ErrorMessageStyle" Text="Binding
LastError" />
</Grid>
```

- 10. 在解决方案管理器（Solution Explorer）中，打开 `AppStyles.xaml` 文件。

- 11. 将以下样式添加到资源字典的末尾。错误消息 `TextBlock` 控件使用此样式：

点击此处查看代码图像

```
<Style x:Key="ErrorMessageStyle" TargetType="TextBlock">
  <Setter Property="HorizontalAlignment" Value="Left"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Top"/>
  <Setter Property="FontSize" Value="20"/>
  <Setter Property="Foreground" Value="White"/>
</Style>
```

- 12. 将以下 `Page.BottomAppBar` 控件添加到页面末尾，紧邻 `</Page>` 结束元素之前。该控件在页面底部显示命令栏，并指示当前显示的是哪个记录。`TextBlock` 控件的 `Run` 元素允许你将多个文本项作为同一控件的一部分显示。

点击此处查看代码图像

```
<Page.BottomAppBar>
<CommandBar>
  <AppBarElementContainer VerticalAlignment="Center">
    <TextBlock Padding="0, 0, 20, 0">
      <Run Text="{Binding Path=CurrentCustomerIndex}" />
      <Run Text=" />
      <Run Text="{Binding Path=CustomerListCount}" />
    </TextBlock>
  </AppBarElementContainer>
</CommandBar>
</Page>
```

现在你可以更新 `ViewModel` 类来调用 Web 服务了。

## 获取数据

1. 在解决方案管理器中，右键点击项目并选择“管理程序包”（Manage Packages）。

2. 在 NuGet 窗口中，输入 `System.Json`。

3. 选择 `System.Json` 包（确保版本为 6.0 或更高）并选择“安装”。

4. 在编辑器中打开 `ViewModel.cs` 文件。

5. 在文件顶部添加以下 `using` 指令：

```
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text.Json;
```

`System.Json` 包包含了用于序列化和反序列化 JSON 文本以及将对象转换为字符串的实用程序。

这些 语句创建并初始化了一个 `HttpClient` 对象。应用程序使用 `HttpClient` 对象向 Web 服务发送 HTTP 请求并获取 Web 服务的任何响应。你在 `BaseAddress` 属性中指定 Web 地址，并通过设置 `DefaultHeaders` 属性指定发送和接收的数据类型。在此应用程序中，你将发送和接收格式为 JSON 字符串的消息。

7. 在构造函数的末尾添加以下代码：

点击此处查看代码图像

```
public ViewModel()
{
    this.client = new HttpClient();
    this.client.BaseAddress = new Uri(ServerUrl);
    this.client.DefaultRequestHeaders.Accept.Add(
        new MediaTypeHeaderValue("application/json"));
}
```

8. 在 `ViewModel` 类中构造函数之后添加所示的 `GetDataAsync` 方法：

点击此处查看代码图像

```
public async Task GetDataAsync(int offset, int count)
{
}
```

这是一个异步方法，它将向 Web 服务的 GET 操作发送请求，使用 `offset` 和 `count` 参数。该方法的目的是获取一组客户并将其添加到列表中。

9. 在 `GetDataAsync` 方法中，实现使用 Web 服务检索客户信息的逻辑，所示：

点击此处查看代码图像

```
public async Task GetDataAsync(int offset, int count)
{
    this.offset = offset;
    this.count = count;
    try {
        this.IsBusy = true;
        var response = await this.client.GetAsync($"/api/customers?offset={this.offset}&count={this.count}");
        if (response.IsSuccessStatusCode) {
            var customersJsonString = await response.Content.ReadAsStringAsync();
            var customersData = JsonSerializer.Deserialize<List<Customer>>(customersJsonString, options);
            if (this.customers == null) {
                this.customers = customersData;
                this.First();
            } else {
                this.customers.AddRange(customersData);
            }
        }
    }
    catch (Exception ex) {
        // Handle exception
    }
    finally {
        this.IsBusy = false;
    }
}
```

```
public class ViewModel: INotifyPropertyChanged
{
    public List<Customer> customers { get; set; }
    private Customer _currentCustomer;
    public Customer Current 
    {
        get => _currentCustomer;
        set { _currentCustomer = value; OnPropertyChanged(nameof(Current)); }
    }
    private int _currentCustomerIndex;
    public int CurrentCustomerIndex
    {
        get => _currentCustomerIndex;
        set { _currentCustomerIndex = value; OnPropertyChanged(nameof(CurrentCustomerIndex)); }
    }

    private const string ServerUrl = "https://yourwebservice.azure.net/";
    private int offset = 0;
    private int count = 0;
    private HttpClient client = null;
    private JsonSerializerOptions options = new ()
    {
        PropertyNameCaseInsensitive = true
    };

    public ViewModel()
    {
        ...
    }

    public event PropertyChangedEventHandler PropertyChanged;
    protected void OnPropertyChanged(string name)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(name));
    }
}
```

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

- `ViewModel` 类的状态被设置为 `Busy`。此操作将导致页面显示 `ProgressRing` 控件。

- 客户端对象的 `GetAsync` 方法向网络服务发送 HTTP GET 请求。请求被发送到 `api/customers` 端点。请求中的 `offset` 和 `count` 参数使用提供给 `GetAsync` 方法的值进行填充。

- 如果客户端对象的 `GetAsync` 方法执行成功，网络服务返回的数据将从 JSON 字符串反序列化为 `Customer` 对象集合。

- 如果 `customers` 集合当前为 `null`，则将其为此 `Customer` 对象集合；否则，将此集合中的数据追加到 `customers` 集合中。

- 如果发生错误，错误消息将赋值给 `LastError` 属性，该属性将在页面上显示。

- 在 `finally` 块中，重置 `Busy` 状态（`ProgressRing` 控件将消失），并更新记录计数以便在页面底部的应用栏中显示。

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

- 12. 在 `MainPage` 构造函数中，通过调用 `GetDataAsync` 方法填充 `ViewModel` 对象。将 `offset` 参数设置为 0（从开始开始），并将 `count` 参数设置为 `BatchSize`：

点击此处查看代码图像

```cs
public MainPage()
{
    ViewModel viewModel = new ViewModel();
    await viewModel.GetDataAsync(0, BatchSize);
    this.DataContext = viewModel;
}
```

- 13. 在“调试”菜单上，选择“启动调试”以编译并运行应用程序。当应用程序启动时，在检索数据期间，你应该能短暂看到 `ProgressRing` 控件，然后第一个客户将出现。

- 14. 选择顶部应用栏中的按钮在客户之间移动。注意底部应用栏中的计数指示了你当前位于哪行。

| ID | Title | First Name | Last Name |
|---|---|---|---|
| 16 | Mr. | Christopher | Beck |
| Email | christopher1@adventure-works.com | | |
| Phone | | 1 (11) 500 555-0132 | | |

- 15. 完成数据浏览后，关闭应用程序并返回 Visual Studio。
