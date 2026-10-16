
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

The initialization of the services as well as the use of the BooksService is done from the Main method. The BooksService is retrieved invoking the GetService method of the IServiceProvider (code file BooksSampleWithDI/Program.cs):

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

When you run the application, you can see that records are added and read from the Books database.

> NOTE You can read more information about dependency injection and the Microsoft.Framework.DependencyInjection package in Chapter 31, “Patterns with XAML Apps,” and also see it in action in Chapter 40, “ASP.NET Core,” and Chapter 41, “ASP.NET MVC.”

## Creating a Model

The first example of this chapter mapped a single table. The second example shows creating a relation between tables. Instead of creating the database with a SQL DDL statement (or by using the designer), in this section C# code is used to create the database.

The sample application MenusSample makes use of the following dependencies and namespaces:

### Dependencies

```
NETStandard.Library
```

### Namespaces

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

### Creating a Relation

Let's start creating a model. The sample project defines a one-to-many relation using the MenuCard and Menu types. The MenuCard contains a list of Menu objects. This relation is simply defined by the Menu property of type List<Menu> (code file MenusSample/MenuCard.cs):

```csharp
public class MenuCard
{
	public int MenuCardId { get; set; }
	public string Title { get; set; }
	public List<Menu> Menus { get; } = new List<Menu>();

	public override string ToString() => Title;
}
```

The relation can also be accessed in the other direction; a Menu can access the MenuCard using the MenuCard property. The MenuCardId property is specified to define a foreign key relationship (code file MenusSample/Menu.cs):

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

The mapping to the database is done by the MenusContext class. This class is defined similarly to the previous context type; it just contains two properties to map the two object types: the properties Menus and MenuCards (code file MenusSamples/MenusContext.cs):

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

## Migrations with .NET CLI

To automatically create the database using C# code, the .NET CLI tools can be extended with the ef tools using the package dotnet-ef. This package contains commands to create C# code for the migration. The commands are made available by installing the dotnet-ef NuGet package. You install it by referencing this package from the tools section in the project configuration file (code file MenusSample/project.json):

```json
"tools": {
    "dotnet-ef":"1.0.0-*"
}
```

With the ef command in place, it offers the commands database, dbcontext, and migrations. The database command is used to upgrade the database to a specific migration state. The dbcontext command lists all DbContext derived types from the project (dbcontext list), and it creates context and entity from the database (dbcontext scaffold). The migrations command allows creating and removing migrations, as well as creating a SQL script to create the database with all the migrations. In case the production database should only be created and modified from the SQL administrator using SQL code, you can hand the generated script over to the SQL administrator.

To create an initial migration to create the database from code, the following command can be invoked from the developer command prompt. This command creates a migration named InitMenuCards:

```
>dotnet ef migrations add InitMenuCards
```

The command migrations add accesses the DbContext derived classes using reflection and in turn the referenced model types. With this information, it creates two classes to create and update the database. With the Menu, MenuCard, and MenusContext classes, two classes are created, the MenusContextModelSnapshot and InitMenuCards. You can find both types in the Migrations folder after the command succeeds.

The MenusContextModelSnapshot class contains the current state of the model to build the database:

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

The InitMenuCards class defines Up and Down methods. The Up method lists all the actions that are needed to create the MenuCard and Menu tables including the primary keys, columns, and the relation. The Down method drops the two tables:

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

> NOTE With every change you’re doing, you can create another migration. The new migration only defines the changes needed to get from the previous version to the new version. In case a customer’s database needs to be updated from any earlier version, the necessary migrations are invoked when migrating the database.
> 
> During the development process, you don’t need all the migrations that you might create with the project, as no database with such interim states might exist. In that case you can remove a migration and create a new, larger one.

## Migrations with MSBuild

In case you are using the Entity Framework migrations with MSBuild-based projects instead of DNX, the commands for migration are different. With full framework Console applications, WPF applications, or ASP.NET 4.6 project types, you need to specify migration commands in the NuGet Package Manager Console instead of the Developer Command Prompt. You start the Package Manager Console from Visual Studio via Tools > Library Package Manager > Package Manager Console.

With the Package Manager Console, you can use PowerShell scripts to add and remove migrations. The command
