

# 项目结构

当你创建 AcmeLibrary 项目时，Visual Studio 会生成几个文件夹和文件。你可以参考解决方案资源管理器（Solution Explorer）工具中的该结构，如图 18-7 所示。

从 Web 应用的角度来看，第一个重要的文件夹是 Content 文件夹。它包含了应用程序的级联样式表（CSS）文件。通常，Content 文件夹下的 Images 文件夹存放网页中使用的图像。你可以通过修改 Site.css 文件或将其更改为其他 CSS 文件（当然，还需要在相应的母页中替换对 Site.css 的引用）来更改网站的整体设计。

第二个重要的文件夹是 Scripts 文件夹。它包含了为你创建的项目提供的约 10 几个 JavaScript 文件。值得提到的是，你的项目内置了对 jQuery 客户端脚本的支持，并且可以在 HTML 表单中实现 jQuery 验证插件到模型的的验证，而无需与服务器进行额外的往返。

正如其名所示，另外三个文件夹（Controllers、Models 和 View）也与 MVC 模式相关。Controllers 文件夹包含了在项目中扮演控制器角色的类。图 18-7 显示 Visual Studio 创建了两个控制器，一个用于首页（HomeController.cs），另一个用于关于页面（AccountController.cs）。

![](img/b5597c749e848b27b0d305153ae16106_804_0.png)

图 18-7：解决方案结构

Views 文件夹是所有在 MVC 模式中扮演视图角类的容器。表示视图及其辅助类被分组在子文件夹中。Account 文件夹存放与登录和账户处理功能相关的视图；Home 封装了与关于页面和首页相关的视图（位于 Index.aspx 文件中，稍后会解释）。Shared 文件夹存放辅助页面和类型，例如 Error.aspx、LogOnUserControl.cs 和 Master.files。

> 当你查看 .aspx、.ascx 和 Master 文件时，你会发现它们与 ASP.NET Web 项目中具有相似扩展的文件不同，它们没有后代码文件。ASP.NET 项目中由后代码处理的许多功能（例如收集表单数据、验证和导航）在 ASP.NET MVC 中以完全不同的方式管理，不需要后代码文件。

Models 文件夹是用于定义 MVC 模式中模型类型的容器。首页和关于页面没有引用任何模型类——你甚至可以说它们使用一个没有任何属性或操作的空模型。该文件夹中的 AccountModel.cs 包含了处理函数的模型类。

Models、Controllers 和 Views 文件夹不仅仅是为了简单组织项目文件。它们还提供了特定角色的右键菜单。例如，当你右键点击 Controllers 文件夹时，在右键菜单的 Add 子菜单中，你可以看到“Controller...”命令，如图 18-8 所示。此命令允许你为网站添加新控制器。

同样，当你右键点击 Views 文件夹时，你会在 Add 子菜单下找到“View...”命令。你可以构建你的应用程序，但它将无法运行（或者至少不符合预期）。你还会丢失右键菜单中针对特定文件夹的命令。请保持文件夹名称不变。

Global.asax 和 Web.config 文件在 MVC 2 中的作用与传统的 ASP.NET 项目相同。

# 它是如何工作的？

当你使用 ASP.NET 创建应用程序时，归根结底请求被映射到 .aspx 文件（或 HTML 文件）。例如，当请求由 http://MySuperWebsite.com/KnowledgeBase/WindowsIssues.aspx URL 表示时，KnowledgeBase 文件夹下的 WindowsIssues .aspx 文件将被渲染以在浏览器中生成 HTML 输出。

MVC 框架的请求方式不同。让我们位于 Views 下 Shared 文件夹中的 Site.Master 文件。列表 18-5 显示了该文件（为了提高可读性，在 <div> 标签后插入了换行和一些注释）。

代码列表 18-5：Site.Master

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

代码文件 [Site.Master] 可在 Wrox.com 下载

虽然 ASP.NET Web 母页继承自派生 System.Web.UI.MasterPage 类型的类，但此页面（如你在此处 %@ Master 标签中所示）继承自派生 System.Web.MasterPage 的 System.Web.Mvc.ViewPage 类。母页的结构与 ASP.NET 非常相似。

```
<div id="container">
  <ul id="menu">
    <li>@Html.ActionLink("Home", "Index", "Home")</li>
    <li>@Html.ActionLink("About", "About", "Home")</li>
  </ul>
</div>
```

