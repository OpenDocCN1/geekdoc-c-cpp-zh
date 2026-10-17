
### 发送 POST 请求

让我们使用 HTTP POST 请求将新对象发送到服务。HTTP POST 请求的工作方式与 GET 请求类似。该请求在服务器端创建新对象。`HttpClient` 类的 `PostAsync` 方法要求将对象作为第二个参数传入。你可以使用 `Json.NET` 的 `JsonConvert` 类将对象序列化为 JSON。成功返回后，`Headers.Location` 属性包含一个链接，通过该链接可以从服务中再次检索该对象。

响应还包含一个带有返回对象的正文。当对象从服务返回时，`Id` 属性已在服务端创建对象时填充。这些新信息会在 JSON 代码反序列化后由 `PostAsync` 方法返回（代码文件 `BookServiceClientApp/HttpClientHelper.cs`）：

```csharp
public async Task<T> PostAsync(string uri, T item)
{
    using (var client = new HttpClient())
    {
        client.BaseAddress = _baseAddress;
        string json = JsonConvert.SerializeObject(item);
        HttpContent content = new StringContent(json, Encoding.UTF8, "application/json");
        HttpResponseMessage resp = await client.PostAsync(uri, content);
        WriteLine($"status from POST {resp.StatusCode}");
        resp.EnsureSuccessStatusCode();
        WriteLine($"added resource at {resp.Headers.Location}");
        json = await resp.Content.ReadAsStringAsync();
        return JsonConvert.DeserializeObject<T>(json);
    }
}
```

通过 `Program` 类，你可以看到添加到服务中的章节。调用 `BookChapterClient` 的 `PostAsync` 方法后，返回的 `Chapter` 包含新的标识符（代码文件 `BookServiceClientApp/Program.cs`）：

```csharp
private static async Task AddChapterAsync()
{
    WriteLine(nameof(AddChapterAsync));
    var client = new BookChapterClient(Addresses.BaseAddress);
    BookChapter chapter = new BookChapter
    {
        Number = 42,
        Title = "ASP.NET Web API",
        Pages = 35
    };
    chapter = await client.PostAsync(Addresses.BooksApi, chapter);
    WriteLine($"added chapter {chapter.Title} with id {chapter.Id}");
    WriteLine();
}
```

`AddChapterAsync` 方法的结果显示了成功创建对象的过程：

```
AddChapterAsync
status from POST Created
added resource at
http://localhost:5000/api/BookChapters/0e99217d-8769-46cd-93a4-2cf615cda5ae
added chapter ASP.NET Web API with id 0e99217d-8769-46cd-93a4-2cf615cda5ae
```

### 发送 PUT 请求

HTTP PUT 请求（用于更新记录）借助 `HttpClient` 的 `PutAsync` 方法发送。`PutAsync` 要求将更新后的内容作为第二个参数，并将包含标识符的服务 URL 作为第一个参数（代码文件 `BookServiceClientApp/HttpClientHelper.cs`）：

```csharp
public async Task PutAsync(string uri, T item)
{
    using (var client = new HttpClient())
    {
        client.BaseAddress = _baseAddress;
        string json = JsonConvert.SerializeObject(item);
        HttpContent content = new StringContent(json, Encoding.UTF8, "application/json");
        HttpResponseMessage resp = await client.PutAsync(uri, content);
        WriteLine($"status from PUT {resp.StatusCode}");
        resp.EnsureSuccessStatusCode();
    }
}
```

在 `Program` 类中，Windows Store Apps 章节被更新为不同的章节号以及标题 Windows Apps（代码文件 `BookServiceClientApp/Program.cs`）：

```csharp
private static async Task UpdateChapterAsync()
{
    WriteLine(nameof(UpdateChapterAsync));
    var client = new BookChapterClient(Addresses.BaseAddress);
    var chapters = await client.GetAllAsync(Addresses.BooksApi);
    var chapter = chapters.SingleOrDefault(c => c.Title == "Windows Store Apps");
    if (chapter != null)
    {
        chapter.Number = 32;
        chapter.Title = "Windows Apps";
        await client.PutAsync(Addresses.BooksApi + chapter.Id, chapter);
        WriteLine($"updated chapter {chapter.Title}");
    }
    WriteLine();
}
```

`UpdateChapterAsync` 方法的控制台输出显示了 HTTP NoContent 结果和更新后的章节标题：

```
UpdateChapterAsync
status from GET OK
status from PUT NoContent
updated chapter Windows Apps
```

### 发送 DELETE 请求

示例客户端演示的最后一个请求是 HTTP DELETE 请求。在调用了 `HttpClient` 类的 `GetAsync`、`PostAsync` 和 `PutAsync` 之后，显而易见，对应的格式就是 `DeleteAsync`。这段代码片段展示的是，`DeleteAsync` 方法只需要一个 URI 参数来标识要删除的对象（代码文件 `BookServiceClientApp/HttpClientHelper.cs`）：

```csharp
public async Task DeleteAsync(string uri)
{
    using (var client = new HttpClient())
    {
        client.BaseAddress = _baseAddress;
        HttpResponseMessage resp = await client.DeleteAsync(uri);
        WriteLine($"status from DELETE {resp.StatusCode}");
        resp.EnsureSuccessStatusCode();
    }
}
```

`Program` 类定义了 `RemoveChapterAsync` 方法（代码文件 `BookServiceClientApp/Program.cs`）：

```csharp
private static async Task RemoveChapterAsync()
{
    WriteLine(nameof(RemoveChapterAsync));
    var client = new BookChapterClient(Addresses.BaseAddress);
    var chapters = await client.GetAllAsync(Addresses.BooksApi);
    var chapter = chapters.SingleOrDefault(c => c.Title == "ASP.NET Web Forms");
    if (chapter != null)
    {
        await client.DeleteAsync(Addresses.BooksApi + chapter.Id);
        WriteLine($"removed chapter {chapter.Title}");
    }
    WriteLine();
}
```

运行应用程序时，`RemoveChapterAsync` 方法首先显示 HTTP GET 方法的状态，因为会先执行 GET 请求来检索所有章节，然后显示成功删除 ASP.NET Web Forms 章节的 DELETE 请求：

```
RemoveChapterAsync
status from GET OK
status from DELETE OK
removed chapter ASP.NET Web Forms
```

### 写入数据库

第 38 章“Entity Framework Core”介绍了如何使用 Entity Framework 将对象映射到关系。ASP.NET Web API 控制器可以轻松使用 `DbContext`。在示例应用中，你完全不需要修改控制器；只需创建并注册一个不同的仓储来使用 Entity Framework。本节将描述所有需要的步骤。

#### 定义数据库

让我们从定义数据库开始。为了在 SQL Server 中使用 Entity Framework，需要将 NuGet 包 `EntityFramework.Core` 和 `EntityFramework.MicrosoftSqlServer` 添加到服务项目中。为了从代码创建数据库，还需要添加 NuGet 包 `EntityFramework.Commands`。

`BookChapter` 类在前面已经定义过。这个类保持不变，用于从数据库填充实例。映射到属性定义在 `BooksContext` 类中。通过该类，重写了 `OnModelCreating` 方法，将 `BookChapter` 类型映射到 `Chapters` 表，并为 `Id` 列定义一个唯一标识符，该标识符使用数据库生成的默认唯一标识符。`Title` 列被限制为最多 120 个字符（代码文件 `BookServiceAsyncSample/Models/BooksContext.cs`）：

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

为了允许使用 .NET CLI 工具创建数据库，在 `project.json` 配置文件中定义了 `ef` 命令，以将其映射到 `EntityFrameworkCore.Commands`（代码文件 `BookServiceAsyncSample/project.json`）：

```json
"tools": {
    "dotnet-ef":"1.0.*"
},
```

使用依赖注入容器时，需要添加 Entity Framework 和 SQL Server，以调用扩展方法 `AddEntityFramework` 和 `AddSqlServer`。刚刚创建的 `BooksContext` 也需要注册。`BooksContext` 通过 `AddDbContext` 方法添加。通过该方法的选项，传入连接字符串（代码文件 `BookServiceAsyncSample/Startup.cs`）：

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

连接字符串本身是通过应用程序设置定义的（代码文件 `BookServiceAsyncSample/appsettings.json`）：

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
