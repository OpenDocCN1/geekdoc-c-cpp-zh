

Manager: Customers window.

7. 在 Solution Explorer 中，双击 ViewModel.cs 以在代码和文本编辑器窗口中显示该文件。

8. 在文件顶部的列表中添加以下 using 指令：

Click here to view code image

```
using System.Net.Http;
using System.Net.Http.Headers;
using Newtonsoft.Json;
```

9. 在 ViewModel 类中，在 ViewModel 构造函数之前添加以下以粗体显示的变量。将 <webappname> 替换为你在上一练习中创建用于托管 Web 服务的 Web 应用的名称。

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    private const string ServerUrl =
"http://<webappname>.azurewebsites.net/";
    private HttpClient client = null;

    public ViewModel()
    {
        ...
    }
    ...
}
```

ServerUrl 变量包含 Web 服务的基础地址。你将使用 client 变量连接到 Web 服务。

10. 在 ViewModel 构造函数中，将 customers 列表初始化为 null 并添加以下以粗体显示的语句来配置 client 变量：

Click here to view code image

```
public ViewModel()
{
    ...
    this.customers = null;
    this.client = new HttpClient();
    this.client.BaseAddress = new Uri(ServerUrl);
    this.client.DefaultRequestHeaders.Accept.
        Add(new MediaTypeWithQualityHeaderValue("application/json"));
}
```

customers 列表包含应用显示的客户；它之前使用你已删除的 DataSource.cs 文件中的数据填充。

*client* 变量使用将发送请求的 Web 服务器的地址进行初始化。REST Web 服务可以接收以多种格式发送请求和响应，但 Customers 应用将使用 JSON。前面代码中的最后一句将 *client* 变量配置为以此格式提交请求。

11. 在 Solution Explorer 中，展开 Customers 项目的根文件夹，双击 Customer.cs 文件以在代码和文本编辑器窗口中显示它。

12. 在 *Phone* 属性之后，立即向 *Customer* 类添加以下以粗体显示的公共属性：

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

13. 返回到 *ViewModel* 类。在构造函数之后，添加此处所示的公共 *GetDataAsync* 方法：

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

此方法为异步；它使用 HttpClient 对象的 GetAsync 方法调用 Web 服务中的 api/customers 操作。此操作从 AdventureWorks 数据库获取客户的详细信息。GetAsync 方法本身也是异步的，并返回包装在 Task 中的 HttpResponseMessage 对象。HttpResponseMessage 对象包含指示请求是否成功的状态代码，如果成功，应用将使用 HttpResponseMessage 对象的 Content 属性的 ReadAsStringAsync 方法实际检索 Web 服务返回的数据。此数据由包含每个客户详细信息的 JSON 格式字符串组成，因此它使用 JsonConvert 类的静态 DeserializeObject 方法转换为 Customer 对象列表并分配给 customers 集合（JsonConvert 类是 Json.NET 包的一部分）。然后 ViewModel 的 currentCustomer 属性设置为指向此集合中的第一个客户，并且 IsAtStart 和 IsAtEnd 属性被初始化以指示 ViewModel 的状态。

## Note

ASP.NET Web API 客户端库假定所有 Web 服务请求都可能需要不确定的时间来运行。因此，像 HttpClient 和 HttpResponseMessage 这样的类被设计为支持异步操作，以防止应用在等待响应时被阻塞。事实上，这些类仅支持异步操作；GetAsync 或 ReadAsStringAsync 没有同步版本。

请注意，目前 GetDataAsync 方法不会处理任何异常或失败，只是静默地消耗它们。你将在本章后面看到在 UWP 应用中报告异常的技术。

## Note

在生产应用中，你不应不必要地通过网络获取数据。相反，你应该选择性地检索数据。然而，在此应用中，AdventureWorks 数据库仅包含几百个客户，因此它们全部被检索并缓存在 customers 列表中。

14. 修改 Current 属性的 get 访问器，如下所示：

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

GetDataAsync 方法是异步的，因此 MainPage 表单上的控件可能在 customers 集合未填充时尝试绑定到客户。在这种情况下，此修改可防止数据绑定在访问 customers 集合时生成空引用异常。

15. 在 ViewModel 构造函数中，更新使每个命令可运行的条件，如以下代码中以粗体所示：

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

16. 在 Solution Explorer 中，展开 MainPage.xaml 并双击 MainPage.xaml.cs 以在代码和文本编辑器窗口中打开它。

17. 将以下以粗体显示的语句添加到 MainPage 构造函数中：

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

表单最初会显示为空白，而 GetDataAsync 方法正在运行，但几秒钟后，第一个客户 Orlando Gee 的详细信息应显示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_849_0.png)

# Adventure Works Customers

19. 使用命令栏中的导航按钮在客户列表中移动，以验证表单按预期工作。

20. 返回 Visual Studio 并停止调试。

作为本节的最后润色，让用户在表单最初显示时知道，尽管表单看起来为空，但应用实际上正在获取数据会很有帮助。在 UWP 应用中，你可以使用 ProgressRing 控件提供此反馈。此控件应在 ViewModel 忙于与 Web 服务通信时显示，否则应处于非活动状态。

## Add a busy indicator to the Customers form

- 1. 在代码和文本编辑器窗口中打开 ViewModel.cs 文件。在 GetDataAsync 方法之后，向 ViewModel 类添加私有 _isBusy 字段和公共 IsBusy 属性，如下所示：

Click here to view code image

```
private bool _isBusy;
public bool IsBusy
```

