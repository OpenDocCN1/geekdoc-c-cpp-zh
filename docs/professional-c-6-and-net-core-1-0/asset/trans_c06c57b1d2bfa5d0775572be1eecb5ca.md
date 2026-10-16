

> 注意：本章仅使用 HttpClient 类发送 HTTP GET 请求。HttpClient 类还允许通过 PostAsync、PutAsync 和 DeleteAsync 方法发送 HTTP POST、PUT 和 DELETE 请求。这些方法将在第 42 章“ASP.NET Web API”中用到，届时这些请求用于调用 Web 服务中相应的操作方法。

创建 HttpRequestMessage 对象后，可以通过 Headers 和 Content 属性提供标头和内容。通过 Version 属性，可以指定 HTTP 版本。

> 注意：HTTP/1.0 于 1996 年发布，几年后 1.1 紧随其后。使用 1.0 时，服务器返回数据后连接总是关闭；使用 1.1 时，增加了 keep-alive 标头，客户端可以表达希望保持连接活跃的意愿，因为客户端可能发出更多请求，不仅要接收 HTML 代码，还要接收 CSS 和 JavaScript 文件以及图像。HTTP/1.1 于 1999 年定义，之后过了 16 年，直到 2015 年 HTTP/2 才完成。版本 2 有什么优势？HTTP/2 允许在同一连接上进行多个并发请求，压缩标头信息，客户端可以决定哪些资源更重要，服务器还可以通过服务器推送向客户端发送资源。支持服务器推送的 HTTP/2 意味着，一旦 HTTP/2 得到全面支持，WebSockets 实际上将变得过时。所有较新版本的浏览器，以及运行在 Windows 10 和 Windows Server 2016 上的 IIS，都支持 HTTP/2。

## 在 Windows 运行时中使用 HttpClient

在撰写本书时，用于控制台应用程序和 WPF 的 HttpClient 类不支持 HTTP/2。然而，用于通用 Windows 平台的 HttpClient 类有一个基于 Windows 10 API 功能的不同实现。因此，HttpClient 支持 HTTP/2，甚至默认使用该版本。

下一个代码示例展示了一个通用 Windows 应用，它对在 TextBox 中输入的链接发送 HTTP 请求，并显示结果以及 HTTP 版本信息。下面的代码片段展示了 XAML 代码，图 25.2 显示了设计视图（代码文件 WinAppHttpClient/MainPage.xaml）：

```
<StackPanel Orientation="Horizontal">
    <TextBox Header="Url" Text="{x:Bind Url, Mode=TwoWay}" MinWidth="200" Margin="5" />
    <Button Content="Send" Click="{x:Bind OnSendRequest}"
```

```
Margin="10,5,5,5"
    VerticalAlignment="Bottom" />
</StackPanel>
<TextBox Header="Version" Text="{x:Bind Version, Mode=OneWay}"
Grid.Row="1"
    Margin="5" IsReadOnly="True" />
<TextBox AcceptsReturn="True" IsReadOnly="True" Text="{x:Bind Result,
    Mode=OneWay}" Grid.Row="2"
ScrollViewer.HorizontalScrollBarVisibility="Auto"
    ScrollViewer.VerticalScrollBarVisibility="Auto" />
```

![](img/3d365b72b289213a91ade7eb366b8f35_901_0.png)

### 图 25.2

> 注意：XAML 代码和依赖属性将在第 29 章“核心 XAML”中说明，编译绑定将在第 31 章“XAML 应用模式”中介绍。

Url、Version 和 Result 属性实现为依赖属性，以便自动更新 UI。下面的代码片段展示了 Url 属性（代码文件 WinAppHttpClient/MainPage.xaml.cs）：

```
public string Url
{
    get { return (string)GetValue(UrlProperty); }
    set { SetValue(UrlProperty, value); }
}
```

```
public static readonly DependencyProperty UrlProperty =
    DependencyProperty.Register("Url", typeof(string),
typeof(MainPage),
    new PropertyMetadata(string.Empty));
```

HttpClient 类在 OnSendRequest 方法中使用。此方法在 UI 中单击 Send 按钮时调用。与前面的示例一样，使用 SendAsync 方法发出 HTTP 请求。为了确认请求确实使用了 HTTP/2 版本，你可以在调试器中检查 `request.Version` 属性。服务器从 `response.Version` 返回的版本会被写入绑定在 UI 中的 `Version` 属性。如今，大多数服务器只支持 HTTP 1.1 版本。如前所述，Windows Server 2016 支持 HTTP/2：

```
private async void OnSendRequest()
{
    try
    {
        using (var client = new HttpClient())
        {
            var request = new HttpRequestMessage(HttpMethod.Get, Url);
            HttpResponseMessage response = await
client.SendAsync(request);
            Version = response.Version.ToString();
            response.EnsureSuccessStatusCode();
            Result = await response.Content.ReadAsStringAsync();
        }
    }
    catch (Exception ex)
    {
        await new MessageDialog(ex.Message).ShowAsync();
    }
}
```

运行应用程序时，你可以向 https://http2.akamai.com/demo 发出请求，以查看返回的 HTTP/2。

## 使用 WebListener 类

使用 Internet Information Server (IIS) 作为 HTTP 服务器通常是一个很好的方法，因为你可以使用许多功能，例如可伸缩性、运行状况监视、用于管理的图形用户界面等等。不过，你也可以轻松创建自己的简单 HTTP 服务器。自 .NET 2.0 以来，你一直可以使用 `HttpListener`，但现在有了 .NET Core 1.0，有了一个新的侦听器：`WebListener` 类。

### 依赖项

- NETStandard.Library
- Microsoft.Net.Http.Server

### 命名空间

- Microsoft.Net.Http.Server
- System
- System.Collections.Generic
- System.Linq
- System.Net
- System.Reflection
- System.Text
- System.Threading.Tasks
- static System.Console

HTTP 服务器的示例代码是一个控制台应用程序（包），它允许传递一个 URL 前缀列表，用于定义服务器的侦听位置。此类前缀的一个示例是 `http://localhost:8082/samples`，其中服务器仅侦听 localhost 上 8082 端口且路径以 samples 开头的请求。无论后续路径如何，服务器都会处理该请求。为了不仅仅支持来自 localhost 的请求，你可以使用 `+` 字符，例如 `http://+:8082/samples`。这样，服务器也可以从其所有主机名访问。如果你没有以提升模式启动 Visual Studio，运行侦听器的用户需要获得权限。你可以通过以提升模式运行命令提示符，并使用以下 `netsh` 命令添加 URL 来完成此操作：

```
```text
>netsh http add urlacl url=http://+:8082/samples user=Everyone
```
```

示例代码检查参数是否至少传递了一个前缀，然后调用 `StartServer` 方法（代码文件 `HttpServer/Program.cs`）：

```
```csharp
static void Main(string[] args)
{
    if (args.Length < 1)
    {
        ShowUsage();
        return;
    }
    StartServerAsync(args).Wait();
    ReadLine();
}

private static void ShowUsage()
{
    WriteLine("Usage: HttpServer Prefix [Prefix2] [Prefix3] [Prefix4]");
}
```
```

程序的核心是 `StartServer` 方法。在这里，实例化 `WebListener` 类，并添加由命令行参数列表定义的前缀。调用 `WebListener` 类的 `Start` 方法会在系统上注册端口。接下来，在调用 `GetContextAsync` 方法之后，侦听器会等待客户端连接并发送数据。一旦客户端发送 HTTP 请求，就可以从 `GetContextAsync` 返回的 `HttpContext` 对象中读取该请求。对于来自客户端的请求和发送的应答，都使用 `HttpContext` 对象。`Request` 属性返回一个 `Request` 对象。`Request` 对象包含 HTTP 标头信息。对于 HTTP POST 请求，`Request` 还包含正文。`Response` 属性返回一个 `Response` 对象，该对象允许你返回标头信息（使用 Headers 属性）、状态代码（StatusCode 属性）和响应正文（Body 属性）：

```
public static async Task StartServerAsync(params string[] prefixes)
{
    try
    {
        WriteLine($"server starting at");
        var listener = new WebListener();
        foreach (var prefix in prefixes)
        {
            listener.UrlPrefixes.Add(prefix);
            WriteLine($"\t{prefix}");
        }

        listener.Start();

        do
        {
            using (RequestContext context = await listener.GetContextAsync())
            {
                context.Response.Headers.Add("content-type", new string[] {"text/html"});
                context.Response.StatusCode = (int)HttpStatusCode.OK;

                byte[] buffer = GetHtmlContent(context.Request);
                await context.Response.Body.WriteAsync(buffer, 0, buffer.Length);
            }
        } while (true);
    }
    catch (Exception ex)
    {
        WriteLine(ex.Message);
    }
}
```

示例代码返回一个使用 GetHtmlContent 方法检索的 HTML 文件。此方法使用 htmlFormat 格式字符串，其中标题和正文有两个占位符。GetHtmlContent 方法使用 string.Format 方法填充占位符。为了填充 HTML 正文，使用了两个辅助方法，它们从请求中检索标头信息以及 Request 对象的所有属性值——GetHeaderInfo 和 GetRequestInfo：

```
private static string htmlFormat =
    "<!DOCTYPE html><html><head><title>{0}</title></head>" +
    "<body>{1}</body></html>";

private static byte[] GetHtmlContent(Request request)
{
    string title ="Sample WebListener";

    var sb = new StringBuilder("<h1>Hello from the server</h1>");
    sb.Append("<h2>Header Info</h2>");
    sb.Append(string.Join("", GetHeaderInfo(request.Headers)));
    sb.Append("<h2>Request Object Information</h2>");
```

