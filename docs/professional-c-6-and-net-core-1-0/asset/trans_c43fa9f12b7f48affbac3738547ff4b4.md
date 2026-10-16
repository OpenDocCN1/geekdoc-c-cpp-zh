
应生成 JSON Schema 文件。使用 UseSwaggerGen 配置的默认网址是 `/swagger/{version}/swagger.json`。在前面代码片段配置了文档后，该网址为 `/swagger/v1/swagger.json`。`UseSwaggerUi` 方法用于定义 Swagger 用户界面的网址。不带参数使用该方法时，网址为 `/swagger/ui`，但当然你也可以通过使用 `UseSwaggerUi` 方法的不同重载来更改这个网址：

```
public void Configure(IApplicationBuilder app,
    IHostingEnvironment env,
    ILoggerFactory loggerFactory)
{
    loggerFactory.AddConsole(Configuration.GetSection("Logging"));
    loggerFactory.AddDebug();

    app.UseIISPlatformHandler();
    app.UseStaticFiles();
    app.UseMvc();

    app.UseSwaggerGen();
    app.UseSwaggerUi();
}
```

在配置了 Swagger 的情况下运行应用程序时，你可以看到服务所提供的 API 的详细信息。图 42.3 展示了 BooksServiceSample、由 Values 服务生成的模板以及 BooksService 示例所提供的 API。你还可以看到按 Swagger 文档配置的标题和描述。

![](img/3d365b72b289213a91ade7eb366b8f35_1657_0.png)

图 42.3

图 42.4 展示了 BookChapters 服务的详细信息。你可以看到每个 API 的详细信息（包括模型），还可以测试 API 调用。

![](img/3d365b72b289213a91ade7eb366b8f35_1658_0.png)

图 42.4

## 创建和使用 OData 服务

ASP.NET Web API 直接支持开放数据协议（OData）。OData 通过 HTTP 协议提供对数据源的 CRUD 访问。发送 GET 请求可检索实体数据集合；POST 请求创建新实体；PUT 请求更新现有实体；DELETE 请求删除实体。在本章中，你已经看到了映射到控制器中操作方法的各种 HTTP 方法。OData 基于 JSON 和 AtomPub（一种 XML 格式）进行数据序列化。你也已经看到了 ASP.NET Web API 对 JSON 和 XML 的直接支持。OData 的更多优势在于，每个资源都可以通过简单的 URI 查询进行访问。为了了解这一点，以及如何使用 ASP.NET Web API 解决这个问题，让我们进入一个示例，并从数据库开始。

对于服务应用程序 BooksODataService，为了提供 OData 功能，需要添加 NuGet 包 `Microsoft.AspNet.OData`。要在 ASP.NET Core 1.0 中使用 OData，你至少需要 `Microsoft.AspNet.OData` 包的 6.0 版本。该示例服务允许你查询 Book 和 Chapter 对象以及它们之间的关系。

### 创建数据模型

该示例服务定义了用于模型的 `Book` 和 `Chapter` 类。`Book` 类定义了简单属性以及与 `Chapter` 类型的一对多关系（代码文件 `BooksODataService/Models/Book.cs`）：

```
public class Book
{
    public Book()
    {
        Chapters = new List<Chapter>();
    }

    public int BookId { get; set; }
    public string Isbn { get; set; }
    public string Title { get; set; }
    public List<Chapter> Chapters { get; }
}
```

`Chapter` 类定义了简单属性以及与 `Book` 类型的多对一关系（代码文件 `BooksODataService/Models/Chapter.cs`）：

```
public class Chapter
{
    public int ChapterId { get; set; }
    public int BookId { get; set; }
    public Book Book { get; set; }
    public string Title { get; set; }
    public int Number { get; set; }
    public string Intro { get; set; }
}
```

`BooksContext` 类定义了 `Books` 和 `Chapters` 属性，以及 SQL 数据库关系的定义（代码文件 `BooksODataService/Models/BooksContext.cs`）：

```
public class BooksContext: DbContext
{
    public DbSet<Book> Books { get; set; }
    public DbSet<Chapter> Chapters { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);
        EntityTypeBuilder<Book> bookBuilder = modelBuilder.Entity<Book>();
        bookBuilder.HasMany(b => b.Chapters)
            .WithOne(c => c.Book)
            .HasForeignKey(c => c.BookId);
        bookBuilder.Property<string>(b => b.Title)
            .HasMaxLength(120)
            .IsRequired();
        bookBuilder.Property<string>(b => b.Isbn)
            .HasMaxLength(20)
            .IsRequired(false);

        EntityTypeBuilder<Chapter> chapterBuilder = modelBuilder.Entity<Chapter>();
        chapterBuilder.Property<string>(c => c.Title)
            .HasMaxLength(120);
    }
}
```

### 创建服务

使用 ASP.NET Core 1.0，你可以轻松地添加 OData 服务。你不需要对控制器进行太多修改。当然，你需要将 OData 添加到依赖注入容器中（代码文件 `BooksODataService/Startup.cs`）：

```
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddEntityFramework()
        .AddSqlServer()
        .AddDbContext<BooksContext>(options => options.UseSqlServer(
            Configuration["Data:BookConnection:ConnectionString"]));
    services.AddOData();
}
```

`BooksController` 类只需要应用 `EnableQuery` 特性。这使它成为 OData 控制器。你可以使用 OData 查询来访问该控制器。应用于 `BooksController` 类的 `Route` 特性为路由定义了 `odata` 前缀。这只是一个约定，你可以根据自己的需要更改路由（代码文件 `BooksODataService/Controllers/BooksController.cs`）：

```
[EnableQuery]
[Route("odata/[controller]")]
public class BooksController: Controller
{
    private readonly BooksContext _booksContext;

    public BooksController(BooksContext booksContext)
    {
        _booksContext = booksContext;
    }

    [HttpGet]
    public IEnumerable<Book> GetBooks() =>
        _booksContext.Books.Include(b => b.Chapters).ToList();

    // GET api/values/5
    [HttpGet("{id}")]
    public Book GetBook(int id) =>
        _booksContext.Books.SingleOrDefault(b => b.BookId == id);

    // etc.
}
```

除了应用 `EnableQuery` 特性这一更改之外，控制器不需要任何其他特殊操作。

### OData 查询

现在，使用此 URL 从数据库中获取所有书籍变得非常简单（端口号在你的系统上可能不同）：

```
http://localhost:50000/odata/Books
```

要获取单本书籍，可以在 URL 中传递书籍的标识符。此请求调用 `GetBook` 操作方法，并传递返回单个结果的键：

```
http://localhost:50000/odata/Books(9)
```

每本书都有多个章节结果。通过 URL 查询，还可以获取一本书的所有章节结果：

```
http://localhost:50000/odata/Books(9)/Chapters
```

OData 还提供了更多 ASP.NET Web API 支持的查询选项。OData 规范允许向服务器传递参数以进行分页、筛选和排序。让我们来了解一下这些选项。

为了只向客户端返回有限数量的实体，客户端可以使用 `$top` 参数限制数量。这还可以通过 `$skip` 实现分页；例如，你可以跳过 3 个并获取 3 个：

```
http://localhost:50000/odata/Books?$top=3&$skip=3
```

使用 `$skip` 和 `$top` 选项，客户端可以决定要检索的实体数量。如果你想要限制客户端的请求内容——例如，有数百万条记录，绝不应该通过一次调用请求——你可以通过配置 `EnableQuery` 特性来限制这一点。将 `PageSize` 设置为 10，则最多只返回 10 个实体：

```
[EnableQuery(PageSize=10)]
```

`Queryable` 特性还有许多其他命名参数来限制查询——例如，最大跳过和获取数量、最大展开深度以及排序限制。

若要基于 `Book` 类型的属性筛选请求，可以将 `$filter` 选项应用于 `Book` 的属性。若要只筛选来自 Wrox Press 出版社的书籍，可以将 `eq` 运算符（等于）与 `$filter` 一起使用：

```
http://localhost:50000/odata/Books?$filter=Publisher eq 'Wrox Press'
```

你也可以将 `lt`（小于）和 `gt`（大于）逻辑运算符与 `$filter` 一起使用。此请求仅返回超过 40 页的章节：

```
http://localhost:50000/odata/Chapters?$filter=Pages gt 40
```

要请求排序结果，`$orderby` 选项定义排序顺序。添加 `desc` 关键字可以按降序排序：

```
http://localhost:50000/odata/Books(9)/Chapters?$orderby=Pages%20desc
```

你可以使用 `HttpClient` 类轻松地向服务发出所有这些请求。但是，还有其他选项，例如使用 WCF Data Services 创建的代理。
