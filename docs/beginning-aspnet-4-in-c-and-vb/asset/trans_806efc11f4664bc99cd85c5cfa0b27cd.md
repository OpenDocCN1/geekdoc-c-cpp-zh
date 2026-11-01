

请注意，为你添加的方法均未实现。实现部分是你的职责，后续章节将展示如何完成这一工作。

## 添加索引操作

最简单的控制器方法是实现 `Index()` 方法。该方法只需根据一组项目返回一个视图。这需要在代码中引用模型，并编写代码来获取并返回视图，如下所示：

```
using PCSMVCMagicShop.Models;

namespace PCSMVCMagicShop.Controllers
{
    public class ProductsController : Controller
    {
        private MagicShopEntities entities = new MagicShopEntities();

        public ActionResult Index()
        {
            return View(entities.Products.ToList());
        }
        ...
    }
}
```

代码片段 PCSMVCMagicShop/Controllers/ProductsController.cs

这段代码所做的是指示 ASP.NET MVC 框架为一个 Product 项目集合（更具体地说，是一个 `IEnumerable<Product>` 实例）构建视图。为了使这能够正常工作，你必须创建一个合适的视图。

## 添加 Products 视图

幸运的是，添加视图并不像听起来那么棘手。实际上，ASP.NET MVC 包含一个向导，可以为你创建许多简单的视图。

要使用此向导，请右键单击返回视图的方法，然后从上下文菜单中选择“添加视图”，如图 42-10 所示。

这将弹出“添加视图”向导，你可以根据要添加的视图对其进行自定义。在这种情况下，你可以将视图名称保留为默认的 Index，但应为数据模型类类型选择强类型视图，并将视图内容更改为 List，如图 42-11 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1324_0.png)

![](img/d7d2ffa0a76feaab821930e95daace93_1324_1.png)

该向导会在 Views 文件夹中添加一个名为 Products 的新文件夹，以及一个名为 Index.aspx 的 Web 窗体。添加到视图中的代码如下所示：

```
<%@ Page Title="" Language="C#" MasterPageFile="~/Views/Shared/Site.Master"
Inherits="System.Web.Mvc.ViewPage<IEnumerable<PCSMVCMagicShop.Models.Product>>" %>

<asp:Content ID="Content1" ContentPlaceHolderID="TitleContent" runat="server">
    Index
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="server">
    <h2>
        Index</h2>
    <table>
        <tr>
            <th>
            </th>
            <th>
                ProductId
            </th>
            <th>
                Name
            </th>
            <th>
                Description
            </th>
            <th>
                Cost
            </th>
        </tr>
        <% foreach (var item in Model) { %>
        <tr>
            <td>
                <%= Html.ActionLink("Edit", "Edit", new { id=item.ProductId }) %>
                |
                <%= Html.ActionLink("Details", "Details", new { id=item.ProductId })%>
            </td>
            <td>
                <%= Html.Encode(item.ProductId) %>
            </td>
            <td>
                <%= Html.Encode(item.Name) %>
            </td>
            <td>
                <%= Html.Encode(item.Description) %>
            </td>
            <td>
                <%= Html.Encode(String.Format("{0:C}", item.Cost)) %>
            </td>
        </tr>
        <% } %>
    </table>
    <p>
        <%= Html.ActionLink("Create New", "Create") %>
    </p>
</asp:Content>
```

使用。例如，前一个代码片段中的第一个调用映射到 `HomeController` 控制器类中的 `Index()` 方法。

使用默认路由设置渲染时，这些 `ActionLink()` 调用会输出以下 HTML：

```
<div id="menucontainer">
<ul id="menu">
<li><a href="/">Home</a></li>
<li><a href="/Home/About">About</a></li>
</ul>
</div>
```

考虑到你对 URL 如何映射到控制器方法以及 Global.asax 中如何为路由设置默认值这些知识的了解，这完全合乎情理。而且它的好处是，你不必自己计算这些链接，也不需要在路由更改时重写它们。

要以相同方式添加指向产品列表页面的链接，请将以下代码添加到母版页中：

```
<div id="menucontainer">
<ul id="menu">
<li><%= Html.ActionLink("Home", "Index", "Home") %></li>
<li><%= Html.ActionLink("About", "About", "Home") %></li>
<li><%= Html.ActionLink("Products", "Index", "Products") %></li>
</ul>
</div>
```

*代码片段 PCSMVCMagicShop/Views/Shared/Site.Master*

`ActionLink()` 的各种重载使你能够执行其他操作，例如向控制器方法传递参数。例如，在你创建的产品列表视图中，编辑项目链接使用以下代码渲染：

```
<%= Html.ActionLink("Edit", "Edit", new { id=item.ProductId }) %>
```

*代码片段 PCSMVCMagicShop/Views/Products/Index.aspx*

此重载使用 linkText、actionName 和 routeValues 参数（控制器名称默认为当前控制器）。在这种情况下，使用了一个名为 id 的路由值，该值映射到 ProductsController 中 Edit 方法的 id 参数。此调用渲染的链接如以下示例 HTML 所示：

```
<a href="/Products/Edit/1">Edit</a>
```

## 使用 Details() 查看项目

当用户在应用程序中点击 Details 链接时，会请求 ProductsController 中的 `Details()` 操作方法。这会导致该方法以产品 ID 作为参数执行。你只需要定位所请求的产品，如果该产品存在，则返回一个新视图，如下所示：

```
public ActionResult Details(int id)
{
    var product = (from e in entities.Products
                    where e.ProductId == id
                    select e).FirstOrDefault();

    if (product != null)
    {
        return View(product);
    }
    else
    {
        return RedirectToAction("Index");
    }
}
```

如果未找到产品，则使用 `RedirectToAction()` 方法，该方法的作用正如其名称所示——将用户重定向到另一个视图，在本例中为 Index 视图。

要添加新视图，请右键单击 `Details()` 方法，并像之前一样单击“添加视图...”菜单项。这一次，为 Product 类创建一个强类型视图，视图内容为 Details，如图 42-13 所示。

现在运行应用程序时，你将能够通过上一节中添加的 Products 菜单项浏览到产品列表，并查看任何项目的详细信息，如图 42-14 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1330_0.png)

图 42-13

![](img/d7d2ffa0a76feaab821930e95daace93_1330_1.png)

图 42-14

如果你手动编辑 URL，使其指向一个不存在产品的 ID，你将被重定向到产品列表页面。

## 使用 Create() 添加项目

与创建新项目相关的操作有两个，目前它们在代码中定义如下：

```
public ActionResult Create()
{
    return View();
}
```

```
[AcceptVerbs(HttpVerbs.Post)]
public ActionResult Create(FormCollection collection)
{
    try
    {
        // TODO: 在此处添加插入逻辑

        return RedirectToAction("Index");
    }
    catch
    {
        return View();
    }
}
```

代码片段 PCSMVCMagicShop/Controllers/ProductsController.cs

第一个方法没有参数，只是重定向到创建视图，你可以像添加其他视图一样添加此视图（记住在“添加视图”向导中将视图内容值设置为 Create）。第二个方法用于实际在数据源中创建新项目，你需要自己实现它。

请注意，第二个 `Create()` 重载包含一个 `AcceptVerbs` 特性。这会将 HTTP 谓词限制为 POST，这是合理的，因为在创建项目时，你通常需要提交比 GET 请求的 URL 所能合理包含的更多信息。

为第一个 `Create()` 方法创建的视图包含以下自动生成的代码：

```
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="server">
<h2>
Create</h2>
<%= Html.ValidationSummary(
"Create was unsuccessful. Please correct the errors and try again.") %>
<%= Html.BeginForm() %>
({
<fieldset>
<legend>Fields</legend>
<p>
<label for="ProductId">
ProductId:</label>
<%= Html.TextBox("ProductId") %>
<%= Html.ValidationMessage("ProductId", "*") %>
</p>
<p>
<label for="Name">
Name:</label>
<%= Html.TextBox("Name") %>
<%= Html.ValidationMessage("Name", "*") %>
</p>
<p>
<label for="Description">
Description:</label>
<%= Html.TextBox("Description") %>
<%= Html.ValidationMessage("Description", "**") %>
</p>
<p>
<label for="Cost">
Cost:</label>
<%= Html.TextBox("Cost") %>
<%= Html.ValidationMessage("Cost", "*") %>
</p>
```

