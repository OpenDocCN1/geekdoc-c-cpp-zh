

```csharp
private void InitializeServices()
{
    const string ConnectionString =
        @"server=
(localdb)\MSSQLLocalDb;database=Books;trusted_connection=true";

    var services = new ServiceCollection();
    services.AddTransient<BooksService>();
    services.AddEntityFramework()
        .AddSqlServer()
        .AddDbContext<BooksContext>(options =>
            options.UseSqlServer(ConnectionString));

    Container = services.BuildServiceProvider();
}

public IServiceProvider Container { get; private set; }
```

服务的初始化以及 `BooksService` 的使用都是在 `Main` 方法中完成的。通过调用 `IServiceProvider` 的 `GetService` 方法来获取 `BooksService`（代码文件 BooksSampleWithDI/Program.cs）：

```csharp
static void Main()
{
    var p = new Program();
    p.InitializeServices();

    var service = p.Container.GetService<BooksService>();
    service.AddBooksAsync().Wait();
    service.ReadBooks();
}
```

运行该应用程序时，您可以看到记录被添加到 Books 数据库并从其中读取。

> 注意 您可以在第31章“使用 XAML 应用程序的模式”中阅读有关依赖注入和 `Microsoft.Framework.DependencyInjection` 包的更多信息，并且还可以在第40章“ASP.NET Core”和第41章“ASP.NET MVC”中看到它的实际应用。

## 创建模型

本章的第一个示例映射了一个单独的表。第二个示例展示了如何在表之间创建关系。本节中，我们使用 C# 代码来创建数据库，而不是使用 SQL DDL 语句（或使用设计器）。

示例应用程序 MenusSample 使用了以下依赖项和命名空间：

### 依赖项

```
NETStandard.Library
```

### 命名空间

- Microsoft.EntityFrameworkCore
- Microsoft.EntityFrameworkCore.ChangeTracking
- System
- System.Collections.Generic
- System.ComponentModel.DataAnnotations
- System.ComponentModel.DataAnnotations.Schema
- System.Linq
- System.Threading
- System.Threading.Tasks
- static System.Console

### 创建关系

让我们开始创建模型。该示例项目使用 `MenuCard` 和 `Menu` 类型定义了一对多关系。`MenuCard` 包含一个 `Menu` 对象的列表。这个关系简单地通过类型为 `List<Menu>` 的 `Menu` 属性来定义（代码文件 MenusSample/MenuCard.cs）：

```csharp
public class MenuCard
{
	public int MenuCardId { get; set; }
	public string Title { get; set; }
	public List<Menu> Menus { get; } = new List<Menu>();

	public override string ToString() => Title;
}
```

这种关系也可以从另一个方向访问；`Menu` 可以通过 `MenuCard` 属性访问 `MenuCard`。指定 `MenuCardId` 属性来定义外键关系（代码文件 MenusSample/Menu.cs）：

```csharp
public class Menu
{
	public int MenuId { get; set; }
	public string Text { get; set; }
	public decimal Price { get; set; }
	public int MenuCardId { get; set; }
	public MenuCard MenuCard { get; set; }

	public override string ToString() => Text;
}
```

到数据库的映射由 `MenusContext` 类完成。该类的定义与之前的上下文类型类似；它仅包含两个属性来映射两个对象类型：`Menus` 和 `MenuCards` 属性（代码文件 MenusSamples/MenusContext.cs）：

```csharp
public class MenusContext: DbContext
{
    private const string ConnectionString = @"server=(localdb)\\MSSQLLocalDb;" +
        "Database=MenuCards;Trusted_Connection=True";

    public DbSet<Menu> Menus { get; set; }
    public DbSet<MenuCard> MenuCards { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        base.OnConfiguring(optionsBuilder);
        optionsBuilder.UseSqlServer(ConnectionString);
    }
}
```

## 使用 .NET CLI 进行迁移

为了使用 C# 代码自动创建数据库，可以通过 `dotnet-ef` 包为 .NET CLI 工具扩展 `ef` 工具。该包包含用于创建迁移 C# 代码的命令。通过从项目配置文件中的 tools 部分引用此包来安装它（代码文件 MenusSample/project.json）：

```json
"tools": {
    "dotnet-ef":"1.0.0-*"
}
```

有了 `ef` 命令后，它就提供了 `database`、`dbcontext` 和 `migrations` 命令。`database` 命令用于将数据库升级到特定的迁移状态。`dbcontext` 命令列出项目中所有从 `DbContext` 派生的类型（`dbcontext list`），并从数据库创建上下文和实体（`dbcontext scaffold`）。`migrations` 命令允许创建和删除迁移，以及创建 SQL 脚本来使用所有迁移创建数据库。如果生产数据库只能由 SQL 管理员使用 SQL 代码创建和修改，您可以将生成的脚本交给 SQL 管理员。

要创建初始迁移以从代码创建数据库，可以从开发者命令提示符中调用以下命令。该命令创建名为 `InitMenuCards` 的迁移：

```
>dotnet ef migrations add InitMenuCards
```

`migrations add` 命令通过反射访问从 `DbContext` 派生的类，并进而访问被引用的模型类型。利用这些信息，它会创建两个类来创建和更新数据库。使用 `Menu`、`MenuCard` 和 `MenusContext` 类，创建了两个类：`MenusContextModelSnapshot` 和 `InitMenuCards`。命令成功后，您可以在 Migrations 文件夹中找到这两种类型。

`MenusContextModelSnapshot` 类包含用于构建数据库的模型的当前状态：

```csharp
[DbContext(typeof(MenusContext))]
partial class MenusContextModelSnapshot: ModelSnapshot
{
    protected override void BuildModel(ModelBuilder modelBuilder)
    {
        modelBuilder
            .HasAnnotation("ProductVersion","7.0.0-rc1-16348")
            .HasAnnotation("SqlServer:ValueGenerationStrategy",
                SqlServerValueGenerationStrategy.IdentityColumn);

        modelBuilder.Entity("MenusSample.Menu", b =>
        {
            b.Property<int>("MenuId")
                .ValueGeneratedOnAdd();
            b.Property<int>("MenuCardId");
            b.Property<decimal>("Price");
            b.Property<string>("Text");
            b.HasKey("MenuId");
        });

        modelBuilder.Entity("MenusSample.MenuCard", b =>
        {
            b.Property<int>("MenuCardId")
                .ValueGeneratedOnAdd();

            b.Property<string>("Title");
            b.HasKey("MenuCardId");
        });

        modelBuilder.Entity("MenusSample.Menu", b =>
        {
            b.HasOne("MenusSample.MenuCard")
                .WithMany()
                .HasForeignKey("MenuCardId");
        });
    }
}
```

`InitMenuCards` 类定义了 `Up` 和 `Down` 方法。`Up` 方法列出了创建 `MenuCard` 和 `Menu` 表所需的所有操作，包括主键、列和关系。`Down` 方法删除这两个表：

```csharp
public partial class InitMenuCards: Migration
{
    protected override void Up(MigrationBuilder migrationBuilder)
    {
        migrationBuilder.CreateTable(
            name:"MenuCard",
            columns: table => new
            {
                MenuCardId = table.Column<int>(nullable: false)
                    .Annotation("SqlServer:ValueGenerationStrategy",
                        SqlServerValueGenerationStrategy.IdentityColumn),
                Title = table.Column<string>(nullable: true)
            },
            constraints: table =>
            {
                table.PrimaryKey("PK_MenuCard", x => x.MenuCardId);
            });
```

```csharp
migrationBuilder.CreateTable(
    name:"Menu",
    columns: table => new
    {
        MenuId = table.Column<int>(nullable: false)
            .Annotation("SqlServer:ValueGenerationStrategy",
                SqlServerValueGenerationStrategy.IdentityColumn),
        MenuCardId = table.Column<int>(nullable: false),
        Price = table.Column<decimal>(nullable: false),
        Text = table.Column<string>(nullable: true)
    },
    constraints: table =>
    {
        table.PrimaryKey("PK_Menu", x => x.MenuId);
        table.ForeignKey(
            name:"FK_Menu_MenuCard_MenuCardId",
            column: x => x.MenuCardId,
            principalTable:"MenuCard",
            principalColumn:"MenuCardId",
            onDelete: ReferentialAction.Cascade);
    });
}

protected override void Down(MigrationBuilder migrationBuilder)
{
    migrationBuilder.DropTable("Menu");
    migrationBuilder.DropTable("MenuCard");
}
```

> 注意 每次进行更改时，您都可以创建另一个迁移。新的迁移只定义从先前版本到新版本所需更改的内容。如果客户数据库需要从任何较早版本更新，迁移数据库时会调用所需的迁移。
> 
> 在开发过程中，您可能不需要项目中创建的所有迁移，因为可能不存在具有此类中间状态的数据库。在这种情况下，您可以删除一个迁移并创建一个新的、更大的迁移。

## 使用 MSBuild 进行迁移

如果您使用的是基于 MSBuild 的项目（而不是 DNX）上的 Entity Framework 迁移，则迁移命令会有所不同。对于完整框架的 Console 应用程序、WPF 应用程序或 ASP.NET 4.6 项目类型，您需要在 NuGet 包管理器控制台中指定迁移命令，而不是开发者命令提示符。您可以通过“工具”>“库包管理器”>“包管理器控制台”从 Visual Studio 启动包管理器控制台。

使用包管理器控制台，您可以使用 PowerShell 脚本添加和删除迁移。该命令

