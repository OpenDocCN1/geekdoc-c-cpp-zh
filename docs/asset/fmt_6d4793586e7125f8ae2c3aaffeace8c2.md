
```aspx
<%@ Page Language="vb" AutoEventWireup="false" CodeBehind="Demo03-Ajax.aspx.vb"
Inherits="Client.Demo03_Ajax" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>Ajax</title>
    <link href="Site.css" rel="stylesheet" type="text/css" />

    <script type="text/javascript">
        var custView;

        function pageLoad() {
            custView = Sys.create.dataView("#customersBody");
            showCustomers();
            $addHandler($get("DropDownList1"), "change", showCustomers);
        }

        function showCustomers() {
            var country = $get("DropDownList1").value;
            Client.NorthwindService.GetCustomersByCountry(
                country, showCustomersComplete);
        }

        function showCustomersComplete(data) {
            custView.set_data(data);
        }
    </script>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:ScriptManager ID="ScriptManager1" runat="server">
                <Scripts>
                    <asp:ScriptReference Path="~/Scripts/MicrosoftAjax.js" />
                    <asp:ScriptReference Path="~/Scripts/MicrosoftAjaxTemplates.js" />
                </Scripts>
                <Services>
                    <asp:ServiceReference Path="NorthwindService.asmx" />
                </Services>
            </asp:ScriptManager>

            <asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
```

![](img/d99870e80390742f93963da7be0b2e61_791_0.png)

### FIGURE 22-35

### SUMMARY

本章和上一章对 ASP.NET 以及你在开发项目中可以提供的一些功能进行了快速概览。ASP.NET 非常专注于开发人员生产力领域，并且在为你提供当今网站所期望的功能访问方面做得非常出色。

所介绍的大多数功能的一个优点是，你可以利用底层技术中内置的向导，也可以跳过这些向导并通过编辑标记来使用技术。两种方式都很好。所介绍的技术另一个有用的方面是，它们都支持大量的定制。你可以更改这些技术的行为和输出，以实现你所需的功能。如果你想更深入地了解 ASP.NET，请务必查看 Professional ASP.NET 4（Evjen 等著，Wiley，2010）。

## 23

## ASP.NET MVC

### WHAT YOU WILL LEARN IN THIS CHAPTER

- The Model-View-Controller (MVC) Pattern
- MVC 模式
- The goals of ASP.NET MVC
- ASP.NET MVC 的目标
- How the MVC pattern has been applied to ASP.NET MVC
- MVC 模式如何应用于 ASP.NET MVC
- Working with controllers and actions
- 使用控制器和操作
- Using scaffolding to help generate views
- 使用脚手架帮助生成视图
- Validation in ASP.NET MVC 2
- ASP.NET MVC 2 中的验证

ASP.NET MVC 是一种 Web 框架，最初于 2009 年 3 月发布，作为 ASP.NET Web Forms 的替代方案。它旨在限制抽象并让开发人员对应用程序中页面的创建拥有很大控制权。具体来说，ASP.NET MVC 被设计为执行以下操作：

- **Provide complete control over HTML markup** — With Web Forms, the final markup is mostly determined by the server controls on a page.
- **对 HTML 标记提供完全控制** — 在 Web Forms 中，最终的标记主要由页面上的服务器控件决定。
- **Have intuitive website URLs** — With Web Forms, the URL is determined by the location and name of the file being addressed.
- **具有直观的网站 URL** — 在 Web Forms 中，URL 由所寻址文件的位置和名称决定。
- **Have a clear separation of concerns** — The Web Forms programming model encourages developers to put business logic and database access code in the code-behind for a page.
- **具有清晰的关注点分离** — Web Forms 编程模型鼓励开发人员将业务逻辑和数据库访问代码放在页面的代码隐藏中。
- **Be testable by default** — Several aspects of the Web Forms model make it difficult to write unit tests for user interface layer logic.
- **默认可测试** — Web Forms 模型的几个方面使得为用户界面层逻辑编写单元测试变得困难。

必须重申，ASP.NET MVC 是 Web Forms 的替代方案，而不是其替代品。MVC 会适合某些开发者的风格，对其他人来说则可能倒退。许多人用手动变速箱与自动变速箱的类比来说明这一点。手动挡（MVC）给你完全的控制，但需要更多努力；自动挡（Web Forms）可能效率稍低，但它为你完成工作。最终，框架的选择由你决定。选择最适合你开发风格的那个。

本书撰写时，ASP.NET MVC 2 处于 Beta 阶段，预计随 Visual Studio 2010 的发布而完成。本章内容基于随 Visual Studio 2010 Beta 2 版本和 .NET 4 提供的 ASP.NET MVC 2 版本。

## MODEL-VIEW-CONTROLLER AND ASP.NET

Model-View-Controller 模式由挪威计算机科学家 Trygve Reenskaug 在 20 世纪 70 年代后期构想。它提供了一种强大而优雅的方式来在应用程序内分离关注点，并且非常适用于 Web 开发。

该模式将应用程序分为三个组件：

- **Model** — The business objects in the application
- **模型** — 应用程序中的业务对象
- **View** — The user interface
- **视图** — 用户界面
- **Controller** — Classes that handle user requests and manage application logic and flow
- **控制器** — 处理用户请求并管理应用程序逻辑和流程的类

在 ASP.NET 对该模式的实现中，请求被路由到控制器类，这些类通常应用应用程序逻辑（例如授权）、与模型交互以检索或更新数据、确定需要在响应中呈现的数据，然后将控制权传递给视图，以格式化数据并向用户呈现最终的标记。

ASP.NET MVC 实现的另一个重要方面是使用约定优于配置。随着我们在下一节构建应用程序，你会看到约定用于确定项目中文件名称和位置，或确定运行时加载哪个类或文件。你不必遵循这些约定，但这样做可以使 ASP.NET MVC 应用程序之间保持一致的体验。

## BUILDING AN ASP.NET MVC APPLICATION

ASP.NET MVC 是 ASP.NET 家族的新成员，对阅读本书的大多数人来说可能都是新的。遵循学习新框架最有效的方法是使用它的原则，我们将在本章剩余部分构建一个 ASP.NET MVC 2 应用程序。

### Creating the Project

打开 Visual Studio 并创建一个名为 `MvcDemo` 的新 ASP.NET MVC 2 Web 应用程序。你会立即被询问是否要创建关联的单元测试项目（见图 23-1）。由于可测试性是 ASP.NET MVC 的核心原则之一，因此项目模板鼓励你这样做是有意义的。保留默认的测试项目名称并单击 OK 以创建项目。

如果查看解决方案资源管理器中的 MVC 项目（见图 23-2），你会看到默认创建了多个文件和文件夹。其中三个文件夹会立即引起你的注意：`Models`、`Views` 和 `Controllers`。这些文件夹映射到该样式应用程序所基于的模式的三个组件。

![](img/d99870e80390742f93963da7be0b2e61_793_0.png)

![](img/d99870e80390742f93963da7be0b2e61_793_1.png)

> 目前，ASP.NET MVC 没有开箱即用的网站项目模板。

如果运行应用程序，你会看到项目模板包含了一些页面（包括母版页）（见图 23-3）。虽然不完全相同，但站点在外观和感觉上与使用非空 Web Forms 项目模板创建的站点相似。

![](img/d99870e80390742f93963da7be0b2e61_794_0.png)

### Controllers and Actions

在传统的 Web 应用程序框架中，请求映射到包含页面标记的文件。在 ASP.NET MVC 中，请求映射到类上的方法。这些类就是前面提到的控制器类，而方法被称为操作。操作方法负责接收用户输入、检索或保存模型数据，并将控制权传递给适当的视图。视图通常会返回页面的标记，但它也可以返回其他内容类型，例如二进制文件或 JSON 格式的数据。典型的操作会处理列出、添加、编辑或删除模型实体的请求。

让我们通过创建一个新控制器来进一步研究这些概念。在解决方案资源管理器中，右键单击 `Controllers` 文件夹并选择 Add ➜ Controller。按照惯例，控制器类的名称应以 `Controller` 结尾。Add Controller 对话框甚至鼓励使用这种约定，如图 23-4 所示。将名称设置为 `SimpleController` 并单击 Add 按钮。

![](img/d99870e80390742f93963da7be0b2e61_794_1.png)

创建的类将继承自基类 `Controller`（`System.Web.Mvc.Controller`），并将具有默认操作方法 `Index` 的外壳：

```
Public Class SimpleController
    Inherits System.Web.Mvc.Controller
```

```
' GET: /Simple/

Function Index() As ActionResult
    Return View()
End Function

End Class
```

`Index` 操作方法简单得不能再简单了。当请求进入此操作时，它只是将控制权传递给视图，而没有任何应用程序逻辑或数据访问。由于操作方法未指定要显示的视图，按照惯例，ASP.NET MVC 应查找匹配模式 `/Views/{Controller}/{Action}.aspx` 的文件。对于 `Index` 操作，这将是 `/Views/Simple/Index.aspx`，目前该文件不存在。

方法上方的注释不是必需的，但它是 Visual Studio 生成代码时通常会看到的内容。它表示此操作将通过 HTTP GET 请求访问 `/Simple`。这说明了另一个约定。MVC 使用的默认路由规则期望形式为 `/{Controller}/{Action}`。如果未指定操作，则 ASP.NET MVC 将默认为调用 `Index` 操作方法，因此请求 `/Simple` 或 `/Simple/Index` 将被路由到 `Index` 操作。你将在本章后面学习路由以及如何添加或修改路由规则。

![](img/d99870e80390742f93963da7be0b2e61_795_0.png)

由于 `Index` 操作的视图不存在，让我们创建它。我们本可以手工轻松完成，但没必要；Visual Studio 会为我们创建。在代码编辑器中，右键单击 `Index` 方法代码中的任意位置并在上下文菜单中选择 Add View 选项。在 Add View 对话框中，保持默认值不变（见图 23-5）并单击 Add 按钮。你应该会看到一个类似以下内容的新内容页：

```
<%@ Page Title="" Language="VB" MasterPageFile="~/Views/Shared/Site.Master" Inherits="System.Web.Mvc.ViewPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="TitleContent" runat="server">
    Index
</asp:Content>

<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="server">
    <h2>Index</h2>
</asp:Content>
```

注意页面的两点：它默认创建在正确的文件夹中（即 `\Views\Simple`），并且它继承自 `System.Web.Mvc.ViewPage` 而不是 `System.Web.UI.Page`。此时你应该能够运行应用程序。加载到浏览器后，导航到 `/Simple`，你将看到如图 23-6 所示的页面。

![](img/d99870e80390742f93963da7be0b2e61_796_0.png)

**图 23-6**

现在我们来看一个将数据从 action 方法传递到视图的示例。回到 `SimpleController` 类，添加一个名为 `SayHello` 的新 action 方法，它接受一个名为 `name` 的字符串参数。当请求发出时，ASP.NET 会将查询字符串上的参数与方法参数进行匹配。action 方法可以通过将其添加到内置的 `ViewData` 集合中，将参数值传递给视图。

```vb
' GET: /Simple/SayHello?name=Rob

Function SayHello(ByVal name As String) As ActionResult
    ViewData("Name") = name
    Return View()
End Function
```

*来自 `\Controllers\SimpleController.vb` 的代码片段*

通过在 `SayHello` 函数的代码中右键单击任意位置，在上下文菜单中选择 Add View，然后单击 Add 按钮来创建视图。在创建的内容页面中，修改 `<h2>` 元素的 value 以输出存储在 `ViewData` 中的 `name` 参数的值：

```aspx
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="server">
    <h2>Hello <%: ViewData("Name") %></h2>
</asp:Content>
```

注意使用了新的 `<%: %>` 语法。这与 `<%= %>` 相同，只是它会自动对输出进行 HTML 编码。这种新语法在 Web Forms 和 MVC 中都适用。

如果运行应用程序并导航到 `/Simple/SayHello?name=Rob`，你应该会看到与图 23-7 所示类似的页面。

## 添加模型

在 MVC 中，模型通常指的是业务或领域对象。这些是代表应用程序中数据的类，以及相应的业务规则和验证。对于我们的示例应用程序，我们将使用 LINQ to SQL 在 Northwind 数据库的数据之上创建一个简单的领域模型。
