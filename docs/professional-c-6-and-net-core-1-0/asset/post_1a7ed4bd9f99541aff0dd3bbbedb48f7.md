
```csharp
// Add Entity Framework services to the services container.
services.AddEntityFramework()
    .AddSqlServer()
    .AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration["Data:DefaultConnection:ConnectionString"]))
    .AddDbContext<MenuCardsContext>(options =>
        options.UseSqlServer(Configuration["Data:MenuCardConnection:ConnectionString"]));

    // etc.
}
```

With the configuration file, the MenuCardConnection connection string is added. This connection string references the SQL instance that comes with Visual Studio 2015. Of course, you can change this and also add a connection string to SQL Azure (code file MenuPlanner/appsettings.json):

```json
{
    "Data": {
        "DefaultConnection": {
            "ConnectionString": "Server=(localdb)\\mssqllocaldb;Database=aspnet5-MenuPlanner-4d3d9092-b53f-4162-8627-f360ef6b2aa8;Trusted_Connection=True;MultipleActiveResultSets=true"
        },
        "MenuCardConnection": {
            "ConnectionString": "Server=(localdb)\\mssqllocaldb;Database=MenuCards;Trusted_Connection=True;MultipleActiveResultSets=true"
        }
    },
    // etc.
}
```

## Creating a Database

You can use Entity Framework commands to create the code to create the database. With a command-line prompt, you use the .NET Core Command Line (CLI) and the ef command to create code to create the database automatically. Using the command prompt, you must set the current folder to the directory where the project.json file is located:

```
>dotnet ef migrations add InitMenuCards --context MenuCardsContext
```

> **NOTE** The dotnet tools are discussed in Chapter 1, “.NET Application Architectures”, and Chapter 17, “Visual Studio 2015.”

Because multiple data contexts (the MenuCardsContext and the ApplicationDbContext) are defined with the project, you need to specify the data context with the --context option. The ef command creates a Migrations folder within the project structure and the InitMenuCards class with an Up method to create the database tables, and the Down method to delete the changes again (code file MenuPlanner/Migrations/[date]InitMenuCards.cs):

```csharp
public partial class InitMenuCards : Migration
{
    public override void Up(MigrationBuilder migrationBuilder)
    {
        migrationBuilder.CreateTable(
            name: "MenuCard",
            columns: table => new
            {
                Id = table.Column<int>(nullable: false)
                    .Annotation("SqlServer:ValueGenerationStrategy",
                        SqlServerValueGenerationStrategy.IdentityColumn),
                Active = table.Column<bool>(nullable: false),
                Name = table.Column<string>(nullable: true),
                Order = table.Column<int>(nullable: false)
            },
            constraints: table =>
            {
                table.PrimaryKey("PK_MenuCard", x => x.Id);
            });
        migrationBuilder.CreateTable(
            name: "Menu",
            columns: table => new
            {
                Id = table.Column<int>(nullable: false)
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

Now you just need some code to start the migration process, filling the database with initial sample data. The MenuCardDatabaseInitializer applies the migration process by invoking the extension method MigrateAsync on the DatabaseFacade object that is returned from the Database property. This in turn checks whether the database associated with the connection string already has the same version as the database specified with the migrations. If it doesn’t have the same version,

## 42 ASP.NET Web API

### What’s In This Chapter?

- Overview of the ASP.NET Web API
- Creating Web API controllers
- Using repositories with dependency injection
- Creating .NET clients calling REST APIs
- Using Entity Framework from services
- Creating Metadata using Swagger
- Using OData

### Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- Book Service Sample
- Book Service Async Sample
- Book Service Client App
- Metadata Samples

### Overview

When Windows Communication Foundation (WCF) was announced with .NET 3.0, it was the technology for communication and replaced several other technologies in the .NET stack (a few mentioned here are .NET Remoting and ASP.NET Web Services). The goal was to have one communication technology that is very flexible and fulfills all needs. However, WCF was initially based on SOAP (Simple Object Access Protocol). Nowadays we have many scenarios where the powerful SOAP enhancements are not needed. For simpler scenarios such as HTTP requests returning JSON, WCF is too complex. That’s why another technology was introduced in 2012: ASP.NET Web API. With the release of ASP.NET MVC 6 and Visual Studio 2015, the third major version of ASP.NET Web API was released. ASP.NET MVC and ASP.NET Web API previously had different types and configurations (the previous versions were ASP.NET MVC 5 and ASP.NET Web API 2), but ASP.NET Web API is now part of ASP.NET MVC 6.

ASP.NET Web API offers a simple communication technology based on Representational State Transfer (REST). REST is an architecture style based on some constraints. Let’s compare a service that is based on the REST architectural style with a service that makes use of SOAP to see these constraints.

Both REST services and services making use of the SOAP protocol make use of a client-server technology. SOAP services can be stateful or stateless; REST services are always stateless. SOAP defines its own message format with a header and body to select a method of the service. With REST, HTTP verbs such as GET, POST, PUT, and DELETE are used. GET is used to retrieve resources, POST to add new resources, PUT to update resources, and DELETE to delete resources.

This chapter takes you through a journey covering various important aspects of ASP.NET Web API—creating a service, using different routing methods, creating a client, using OData, securing the service, and using custom hosts.

> **NOTE** *SOAP and WCF are covered in Chapter 44, “Windows Communication Foundation.”*

### Creating Services

Let’s start with creating a service. Using the new .NET Core framework, you need to start with an ASP.NET web application and select the ASP.NET Core 1.0 Template Web API (see [Figure 42.1]). This template adds folders and references needed with ASP.NET Web API. You can also use the template Web Application in case you need both web pages and services.
