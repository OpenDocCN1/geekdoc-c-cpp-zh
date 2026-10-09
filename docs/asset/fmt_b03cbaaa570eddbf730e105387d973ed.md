
```javascript
if (form.onsubmit || (form.onsubmit() != false)) {
  form.EVENTTARGET.value = eventTarget;
}
```
```
//]]>
```

继续

## 32 | 第 2 章 Web 的工作原理

## 列表 2-5（续）

```javascript
theForm.__EVENTARGUMENT.value = eventArgument;
theForm.submit();
}
//]]>
</script>
<div>
  <input type="hidden" name="__EVENTVALIDATION" id="__EVENTVALIDATION" value="wEWAgKwgo2ZwCzl9r7AbKfiEt1R2MFVeeJ0uFQNcv8cpj" />
</div>
<div>
  Request Type: <span id="requestType">GET</span> <br />
  <span>PostBack: <span id="cameFromPostBack">False</span> <br />
  <span><span id="message"></span> <br />
  <a id="button" href="javascript:__doPostBack('button', '')">Click me!</a>
</div>
</form>
```

### Post Parameters

```html
<body>
</html>
```

HTML 源代码包含了一些值得关注的点。当编写本章时创建此页面时，它被称为 `PostbackDemo.aspx`。页面中 HTML 表单的 `Action` 参数指向页面本身。你还会发现页面有四个 ASP.NET 服务器中不存在的表单字段：`__EVENTTARGET`、`__ARGUMENT`、`__EVENTVALIDATION` 和 `__VIEWSTATE`。还插入了一些 JavaScript，其中包含一个 `doPostBack()` 函数。最后，链接按钮被渲染为一个 `<a>` 元素，带有一个客户端事件，该事件调用插入的 `__doPostBack()` 函数，并传入按钮名称。

当你检查 `__doPostBack()` 函数时，你会发现在调用表单的 JavaScript `submit` 方法（这会导致浏览器提交）之前，其中两个隐藏字段 `__EVENTTARGET` 和 `__ARGUMENT` 会包含隐藏字段在内提交。

正是通过 JavaScript 设置事件源（以及任何参数）并将页面回传到自身（PostBack），使得 ASP.NET 实现了其事件模型。PostBack 的生命周期如下：

- 1. 你的页面首次加载（通常通过 GET 请求）。ASP.NET 创建 `Page` 对象及其内部的控件。触发 `Page` 事件，页面的 HTML 被渲染并返回给客户端。此时，`Page` 对象（及其所有内容）被释放，并最终在 .NET 垃圾回收器运行之前，它占用的内存将被释放。
- 2. 在客户端浏览器中，用户将执行创建 PostBack 的操作，例如点击链接、按钮或在列表框中选择一个选项。这些操作与客户端 JavaScript 事件关联，最终导致调用 `__doPostBack()`。页面和表单数据 [见第 60 页]
- 3. ASP.NET 创建 `Page` 对象及其内部的控件。触发 `Page` 事件，页面的 HTML 被渲染并返回给客户端。此时，`Page` 对象（及其所有内容）被释放，并最终在 .NET 垃圾回收器运行之前，它占用的内存将被释放。
- 4. 在客户端浏览器中，用户将执行创建 PostBack 的操作，例如点击链接、按钮或在列表框中选择一个选项。这些操作与客户端 JavaScript 事件关联，最终导致调用 `__doPostBack()`。页面和表单数据。
- 5. 最后，链接按钮被渲染为一个 `<a>` 元素，带有一个客户端事件，该事件调用插入的 `__doPostBack()` 函数，并传入按钮名称。

正是通过 JavaScript 设置事件源（以及任何参数）并将页面回传到自身（PostBack），使得 ASP.NET 实现了其事件模型。PostBack 的生命周期如下：

- 1. 你的页面首次加载（通常通过 GET 请求）。ASP.NET 创建 `Page` 对象及其内部的控件。触发 `Page` 事件，页面的 HTML 被渲染并返回给客户端。此时，`Page` 对象（及其所有内容）被释放，并最终在 .NET 垃圾回收器运行之前，它占用的内存将被释放。
- 2. 在客户端浏览器中，用户将执行创建 PostBack 的操作，例如点击链接、按钮或在列表框中选择一个选项。这些操作与客户端 JavaScript 事件关联，最终导致调用 `__doPostBack()`。页面和表单数据。
- 3. ASP.NET 创建 `Page` 对象及其内部的控件。触发 `Page` 事件，页面的 HTML 被渲染并返回给客户端。此时，`Page` 对象（及其所有内容）被释放，并最终在 .NET 垃圾回收器运行之前，它占用的内存将被释放。
- 4. 在客户端浏览器中，用户将执行创建 PostBack 的操作，例如点击链接、按钮或在列表框中选择一个选项。这些操作与客户端 JavaScript 事件关联，最终导致调用 `__doPostBack()`。页面和表单数据。
- 5. 最后，链接按钮被渲染为一个 `<a>` 元素，带有一个客户端事件，该事件调用插入的 `__doPostBack()` 函数，并传入按钮名称。

## 查看 AspNet 管道

现在你理解了 ASP.NET 如何创建页面，只剩一块拼图了：ASP.NET 如何知道请求是什么，以及使用什么代码来处理它？ASP.NET 工作在一个管道中。请求通过管道 HTTP Modules，这些模块可以重写 URL，甚至停止后续并返回错误。IIS6 和 IIS7 有不同的管道。ASP.NET 根据扩展名路由到处理程序。`.aspx` 文件路由到 `System.Web.PageHandler`。`.svc` 文件路由到 `System.ServiceModel.Activation.HttpHandler`，此类此类。IIS6 和 IIS7 有不同的管道。IIS6 只映射到 ASP.NET ISAPI 过滤器，而 IIS7 引入了集成管道，所有请求都通过 ASP.NET 管道并可以通过 HTTP Modules 进行检查。

处理器和模块在机器或 Web 站的 `web.config` 文件中注册。如果你检查 `C:\Microsoft\.NET\Framework\v2.0.50727\CONFIG` 目录下的 `web.config` 文件，可以看到 httpHandlers 和 modules 部分的默认处理器和模块。如果你在站点上，可以将其添加到 .NET 框架的 web.config。如果你想为单个站点注册，则将其添加到该站点的 `web.config` 文件。

编写 HTTP Handler 是罕见的情况，适用于你想创建如 .RSS 的自定义文件扩展名的情况。HTTP Handler 可以根据请求选择性响应 GET、POST 以及 HTTP 支持的任何其他动。

要注册 HTTP Handler，只需在 `web.config` 文件的 `httpHandlers` 部分添加元素，所示：

```
<httpHandlers>
  <add verb="supported http verbs" path="path"
       type="namespace.classname, assemblyname" />
</httpHandlers>
```

## HTTP Modules

每个 ASP.NET 请求都会通过每个注册的 HTTP Module。模块可以提供验证和校验功能。第 4 章详细介绍了如何创建一个防止被称为跨站请求伪造（CSRF）攻击的 HTTP Module。

## 尝试编写一个 HTTP 模块

在本练习中，你将编写一个简单的 HTTP 模块，为发送到 ASP.NET Web 页面的每个请求顶部添加一个时间戳。

HTTP 模块是实现 `IHttpModule` 接口的类。该接口有两个方法：`public Init(HttpApplication context)` 和 `public void Dispose()`。

- 1. 在 Visual Studio 中，通过“文件 -> 新项目”，并在“新建项目”对话框中选择“ASP.NET Web Application”创建一个新的 Web 。将项目命名为 SimpleHppModule。
- 2. 在解决方案管理器中右键点击项目，选择“添加 -> 类”。将你的新类命名为 `TimestampModule.cs`。用以下骨架实现替换默认类：

```cs
using System;
using System.Web;
namespace SimpleTimestampModule
{
    public class TimestampModule : IHttpModule
    {
        public void Dispose()
        {
        }
        public void Init(HttpApplication application)
        {
        }
    }
}
```

- 3. 在 `Init` 方法中，你可以通过 `context` 参数检查 `Request`，包括添加在请求开始和结束时触发的事件。因此，为模块添加一个事件，以便在请求向输出添加时间戳时触发。向类中添加该方法：

```cs
void OnEndRequest(object sender, EventArgs e)
{
    HttpContext.Current.Response.Write("<p> Served at " + DateTime.Now + "</p>");
}
```

- 4. 最后，你必须在模块的 `Init` 方法中编写事件，因此在 `Init` 方法中添加以下行：

```cs
public void Init(HttpApplication application)
{
    context.EndRequest += OnEndRequest;
}
```

- 5. 现在，你必须通过将添加到应用程序的 `web.config` 文件将模块连接到 ASP 中。编辑应用程序中的 `web.config`，并在 `httpModules` 部分添加以下行，给出模块条目名称，并通过列出完整类名和包含该类的程序集来指定类型：

```xml
<httpModules>
  <add name="TimestampModule" type="SimpleHttp.TimestampModule, SimpleHttpModule"/>
  // other modules
</httpModules>
```

- 6. 因为模块是编译项目时生成的程序集的一部分，通过选择“生成 B”来编译它；右键点击 `default.aspx` 并选择“在浏览器中查看”。你会发现模块已经在请求的底部添加了时间戳。

这种实现的一个问题是，它会影响通过 ASP.NET 发送的每一个请求，包括 JavaScript 请求、Web 服务以及不需要标记时间戳的请求。为了将时间戳限制在 ASP.NET 上，你可以检查处理请求的 ASP.NET HTTP Handler，并尝试创建 `System.Web.UI.Page` 实例。如果类型转换成功，你就知道它是一个 ASP.NET Web 页，可以安全地附加时间戳。实现以下的 `OnRequest` 方法：

```cs
void OnRequest(object sender, EventArgs args)
{
  if (HttpContext.Current.Handler != null)
  {
    System.Web.UI.Page page = HttpContext.Current.Handler as System.Web.UI.Page;
    if (page != null)
    {
      HttpContext.Current.Response.Write("<p> Served at " + DateTime.Now + "</p>");
    }
  }
}
```

现在时间戳只会应用于由 ASP.NET 页面处理器提供的页面。你现在已经编写了第一个 HTTP 模块。与其简单的时间戳，你还可以检查 IP 地址、带有查询参数的入站请求、各种请求检查和验证——并在它们访问你的页面类之前拦截它们。

你现在应该已经理解了 ASP.NET 管道以及如何编写简单的 HTTP 模块。如果你想了解更多关于编写 HTTP 模块和 HTTP 处理器的信息，Chris Lowe 编写了两篇 Wrox 博客文章，“利用 httpHandlers”和“利用 httpModules 改进 ASP”。

## 总结

本章旨在简单介绍 ASP.NET 管道以及如何编写简单的 HTTP 模块。在本章中，你学习了：

- HTTP 协议
- 请求和响应是如何构造的
- GET 和 POST 请求之间的区别
- 如何通过浏览器创建请求
- 如何 ASP.NET 触发事件
- 如何修改你的请求

# 第3章 安全地接收用户输入

ASP 提供的基本功能之一是接受用户输入。输入可以以各种形式呈现——来自表单、从数据库读取的数据（或从 Web 服务获取）、来自 Web 服务器本身的文件。在本章中，你将学习：

- 输入是危险的
- 如何安全地接收输入
- 如何在 Web 页面上输入
- ASP.NET 控制如何工作

## 定义输入

输入是指从外部进入程序的内容。这可以来自各种来源——包括用户提交的表单、来自 Web 服务的数据、浏览器的头部。所有数据类型都可以被应用程序处理并影响其输出。

在非常推荐的书《Writing Secure Code, Second Edition》（Redmond, Washington: Microsoft Press, 2003）中，作者 Michael Howard 和 David LeBlanc 简洁地指出问题：“除非证明，否则所有输入都是恶性的。”作为开发者，你的工作是判断进入的输入是否安全，或者使其安全或拒绝“恶性”输入。

# 安全地接收用户输入

判断输入是否安全的常用概念是“信任边界”，它可以被认为是应用程序中的边界或线条。在边界的一侧，数据是不可信的；在边界的另一侧，可以假设数据是安全的。验证逻辑负责允许数据从不可信侧安全移动到信任侧。图 1 显示了一个小系统及其信任边界。

![](img/742122f18debcb6f7bd43fe51fe45bd_67_0.png)

图 3-1：信任边界和验证位置

Howard 和 LeBlanc 指出，基本的原则是信任一切。正如你在第 2 章中发现的，伪造 HTML 请求很容易，这表明应用程序接收到的任何请求都可能来自用户或浏览器，也可能来自外部服务或从外部数据源加载的数据。对于其他输入源，它们位于信任边界内还是外部是一个判断。例如，`web.config` 通常位于信任边界内。然而，如果存在向 Web 服务器上传文件的能力（即使是无意的），那么存在 `web.config` 或其他文件被更改的风险。

## 安全地输出用户输入

跨站脚本 (XSS) 允许攻击者由于 Web 网站显示用户数据的方式更改漏洞 Web 网站上的页面。虽然这听起来可能没问题，但它可能导致许多不当用途，包括：

- 安装/利用浏览器插件——攻击者可以在页面中插入 `<object>` 标签，其中包含 ActiveX 、Flash、Java 或任何其他通过这种方式控制的插件，并利用插件的漏洞来窃取或暴露用户信息。

# 第 3 章 安全地接收用户输入

拒绝服务（DoS）攻击——攻击者可以在主要的网站上插入一个图像标签，加载其想要进行 DoS 攻击的网站最大的图像。由于受影响网站上有大量观众加载该用于 DoS 的图像，这可能会提供足够的带宽来将其切断。此外，由于图像是由无辜的代理加载的，很难追溯问题所在。

需要意识到的重要的一点是，XSS 攻击是在受攻击网站的上下文中运行的。例如，如果 www.example.com 受到 XSS 攻击，攻击者可以更改或在页面中插入文本。如果攻击者插入了 JavaScript 命令，它们看起来就像页面的合法部分，用户无法轻易区分攻击和任何合法脚本。

> 注意：XSS 是一个常见问题，Google 和微软并不受到此类攻击的影响。2008 年 4 月，Bill Rios 发现了一个 Google 电子表格的 XSS 漏洞，允许攻击者窃取所有用户的 cookie。（更多信息，请参见 http://xs-sniper.com/blog/2008/04/14-xss/）2006 年，一名 16 岁的荷兰学生 Adrian Gras 暴露了 Hotmail 的缺陷，该缺陷允许盗会会 cookie，并允许攻击者通过重新创建被盗 cookie 来劫持账户。更多信息，请参见 http://www.acunetix.com/news/hotmail.htm

## 尝试编写一个存在 XSS 漏洞的网页

此示例的目的是展示一个简单的网站如何变得受到 XSS 攻击。

- 1. 创建一个简单的 ASP.NET 网页：

```asp
@Page Language="C#" AutoEventWire="true"
CodeFile="Default.aspx" Inherits="_Default %>
<!DOCTYPE html>
<html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN//"
"http://www.w3.org/TR/DTD/html-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<html runat="server">
<head>
```
