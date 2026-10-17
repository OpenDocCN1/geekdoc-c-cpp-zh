
Google Chrome 47.0 版本会显示这些信息，包括来自 AppleWebKit、Chrome 和 Safari 的版本号：

```
Connection: keep-alive
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*
Accept-Encoding: gzip, deflate, sdch
Accept-Language: en-US;en;q=0.8
Host: localhost:5000
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome 47.0.2526.80 Safari/537.36
```

而 Microsoft Edge 会显示这些信息，包括来自 AppleWebKit、Chrome、Safari 和 Edge 的版本号：

```
Connection: Keep-Alive
Accept: text/html,application/xhtml+xml,image/jxr,*/*
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.8,de-AT;q=0.6,de-DE;q=0.4,de;q=0.2
Host: localhost:5000
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML,
```

您可以从这些请求头信息中得到什么？

`Connection` 请求头是 HTTP 1.1 协议的一项增强。通过该请求头，客户端可以请求保持连接打开。通常对于 HTML，客户端会发出多个请求，例如获取图片、CSS 和 JavaScript 文件。服务器可能会满足该请求，也可能忽略该请求，以防负载过高而更适合关闭连接。

`Accept` 请求头定义了浏览器接收的 MIME 格式。列表按首选格式排序。根据这些信息，您可以根据客户端的需求返回不同格式的数据。IE 首选 HTML，其次是 XHTML 和 JXR。Google Chrome 则有不同的列表。它首选以下格式：HTML、XHTML、XML 和 WEBP。其中一些信息中还定义了量化符。用于输出结果的浏览器都在此列表末尾带有 */*，以接受返回的所有数据。

`Accept-Language` 请求头信息显示用户已配置的语言。利用这些信息，您可以返回本地化信息。本地化将在第 28 章“本地化”中讨论。

> **注意** 在早期，服务器维护着包含大量浏览器特性的列表。这些列表曾被用来了解哪个浏览器支持哪些功能。为了识别浏览器，会使用浏览器的代理字符串来映射这些特性。随着时间推移，浏览器会通过提供错误信息来撒谎，甚至允许用户配置应使用的浏览器名称，从而获得更多功能（因为服务器上的浏览器列表常常不会更新）。在过去，Internet Explorer（IE）通常需要与其他所有浏览器不同的编程方式。Microsoft Edge 与 IE 有很大不同，并且与其他厂商的浏览器有更多共同的特性。这就是为什么 Microsoft Edge 在 `User-Agent` 字符串中显示 Mozilla、AppleWebKit、Chrome、Safari 和 Edge 的原因。最好不要使用这个 `User-Agent` 字符串来获取可用功能列表。相反，应以编程方式检查您需要的特定功能。

到目前为止您看到的由浏览器发送的请求头信息只是非常简单的网站所发送的信息。通常，会有更多细节，例如 cookie、身份验证信息以及自定义信息。要查看与服务器之间发送和接收的所有信息（包括请求头信息），您可以使用浏览器的开发者工具并启动 Network 会话；您不仅会看到发送到服务器的所有请求，还会看到请求头、正文、参数、cookie 和计时信息，如图 40.11 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1545_0.png)

#### 图 40.11

### 查询字符串

您可以使用 `Add` 方法来分析查询字符串。该方法需要 `x` 和 `y` 参数，如果这些参数是数字，则进行加法运算，并在 div 标签中返回计算结果。上一节中展示的 `GetRequestInformation` 方法演示了如何使用 `HttpRequest` 对象的 `QueryString` 属性访问完整的查询字符串。要访问查询字符串的各个部分，您可以使用 `Query` 属性。以下代码片段使用 `Get` 方法访问 `x` 和 `y` 的值。如果在查询字符串中找不到对应的键，此方法返回 null（代码文件 `WebSampleApp/RequestAndResponseSample.cs`）：

```
public static string QueryString(HttpRequest request)
{
    var sb = new StringBuilder();
    string xtext = request.Query["x"];
    string ytext = request.Query["y"];
    if (xtext == null && ytext == null)
    {
        return "x and y must be set";
    }
    int x, y;
    if (!int.TryParse(xtext, out x))
    {
        return $"Error parsing {xtext}";
    }
    if (!int.TryParse(ytext, out y))
    {
        return $"Error parsing {ytext}";
    }
    return $"{x} + {y} = {x + y}".Div();
}
```

从 `Query` 字符串返回的 `IQueryCollection` 还允许您使用 `Keys` 属性访问所有键，并且它提供了 `ContainsKey` 方法来检查指定键是否可用。

使用 URL `http://localhost:5000/add?x=39&y=3` 会在浏览器中显示以下结果：

```
39 + 3 = 42
```

### 编码

返回用户输入的数据可能是危险的。让我们使用 `Content` 方法来演示。以下方法直接返回通过查询 `data` 字符串传递的数据（代码文件 `WebSampleApp/RequestAndResponseSample.cs`）：

```
public static string Content(HttpRequest request) =>
    request.Query["data"];
```

使用 URL `http://localhost:5000/content?data=sample` 调用此方法时，仅返回字符串 sample。使用同样的方法，用户还可以传递 HTML 内容，例如 `http://localhost:5000/content?data=<h1>Heading 1</h1>`。结果如何？图 40.12 显示了 `h1` 元素被浏览器解释，文本以标题格式显示。有些情况下您可能希望允许这样做——例如，当用户（也许不是匿名用户）正在为某个网站撰写文章时。

![](img/3d365b72b289213a91ade7eb366b8f35_1546_0.png)

图 40.12

如果不检查用户输入，用户还可以传递 JavaScript，例如 `http://localhost:5000/content?data=<script>alert("hacker");</script>`。您可以使用 JavaScript 的 `alert` 函数弹出一个消息框。同样，也很容易将用户重定向到另一个网站。当这种用户输入被存储在站点中时，一个用户可以输入这样的脚本，所有其他打开此页面的用户都会被相应地重定向。

返回用户输入的数据应始终进行编码。让我们看看编码和不编码的结果有何不同。您可以使用 `HtmlEncoder` 类进行 HTML 编码，如下面的代码片段所示（代码文件 `WebSampleApp/RequestAndResponseSample.cs`）：

```
public static string ContentEncoded(HttpRequest request) =>
    HtmlEncoder.Default.Encode(request.Query["data"]);
```

> **注意** 使用 `HtmlEncoder` 需要 NuGet 包 `System.Text.Encodings.Web`。

当应用程序运行时，使用编码的相同 JavaScript 代码通过 `http://localhost:5000/encoded?data= <script>alert("hacker");</script>` 传递，客户端在浏览器中只会看到 JavaScript 代码，而不会被执行（参见图 40.13）。

![](img/3d365b72b289213a91ade7eb366b8f35_1547_0.png)

图 40.13

发送的编码字符串看起来像以下示例——带有字符引用小于号（`<`）、大于号（`>`）和引号（`"`）：

```
&lt;script&gt;alert(&quot;hacker&quot;);&lt;/script&gt;
```

### 表单数据

除了使用查询字符串将数据从用户传递给服务器之外，还可以使用表单 HTML 元素。此示例使用 HTTP POST 请求而不是 GET。使用 POST 请求时，用户数据通过请求正文传递，而不是在查询字符串中传递。

使用表单数据需要两个请求。首先，通过 GET 请求将表单发送到客户端，然后用户填写表单并通过 POST 请求提交数据。当请求 `/form` 路径时，所调用的方法会根据 HTTP 方法类型转而调用 `GetForm` 或 `ShowForm` 方法（代码文件 `WebSampleApp/RequestResponseSample.cs`）：

```
public static string GetForm(HttpRequest request)
{
    string result = string.Empty;
    switch (request.Method)
    {
        case "GET":
            result = GetForm();
            break;
        case "POST":
            result = ShowForm(request);
            break;
        default:
            break;
    }
    return result;
}
```

该表单由一个名为 `text1` 的 input 元素和一个 Submit 按钮构成。单击 Submit 按钮时，会使用 `method` 参数定义的 HTTP 方法调用表单的 `action` 方法：

```
private static string GetForm() =>
    "<form method=\"post\" action=\"/form\">" +
    "<input type=\"text\" name=\"text1\" />" +
    "<input type=\"submit\" value=\"Submit\" />" +
    "</form>";
```

为了读取表单数据，`HttpRequest` 类定义了 `Form` 属性。该属性返回一个 `IFormCollection` 对象，其中包含发送到服务器的表单中的所有数据：

```
private static string ShowForm(HttpRequest request)
{
    var sb = new StringBuilder();
    if (request.HasFormContentType)
    {
        IFormCollection coll = request.Form;
        foreach (var key in coll.Keys)
        {
            sb.Append(GetDiv(key, HtmlEncoder.Default.Encode(coll[key])));
        }
        return sb.ToString();
    }
    else
        return "no form".Div();
}
```

使用 `/form` 链接，通过 GET 请求接收表单（参见图 40.14）。单击 Submit 按钮时，表单通过 POST 请求发送，您可以看到表单数据的 `text1` 键（参见图 40.15）。

![](img/3d365b72b289213a91ade7eb366b8f35_1548_0.png)

图 40.14

![](img/3d365b72b289213a91ade7eb366b8f35_1548_1.png)

图 40.15

### Cookie

为了在多个请求之间记住用户数据，可以使用 cookie。向 `HttpResponse` 对象添加 cookie 会在 HTTP 标头中从服务器向客户端发送 cookie。默认情况下，cookie 是临时的（不会存储在客户端上），如果 URL 与 cookie 来源的域相同，浏览器会将其发送回服务器。您可以通过设置 `Path` 来限制浏览器何时返回 cookie。在这种情况下，只有当 cookie 来自同一域且使用路径 `/cookies` 时，才会返回 cookie。设置 `Expires` 属性后，cookie 成为持久性 cookie，并会存储在客户端上。当过期时间过后，cookie 将被删除。但是，无法保证 cookie 不会被提前删除（代码文件 `WebSampleApp/RequestResponseSample.cs`）：

```
public static string WriteCookie(HttpResponse response)
{
    response.Cookies.Append("color", "red",
        new CookieOptions
        {
            Path = "/cookies",
            Expires = DateTime.Now.AddDays(1)
        });
    return "cookie written".Div();
}
```

可以通过读取 `HttpRequest` 对象来再次读取 cookie。`Cookies` 属性包含浏览器返回的所有 cookie：

```
public static string ReadCookie(HttpRequest request)
{
    var sb = new StringBuilder();
    IRequestCookieCollection cookies = request.Cookies;
    foreach (var key in cookies.Keys)
    {
        sb.Append(GetDiv(key, cookies[key]));
    }
    return sb.ToString();
}
```

要测试 cookie，还可以使用浏览器的开发者工具。这些工具显示关于发送和接收的 cookie 的所有信息。

### 发送 JSON

服务器返回的不仅仅是 HTML 代码，还返回多种不同的数据格式，例如 CSS 文件、图像和视频。客户端借助响应标头中的 MIME 类型来得知它接收的是什么类型的数据。

方法 `GetJson` 从一个包含 `Title`、`Publisher` 和 `Author` 属性的匿名对象创建 JSON 字符串。为了使用 JSON 序列化此对象，添加了 NuGet 包 `Newtonsoft.Json`，并导入了命名空间 `Newtonsoft.Json`。JSON 格式的 MIME 类型是 `application/json`。这是通过 `HttpResponse` 的 `ContentType` 属性设置的（代码文件 `WebSampleApp/RequestResponseSample.cs`）：

```
public static string GetJson(HttpResponse response)
{
    var b = new
    {
        Title = "Professional C# 6",
        Publisher = "Wrox Press",
        Author = "Christian Nagel"
    };
    string json = JsonConvert.SerializeObject(b);
    response.ContentType = "application/json";
    return json;
}
```

> **注意** 要使用 `JsonConvert` 类，需要添加 NuGet 包 `Newtonsoft.Json`。

这是返回给客户端的数据。

```
{"Title":"Professional C# 6","Publisher":"Wrox Press",
"Author":"Christian Nagel"}
```
