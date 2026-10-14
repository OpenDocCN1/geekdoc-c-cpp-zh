

30. 在 AdventureWorksEntities 类中，添加一个接受名为 password 的字符串参数的构造函数。构造函数应使用实体数据模型向导（在“选择数据连接”页面上指定）之前写入 web.config 文件的连接字符串的名称调用基类构造函数。

```
public partial class AdventureWorksEntities
{
    public AdventureWorksEntities(string password)
        : base("name=AdventureWorksEntities")
    {
    }
}
```

31. 将下面以粗体显示的代码添加到构造函数中。此代码修改实体框架使用的连接字符串以包含密码。Customers 应用将调用此构造函数并在运行时提供密码。

```
public partial class AdventureWorksEntities
{
    public AdventureWorksEntities(string password)
        : base("name=AdventureWorksEntities")
    {
        this.Database.Connection.ConnectionString += ";Password={password}";
    }
}
```

## 创建和使用 REST Web 服务

您已创建了一个实体模型，可提供检索和维护客户信息的操作。下一步是实现一个 Web 服务，以便 UWP 应用可以访问实体模型。

使用 Visual Studio 2015，您可以直接基于实体框架生成的实体模型在 ASP.NET Web 应用中创建 Web 服务。Web 服务使用实体模型从数据库检索数据并更新数据库。您使用 Add Scaffold 向导创建 Web 服务。此向导可以生成实现 REST 模型的 Web 服务，该模型使用导航方案通过网络和 HTTP 协议表示业务对象和服务，并传输访问这些对象和服务的请求。访问资源的客户端应用以 URL 的形式提交请求，Web 服务对其进行解析和处理。例如，Adventure Works 可能会发布客户信息，将每个客户的详细信息作为单个资源公开，使用类似以下的方案：

```
http://Adventure-Works.com/DataService/Customers/1
```

访问此 URL 会导致 Web 服务检索客户 1 的数据。此数据可以以多种格式返回，但为了可移植性，最常见的格式包括 XML 和 JavaScript Object Notation（JSON）。由 REST Web 服务请求发出前一个查询时生成的典型 JSON 响应如下所示：

```
{
"CustomerID":1,
"Title":"Mr",
"FirstName":"Orlando",
"LastName":"Gee",
"EmailAddress":"orlando0@adventure-works.com",
"Phone":"245-555-0173"
}
```

REST 模型依赖于访问数据的应用在请求中发送适当的 HTTP 动词以访问数据。例如，前面显示的简单请求应向 Web 服务发送 HTTP GET 请求。HTTP 还支持其他动词，例如 POST、PUT 和 DELETE，您可以使用它们分别创建、修改和删除资源。编写生成适当的 HTTP 请求的代码并解析 REST Web 服务返回的响应听起来相当复杂。幸运的是，Add Scaffold 向导可以为您生成大部分代码。

在以下练习中，您将为 AdventureWorks 实体模型创建一个简单的 REST Web 服务。此 Web 服务将使客户端应用能够查询和维护客户信息。

## 创建 AdventureWorks Web 服务

- 1. 在 Visual Studio 中，在 AdventureWorksService 项目中，右键单击 Controllers 文件夹，指向 Add，然后单击 New Scaffolded Item。
- 2. 在 Add Scaffold 向导中，在中间窗格中，单击 Web API 2 Controller With Actions, Using Entity Framework 模板，然后单击 Add。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_834_0.png)

3. 在 Add Controller 对话框中，在 Model Class 下拉列表中，选择 Customer (AdventureWorksService.Models)。在 Data Context Class 下拉列表中，选择 AdventureWorksEntities (AdventureWorksService.Models)。选中 Use Async Controller Actions 复选框。验证 Controller name 是否设置为 CustomersController，然后单击 Add。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_834_1.png)

使用 ASP.NET Web API 模板创建的 Web 服务中，所有传入的 Web 请求都由一个或多个控制器类处理，每个控制器类公开映射到控制器公开的每个资源的各种类型 REST 请求的方法。例如，CustomersController 看起来像这样：

```
public class CustomersController : ApiController
{
    private AdventureWorksEntities db = new AdventureWorksEntities();

    // GET: api/Customers
    public IQueryable<Customer> GetCustomers()
    {
        return db.Customers;
    }

    // GET: api/Customers/5
    [ResponseType(typeof(Customer))]
    public async Task<IHttpActionResult> GetCustomer(int id)
    {
        Customer customer = await db.Customers.FindAsync(id);
        if (customer == null)
        {
            return NotFound();
        }

        return Ok(customer);
    }

    // PUT: api/Customers/5
    [ResponseType(typeof(void))]
    public async Task<IHttpActionResult> PutCustomer(int id, Customer customer)
    {
        if (!ModelState.IsValid)
        {
            return BadRequest(ModelState);
        }

        if (id != customer.CustomerID)
        {
            return BadRequest();
        }

        db.Entry(customer).State = EntityState.Modified;

        try
        {
            await db.SaveChangesAsync();
        }
        catch (DbUpdateConcurrencyException)
        {
            if (!CustomerExists(id))
            {
                return NotFound();
            }
            else
            {
                throw;
            }
        }
```

```
}
    return StatusCode(HttpStatusCode.NoContent);
}

// POST: api/Customers
[ResponseType(typeof(Customer))]
public async Task<IHttpActionResult> PostCustomer(Customer customer)
{
    ...
}

// DELETE: api/Customers/5
[ResponseType(typeof(Customer))]
public async Task<IHttpActionResult> DeleteCustomer(int id)
{
    ...
}

...
}
```

*GetCustomers* 方法处理检索所有客户的请求，它通过简单地返回您之前创建的实体框架数据模型中的整个 *Customers* 集合来满足此请求。在幕后，实体框架从数据库获取所有客户，并使用此信息填充 *Customers* 集合。如果应用向此 Web 服务的 *api/Customers* URL 发送 HTTP GET 请求，则会调用此方法。

*GetCustomer* 方法（不要与 *GetCustomers* 混淆）接受一个整数参数。此参数指定特定客户的 CustomerID，方法使用实体框架查找此客户的详细信息然后返回它。当应用向 *api/Customers/n* URL 发送 HTTP GET 请求时，*GetCustomer* 会运行，其中 *n* 是要检索的客户的 ID。

*PutCustomer* 方法在应用向 Web 服务发送 HTTP PUT 请求时运行。请求指定客户 ID 和客户的详细信息，此方法中的代码使用实体框架使用详细信息更新指定的客户。*PostCustomer* 方法响应 HTTP POST 请求，并以客户的详细信息作为其参数。此方法将具有这些详细信息的客户添加到数据库中（前面的代码示例中未显示详细信息）。最后，*DeleteCustomer* 方法处理 HTTP DELETE 请求并删除具有指定客户 ID 的客户。

### Note

Web API 模板生成的代码乐观地假设它将始终能够连接到数据库。在分布式系统的世界中，数据库和 Web 服务位于不同的服务器上，这可能并不总是如此。网络容易出现瞬时错误和超时；连接尝试可能因临时故障而失败，如果稍后重试则可能成功。将临时故障报告给客户端作为错误可能会让用户感到沮丧。如果可能，最好在重试次数不过多时静默重试失败的操作（您不希望 Web 服务在数据库真的不可用时冻结）。有关此策略的详细信息，请参阅“Cloud Service Fundamentals Data Access Layer—Transient Fault Handling” at http://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx。

ASP.NET Web API 模板自动生成将请求定向到控制器类中适当方法的代码，如果需要管理其他资源，例如产品或订单，您可以添加更多控制器类。

### Note

有关使用 ASP.NET Web API 模板实现 REST Web 服务的详细信息，请参阅“Web API” at http://www.asp.net/web-api。

您也可以手动创建控制器类，使用与 CustomersController 类所示相同的模式——您不必使用实体框架从数据库获取和存储数据。ASP.Net Web API 模板在 ValuesController.cs 文件中包含一个示例控制器，您可以复制并用自己的代码增强它。

- 4. 在 CustomersController 类中，修改创建 AdventureWorksEntities 上下文对象的语句，使其使用接受密码作为其参数的构造函数。作为构造函数的参数，提供您在创建数据库时指定的管理员密码。（在以下代码示例中，将字符串 YourPassword 替换为您自己的密码。）

