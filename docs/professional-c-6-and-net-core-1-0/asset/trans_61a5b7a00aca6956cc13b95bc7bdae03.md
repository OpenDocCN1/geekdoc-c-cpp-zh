

> **注意** 反射将在第16章中讲解。

`Process`方法的最后一部分遍历集合中的所有项，并为每一项创建更多的行（`tr`）。对于每个属性，都会添加一个`td`元素，并将属性值作为内部文本写入。最后，将创建的表格元素的内部HTML代码写入输出：

```
foreach (var item in Items)
{
    tr = new TagBuilder("tr");
    foreach (var prop in properties)
    {
        var td = new TagBuilder("td");
        td.InnerHtml.Append(prop.GetValue(item).ToString());
        tr.InnerHtml.AppendHtml(td);
    }
    table.InnerHtml.AppendHtml(tr);
}
output.Content.AppendHtml(table.InnerHtml);
```

创建好标签助手（Tag Helper）后，创建视图就变得非常简单。定义好模型后，你使用`addTagHelper`并传入程序集名称来引用标签助手。当你使用`items`属性定义HTML表格时，标签助手本身就会被实例化（代码文件`MVCSampleApp/Views/TagHelpers/CustomHelper.cshtml`）：

```
@model IEnumerable<Menu>
@addTagHelper "*, MVCSampleApp"

<table items="Model" class="sample"></table>
```

运行应用程序时，你看到的表格应类似于图41.12所示。创建好标签助手后，使用起来非常容易。所有使用CSS定义的格式仍然有效，因为所定义的HTML表格的所有属性仍然保留在最终的HTML输出中。

![](img/3d365b72b289213a91ade7eb366b8f35_1609_0.png)

图41.12

## 实现操作过滤器

ASP.NET MVC在许多方面都是可扩展的。例如，你可以实现一个控制器工厂来搜索并实例化控制器（接口`IControllerFactory`）。控制器实现`IController`接口。通过使用`IActionInvoker`接口来解析在控制器中查找操作方法。你可以使用派生自`ActionMethodSelectorAttribute`的特性类来定义允许的HTTP方法。通过实现`IModelBinder`接口，可以自定义将HTTP请求映射到参数的模型绑定器。“模型绑定器”部分使用了`FormCollectionModelBinder`类型。你可以使用实现`IViewEngine`接口的不同视图引擎。本章使用Razor视图引擎。你还可以通过使用HTML助手、标签助手和操作过滤器来自定义。大多数扩展点不在本书的讨论范围内，但操作过滤器很可能是你会实现或使用的内容，因此这里会加以介绍。

操作过滤器在操作执行之前和之后被调用。它们通过特性应用到控制器或控制器的操作方法上。操作过滤器通过创建一个派生自基类`ActionFilterAttribute`的类来实现。使用这个类，可以重写基类成员`OnActionExecuting`、`OnActionExecuted`、`OnResultExecuting`和`OnResultExecuted`。`OnActionExecuting`在操作方法被调用之前调用，`OnActionExecuted`在操作方法完成时调用。之后，在返回结果之前，会调用`OnResultExecuting`方法，最后调用`OnResultExecuted`。

在这些方法中，你可以访问`Request`对象来获取调用者的信息。使用`Request`对象，你可以根据浏览器决定某些操作，可以访问路由信息，可以动态更改视图结果等等。以下代码片段从路由信息中访问`language`变量。要将此变量添加到路由中，你可以按照本章前面“定义路由”一节所述的方式更改路由。通过向路由信息添加`language`变量，你可以使用`RouteData.Values`访问URL提供的值，如下面的代码片段所示。你可以使用检索到的值来更改用户的文化设置：

```
public class LanguageAttribute : ActionFilterAttribute
{
    private string _language = null;
    public override void OnActionExecuting(ActionExecutingContext filterContext)
    {
        _language = filterContext.RouteData.Values["language"] == null ?
            null :
            filterContext.RouteData.Values["language"].ToString();
        // ...
    }

    public override void OnResultExecuting(ResultExecutingContext filterContext)
    {
    }
}
```

> **注意** *全球化和本地化、设置文化以及其他区域特定内容将在第28章“本地化”中讲解。*

使用创建的操作过滤器特性类，你可以将该特性应用到控制器上，如下面的代码片段所示。将特性用于类时，特性类的成员会随每个操作方法一起被调用。你也可以将该特性应用到某个操作方法上，这样只有在调用该操作方法时才会调用这些成员：

```
[Language]
public class HomeController : Controller
{
```

`ActionFilterAttribute`实现了多个接口：`IActionFilter`、`IAsyncActionFilter`、`IResultFilter`、`IAsyncResultFilter`、`IFilter`和`IOrderedFilter`。

ASP.NET MVC包含一些预定义的操作过滤器，例如用于要求HTTPS、授权调用者、处理错误或缓存数据的过滤器。

使用`Authorize`特性将在本章后面的“身份验证和授权”一节中介绍。

## 创建数据驱动应用程序

现在你已经了解了ASP.NET MVC的所有基础知识，是时候研究一个使用ADO.NET实体框架的数据驱动应用程序了。在这里，你可以看到ASP.NET MVC与数据访问结合所提供的功能。

> **注意** *ADO.NET实体框架将在第38章“实体框架Core”中详细讲解。*

示例应用程序`MenuPlanner`用于维护数据库中的餐厅菜单条目。只有经过身份验证的账户才能执行数据库条目的维护。未经过身份验证的用户应该可以浏览菜单。

该项目通过使用ASP.NET Core 1.0 Web应用程序模板启动。对于身份验证，你使用默认选择的“个人用户账户”。此项目模板为ASP.NET MVC和控制器添加了几个文件夹，包括`HomeController`和`AccountController`。它还添加了几个脚本库。

### 定义模型

首先在Models目录中定义模型。你使用ADO.NET实体框架创建模型。`MenuCard`类型定义了一些属性以及与菜单列表的关系（代码文件`MenuPlanner/Models/MenuCard.cs`）：

```
public class MenuCard
{
    public int Id { get; set; }
    [MaxLength(50)]
    public string Name { get; set; }
    public bool Active { get; set; }
    public int Order { get; set; }
    public virtual List<Menu> Menus { get; set; }
}
```

从`MenuCard`引用的菜单类型由`Menu`类定义（代码文件`MenuPlanner/Models/Menu.cs`）：

```
public class Menu
{
    public int Id { get; set; }
    public string Text { get; set; }
    public decimal Price { get; set; }
    public bool Active { get; set; }
    public int Order { get; set; }
    public string Type { get; set; }
    public DateTime Day { get; set; }
    public int MenuCardId { get; set; }
    public virtual MenuCard MenuCard { get; set; }
}
```

与数据库的连接，以及`Menu`和`MenuCard`两种类型的集合，都由`MenuCardsContext`管理。通过使用`ModelBuilder`，该上下文指定`Menu`类型的`Text`属性不能为null，并且其最大长度为50（代码文件`MenuPlanner/Models/MenuCardsContext.cs`）：

```
public class MenuCardsContext : DbContext
{
    public DbSet<Menu> Menus { get; set; }
    public DbSet<MenuCard> MenuCards { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Menu>().Property(p => p.Text)
            .HasMaxLength(50).IsRequired();
        base.OnModelCreating(modelBuilder);
    }
}
```

Web应用程序的启动代码定义了`MenuCardsContext`作为数据上下文，并从配置文件中读取连接字符串（代码文件`MenuPlanner/Startup.cs`）：

```
public IConfiguration Configuration { get; set; }

public void ConfigureServices(IServiceCollection services)
{
```

