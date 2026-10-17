
```
    return _context.Customers.Any(e => e.CustomerID == id);

}
```

`GetCustomers` 方法处理检索所有客户的请求。它通过简单返回之前创建的 Entity Framework 数据模型中的整个 `Customers` 集合 (`DbSet`) 来满足这些请求。在后台，Entity Framework 从数据库获取所有客户，并使用这些信息填充 `Customers` 集合。如果应用程序向此 Web服务的 `api/Customers` URL 发送 HTTP GET 请求，就会调用此方法。

`GetCustomer` 方法（不要与 `GetCustomers` 混淆）接收一个整数参数。该参数指定特定客户的 `CustomerID`，方法在返回结果之前会使用 Entity Framework 查找该客户的详细信息。当应用程序向 `api/Customers/n` URL 发送 HTTP 请求时（其中 `n` 是要检索的客户的 ID)，将运行 `GetCustomer`。

`PutCustomer` 方法在应用程序向 Web 服务发送 HTTP PUT 请求时运行。请求指定了客户 ID 和客户详细信息，该方法中的代码使用 Entity Framework 用详细信息更新指定的客户。

`PostCustomer` 方法响应 HTTP POST 请求，并接收客户详细信息作为参数。该方法将带有这些详细信息的新客户添加到数据库中（前面的代码示例未显示这些信息）。

最后，`DeleteCustomer` 方法处理 HTTP DELETE 请求并删除指定客户 ID 的客户。

注意，所有这些方法都是异步的。通过互联网连接 Web 服务并从数据库获取数据可能需要几秒钟，你不希望在此处理发生期间占用 Web 服务中的一个线程。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1090_0.png)

### 注意

Web API 模板生成的代码乐观地假设它始终能够连接到数据库。然而，在分布式系统世界，由于数据库和 Web 服务位于不同的服务器上，情况可能并不总是如此。网络容易出现瞬态错误和超时；连接尝试可能会因为临时故障而失败，如果稍后重试则可能会成功。向客户端报告临时故障可能会让用户感到沮丧。如果可能，只要重试不过度，静默重试失败的操作可能会更好（你不希望在数据库真的不可用时 Web 服务发生冻结）。有关此策略的详细信息，请参阅“云基础数据访问层：瞬态故障处理”，http://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx。

ASP.NET Web API 模板会自动生成代码，将请求引导控制器类中的适当方法。如果你需要管理其他资源（例如产品或订单），可以添加更多控制器类。

你也可以使用与 `CustomersController` 类相同的模式手动创建控制器类——你不一定需要使用 Entity Framework 在数据库中获取和存储数据。ASP.NET Core Web API 模板在 `ValuesController.cs` 文件中包含一个示例控制器，你可以复制它并用自己的代码进行更新。

- 4. 在解决方案资源管理器中，右键点击 `AdventureWorksService` 项目，指向“调试”，并选择“启动新实例”。

此操作将启动 IISExpress Web 服务器，该服务器托管 Web 服务。

- 5. 如果出现“信任 ASP.NET Core SSL 证书”对话框，选择“是”，允许 Visual Studio 安装证书。IISExpress 使用此证书来支持 SSL 连接的本地测试。

打开调试控制台窗口，显示诊断信息。你的网络浏览器也应该打开并显示如下所示的页面。这是 Swagger 测试页面。它显示了 Web 服务提供的操作，并允许你测试这些操作。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1092_0.png)

6. 在 Swagger页面上，点击 `api/Customers` 操作的 **GET** 按钮。（记住此操作将检索所有。）选择 **Try out** 然后选择 **Execute** 查看结果。

# Customers

### GET api/Customers

### 参数

无参数

### 请求

```bash
curl -X GET "https://localhost:5001/api/Customers" -H "accept: application/json"
```

### 响应

#### 响应: 200

```json
[
  {
    "CustomerID": 1,
    "FirstName": "Orlando",
    "LastName": "Bello",
    "EmailAddress": "orlando@adventure-works.com"
  },
  {
    "CustomerID": 2,
    "FirstName": "Keith",
    "LastName": "Harrison",
    "EmailAddress": "keith@adventure-works.com"
  },
  {
    "CustomerID": 3,
    "FirstName": "Dennis",
    "LastName": "Seycock",
    "EmailAddress": "dennis@adventure-works.com"
  }
]
```

### GET api/Customers/{id}

7. 在 Swagger 页面上，滚动到 `api/Customers/{id}` 操作。此操作返回单个客户的详细信息。选择 **GET**，然后在参数部分指定 id 为 55，选择 **Execute**。应显示 Eric Lang 的详情。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1094_0.png)

8. POST、PUT 和 DELETE 按钮允许你对 Web 服务进行插入、更新和删除操作。请随意尝试这些操作。

9. 完成后，关闭浏览器、关闭调试控制台窗口并返回 Visual Studio。

目前，虽然 Web API 功能完善，但它并不是最具可扩展性的服务。例如，如果你的数据库包含成千上万客户，你真的希望 GET 操作检索所有内容吗？这可能会花费时间并消耗大量资源。在这种情况下，大多数现代应用程序每次检索 100 行数据。用户仍然可以获取并浏览每一行，如果他们只对前十二行感兴趣，检索每一行就是浪费。

此外，Web API 允许用户通过客户 ID 搜索客户，但在许多情况下，通过其他属性（如名称甚至电子邮件）检索客户会更好。在接下来的练习中，你将修改 Web API 以满足这些需求。

# 检索块客户

- 1. 在 `CustomersController.cs` 文件中，找到 `GetCustomers` 方法。

- 2. 修改此方法的签名以接收两个参数：offset（偏移量）和 count（计数）。该方法将从数据库中的行偏移量开始检索计数个客户。

- 3. 按此处所示加粗的代码修改方法体中的代码：

```c
{
  if (offset < 0 || count < 0) {
    return BadRequest();
  }
  return await _context.Customers
    .OrderBy(r => r.CustomerID)
    .Skip(offset)
    .Take(count).ToListAsync();
}
```

此代码会快速检查 `offset` 和 `count` 值是否为负数。如果参数有效，该方法将使用 Entity Framework 获取数据。`Skip` 方法会跳过指定的行数，而 `Take` 方法会获取所需的订单。在像 SQL Server 的关系型数据库中，行的存储顺序并不一定是有保证的，因此从 `offset` 位置开始检索 `count` 行将返回一个随机的客户集合。为了解决这个问题，`OrderBy` 方法确保了数据首先按 `CustomerID` 排序。

# 实现增强型搜索

- 1. 在 `CustomersController` 类中创建另一个方法 `FindCustomers`。该方法应返回一个客户列表，并接收一组定义搜索准标准的参数集。该方法将返回所有符合这些准标准的客户。搜索标准具有默认值 `%`。该字符是 SQL 通配符。如果用户省略了任何参数，它们将被视为匹配任何值。

点击此处查看代码图片

注意，该函数具有 `[HttpGet]` 特性，其相对 URI 为 "find"。用户通过 Web 服务中的 `api/Customers/find` 地址来调用此函数。

- 2. 在 `FindCustomers` 方法的主体中添加以下加粗代码：

点击此处查看代码图片

```c
public async Task<ActionResult<IEnumerable<CustomerModel>>>
FindCustomers(
    string title = "", string firstName = "", string lastName = "",
    string email = "", string phone = "")
{
    var query = from c in _context.Customers
                where EF.Functions.Like(c.Title, title) &&
                      EF.Functions.Like(c.FirstName, firstName) &&
                      EF.Functions.Like(c.LastName, lastName) &&
                      EF.Functions.Like(c.EmailAddress, email) &&
                      EF.Functions.Like(c.Phone, phone)
                select c;
    return await query.ToListAsync();
}
```

此代码运行了一个 LINQ 查询，使用 Entity Framework 库提供的静态 `Like` 函数来查找所有与作为参数传递的标准匹配的行。`Like` 函数是 Entity Framework 库中静态 `EF` 类的一部分。

- 3. 在“生成”（Build）菜单上，选择“重新生成解决方案”（Rebuild Solution）。验证 Web 服务重新生成时没有任何错误或警告。

- 4. 在“解决方案管理器”（Solution Explorer）中，右键点击 `AdventureWorksService` 项目，指向“调试”（Debug），然后选择“新建实例”（New Instance）。

- 5. 当 Swagger 页面出现时，选择针对 `/api/Customers` 操作的 GET 按钮，然后选择“尝试执行”（Try out）。

- 6. 将 `offset` 参数设置为 10，将 `count` 参数设置为 5。然后选择“执行”（Execute）。该操作应返回五个客户。

- 7. 向下滚动 Swagger 页面，选择 `/api/Customers/find` 操作的 GET，然后选择“尝试执行”（Try out）。

- 8. 在 `firstName` 字段中输入 `O%`，在 `lastName` 字段中输入 `%a%`，保留其他字段的默认值（`%`），并选择“执行”。此搜索应返回所有名字以 O 开头且姓氏中某处包含 a 的客户。查询应返回三个客户，ID 为 348、452 和 29511。

- 9. 尝试一些你自己的搜索。完成后，关闭网络浏览器，关闭调试控制台窗口，并返回 Visual Studio。

该 Web API 目前在你的计算机上运行 IISExpress。为了让其他用户可以使用，你应该将其部署到 Azure。你可以通过使用 Visual Studio 2022 提供的“发布”向导来完成此操作，如下练习所示。

# 将 Web 服务部署到云端

- 1. 在“解决方案管理器”中，右键点击 `AdventureWorksService` 项目，然后选择“发布”（Publish）。

- 2. 在“发布”向导中，在“目标”（Target）页面上，选择 Azure，然后选择“下一步”。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1098_0.png)

- 3. 在“特定目标”（Specific target）页面上，选择 Azure App Service (Windows)。然后选择“下一步”。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1099_0.png)

- 4. 在 App Service 页面上，如果提示，请登录你的 Azure 账户。然后选择你的 Azure 订阅。在 App Service 实例框上方，选择加号图标 (+) 以创建一个新的 Azure App Service。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1100_0.png)

- 5. 在 App Service (Windows) 对话框中，接受默认的应用程序名称，选择你的订阅，并将资源组设置为 **awgroup**（你之前使用 Azure 门户创建了此资源组）。然后接受默认的托管计划名称，并选择“创建”（Create）。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1101_0.png)

App Service 为你的 Web 服务提供托管环境。在后台，Microsoft 将你的 API 应用程序托管在 Web 服务器上。

- 6. 回到“发布”向导，验证 **App Service instances** 框列出了你新的 App Service 实例，然后选择“下一步”（Next）。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1102_0.png) - 7. 在“发布”页面上，选择跳过（Skip）。

- 8. 等向导完成。然后，在 Visual Studio 中，在“发布”页面上选择“发布”（Publish）。

- 9. 在地址栏中输入 **/Customers?offset=20&count=15** 并按回车。这将发送一个带有参数的 GET 请求。结果如下：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1105_0.png) - 10. 关闭浏览器并返回 Visual Studio。

# 更新 UWP 应用以使用 Web 服务

旅程的阶段阶段是从 UWP 应用连接到 Web 服务并使用获取某些数据。在此之前，你将更新 Customers 项目中的 UI。向 Web 服务发送请求可能是一项耗时操作，你需要确保用户意识到操作正在进行。此外，通过网络发送请求本质上是容易出错的操作；网络经常失败或超时，因此你还将为 UI 添加显示错误消息的能力。

启用 UWP 支持耗时操作和错误报告

1. 在“解决方案管理器”中，展开 Customers 项目，并在代码和编辑器窗口中打开 ViewModelcs 文件。

2. 在 ViewModel 类中、构造函数之后添加以下字段和属性：

```csharp
private bool _isBusy;
public bool IsBusy
{
    get => this._isBusy;
    set {
        this._isBusy = value;
        this.OnPropertyChangedChanged(nameof(IsBusy));
    }
}
```

```csharp
private string _lastError = null;
public string LastError
{
    get => this._lastError;
    private set {
        this._lastError = value;
        this.OnPropertyChangedChanged(nameof(LastError));
    }
}
```

3. 在 ViewModel 类开头添加此处显示的加粗属性。（未加粗的字段应该已经存在）。应用程序将使用这些属性来指示 UI 当前显示哪个记录。

```csharp
private List<Customer> customers;
public int CustomerListCount { get => customers is null ? 0 : customers.Count; }
private int currentCustomer;
public int currentCustomerIndex { get => currentCustomer + 1; }
```

4. 更新 Next、Previous、First 和 Last 方法的代码，以便在用户在客户之间导航时指示当前记录已发生更改，如此处加粗所示：

点击此处查看代码图像

```
private void Next()
{
    if (this.customers.Count - 1 > this.currentCustomer)
    {
        this.currentCustomer++;
        this.OnPropertyChanged(nameof(Current));
        this.OnPropertyChanged(nameof(CurrentCustomerIndex));
