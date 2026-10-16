
属性定义在 BooksContext 类中。通过该类，重写了 OnModelCreating 方法，将 BookChapter 类型映射到 Chapters 表，并为 Id 列定义一个唯一标识符，该标识符使用数据库生成的默认唯一标识符。Title 列被限制为最多 120 个字符（代码文件 BookServiceAsyncSample/Models/BooksContext.cs）：

```csharp
public class BooksContext: DbContext
{
    public DbSet<BookChapter> Chapters { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);
        EntityTypeBuilder<BookChapter> chapter = modelBuilder
            .Entity<BookChapter>();
        chapter.ToTable("Chapters").HasKey(p => p.Id);
        chapter.Property<Guid>(p => p.Id)
            .HasColumnType("UniqueIdentifier")
            .HasDefaultValueSql("newid()");
        chapter.Property<string>(p => p.Title)
            .HasMaxLength(120);
    }
}
```

为了允许使用 .NET CLI 工具创建数据库，在 project.json 配置文件中定义了 ef 命令，以将其映射到 EntityFrameworkCore.Commands（代码文件 BookServiceAsyncSample/project.json）：

```json
"tools": {
    "dotnet-ef":"1.0.*"
},
```

使用依赖注入容器时，需要添加 Entity Framework 和 SQL Server，以调用扩展方法 AddEntityFramework 和 AddSqlServer。刚刚创建的 BooksContext 也需要注册。BooksContext 通过 AddDbContext 方法添加。通过该方法的选项，传入连接字符串（代码文件 BookServiceAsyncSample/Startup.cs）：

```csharp
public async void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().AddXmlSerializerFormatters();

    // etc.

    services.AddEntityFramework()
        .AddSqlServer()
        .AddDbContext<BooksContext>(options =>
            options.UseSqlServer(
                Configuration["Data:BookConnection:ConnectionString"]));
    // etc.
}
```

连接字符串本身是通过应用程序设置定义的（代码文件 BookServiceAsyncSample/appsettings.json）：

```json
"Data": {
  "BookConnection": {
    "ConnectionString":
      "Server=(localdb)\\mssqllocaldb;Database=BooksSampleDB;
       Trusted_Connection=True;MultipleActiveResultSets=true"
  }
},
```

有了这些设置，现在就可以创建迁移和数据库了。要将基于代码的迁移添加到项目中，可以从“开发者命令提示符”启动此 `dotnet` 命令，并将当前目录更改为项目目录——即放置 `project.json` 文件的目录。该语句使用定义在 `project.json` 文件中的 `ef` 命令来调用迁移，并向项目添加 `InitBooks` 迁移。成功运行此命令后，你可以在项目中看到一个 `Migrations` 文件夹，其中包含用于创建数据库的类：

```text
>dotnet ef migrations add InitBooks
```

以下命令根据启动代码中定义的连接字符串创建数据库：

```text
>dotnet ef database update
```

## 创建存储库

为了使用 `BooksContext`，你需要创建一个实现 `IBookChaptersRepository` 接口的存储库。`BookChaptersRepository` 类使用 `BooksContext`，而不是像 `SampleBookChaptersRepository` 那样使用内存字典（代码文件 `BookServiceAsyncSample/Models/BookChaptersRepository.cs`）：

```csharp
public class BookChaptersRepository: IBookChaptersRepository,
IDisposable
{
    private BooksContext _booksContext;

    public BookChaptersRepository(BooksContext booksContext)
    {
        _booksContext = booksContext;
    }

    public void Dispose()
    {
        _booksContext?.Dispose();
    }

    public async Task AddAsync(BookChapter chapter)
    {
        _booksContext.Chapters.Add(chapter);
        await _booksContext.SaveChangesAsync();
    }

    public Task<BookChapter> FindAsync(Guid id) =>
        _booksContext.Chapters.SingleOrDefaultAsync(c => c.Id == id);

    public async Task<IEnumerable<BookChapter>> GetAllAsync() =>
        await _booksContext.Chapters.ToListAsync();

    public Task InitAsync() => Task.FromResult<object>(null);

    public async Task<BookChapter> RemoveAsync(Guid id)
    {
        BookChapter chapter = await _booksContext.Chapters
            .SingleOrDefaultAsync(c => c.Id == id);
        if (chapter == null) return null;

        _booksContext.Chapters.Remove(chapter);
        await _booksContext.SaveChangesAsync();
        return chapter;
    }

    public async Task UpdateAsync(BookChapter chapter)
    {
        _booksContext.Chapters.Update(chapter);
        await _booksContext.SaveChangesAsync();
    }
}
```

如果你对上下文的使用感到困惑，可以阅读第 38 章，其中涵盖了有关 Entity Framework Core 的更多信息。

要使用此存储库，你必须从容器中的注册中移除 `SampleBookChaptersRepository`（或将其注释掉），并添加 `BookChaptersRepository`，以便在请求 `IBookChaptersRepository` 接口时，让依赖注入容器创建该类的实例（代码文件 BookServiceAsyncSample/Startup.cs）：

```csharp
public async void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().AddXmlSerializerFormatters();
    // comment the following three lines to use the BookChaptersRepository
    //IBookChaptersRepository repos = new SampleBookChaptersRepository();
    //services.AddSingleton<IBookChaptersRepository>(repos);
    //await repos.InitAsync();

    services.AddEntityFramework()
        .AddSqlServer()
        .AddDbContext<BooksContext>(options => options.UseSqlServer(
            Configuration["Data:BookConnection:ConnectionString"]));

    services.AddSingleton<IBookChaptersRepository, BookChaptersRepository>();
}
```

现在——无需更改控制器或客户端——你可以再次运行服务和客户端。根据你最初在数据库中输入的数据，你会看到 GET/POST/PUT/DELETE 请求的结果。

## 创建元数据

为服务创建元数据可以获取服务的描述，也允许你使用此元数据创建客户端。

对于使用 SOAP 的 Web 服务，自 SOAP 早期以来就有了元数据——即 Web 服务描述语言（WSDL）。WSDL 在第 44 章中有详细说明。如今，REST 服务的元数据也已出现。目前它还不是像 WSDL 那样的标准，但最流行的 API 描述框架是 Swagger（http://www.swagger.io）。自 2016 年 1 月起，Swagger 规范已更名为 OpenAPI，并且一项标准正在制定中（http://www.openapis.org）。

要将 Swagger 或 OpenAPI 添加到 ASP.NET Web API 服务，你可以使用 Swashbuckle。NuGet 包 Swashbuckle.SwaggerGen 包含生成 swagger 的代码，而包 Swashbuckle.SwaggerUi 提供动态创建的用户界面。两个包都将用于扩展 BooksServiceSample 项目。

添加 NuGet 包后，你需要向服务集合添加 Swagger。AddSwaggerGen 是向集合添加 swagger 服务的扩展方法。要配置 Swagger，需要调用 ConfigureSwaggerDocument 和 ConfigureSwaggerSchema 方法。ConfigureSwaggerDocument 配置标题、描述和 API 版本。ConfigureSwaggerSchema 定义生成的 JSON 架构的外观。示例代码配置为不显示已过时的属性，枚举值应显示为字符串（代码文件 BooksServiceSample/Startup.cs）：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add framework services.
    services.AddMvc();

    IBookChaptersRepository repos = new SampleBookChaptersRepository();
    repos.Init();
    services.AddSingleton<IBookChaptersRepository>(repos);

    services.AddSwaggerGen();
    services.ConfigureSwaggerDocument(options =>
    {
        options.SingleApiVersion(new Info
        {
            Version ="v1",
            Title ="Book Chapters",
            Description ="A sample for Professional C# 6"
        });
        options.IgnoreObsoleteActions = true;
    });

    services.ConfigureSwaggerSchema(options =>
    {
        options.DescribeAllEnumsAsStrings = true;
        options.IgnoreObsoleteProperties = true;
    });
}
```

剩下的就是在 Startup 类的 Configure 方法中进行 Swagger 配置。扩展方法 UseSwaggerGen 指定一个

