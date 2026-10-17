
                    .Annotation("SqlServer:ValueGenerationStrategy",

                        SqlServerValueGenerationStrategy.IdentityColumn),

                Active = table.Column<bool>(nullable: false),

                Day = table.Column<DateTime>(nullable: false),

                MenuCardId = table.Column<int>(nullable: false),

                Order = table.Column<int>(nullable: false),

                Price = table.Column<decimal>(nullable: false),

                Text = table.Column<string>(nullable: false),

                Type = table.Column<string>(nullable: true)

            },

            constraints: table =>

            {

                table.PrimaryKey("PK_Menu", x => x.Id);

                table.ForeignKey(

                    name: "FK_Menu_MenuCard_MenuCardId",

                    column: x => x.MenuCardId,

                    principalTable: "MenuCard",

                    principalColumn: "Id",

                    onDelete: ReferentialAction.Cascade);

            });

    }

    public override void Down(MigrationBuilder migration)

    {

        migration.DropTable("Menu");

        migration.DropTable("MenuCard");

    }

}

```

现在，您只需要一些代码来启动迁移过程，并用初始示例数据填充数据库。`MenuCardDatabaseInitializer` 通过在 `Database` 属性返回的 `DatabaseFacade` 对象上调用扩展方法 `MigrateAsync` 来应用迁移过程。这会检查与连接字符串关联的数据库是否已经具有与迁移指定的数据库相同的版本。如果版本不同，

### 42 ASP.NET Web API

#### 本章内容

- ASP.NET Web API 概述
- 创建 Web API 控制器
- 将存储库与依赖注入结合使用
- 创建调用 REST API 的 .NET 客户端
- 在服务中使用 Entity Framework
- 使用 Swagger 创建元数据
- 使用 OData

#### 本章的 Wrox.com 代码下载

本章的 wrox.com 代码下载可在 www.wrox.com/go/professionalcsharp6 的 Download Code 选项卡中找到。本章代码分为以下几个主要示例：

- Book Service 示例
- Book Service Async 示例
- Book Service 客户端应用
- 元数据示例

#### 概述

当 Windows Communication Foundation（WCF）随 .NET 3.0 发布时，它成为通信技术，并取代了 .NET 堆栈中的其他几种技术（这里仅提及几个：.NET Remoting 和 ASP.NET Web Services）。其目标是提供一种非常灵活且能满足所有需求的通信技术。然而，WCF 最初基于 SOAP（简单对象访问协议）。如今，在许多场景下，我们并不需要强大的 SOAP 增强功能。对于更简单的场景（如返回 JSON 的 HTTP 请求），WCF 过于复杂。因此，2012 年引入了另一种技术：ASP.NET Web API。随着 ASP.NET MVC 6 和 Visual Studio 2015 的发布，ASP.NET Web API 的第三个主要版本也随之发布。ASP.NET MVC 和 ASP.NET Web API 之前具有不同的类型和配置（先前版本为 ASP.NET MVC 5 和 ASP.NET Web API 2），但现在 ASP.NET Web API 已成为 ASP.NET MVC 6 的一部分。

ASP.NET Web API 提供了一种基于表述性状态转移（REST）的简单通信技术。REST 是一种基于若干约束的架构风格。让我们将基于 REST 架构风格的服务与使用 SOAP 的服务进行比较，以了解这些约束。

REST 服务和使用 SOAP 协议的服务都使用客户端-服务器技术。SOAP 服务可以是有状态的或无状态的；REST 服务始终是无状态的。SOAP 定义了自己的消息格式，带有标头和正文，用于选择服务的方法。REST 使用 HTTP 动词，如 GET、POST、PUT 和 DELETE。GET 用于检索资源，POST 用于添加新资源，PUT 用于更新资源，DELETE 用于删除资源。

本章将带您了解 ASP.NET Web API 的各个重要方面——创建服务、使用不同的路由方法、创建客户端、使用 OData、保护服务以及使用自定义主机。

> **注意** *SOAP 和 WCF 将在第 44 章“Windows Communication Foundation”中介绍。*

#### 创建服务

让我们从创建服务开始。使用新的 .NET Core 框架，您需要从 ASP.NET Web 应用程序开始，并选择 ASP.NET Core 1.0 模板 Web API（参见 [图 42.1]）。该模板会添加 ASP.NET Web API 所需的文件夹和引用。如果您同时需要网页和服务，也可以使用 Web Application 模板。

![](img/3d365b72b289213a91ade7eb366b8f35_1634_0.png)

#### 图42.1

> 注意 ASP.NET MVC 在第41章“ASP.NET MVC”中讨论，而作为 ASP.NET MVC 基础的核心技术在第40章“ASP.NET Core”中讨论。

使用此模板创建的目录结构包含创建服务所需的文件夹。controllers 目录包含 Web API 控制器。在第41章中你已经见过这样的控制器，实际上，ASP.NET Web API 和 ASP.NET MVC 使用相同的基础架构。以前版本并非如此。

Models 目录用于数据模型。你可以将实体类型以及返回模型类型的仓库添加到该目录。

创建的服务返回书籍章节列表，并允许动态添加和删除章节。提供此服务的示例项目名为 BookServiceSample。

### 定义模型

首先，你需要一个表示要返回和更改的数据的类型。在 Models 目录中定义的类名为 BookChapter，并包含表示章节的简单属性（代码文件 BookServiceSample/Models/BookChapter.cs）：

```csharp
public class BookChapter
{
    public Guid Id { get; set; }
    public int Number { get; set; }
    public string Title { get; set; }
    public int Pages { get; set; }
}
```

### 创建仓库

接下来，创建一个仓库。仓库提供的方法由接口 `IBookChapterRepository` 定义——用于检索、添加和更新书籍章节的方法（代码文件 `BookServiceSample/Models/IBookChaptersRepository.cs`）：

```csharp
public interface IBookChaptersRepository
{
    void Init();
    void Add(BookChapter bookChapter);
    IEnumerable<BookChapter> GetAll();
    BookChapter Find(Guid id);
    BookChapter Remove(Guid id);
    void Update(BookChapter bookChapter);
}
```

仓库的实现由类 `SampleBookChaptersRepository` 定义。书籍章节保存在一个集合类中。由于来自不同客户端请求的多个任务可以并发访问该集合，因此对书籍章节使用了 `ConcurrentList` 类型。这个类线程安全。`Add`、`Remove` 和 `Update` 方法利用该集合添加、移除和更新书籍章节（代码文件 `BookServiceSample/Models/SampleBookChapterRepository.cs`）：

```csharp
public class SampleBookChaptersRepository : IBookChapterRepository
{
    private readonly ConcurrentDictionary<Guid, BookChapter> _chapters =
        new ConcurrentDictionary<Guid, BookChapter>();

    public void Init()
    {
        Add(new BookChapter
        {
            Number = 1,
            Title = "Application Architectures",
            Pages = 35
        });
        Add(new BookChapter
        {
            Number = 2,
            Title = "Core C#",
            Pages = 42
        });
        // more chapters
    }

    public void Add(BookChapter chapter)
    {
        chapter.Id = Guid.NewGuid();
        _chapters[chapter.Id] = chapter;
    }

    public BookChapter Find(Guid id)
    {
        BookChapter chapter;
        _chapters.TryGetValue(id, out chapter);
        return chapter;
    }

    public IEnumerable<BookChapter> GetAll() => _chapters.Values;

    public BookChapter Remove(Guid id)
    {
        BookChapter removed;
        _chapters.TryRemove(id, out removed);
        return removed;
    }

    public void Update(BookChapter chapter)
    {
        _chapters[chapter.Id] = chapter;
    }
}
```

> **注意** *在示例代码中，`Remove` 方法确保通过 `id` 参数传递的 `BookChapter` 不在字典中。如果字典中已经不包含该书籍章节，也没有关系。*
> *`Remove` 方法的另一种实现可以在找不到传递的书籍章节时抛出异常。*

> **注意** *并发集合在第12章“特殊集合”中讨论。*

在启动时，`SampleBookChapterRepository` 通过依赖注入容器的 `AddSingleton` 方法注册，以便为所有请求服务的客户端只创建一个实例。在此代码片段中，使用了 `AddSingleton` 的一个重载方法，该方法允许传递先前创建的实例，从而可以通过调用 `Init` 方法初始化该实例（代码文件 `BookServiceSample/Startup.cs`）：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    IBookChaptersRepository repos = new SampleBookChaptersRepository();
    repos.Init();
    services.AddSingleton<IBookChaptersRepository>(repos);
    // etc.
}
```

### 创建控制器

ASP.NET Web API 控制器使用该仓库。可以从解决方案资源管理器的上下文菜单中选择“添加新项”->“Web API 控制器类”来创建控制器。管理书籍章节的控制器类名为 `BookChaptersController`。该类派生自基类 `Controller`。控制器的路由通过 `Route` 属性定义。路由以 `api` 开头，后跟控制器名称——即控制器类名去掉 `Controller` 后缀。`BookChaptersController` 的构造函数需要一个实现 `IBookChapterRepository` 接口的对象。该对象通过依赖注入注入（代码文件 `BookServiceSample/Controllers/BookChaptersController.cs`）：

```csharp
[Route("api/[controller]")]
public class BookChaptersController : Controller
{
    private readonly IBookChapterRepository _repository;

    public BookChaptersController(IBookChapterRepository bookChapterRepository)
    {
        _repository = bookChapterRepository;
    }
}
```

从模板创建的 `Get` 方法被重命名并修改为返回 `IEnumerable<BookChapter>` 类型的完整集合：

```csharp
// GET api/bookchapters
[HttpGet]
public IEnumerable<BookChapter> GetBookChapters() => _repository.GetAll();
```

带参数的 `Get` 方法被重命名为 `GetBookChapterById`，并使用 `Find` 方法过滤仓库的字典。过滤器的参数 `id` 从 URL 中获取。如果未找到章节，仓库的 `Find` 方法返回 `null`。在这种情况下，返回 `NotFound`。`NotFound` 返回 404（未找到）响应。当找到对象时，通过创建新的 `ObjectResult` 返回该对象：`ObjectResult` 返回状态码 200，并在正文中包含书籍章节：

```csharp
// GET api/bookchapters/guid
[HttpGet("{id}", Name = nameof(GetBookChapterById))]
public IActionResult GetBookChapterById(Guid id)
{
    BookChapter chapter = _repository.Find(id);
    if (chapter == null)
    {
        return NotFound();
    }
    else
    {
        return new ObjectResult(chapter);
    }
}
```

> **注意** 有关定义路由的信息，请参阅第41章。

在添加新的书籍章节时，添加了 `PostBookChapter` 方法。该方法接收作为 HTTP 正文一部分的 `BookChapter`，在反序列化后分配给方法参数。如果参数 `chapter` 为 `null`，则返回 `BadRequest`（HTTP 错误 400）。添加 `BookChapter` 后，该方法返回 `CreatedAtRoute`。`CreatedAtRoute` 返回 HTTP 状态码 201（已创建）和序列化后的对象。返回的头信息包含指向资源的链接——即指向 `GetBookChapterById` 的链接，其 `id` 设置为新建对象的标识符：

```csharp
// POST api/bookchapters
[HttpPost]
public IActionResult PostBookChapter([FromBody] BookChapter chapter)
{
    if (chapter == null)
    {
        return BadRequest();
    }
    _repository.Add(chapter);
    return CreatedAtRoute(nameof(GetBookChapterById), new { id = chapter.Id }, chapter);
}
```
