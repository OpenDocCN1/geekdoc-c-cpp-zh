
RedirectPermanent 告诉客户端页面已永久移动。这在你想告诉搜索引擎停止查找旧页面，而改为索引新页面时很有用。例如，假设你的网站有一个名为 Index.aspx 的页面，你不再使用它。搜索引擎可能会继续请求此页面。如果你将以下代码添加到 Index.aspx 的代码后置中，客户端（包括搜索引擎）将被发送到 Default.aspx。此外，搜索引擎会记住重定向的永久性，并将停止请求 Index.aspx，而专注于 Default.aspx。

### VB.NET
```
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Response.RedirectPermanent("Default.aspx")
End Sub
```

### C#
```
protected void Page_Load(object sender, EventArgs e)
{
    Response.RedirectPermanent("Default.aspx");
}
```

这两个方法各有一个第二个版本（称为重载），它接受一个额外的布尔参数 endResponse，该参数使你能够在为该参数传递 False（C# 中为 false）时在重定向操作后执行任何剩余代码。这通常是不必要的，因此最好调用第一个版本，该版本默认结束响应。

经常，当你想将用户发送到另一个页面时，你想发送一些附加信息。你可以通过将其放在查询字符串中来做到这一点，查询字符串是地址中在页面名称之后的部分，以问号分隔。请考虑以下 URL：

```
http://localhost:49246/Demos/Target.aspx?CategoryId=10&From=Home
```

整个粗体部分（问号之后）被视为查询字符串。它由名称-值对组成，每个对之间由一个与号（&）分隔。在这种情况下，你有两个对：CategoryId 的值为 10，From 的值为单词 Home。页面（本例中为 Target.aspx）能够使用 Request.QueryString 读取这些值。你将在下一个练习中看到如何使用查询字符串。

## 试一试 将用户重定向到另一个页面

为了更详细地了解其工作原理，本练习展示了如何使用 Response.Redirect 创建一个从一个页面重定向到另一个页面的页面。示例使用临时重定向（重定向后初始页面仍然可访问），因此代码使用 Response.Redirect 而不是 Response.RedirectPermanent。

- 1. 在 Demos 文件夹中，基于你自定义的 MyBasePage 模板创建两个新的 Web 窗体。分别将它们命名为 Source.aspx 和 Target.aspx。分别将其 Title 设置为 Source 和 Target。
- 2. 在设计视图中打开 Source.aspx，并在页面 ContentPlaceHolder 外部的灰色只读区域的某处双击以设置 Page_Load 处理程序。在此处理程序内部，编写以下代码以将用户重定向到 Target.aspx 页面。为了向你展示如何通过查询字符串传递附加数据以及如何在目标页面中读取该信息，代码传递了一个名为 Test 的查询字符串字段，其值为 SomeValue：

VB.NET
```
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Response.Redirect("Target.aspx?Test=SomeValue")
End Sub
```

C#
```
protected void Page_Load(object sender, EventArgs e)
{
    Response.Redirect("Target.aspx?Test=SomeValue");
}
```

- 3. 打开 Target.aspx，切换到设计视图，并向 cpMainContent 内容控件添加一个 Label 控件。将其 ID 保持为 Label1。通过双击页面的灰色只读区域设置与上一步中创建的类似的 Page_Load 处理程序，然后添加以下代码：

VB.NET
```
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Label1.Text = Request.QueryString.ToString()
End Sub
```

C#
```
protected void Page_Load(object sender, EventArgs e)
{
    Label1.Text = Request.QueryString.ToString();
}
```

- 4. 保存所有更改，返回到 Source.aspx，然后按 Ctrl+F5 在浏览器中打开它。看不到 Source.aspx 了，你现在看到的是图 7-12 所示的页面。

![](img/eadab2ccd79b253c01a3fdff2321202d_323_0.png)

图 7-12

请注意，地址栏现在显示为 Target.aspx?Test=SomeValue，即你在源页面的 Page_Load 事件处理程序中重定向到的页面。目标页面中的 Label 显示传递给此页面的查询字符串。请注意，QueryString.ToString() 仅包含 Test=SomeValue。地址和问号不是页面查询字符串的一部分。

## 工作原理

与指示浏览器获取新页面不同，Server.Transfer 完全在服务器上进行。旧页面的输出被丢弃，并为被传输到的页面启动一个新的页面生命周期。然后该页面生成其内容并将其发送回浏览器，同时保持浏览器的地址栏不变。

如果在浏览器中查看发出的 HTML，你会看到表单 action 被设置为新页面，因此发生的任何回发都将针对该页面执行，这反过来会更改地址栏中的地址：

```
<form method="post" action="Target.aspx?Test=SomeValue" id="form1">
...
</form>
```

> 注 ASP.NET 支持一种称为路由的概念，它使你能够自由定义自己的 URL 结构并将其链接到站点中的页面。例如，你可以使用路由来实现本章中显示的汽车示例，而不会出现 action 属性更改的缺点。查看本文以了解有关路由的更多信息：http://tinyurl.com/RoutingWebForms.

通过以编程方式将用户发送到另一个页面的方法，你已经完成了本章关于导航的内容。通过本章中展示的概念，你拥有创建站点中高效导航系统所需的所有知识，既包括客户端浏览器，也包括你自己的服务器端代码。

## 导航实用技巧

以下列表提供了一些关于导航的实用技巧：

- 当你开始构建一个你认为未来会增长的网站时，立即创建一个逻辑结构。不要将所有文件都放在网站的根目录中，而应将逻辑相关的文件分组到同一文件夹中。这种逻辑分组使你更容易管理站点，并使你的用户更容易找到他们想要的页面。虽然使用 Web.sitemap 文件在 Menu 或 TreeView 中移动页面很容易，但如果你同时使用编程重定向或传输，则会更困难，因为你还需要更新服务器端代码以反映新的站点结构。要创建坚实的页面结构，你可以在开始站点之前将其画在纸上，或使用站点地图绘图工具，如 Microsoft Visio。
- 尽量限制在 Menu 或 TreeView 控件中显示的主项和子项数量。当用户面对长长的选项列表时，他们往往会迷路或感到困惑。
- 在创建用于存储页面的文件夹时，请为其提供简短且有逻辑的名称。使用 www.PlanetWrox.com/Reviews 导航到页面比导航到包含缩写和数字的长名称文件夹更直观。

## 摘要

本章使你熟悉了 ASP.NET 网站中的导航。用户不仅仅直接输入网页地址，因此提供清晰直接的导航系统很重要。

良好的导航系统的关键基础是对 URL 的工作原理有良好的理解。URL 有两种类型：相对 URL 和绝对 URL。相对 URL 用于指向你自己的站点内的资源。绝对 URL 使你能够通过其完整位置（包括协议和域信息）指向资源。绝对 URL 在你想要指向自己网站之外的资源时最有用。

ASP.NET 提供了三种在网站用户界面中使用的导航控件。这些控件使你的用户能够访问站点中的不同页面。Menu 控件显示为垂直或水平菜单，子菜单折叠或下拉。TreeView 控件可以以层次方式显示站点的完整结构。SiteMapPath 控件显示面包屑导航，为用户提供他们在站点中的位置的视觉提示。

除了内置的导航控件之外，你还可以以编程方式将用户发送到不同的页面。ASP.NET 支持两种主要方法来实现这一点：客户端使用 Response.Redirect 和 Response.RedirectPermanent，服务器端使用 Server.Transfer。重定向方法指示浏览器从服务器获取新页面，而传输方法在服务器上执行。

在下一章中，你将了解有关 ASP.NET 用户控件的更多信息，这些控件使你能够在网站的不同页面中重用特定的代码和用户界面元素。

## 练习

- 1. TreeView 控件公开了许多样式属性，使你能够更改树中的项。如果你想影响树中每个项的背景颜色，需要更改哪个属性？更改背景颜色的最佳方式是什么？
- 2. 你有哪些选项可以以编程方式将用户重定向到另一个页面？它们之间有什么区别？
- 3. 你可以用两种不同的方式使用 TreeView 控件：要么作为一个列表，其中包含可以通过单击折叠和展开的项和子项，要么作为一个静态列表，显示所有项，无法折叠或展开。你需要在控件上设置什么属性以防止用户展开或折叠树中的项？

你可以在附录 A 中找到这些练习的答案。
