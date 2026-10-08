

## 第 4 章：利用 .NET Framework

本章内容

- 使用 .NET Framework
- 处理请求
- 使用 ASP.NET 安全
- 使用站点地图
- 管理文件和 Cookie
- 跟踪与调试

让我们明确一下 ASP.NET 和 .NET Framework 的区别。它们是不同的。ASP.NET 依赖于 .NET Framework，但它实际上被定义为第 3 章中控件的集合以及其他内容。.NET Framework 提供了另一套工具。

ASP.NET 中的控件是侧重于**用户体验**的——它们关注用户查看应用程序的方式。而 Framework 中的工具是侧重于**传输**的——关注在客户端和服务器之间传递信息。如果你查看 `System.Web` 命名空间（大部分这些代码存储在这里），你会很快发现大多数类都以 "Http" 开头。这是有原因的：HTTP 是传输协议。

这一点非常重要，因为处理客户端和服务器之间往来的信息是在 Web 应用程序中进行任何自定义操作的首选方法。每当控件或服务器的默认状态不符合你的要求时，你首先应该寻找 `System.Web` 命名空间中的类。

ASP.NET 中的控件和 .NET Framework 中的控件有很大重叠，但每组都是是独立的。你应该始终记住自己手头有哪些工具以及如何最好地使用它们。

## 浏览 Web 流

ASP.NET 的核心是文本流的发送和接收。客户端发送请求，服务器发送 HTML。有时我们的应用程序是客户端，有时又是服务器。`System.Web` 命名空间中的类处理了所有这些情况。

注意，这些解决方案以及 `System.Web` 命名空间中的许多其他方案并不限于 ASP.NET 网站。其他应用程序也可以利用 `System.Web` 提供的优势，因此请慎重考虑！

## 拦截请求

在一次突然的合理命名中，微软决定将包含客户端请求所有数据的对象命名为：“Request”。那个命名的人已经被解雇了。

查看请求有几种不同的方式，但我们关注的是当前请求，或者说上下文请求。幸运的是，这是 ASP.NET 空间中的默认请求。你可以用 ASP.NET “拦截”该请求。但让我们先退一步。

## 挖掘请求数据

每当用户输入 URL 或点击按钮时，就会发出一个请求。请求由服务器处理，你可以通过当前上下文访问它们。

不要被语言误导了：我所说的“当前上下文”是指 ASP.NET 在处理请求时提供给你的那个对象。简而言之，该类名为 `HttpRequest`，ASP.NET 创建一个实例并将其命名为 `Request`。它是 `HttpRequest` 类的一个实例，是 `HttpRequest.Request` 属性。

为了创建一个环境来展示我的意思，请按照以下步骤设置项目：

1. 创建一个新的 ASP.NET 项目。
2. 添加一个名为 `Request.aspx` 的页面。
3. 右键点击新的 `Request.aspx` 页面并将其设置为启动页。
4. 在设计器中向页面拖入一个按钮控件。
5. 双击新按钮获取 `Click` 事件处理程序。
6. 在新的 `Button1_Click` 方法中添加一些代码来遍历 `Request` 对象。

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    foreach (String requestInfo in Request.Form)
    {
        Debug.WriteLine(requestInfo);
    }
}
```

我们在这里做的只是查看请求返回的上下文。实际上，这只是我们用来放置调试器的一个位置。

7. 右键点击 `Debug` 语句并解析 `System.Diagnostics` 引用。
8. 在 `Page_Load` 中大致添加以下代码，以便我们看到原始请求和回传（postback）之间的区别。

注意检查回传的语句。

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (Page.IsPostBack)
    {
        foreach (String requestInfo in Request.Form)
        {
            Debug.WriteLine(requestInfo);
        }
    }
}
```

9. 在两个 `foreach` 语句旁边设置断点。
10. 按下 <F5> 运行应用程序。

当你运行时，Web 应用程序出现，程序会断在 `Page_Load` 方法中的 `foreach` 处。再次将鼠标悬停在 `Request` 对象上，你将看到类似于图 4-1 的内容。注意 `ContentLength` 为 0 且 `HttpMethod` 为 GET。这是对页面的初始 URL 请求。

现在按 F10 直到 `Page_Load` 事件将控制权交回 Web 浏览器。注意 `Debug.WriteLine` 从未被调用。为什么？`ContentLength` 为 0。没有表单（就像“没有勺子”）。内容是空的，因为这是一个初始请求。`Form` 集合是空的。除了基础请求信息外空无所有。

当浏览器返回时点击按钮。Visual Studio 再次断在 `Button1_Click` 方法中的另一个 `foreach` 语句处。再次将鼠标悬停在 `Request` 对象上。注意图 4-2 所示的 `Form` 集合。其中有三个项：ASP.NET 添加的两个隐藏字段以及我们添加的按钮 `Button1`。

图 4-1: [图像链接]
图 4-2: [图像链接]

