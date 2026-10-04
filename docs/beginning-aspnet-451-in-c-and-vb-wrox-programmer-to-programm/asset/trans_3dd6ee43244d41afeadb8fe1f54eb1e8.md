

除了菜单（Menu）等视觉控件外，导航还关乎结构。一个组织良好的站点便于用户进行导航。导航控件使用的 Web.sitemap 文件有助于定义你网站的逻辑结构。

导航的另一个重要部分发生在服务器端。在后台代码（Code behind）中根据某些条件将用户从一个页面引导到另一个页面是非常常见的场景。例如，想象一个管理员在网站的 {（Management）部分输入了一张新的 CD 或音乐会会目。当审核完成后，你可能希望通过将她重定向到新页面向管理员显示完整详情。

在本章中，你将学习如何使用网站的导航选项。不过，在查看内置导航控件之前，你首先需要了解处理网站中资源（如 ASPX 页面和图像）的各种选项。

## 在你的站点中移动的各种方式

将用户从一个页面移动到另一个页面的最方法是使用 `<a>` 元素。该元素有一个 `href` 属性，允许你定义想要链接的页面或其他资源的地址。在标签之间，你可以放置想要链接的内容，例如文本、图像或其他 HTML。接下来的代码片段显示了 `<a>` 元素的一个简单示例：

```html
<a href="Login.aspx">You can log in here</a>
```

在网页中使用此代码后，用户点击“You can log in here”，他们将被带到 Login.aspx 页面，该页面应与包含链接的页面位于同一个文件夹中。

`<a>` 元素是一个名为 HyperLink 的服务器端控件。它最终在页面中呈现为 `<a>` 元素。该控件的 `NavigateUrl` 属性直接映射 `<a>` 元素的 `href` 属性。例如，内容页面中的服务器端 HyperLink 看起来如下：

```asp
<asp:HyperLink id="LoginLink" runat="server" NavigateUrl="Login.aspx">
You can log in here;
</asp:HyperLink>
```

除了 ASP.NET 运行时分配的 `id` 之外，此代码与之前的示例完全相同。在两种情况下，`href` 属性都使用相对 URL 指向 Login.aspx 页面。下一个主题将描述相对 URL 和绝对 URL 之间的区别。

```html
<a id="LoginLink" href="Login.aspx">You can log in here</a>
```

## 理解绝对 URL 和相对 URL

在站点中处理链接的关键在于良好理解网站内部或外部的统一资源定位符（URL）可以包含什么。URL 用于唯一标识你的网站或另一个网站中的资源。这些 URL 使用在不同的地方，包括超链接的 `href` 属性或指向 CSS 文件的 `<link>` 元素、指向图像或 JavaScript 源文件的 `src` 属性，以及 CSS 属性的 `url()` 值。URL 可以表示为相对 URL 或绝对 URL。这两者都具有你应该注意的优点和缺点。

## 相对 URL

在之前的示例中，你看到了一个相对 URL，它指向相对于 URL 使用位置的另一个资源（注：此处原文意如此）。这意味着包含 `<a>` 元素的页面和 Login.aspx 页面都应该放置在你站点中的同一个文件夹中。要引用其他文件夹中的资源，可以使用以下 URL。所有的示例都基于图 7-1 所示的站点结构。

从根目录下的 Login.aspx 链接到 Management 文件夹下的 Default.aspx，可以使用此 URL：

```html
<a href="/Management/Default.aspx">Management</a>
```

从 Management 文件夹下的 Default.aspx 引用 Header.jpg，可以使用此 URL：

```html
<img src="../Images/Header.jpg" />
```

前面的点 ".." 向上导航一个文件夹到根目录，然后对于站点层次结构中你想要返回的每个文件夹，就像 `<img>` 元素一样。

对于更深层次结构，你可以使用多个点，就像 `<img>` 元素一样。你可以用它引用来自 Reviews 文件夹的图像，该文件夹位于 Management 文件夹下：

```html
<img src="../Images/Header.jpg" />
```

相对 URL 的优点是，你可以文件移动到相同层级的另一个目录，而不会破坏内部链接。然而，同时这使得将文件移动到站点层次结构中的不同级别变得困难。如果你将 Login.aspx 页面移动到像 Members这样的单独文件夹，指向 Management 文件夹的链接将会失效。New Members 文件夹没有 Management 作为其子文件夹，因此 Management/Default.aspx 不再是有效的链接。

为了解决这个问题，你可以使用基于根的 URL。

## 基于根的相对 URL

基于根的相对 URL 始终以斜杠 `/` 开头，表示网站的根。如果你取指向 Management 文件夹的链接，其基于根的版本如下：

```html
<a href="/Management/Default.aspx">Management</a>
```

注意 Management 前面的斜杠，它表示网站的根。此链接是不歧义的。它始终指向根目录下 Management 文件夹中的 Default.aspx 文件。有了此链接，将 Login.aspx 页面移动到子文件夹不会破坏它；它仍然指向完全相同的文件。

## 服务器端控件中的相对 URL

使用 ASP.NET 服务器端控件，你还有另一个可用选项来引用网站中的资源：你可以使用波浪号 `~` 字符指向网站的当前根。当你将网站作为主网站下的一个独立应用程序文件夹运行时，这尤其为有用。

![](img/9e033e3b9560597824f8b22941d6d8bb_278_0.png)

例如，如果你的站点运行在 www.PlanetWrox.com/Site 而不是 www.PlanetWrox.com，情况就是如此。要了解这意味着什么，请考虑这张在 ImageUrl 中使用波浪号的图像：

```asp
<asp:Image ID="Image" runat="server" ImageUrl="~/Images/Header.jpg" />
```

当你使用名为 Site 的应用程序文件夹时，将在 /Site/Images/Header.jpg 处搜索图像。如果你重新配置站点在不带应用程序文件夹的情况下运行，则将在 /Images/Header.jpg 查找图像，而无需更改任何代码。

你也可以在 HTML 元素上使用 `~` 语法，只要你添加了 `runat` 属性。这样，路径就会服务器端处理并返回给客户端。下面的示例显示了一个链接到 Management 文件夹中页面的纯 HTML 链接：

```html
<a href="~/Management/Default.aspx" runat="server">Management</a>
```

作为 VS 服务的 Web 服务器，IIS Express 总是从根目录启动新站点。因此，基于根的 URL 将按预期工作。

## 绝对 URL

与指向资源或站点根的相对 URL 相，你也可以使用通过完整路径引用资源的绝对 URL。与其直接引用指定文件夹的图像，你包含了完整的域名名称和协议信息（`//` 前缀）。这里有一个引用 Wrox 程序员站点（http://p2p.wrox.com）中 Wrox 标志的示例，你可以那里获取关于 Wrox 和其他书籍的问题或关于编程的通用问题：

```html
<img src="http://p2p.wrox.com/images/header/wrox_logo.gif" />
```

如果你想引用你网站之外的资源，则必须使用绝对 URL。对于此类 URL，`//` 前缀是强制性的。如果你漏掉它，浏览器将在你自己的网站内部查找名为 p2p.wrox.com 的文件夹。

绝对 URL 是不歧义的。它们指向固定位置，这有助于确保无论源文档位于何处，获取的都是相同的资源。你可能认为它们对于所有地方（包括对网站内部资源的引用）都是理想的，但事实并非如此。协议和域名信息影响浏览器中页面的大小，使其下载速度变得异常缓慢。更重要的是，当你更改域名时这会产生困难。例如，如果你的站点运行在 www.myapplication.com，而你现在正移动到 www.anotherdomain.com，你需要更新整个网站中所有的绝对 URL。

