
当你向 DI 请求一个构造函数时，你将获得一个实例，其依赖项（例如对父实例的引用或其他链接实例）将由容器解析。

DI 容器可以使用不同的注入技术将依赖项注入到实体中：

- `构造函数注入` — 实体在其构造函数参数或参数中获取依赖对象（假设它有多个依赖对象）。当类实例化时（即执行其构造函数时），DI 容器会注入构造函数的部分或全部参数。
- `属性（Setter器）注入` — 实体通过属性（或多个属性）获取其依赖项（或对象）。
- `方法调用注入` — 实体的依赖对象通过一次或多次调用设置，其中依赖项作为方法参数传递。这种注入经常用于父子类层次结构的初始化。

DI 容器的行为像一个接口-类关联的注册表，其键名为类实例。在使用容器解析特定接口之前，你必须先将该接口与具体实现进行注册。

# 服务定位器模式

服务定位器模式集中了分布式服务对象的查找，提供了一个集中的控制点，并可以作为一个消除冗余查找的缓存。它用于软件开发中，通过强抽象层封装涉及获取服务的过程。

在解耦的系统中，你并不知道代码将运行的环境，或者你可能想要创建一个可以在多个环境中运行的组件。例如，你可能需要一个既用于 Web 应用程序又用于 Windows 服务的组件。在后者，你无法访问有效的 `HttpClient` 实例，但你可以依赖于某些接口实现，如 `IEmailSenderService`。

`Service Locator` 的实现提供了其自身的单例实例，并且它只需要对持有注册数据的 DI 容器进行一次性注册。

列表 18-4 显示了如何使用 Unity 的 `ServiceLocator` 实现来解析另一个服务。

```cs
public class BookService{
    public void SendMailAboutNewBooks () {
        var emailSenderService = ServiceLocator.Current;
        GetInstance<IEmailSenderService>();
    }
}
```

# MVC 中的扩展性

MVC 框架在设计时考虑了扩展性。设计模式在 MVC 的扩展性功能中起着重要作用。通过这些功能，你可以根据自己的喜好定制整个框架。

在内部，MVC 被构建为一组一致的独立组件，这些组件可以被其他组件替换。你有一套 MVC 组件的默认实现，可以在应用程序中使用。然而，如果你需要比默认实现更复杂的东西，你有两个选择：

- 你继承代表 MVC 组件的类，并实现具有更多控制权的你自己的组件——或者相反，简化它们（例如，使用默认值）。
- 框架中的所有组件都派生自基类或实现接口。你可以替换原始组件来创建你自己的组件。

MVC 中有许多扩展点。我们不会单独讨论它们，而是在之后在它们使用的上下文中遇到它们。

## 创建 MVC 2 应用程序

`Visual Studio 2010` 自带了 MVC 2。你可以通过“文件 > 新项目”命令开始开发 MVC 2 应用程序。“新建项目”对话框包含两个模板（ASP.NET MVC 2 Web 应用程序和 ASP.NET MVC 2 空 Web 应用程序），均适用于 C# 语言。图 18-4 显示了这些模板。

在本章中，你通过一个名为 `AcmeLibrary` 的示例来学习 MVC 开发。在本节，你将创建此项目并学习其结构如何支持 MVC 模式。

显示“新建项目”对话框（文件 > 新项目），并选择 `Visual C#` 类别下的 ASP.NET MVC 2 Web 应用程序。选择项目名称为 `AcmeLibrary` 并点击确定。

`Visual Studio` 显示如图 18-5 所示的对话框，询问你是否要为应用程序创建单元测试。如前所述，MVC 利用了 TDD 方法，此对话框强调了这一意图。在示例中，你将不会创建单元测试，因此选择对话框中的第二个选项（如图 18-5 所示）并点击确定。

几秒钟后，`Visual Studio 2010` 创建了可以立即构建运行的项目骨架。使用“调试 + 无调试启动”命令（或按 `Ctrl+F5`）并运行 `AcmeLibrary`。ASP.NET 开发服务器启动并显示 `AcmeLibrary` 的主页，如图 18-6 所示。

如图 18-6 所示，应用程序提供了从主页到关于页的链接，还有一个登录链接。关闭 Web 浏览器中的应用程序页面并返回 `Visual Studio`。

# 项目结构

当你创建 `AcmeLibrary` 项目时，`Visual Studio` 会生成几个文件夹和文件。你可以参考解决方案资源管理器（Solution Explorer）工具中的该结构，如图 18-7 所示。

从 Web 应用的角度来看，第一个重要的文件夹是 `Content` 文件夹。它包含了应用程序的级联样式表（CSS）文件。通常，`Content` 文件夹下的 `Images` 文件夹存放网页中使用的图像。你可以通过修改 `Site.css` 文件或将其更改为其他 CSS 文件（当然，还需要在相应的母页中替换对 `Site.css` 的引用）来更改网站的整体设计。

第二个重要的文件夹是 `Scripts` 文件夹。它包含了为你创建的项目提供的约 10 几个 JavaScript 文件。值得提到的是，你的项目内置了对 `jQuery` 客户端脚本的支持，并且可以在 HTML 表单中实现 `jQuery` 验证插件到模型的的验证，而无需与服务器进行额外的往返。

正如其名所示，另外三个文件夹（`Controllers`、`Models` 和 `View`）也与 MVC 模式相关。`Controllers` 文件夹包含了在项目中扮演控制器角色的类。图 18-7 显示 `Visual Studio` 创建了两个控制器，一个用于首页（`HomeController.cs`），另一个用于关于页面（`AccountController.cs`）。

![](img/b5597c749e848b27b0d305153ae16106_804_0.png)

图 18-7：解决方案结构

`Views` 文件夹是所有在 MVC 模式中扮演视图角类的容器。表示视图及其辅助类被分组在子文件夹中。`Account` 文件夹存放与登录和账户处理功能相关的视图；`Home` 封装了与关于页面和首页相关的视图（位于 `Index.aspx` 文件中，稍后会解释）。`Shared` 文件夹存放辅助页面和类型，例如 `Error.aspx`、`LogOnUserControl.cs` 和 `Master.files`。

> 当你查看 `.aspx`、`.ascx` 和 `Master` 文件时，你会发现它们与 ASP.NET Web 项目中具有相似扩展的文件不同，它们没有后代码文件。ASP.NET 项目中由后代码处理的许多功能（例如收集表单数据、验证和导航）在 ASP.NET MVC 中以完全不同的方式管理，不需要后代码文件。

`Models` 文件夹是用于定义 MVC 模式中模型类型的容器。首页和关于页面没有引用任何模型类——你甚至可以说它们使用一个没有任何属性或操作的空模型。该文件夹中的 `AccountModel.cs` 包含了处理函数的模型类。

`Models`、`Controllers` 和 `Views` 文件夹不仅仅是为了简单组织项目文件。它们还提供了特定角色的右键菜单。例如，当你右键点击 `Controllers` 文件夹时，在右键菜单的 Add 子菜单中，你可以看到“`Controller...`”命令，如图 18-8 所示。此命令允许你为网站添加新控制器。

同样，当你右键点击 `Views` 文件夹时，你会在 Add 子菜单下找到“`View...`”命令。你可以构建你的应用程序，但它将无法运行（或者至少不符合预期）。你还会丢失右键菜单中针对特定文件夹的命令。请保持文件夹名称不变。

`Global.asax` 和 `Web.config` 文件在 MVC 2 中的作用与传统的 ASP.NET 项目相同。

# 它是如何工作的？

当你使用 ASP.NET 创建应用程序时，归根结底请求被映射到 `.aspx` 文件（或 HTML 文件）。例如，当请求由 `http://MySuperWebsite.com/KnowledgeBase/WindowsIssues.aspx` URL 表示时，`KnowledgeBase` 文件夹下的 `WindowsIssues.aspx` 文件将被渲染以在浏览器中生成 HTML 输出。

MVC 框架的请求方式不同。让我们位于 `Views` 下 `Shared` 文件夹中的 `Site.Master` 文件。列表 18-5 显示了该文件（为了提高可读性，在 `<div>` 标签后插入了换行和一些注释）。

代码列表 18-5：`Site.Master`

![](img/b5597c749e848b27b0d305153ae16106_805_0.png)

可在 Wrox.com 下载

```
<div id="title">
  <html>
    <h1>My MVC Application</h1>
  </html>
  <div> <!-- <div id="logindisplay"> -->
    @Html.RenderPartial("LogOnUserControl") %>
  </div>
  <div id="menu">
    <ul id="menu">
      <li>@Html.ActionLink("Home", "Index", "Home")</li>
      <li>@Html.ActionLink("About", "About", "Home")</li>
    </ul>
  </div>
  <div> <!-- Header -- -->
    <div id="main">
      <asp:ContentPlaceHolder Id="MainContent" runat="server" />
      <div id="footer"></div>
    </div>
  </div>
  <div> <!-- Page -- -->
  </div>
</div>
</body>
</html>
```

代码文件 `[Site.Master]` 可在 Wrox.com 下载

虽然 ASP.NET Web 母页继承自派生 `System.Web.UI.MasterPage` 类型的类，但此页面（如你在此处 `%@ Master` 标签中所示）继承自派生 `System.Web.MasterPage` 的 `System.Web.Mvc.ViewPage` 类。母页的结构与 ASP.NET 非常相似。

```
<div id="container">
  <ul id="menu">
    <li>@Html.ActionLink("Home", "Index", "Home")</li>
    <li>@Html.ActionLink("About", "About", "Home")</li>
  </ul>
</div>
```

`RouteCollection` 类的 `IgnoreRoute` 和 `MapRoute` 扩展方法由 MVC 框架提供。图 18-10 显示了 HTTP 请求从客户端浏览器通过路由组件发送后，是如何转发到负责处理它的实体的。

请求进入 IIS 的第一个点是 ASP.NET 提供的 `UrlRoutingModule`。它的任务是将请求格式化并传递给 `UrlRoutingHandler`。`UrlRoutingHandler` 在其 `RouteCollection` 中检查传入的 URL，如果找到匹配，它会将请求转发给适当的处理器。

![](img/b5597c749e848b27b0d305153ae16106_809_0.png)

`IgnoreRoute` 方法创建一个与 `StopRoutingHandler` 关联的路由，这意味着 ASP.NET 停止处理 URL 并将其转发到在 IIS 中注册的其他处理器。

`MapRoute` 方法创建一个与 `MvcHandler` 关联的路由，它是 MVC 应用程序的第一个真实入口。从这一点开始，你可以使用 `RequestContext` 来实例化满足请求所需的所有数据。`RequestContext` 包含了当前的 `HttpContext` 和匹配的 `RouteData`。

现在，通过这个简短解释，你可以看到 `AcmeLibrary` 的 HTML 表示中“Home”和“About”菜单项的链接是如何工作的：

```
<ul id="menu">
  <li><a href="/">Home</a></li>
  <li><a href="/Home/About">About</a></li>
</ul
```

当请求为 `/` 时（例如 URL 为 `http://AcmeLibrary.com/`），没有提供控制器和动作名称，将使用默认的 "Home" 控制器和默认的 "Index" 动作。图 18-9 所示的 `ControllerFactory` 组件将 "Home" 名称解析为 `HomeController` 类，而 `ActionInvoker` 组件将 "Index" 名称解析为 `Index` 公有方法。

当请求为 `/Home/About` 时（例如 URL 为 `http://AcmeLibrary.com/Home/About`），将使用 "Home" 控制器和 "About" 动作，该动作映射到 `HomeController` 类的 `About` 公有方法。

## Controller 类

让我们来看看 `HomeController` 类，它包含了负责执行 `Index` 和 `About` 动作的代码。列表 18-7 显示了该类的源代码，其结构非常地紧凑。

> 列表 18-7: `HomeController`

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;

namespace AcmeLibrary.Controllers
{
    [HandleError]
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            ViewData["Message"] = "Welcome to ASP.NET MVC!";
            return View();
        }

        public ActionResult About()
        {
            return View();
        }
    }
}
```

`HomeController` 继承自 `System.Web.Mvc` 命名空间下的 `Controller` 类。装饰此类的 `[HandleError]` 特性声明该控制器应通过将错误重定向到 `Error.aspx` 页面来处理默认错误。

`Index` 和 `About` 两个方法代表动作并返回 `ActionResult` 实例。两个方法都调用 `View` 方法来获取一个 `View` 实例——`ViewResult` 继承自 `ActionResult`。

**View** 方法从 `Views` 子文件夹返回与动作结果匹配的视图，该视图又匹配控制器名称。因此，在这种情况下，`View` 方法分别为 `Index` 和 `About` 动作返回指向 `Views/Home/Index.aspx` 或 `Views/About.aspx` 的实例。在 `Index` 方法中设置的 `ViewData` 成员是一个字典——其类型为 `ViewData`——存储带有字符串键和 `System.Object` 值的条目。`Index` 方法将 `Message` 键条目设置为欢迎字符串。

当动作方法检索 `ActionResult` 实例时，控制器会解释结果并决定采取什么活动。在 `Index` 和 `About` 动作的情况下，结果是一个 `View`，因此控制器隐式或显式地导航到由该结果命名的视图。

## View

`Views/` 文件夹中的 `Index.aspx` 和 `About.aspx` 页面定义的 `Index` 和 `About` 视图是简单的，如列表 18-8 和列表 18-9 所示。

列表 18-8: `Index.aspx`

```
<%@ Page Language="#C#" MasterFilePath="~/Views/Shared/Site.Master"
Inherits="System.Web.Mvc.Page" %>
<asp:Content ID="Content1" ContentHolderID="TitleContent" runat="server">
  Home Page
</asp:Content>
<asp:Content ID="Content2" ContentHolderID="MainContent" runat="server">
<h2><%: ViewData["Message"] %></h2>
<p>
  To learn more about ASP.NET MVC visit
  <a href="http://asp.net/mvc" title="ASP.NET MVC Website">http://asp.net/mvc</a>
</p>
</asp:Content>
```

*代码文件 [Index.aspx] 可在 Wrox.com 下载*

列表 18-9: `About.aspx`

```
<%@ Page Language="#C#" MasterFilePath="~/Views/Shared/Site.Master"
Inherits="System.Web.Mvc.Page" %>
<asp:Content ID="aboutTitle" ContentHolderID="TitleContent" runat="server">
  About Us
</asp:Content>
<asp:Content ID="aboutContent" ContentHolderID="MainContent" runat="server">
<h2>About</h2>
<p>
</p>
</asp:Content>
```
