
## 第 4 章：利用 .NET Framework

### 本章内容

- ✔ 使用 .NET Framework
- ✔ 处理请求
- ✔ 使用 ASP.NET 安全性
- ✔ 使用站点地图
- ✔ 管理文件和 Cookie
- ✔ 跟踪和调试

让我们明确 ASP.NET 和 .NET Framework 的区别。它们是不同的。ASP.NET 依赖于 .NET Framework，但它实际上被定义为第 3 章中的控件集合，外加其他控件。.NET Framework 带来了一组不同的工具。

ASP.NET 中的控件侧重于用户体验——它们关注用户查看应用程序的方式。Framework 中的工具侧重于传输——关注在客户端与服务器之间来回传递信息。如果你查看 System.Web 命名空间（这些组件大多存储于此），很快就会发现其中大多数类都以“Http.”开头。这是有原因的：HTTP 是传输协议。

这一点很重要，因为操纵客户端与服务器之间往返的信息，是在 Web 应用程序中做任何非常规操作的首要且最佳方式。每当控件、服务器或客户端的默认状态并不完全符合你的需要时，你首先应该求助的就是 System.Web 命名空间中的类。

ASP.NET 中的控件与 .NET Framework 中的控件有相当多的重叠，但每一组都各具特色。你应始终牢记哪些工具可供你使用，以及如何最好地使用它们。

## 浏览 Web 流

从核心上说，ASP.NET 关乎文本流的发送与接收。客户端发送请求，服务器发出 HTML。有时我们的应用程序是客户端，有时它是服务器。System.Web 命名空间中的类处理所有这些情况。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_711_0.png)

请注意，这些解决方案以及 System.Web 命名空间中的许多其他解决方案，并非只与 ASP.NET 网站相关。其他应用程序有时也可以利用 System.Web 提供的好处，因此请仔细考虑！

### 拦截请求

微软突然灵光一现，采用了合理的命名方式，决定把包含客户端请求所有数据的对象命名为“Request”。那个人后来被解雇了。

查看请求有几种不同方式，但我们这里关心的是当前请求，也就是上下文请求。幸运的是，这是 ASP.NET 空间中的默认请求。你可以用 ASP.NET“拦截”该请求。不过，我们先退一步。

### 挖掘请求数据

每当用户输入 URL 或单击按钮时，就会发出一个请求。请求由服务器处理，你可以通过当前上下文访问它们。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_711_1.png)

别被措辞迷惑：我说的“当前上下文”，只是 ASP.NET 在请求处理期间为你提供的对象集合。简而言之，这个类叫 HttpRequest，ASP.NET 会创建一个实例并称其为 Request。它是 HttpRequest 类的一个实例，也是 HttpContext.Request 属性。

为了创建一个环境来演示我的意思，请按以下步骤设置项目：

- 1. 创建一个新的 ASP.NET 项目。
- 我将其命名为 Chapter4。
- 2. 添加一个名为 Request.aspx 的页面。
- 3. 右键单击新的 Request.aspx 页面，并将其设为起始页。
- 4. 在设计器中将一个按钮控件拖到页面上。
- 5. 双击新按钮以获取 Click 事件处理程序。
- 6. 在新的 Button1_Click 方法中，添加一些代码来遍历 Request 对象。

```
protected void Button1_Click(object sender, EventArgs e)
{
    foreach (String requestInfo in Request.Form)
    {
        Debug.WriteLine(requestInfo);
    }
}
```

我们在这里所做的只是查看请求返回的上下文。实际上，这只是给调试器找个落脚点。

- 7. 右键单击 Debug 语句并解析 System.Diagnostics 引用。
- 8. 在 Page_Load 中，添加大致相同的代码，以便我们能看到原始请求与回发之间的差异。

注意这里检查了回发语句。

```
protected void Page_Load(object sender, EventArgs e)
{
    if (!(Page.IsPostBack))
    {
        foreach (String requestInfo in Request.Form)
        {
            Debug.WriteLine(requestInfo);
        }
    }
}
```

- 9. 在两个 foreach 语句旁边设置断点。
- 10. 按 <F5> 运行应用程序。

运行后，在 Web 应用程序出现之前，应用程序会在 Page_Load 方法中的 foreach 处中断。将鼠标悬停在其中的 Request 对象上，你会看到类似图 4-1 的内容。注意 ContentLength 为 0，HttpMethod 为 GET。这是针对页面的初始基于 URL 的请求。

现在按 <F10>，直到 Page_Load 事件结束，Visual Studio 将控制权交还给 Web 浏览器。注意 Debug.WriteLine 语句从未被调用。为什么？ContentLength 为 0。没有 Form。（有点像“根本没有勺子。”）内容是空的，因为这是初始请求。Form 集合为空。除了基本请求信息之外，什么都没有。

当浏览器恢复后，按下按钮。Visual Studio 会再次在 Button1_Click 方法中的另一个 foreach 语句处中断。再次将鼠标悬停在 Request 对象上。注意 Form 集合，如图 4-2 所示。其中有三个项：ASP.NET 添加的两个隐藏字段，以及我们添加的按钮 Button1。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_713_0.png)

图 4-1：
初始请求。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_713_1.png)

图 4-2：
表单请求。

这是第二种请求——POST。它是对表单的响应。这里可以找到大量有用的信息。

## 使用请求中的信息

请求是一个可以收集用户需求信息并加以使用的地方。尤其是在回发时（但不仅限于那时），有大量信息可供使用，包括以下内容：

- ♦ 请求的内容。请求的类型（ContentType）告诉我们它是包含数据还是只有文本。我可以了解它是 ISO 还是 Unicode（ContentEncoding）。我也知道请求的长度（ContentLength）。
- ♦ 请求本身的文本。例如，我可以获得 URL（Uri）以及前一个请求（UrlReferrer）的全部文本。如果我只想要查询字符串（问号后面的部分），可以通过 QueryString 获取。
- ♦ 用户是否已登录到域（IsAuthenticated），如果是，用户是谁（LogonUserIdentity）。
- ♦ 访问 Cookies 集合（Cookies）。

当你能够访问请求时，就可以就内容做出决策。如果你需要了解他们的登录信息，你已经有了。检查 Cookie——没问题。确认查询字符串。无论需要做什么。你把信息传到业务层，取回所需内容，组合新的控件页面，然后需要修改响应。这时就需要 HttpResponse 类。

## 更改发送给客户端的内容

ASP.NET 和 IIS 在为客户端浏览器设置标记方面做得很好。你甚至可以告诉 Visual Studio 你面向某个特定浏览器（比如在工作组环境中），它会调整发送给客户端的 HTML，使其更接近该浏览器所支持的 HTML 标准的具体实现。

有时你需要更改页面在客户端上的呈现方式。更常见的是，你需要更改页面的元数据传递给客户端的方式。HTML 页面包含的内容远不止你在屏幕上看到的值。HttpResponse 可帮助你管理哪些内容可见、哪些不可见。

## 将用户发送到其他地方

Response 对象最常见的用途之一，就是将用户完全发送到另一个地方。如果你查看请求标头，并（例如）意识到用户未登录 Windows 域账户（使用 HttpRequest.IsAuthenticated），就可以将用户重定向到登录屏幕：
