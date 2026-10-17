
`metadata=res://*/AdventureWorksModel.csdl|res://*/AdventureWorksModel.ssdl|res://*/AdventureWorksModel.msl;provider=System.Data.SqlClient;provider connection string="data source=tcp:csharpstepbystep.database.windows.net,1433;initial catalog=AdventureWorks;user id=johnsharp;MultipleActiveResultSets=True;App=EntityFramework"`

Save connection settings in Web.Config as:

`AdventureWorksEntities`

< Previous

Next >

Finish

Cancel

21. 在“选择您的版本”页面上，选择 Entity Framework 6.x，然后单击 Next。

22. 在“选择您的数据库对象和设置”页面上，展开 Tables，展开 SalesLT，然后选择 Customer。验证是否已选择 Pluralize Or Singularize Generated Object Names 复选框。 （此页上的另外两个选项也将默认选中。）请注意，实体框架在 `AdventureWorksModel` 命名空间中为实体模型生成类，然后单击 Finish。

## Entity Data Model Wizard

## Choose Your Database Objects and Settings

您要在模型中包含哪些数据库对象？

- - Tables
  - - dbo
  - - SalesLT
    - - Address
    - - Customer
    - - CustomerAddress
    - - Product
    - - ProductCategory
    - - ProductDescription
    - - ProductModel
    - - ProductModelProductDescription
    - - SalesOrderDetail

- - Pluralize or singularize generated object names
- - Include foreign key columns in the model
- - Import selected stored procedures and functions into the entity model

模型命名空间：

`AdventureWorksModel`

< Previous

Next >

Finish

Cancel

实体数据模型向导为 Customer 表生成实体模型，并在屏幕上的实体模型编辑器中显示图形表示，如下所示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_829_0.png)

如果出现以下“安全警告”消息框，请选中“不再显示此消息”复选框，然后单击 OK。此安全警告出现是因为实体框架使用一种称为 T4 模板的技术来为您的实体模型生成代码，并且它已使用 NuGet 从网络下载了这些模板。实体框架模板已由 Microsoft 验证过，使用是安全的。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_829_1.png)

23. 在实体模型编辑器中，右键单击 MiddleName 列，然后单击 Delete From Model。使用相同过程，从实体模型中删除 Suffix、CompanyName 和 SalesPerson 列。

Customers 应用不使用这些列，也没有必要从数据库中检索它们。它们允许空值，因此可以安全地保留为数据库表的一部分。但是，您不应删除 rowguid 和 ModifiedDate 列。这些列用于数据库标识 Customer 表中的行并跟踪多用户环境中对这些行的更改。如果删除这些列，您将无法正确地将数据保存回数据库。

24. 在 Build 菜单上，单击 Build Solution。

25. 在 Solution Explorer 中，在 AdventureWorksService 项目中，展开 Models 文件夹，展开 AdventureWorksModel.edmx，展开 AdventureWorksModel.tt，然后双击 Customer.cs。

此文件包含实体数据模型向导生成的用于表示客户的类。此类包含 Customer 表中您已包含在实体模型中的每一列的自动属性：

Click here to view code image

```
public partial class Customer
{
    public int CustomerID { get; set; }
    public string Title { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string EmailAddress { get; set; }
    public string Phone { get; set; }
    public System.Guid rowguid { get; set; }
    public System.DateTime ModifiedDate { get; set; }
}
```

26. 在 Solution Explorer 中，在 AdventureWorksModel.edmx 条目下，展开 AdventureWorksModel.Context.tt，然后双击 AdventureWorksModel.Context.cs。

此文件包含名为 `AdventureWorksEntities` 的类的定义。 （它与您在实体数据模型向导中生成数据库连接时使用的名称相同。）

Click here to view code image

```
public partial class AdventureWorksEntities : DbContext
{
    public AdventureWorksEntities()
        : base("name=AdventureWorksEntities")
    {
    }
    protected override void OnModelCreating(DbModelBuilder modelBuilder)
    {
        throw new UnintentionalCodeFirstException();
    }
    public DbSet<Customer> Customers { get; set; }
}
```

`AdventureWorksEntities` 类派生自 `DbContext` 类，此类提供应用程序用于连接到数据库的功能。默认构造函数将参数传递给基类构造函数，该参数指定用于连接到数据库的连接字符串的名称。如果您查看 web.config 文件，您将在 `<ConnectionStrings>` 部分中找到此字符串。它包含您在运行实体数据模型向导时指定的参数（其中包括其他内容）。但是，此字符串不包含用于对连接进行身份验证的密码信息，因为您选择在运行时提供此数据。您将在以下步骤中处理此问题。

您可以忽略 `AdventureWorksEntities` 类中的 `OnModelCreating` 方法。唯一的其他项是 `Customers` 集合。此集合的类型为 `DbSet<Customer>`。`DbSet` 泛型类型提供可用于向数据库添加、插入、删除和查询对象的方法。它与 `DbContext` 类协同工作，生成获取客户信息并填充集合所需的适当 SQL SELECT 命令。它还用于创建在向集合添加、修改或删除 Customer 对象时运行的 SQL INSERT、UPDATE 和 DELETE 命令。`DbSet` 集合通常称为实体集。

+ 27. 在 Solution Explorer 中，右键单击 Models 文件夹，单击 Add，然后单击 Class。

+ 28. 在“添加新项 – AdventureWorksService”对话框中，确保已选择 Class 模板。在“名称”框中，键入 AdventureWorksEntities，然后单击 Add。

一个名为 `AdventureWorksEntities` 的新类已添加到项目中并显示在代码和文本编辑器窗口中。此类目前与实体框架生成的同名现有类冲突，但您将使用此类通过将其转换为 partial 类来增强实体框架代码。`partial` 类是代码分布在两个或多个源文件中的类。这种方法对于实体框架等工具很有用，因为它使您可以添加自己的代码，而不会因将来重新生成实体框架代码而意外覆盖的风险。

+ 29. 在代码和文本编辑器窗口中，修改 `AdventureWorksEntities` 类的定义，使其成为 partial，如以下以粗体显示所示。

Click here to view code image

```
public partial class AdventureWorksEntities
{
}
```

30. 在 `AdventureWorksEntities` 类中，添加一个接受名为 password 的字符串参数的构造函数。构造函数应使用实体数据模型向导（在“选择数据连接”页面上指定）之前写入 web.config 文件的连接字符串的名称调用基类构造函数。

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

使用 ASP.NET Web API 模板创建的 Web 服务中，所有传入的 Web 请求都由一个或多个控制器类处理，每个控制器类公开映射到控制器公开的每个资源的各种类型 REST 请求的方法。例如，`CustomersController` 看起来像这样：

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
```
