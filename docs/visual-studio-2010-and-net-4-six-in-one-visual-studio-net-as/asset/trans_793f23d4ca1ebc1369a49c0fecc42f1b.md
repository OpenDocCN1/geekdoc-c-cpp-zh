

# 列表 18-21: Publisher.ascx

```
<@ Control Language="C#" Inherits="System.Web.Mvc.ViewControl<string> %>
<: Html.DropDownList(Self, new SelectList(
{
    new(name="Self-Published"),
    new(name="Wrox"),
    new(name="Wiley"),
    new(name="(unknown)")
},
    "name", "name",
    Model,
    "Select a publisher")
>
```

此用户控件使用了 `DropList` 辅助方法。它传递了一个 `SelectList` 实例，该实例由一个显示在列表中对象集合初始化。`SelectList` 构造函数的两个 "name" 字面量分别通过 `name` 属性的值处理项目的标识符和其显示内容。

当你在为 `BookController` 类生成编辑视图时，必须生成这些自定义模板所使用的模板。这非常简单；你只需要向 `BookMetadata` 类中添加 `UIHint` 属性。你也可以添加 `DisplayName` 属性来更改属性的标签。

列表 18-22 展示了如何创建 `BookMetadata` 类。

# 列表 18-22: BookMetadata.cs (摘录)

```
public class BookMetadata
{
    [HiddenInput(DisplayName = false)]
    public int Id { get; set; }

    [Required(ErrorMessage = "Please provide the author(s) name")]
    [DisplayName("Author(s) name:")]
    [UIHint("LongerText")]
    public string Author { get; set; }

    [Required(ErrorMessage = "Please provide a title")]
    [DisplayName("Title of the book:")]
    [UIHint("LongerText")]
    public string Title { get; set; }

    [RegularExpression(@"@[0-9]{13}",
    ErrorMessage = "ISBN must be exactly 13 digits")]
    [DisplayName("ISBN-13:")]
    public string ISBN { get; set; }
```

# 列表 18-22 (续)

```
[DisplayName("Date of publication:")]
public DateTime Published { get; set; }

[DisplayName("Published by:")]
[UIHint("Publisher")]
public string Publisher { get; set; }
}
```

代码文件 `[BookMetadata.cs]` 可在 Wrox 下载。

生成并运行 `AcmeLibrary` 项目并选择一本书进行编辑。你可以立即看到更改，如图 18-25 所示。

Publisher 视图有一个下拉列表。`Author` 和 `Title` 属性具有较长的文本框，并且所有属性都有新的标签。

# 视图引擎 (View Engines)

视图引擎是负责渲染视图内容的组件。Microsoft ASP.NET MVC 2 提供了基于 Web Forms 的视图引擎实现。然而，这并不意味着使用 Web Forms 是表示视图的唯一方法。

MVC 使用 `IViewEngine` 接口来定义视图引擎的职责，其默认实现是 `WebViewEngine`（两者都在 `System.Web.Mvc` 命名空间中）。如果你熟悉 ASP.NET 开发，为 MVC 构建视图的方法将如下：

`IViewEngine` 接口的定义如下：

```c
namespace System.Web.Mvc
{
public interface IViewEngine
{
ViewEngineResult FindPartialView(
ControllerContext controllerContext,
string partialViewName,
bool useCache);

ViewEngineResult FindView(
```

```

![](img/b5597c749e848b27b0d305153ae16106_855_0.png)

图 18-25: 使用自定义模板的编辑视图

```c
ControllerContext controllerContext,
string viewName,
string masterName,
bool useCache);
```

```c
void ReleaseView(
ControllerContext controllerContext,
IView view);
```

默认的 `WebFormEngine` 实现派自 `VirtualPathProviderEngine` 抽象类，这是一个基于 ASP.NET 的实现，但不是 Web 特有的。该类使用 ASP.NET 基于虚拟路径程序的支持来进行视图发现。

还有其他你可以配合 MVC 使用的视图引擎实现，如表 18-4 所示。

# 表 18-4: 可选视图引擎

| 视图引擎 | 描述 |
| :--- | :--- |
| Spark View Engine | Spark View Engine 是一个完整的视图引擎，背后有一个自己的文本模板引擎。该引擎的目标是减少视图中的混乱，并提供更整洁的 HTML（参阅 http://dev.dejardin.org）。 |
| Brail Engine | 该引擎是来自 MonoRail 的 .NET 端口。该引擎使用的模板是 Boo。背后的原因是，使用 MonoRail 框架，你也可以用 Boo 编写代码，因此你不需要为编写视图学习新的模板语言。该项目可以在流行的 MVCContrib CodePlex 中找到：http://mvccontrib.codeplex.com。 |
| Tiles View Engine | 该引擎使用基于 Java 标准标签库 (JSTL) 语法的模板引擎。通过这种方式，它将 JSTL 语法引入了 ASP.NET MVC 应用程序。（参阅 http://sharptiles.org）。 |
| NH View Engine | 该引擎是 Rails 上提供的 Haml 视图引擎的 .NET 端口。该标记语言的目标是实现在使用内联代码块的情况下编写整洁的 HTML。（参阅 http://code.google.com/p/nhlam）。 |
| Django View Engine | Django（该引擎 .NET 实现的基础）是为 Python 开发者提供的模板语言。Django 是 .NET 端口，并且开箱即用提供了 ASP.NET MVC 的视图引擎实现。（参阅 http://ndjango.org）。 |

如你所见，你有大量的选择来编写视图，这与你的开发背景几乎没有关系。通过这些不同的可用视图引擎，你可能会发现一个可以开始使用的的引擎。

# 路由详情 (ROUTING DETAILS)

路由组件是 MVC 框架的灵魂。它提供了一种直观的方法将请求映射到控制器类和操作方法。它的实现非常复杂，允许你以声明式的方式控制操作方法的执行方式，并允许你处理授权、请求和结果过滤等方面。与 MVC 框架中的所有组件一样，路由也是可扩展的。

本节提供了关于路由的重要细节。

# 控制器工厂 (Controller Factory)

在本章较早时候，讨论路由算法时（再次查看图 18-9 和图 18-10），你已经了解到 `MvcHandler` 接收到请求后，需要查找与请求的 `RouteData` 关联的控制器。为了完成此任务，处理器提取了强制性的 "controller" 参数。

控制器工厂的职责由 `IControllerFactory` 接口描述：

```csharp
namespace System.Web.Mvc
{
    using System.Web.Routing;

    public interface IControllerFactory
    {
        IController CreateController(
            HttpContext context,
            string controllerName);

        void ReleaseController(IController controller);
    }
}
```

如你所见，该接口有两个方法：`CreateController` 和 `ReleaseController`（销控制器）。当然，在 MVC 框架中，你有一个默认实现 `DefaultControllerFactory`。该类使用反射搜索带有 Controller 后缀并实现 `IController` 接口的默认命名空间。

由于控制器工厂是实例化特定控制器的组件，在 TDD 场景，可以使用能够注入适当领域模型（数据访问）层的工厂。

在本章的示例中，所有控制器（`HomeController`、`AboutController` 和 `BookController`）都定义在同一个程序集的同一个命名空间内，MVC 引擎可以很容易地根据 "Home"、About" 和 "Book" 等名称找到它们。然而，你可能在外部程序集中拥有独立命名空间的控制器。那么，如何解析控制器的名称呢？

控制器工厂有几种方法可以声明 DefaultControllerFactory 搜索的外部命名空间。一种方法是在 `MapRoute` 方法中描述外部命名空间（记住 Global.asax 文件中的 `RegisterRoutes` 方法使用了 `MapRoute`），如下所示：

```csharp
routes.MapRoute(
  "RouteWithNamespaceTag",
  "/{controller}/{action}",
  new {
    controller = "ControllerInExternalAssembly",
    action = "Index"
  },
  new {
    "MyApp.ExternalControllers.Controllers"
  }
);
```

