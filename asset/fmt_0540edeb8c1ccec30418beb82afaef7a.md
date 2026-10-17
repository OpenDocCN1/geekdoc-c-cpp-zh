
```html
<html xmlns="http://www.w3.org/1999/xhtml">
  <head runat="server">
    <title>Untitled Page</title>
  </head>
  <body>
    <form id="form">
      <div>
        <a href="friendlylink.aspx">Click this friendly link</a>
      </div>
    </form>
  </body>
</html>
```

如你所见，你只是创建了一个链接到友好且易记的 URL 的超链接。现在，创建第二个页面 `friendly.aspx`。当用户点击 `friendlylink.aspx` 页面中的超链接时，处理程序实际执行该页面。列表 27-5 显示了如何创建 `unfriendly.aspx`。

### 列表 27-5：unfriendly.aspx Web 页面

```vb
<%@ Page Language="VB" %>

<script runat="server">
  Protected Sub Page_Load(ByVal sender As Object,
  ByVal args As EventArgs) Handles Me.Load
    Label.Text = Request("firstName").ToString() & _
    " " & Request("lastName").ToString()
  End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
  <head runat="server">
    <title>Friendly Web Page</title>
  </head>
```

## 第 27 章：模块与处理程序

```cs
//重写请求路径
_application.Context.RewritePath("~/friendly.aspx?firstname=" +
  firstname + "&lastname=" + lastname);

}
}
```

如列表所示，在此示例中，你在 `HttpModule` 中解析传入的 HTTP 请求时使用了 `BeginEvent`，并创建了一个要执行的新 URL。通常情况下，当你点击超链接 `friendlyurl.aspx` 时，会向服务器发送 HTTP 请求进行执行，然后 IIS 返回超链接中请求的页面。在这种情况下，你可能会为该页面创建一个请求：

```
http://localhost:1234/WebProject1/John/Smith/trickiis.aspx
```

但是，由于你在请求处理流水线中使用了 `HttpModule`，你可以修改 HTTP 请求并更改其行为。模块的 `BeginRequest` 方法中的代码请求使用 `friendly.aspx` 页面解析查询字符串并理解和执行。因此，当你执行列表中的代码时，你将原始路径转换为以下内容：

```
http://localhost:1234/WebProject1/friendly.aspx?var=John&var2=Smith
```

此 URL 正如页面名称所示，并不“友善”（friendly）；而且用户不太可能记住并输入此 URL。最后，模块使用 `RewritePath` 方法告诉 ASP.NET 你可以重写用于此请求的执行执行路径。

在你完成此示例的代码创建后，尝试在浏览器中加载 `friendlylink.aspx`。当你点击页面上的超链接时，你应该注意到两点。首先，注意浏览器地址栏中的 URL 显示你已获取了所请求的页面 `trickiis.aspx`，但页面的内容显示实际上提供的是 `friendly.aspx`。

图 27-4 显示了浏览器的外观。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1330_0.png)

图 27-4

## IIS 通配符

然而，这种类型的 URL 重写有一个缺点。当 IIS 接收到提供资源的请求时，它会首先检查资源是否存在。如果资源不存在，则会将请求传递给相应的处理程序；在这种情况下，处理程序是 ASP.NET，由它处理请求。IIS 然后将结果返回给客户端。然而，如果请求的资源不存在，IIS 会向客户端返回 404 File Not Found 错误。然后它会将请求交给 ASP.NET。为了让某个方法执行，你必须在 Web 服务器上创建一个实际存在的端点。

在在上一个示例中，你必须创建 `/WebProject1/John/Smith/trickiis.aspx` 路径，以便 IIS 知道将请求交给哪个处理程序。由于没有创建该路径，IIS 仅返回了 404 错误。遗憾的是，如果你为了启用 URL 重写而创建大量的目录或资源，这将变成一个问题。但是，IIS 中存在解决此问题的方案：通配符（Wildcards）允许你告诉 IIS 它应该处理所有传入的请求，无论请求的路径或文件扩展名是什么。在上示例中，添加通配符可以让你无需为模块实际创建一个条目。

## 在 IIS 5 中添加通配符

要在 IIS 5 中添加通配符，首先打开 IIS 管理控制台。控制台打开后，右键点击网站或虚拟目录进行修改，并从上下文菜单中选择“属性”选项。打开属性对话框后，从“主目录”选项卡中选择“配置”按钮。配置对话框是你可以创建或修改现有应用程序扩展名映射的地方。如果你花时间查看现有的映射，你会发现大多数文件扩展名（如 `.asp`、`.asm` 和 `.html`）都已配置。

要添加创建新映射所需的通配符，请点击图 27-5 所示的“添加应用程序扩展名映射”对话框。你创建的映射将引导 IIS 使用 ASP.NET ISAPI DLL 来处理每个传入的请求。执行此操作，只需将 ISAPI DLL 的路径（通常为 `C:\Windows\.NETFramework\v1.1.4322\aspnet_isapi.dll`）放入“可执行”字段中，直接使用 `*`，它表示任何文件扩展名。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1331_0.png)

图 27-5

www-it-ebooks.info

此外，取消勾选“检查文件”（Check That File Ex）以告诉 IIS 在处理之前不要检查请求的文件是否存在（因为你知道它不存在）。

现在，你不需要为你的 网站添加存根文件了。IIS 将把收到的任何请求传递给 ASP.NET 处理，无论该文件是否存在。

## 在 IIS 6 中添加通配符

在 IIS 6 中添加通配符与在 IIS 5 中添加类似。打开 IIS 管理控制台，选择要修改的网站或虚拟目录，然后从主目录选项卡中选择配置按钮。IIS 的配置对话框略有不同。通配符应用程序映射现在有独立的列表，如图 27-6 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1332_0.png)

图 27-6

要添加通配符，点击“插入”按钮，添加 ISAPI DLL 的路径并确保“验证文件”框未勾选。

## HttpHandlers

## 第 27 章：模块与处理程序

在本节中，我们演示了创建简单 HttpHandler 的两种方法。首先，我们使用 ASHX 文件创建 HttpHandler。然后你将学习如何通过将 HttpHandler 映射到自定义扩展名来获得更多控制。

## 通用处理程序

在早期版本的 Visual Studio 中，HttpHandlers 很难理解和创建，因为没有足够的文档帮助。然而，从 Visual Studio 2005 开始，情况发生了变化，Visual Studio 为 HttpHandlers 提供了一个标准模板。要在你的项目中添加通用处理程序，只需选择“Handler”文件类型。图 27-7 显示了此对话框。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1333_0.png)

图 27-7

我们可以看到，当你向项目中添加通用处理程序时，它会添加一个 `.ashx` 扩展的文件。该扩展名是 ASP.NET 默认的。这非常方便，否则你将负责添加扩展名。这显然是不可能的，但它是实用的。使用自定义处理器文件类型可以避免额外的配置。

注意文件类型自动为你创建的类存根。列表 27-7 显示了类。

## 列表 27-7：HttpHandler 模板

```vb
<@ WebHandler Language="VB" Class="Handler" %>

Imports System.Web

Public Class Handler
    Implements IRequestHandler

    Public Sub ProcessRequest(ByVal context As HttpContext)
        Implements IRequestHandler.ProcessRequest
        context.Response.ContentType = "text/plain"
        context.Response.Write("Hello World")
    End Sub

    Public ReadOnly Property IsReusable() As Boolean
        Implements IRequestHandler.IsReusable
        Get
            Return False
        End Get
    End Property
End Class
```

```cssharp
<@ WebHandler Language="C#" Class="Handler" %>

using System.Web;

public class Handler : IRequestHandler {

    public void ProcessRequest(HttpContext context) {
        context.Response.ContentType = "text/plain";
        context.Response.Write("Hello World");
    }

    public bool IsReusable {
        get {
            return false;
        }
    }
}
```

注意存根实现了 `IRequestHandler` 接口，该接口要求 `ProcessRequest` 方法和 `IsReusable` 属性。`ProcessRequest` 方法是我们用于实际处理传入的 HTTP 请求的方法。默认情况下，类存根将内容类型更改为纯文本并写入

# 第 27 章：模块与处理器

将“Hello World”字符串输出到输出流。`IsReusable` 属性只需让 ASP.NET 知道传入的 HTTP 请求是否可以重用此 HttpHandler 的示例实例。

默认情况下，此处理器已准备好立即运行。在浏览器中执行此处理器会发生什么。关于此处理器需要注意的一点是，它将内容更改为 `text/plain`，浏览器根据许多因素以完全不同的方式处理来自此处理器的响应：

- 浏览器类型和版本

- 系统加载的可能映射到 MIME 类型的应用程序

- 操作系统和服务程序包级别

根据这些因素，你可能会在浏览器中看到返回的文本，可能会看到记事本打开并显示文本，或者可能会收到 IE 的打开/保存/取消提示。请确保你理解更改 `ContentType` 头的潜在后果。

你可以通过修改示例以返回实际文件来继续该示例。在这种情况下，你使用处理器来返回一个图像。要实现这一点，你只需修改 `ProcessRequest` 方法中的代码，如列表 27-8 所示。

# 列表 27-8：从 HttpHandler 输出图像

```vb
<@ WebHandler Language="VB" Class="Handler" %>
Imports System.Web
Public Class Handler : Implements IHttpHandler
    Public Sub ProcessRequest(ByVal context As HttpContext) -  
        Implements IHttpHandler.ProcessRequest
        '获取图像文件的逻辑
        context.Response.ContentType = "image/jpeg"
        context.Response.WriteFile("Garden.jpg")
    End Sub
    Public ReadOnly Property IsReusable() As Boolean -  
        Implements IHttpHandler.IsReusable
        Get
            Return False
        End Get
    End Property
End Class
```

```csharp
<@ WebHandler Language="C#" Class="Handler" %>

using System.Web;
public class Handler : IHttpHandler {

    public void ProcessRequest(HttpContext context) {
    //获取图像文件的逻辑
        context.Response.ContentType = "image/jpeg";
        context.Response.WriteFile("Garden.jpg");
    }

    public bool IsReusable {
        get {
            return false;
        }
    }
}
```

如你所示，你只需将 `ContentType` 更改为 `image/jpeg` 以表示你正在返回一个 JPEG 图像；然后你使用 `WriteFile()` 方法将图像文件写入输出流。将处理器加载到浏览器中，你将看到处理器显示图像。图 27-8 显示了生成的 Web 页面。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1336_0.png)

图 27-8

现在，你创建一个简单的 Web 页面来显示图像处理器。列表 27-9 显示了 Web 页的代码。

# 列表 27-9：使用 HttpHandler 作为图像源的示例 Web 页面

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>HttpHandler 提供图像</title>
  </head>
  <body>
    <form id="form" runat="server">
      <div>
        <img src="Handler.ashx" />
      </div>
    </form>
  </body>
</html>
```

尽管这很简单，但你仍然通过向处理器传递查询字符串（querystring）参数并使用它们在内核中执行附加逻辑来增强它。例如，你可以传递一个 ID 来从 SQL 数据库中动态检索图像并将其返回给客户端，如下：

```html
<img src="Handler.ashx?imageId=123" />
```

# 在 IIS 中映射文件扩展名

尽管 `.ashx` 文件扩展名很方便，但你可能想为自定义文件扩展名或常用扩展名创建一个 HTTP 处理器。使用图像处理器的代码来演示这一点。

在项目的 `App_Code` 目录中创建一个新类。你可以简单地将现有图像处理器的代码复制到此类中，如列表 27-10 所示。注意，你删除了 `WebHandler` 指令，因为这只是一个类，而不是通用的处理器控制器。除外，代码是相同的。

# 列表 27-10：基于类的图像 HttpHandler

```vb
Imports System.Web

Public Class MapHandler : Implements IHttpHandler

    Public Sub ProcessRequest(ByVal context As HttpContext) - 
        Implements HttpHandler.ProcessRequest
        context.Response.ContentType = "image/jpeg"
        context.Response.WriteFile("Garden.jpg")
    End Sub

    Public ReadOnly Property IsReusable() As Boolean - 
        Implements HttpHandler.IsReusable
        Get
            Return False
        End Get
    End Property
```
