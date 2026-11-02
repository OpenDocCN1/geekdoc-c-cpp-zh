
利用这个 blob 可以做许多事情。如果想在 `img` 元素中显示它，可以直接对这个 blob 使用 `URL.createObjectURL`。这意味着你可以轻松地在离屏 WebView 中加载一段 HTML（确保显示样式*不是*“none”），然后捕获 blob 并在 `img` 中显示结果。除了阻止交互之外，你还可以比完整 WebView 更高效地为该图像添加动画，例如应用 3D CSS 变换。我的 WebViewExtras 示例中的场景 3 演示了这一点。

对于其他用途，例如共享超级按钮，可以调用此 blob 的 `msDetachStream` 方法，它能方便地生成正好需要提供给数据包的 `setBitmap` 方法的内容。SDK 的 HTML WebView 控件示例中的场景 7 演示了这一点。

## HTTP 请求

如上一节所示，使用 WebView 元素将 Web 内容直接呈现到布局中非常棒——前提是你确实希望此类内容直接出现在布局中！在许多情况下，你更想通过 HTTP 请求从 Web 检索数据。然后你可以进一步操作、组合和处理这些数据，以便在其他控件中显示，或仅仅用来驱动应用体验。你还会遇到许多需要通过 HTTP 请求向 Web 发送信息的情况，此时像 WebView 这样的单向元素用处不大。

Windows 提供了多种与 Web 交换数据的方式。本节我们将了解用于 HTTP 请求的 API，这些 API 通常要求应用正在运行。一个例外是，Windows 允许你指明它可能会自动缓存的 Web 内容，这样下次应用启动（或恢复）时发出的请求就完全无需访问 Web 即可完成。这利用了应用宿主像浏览器一样缓存 Web 内容这一事实，以减少网络流量并提高性能。这种预缓存能力只是利用了这一点，但它受某些条件限制，并且并不保证对每个请求的 URI 都有效。

另一个例外是我们将在下一节“后台传输”中讨论的内容。Windows 可以代你执行后台上传和下载，即使应用挂起或终止，这些操作也会继续工作。因此，如果你的场景涉及数据传输，而这类传输可能会考验用户盯着可爱却极其烦人的进度指示器的耐心，并诱使他们切换到其他应用，请使用后台传输 API，而不是通过 HTTP 请求自行处理。

当然，HTTP 请求是 RESTful Web 和许多 Web API 的基础，通过它们可以获取大量有趣的数据，当然包括网页和 RSS 源。而且，由于 SOAP 等其他协议本质上构建在 HTTP 请求之上，这里我们将重点讨论后者。RSS 和 AtomPub 也有单独的 WinRT API，详细信息可在附录 C 中找到。

没错！我说过，执行 HTTP 请求有多种方式。如下所示：

- **XMLHttpRequest** 这个内置 JavaScript 对象在 Windows 商店应用中工作正常，这对第三方库非常有帮助。此异步函数的结果通过其 `readystatechange` 事件返回。
- **WinJS.xhr** 这个包装器围绕 `XMLHttpRequest` 提供 promise 结构，就像上一节中我们对 WebView 的异步方法所做的那样。`WinJS.xhr` 在设置标头等方面提供了相当大的灵活性，并且通过返回 promise，可以轻松地将 `WinJS.xhr` 调用与 WinRT 文件 I/O 等其他异步操作链接起来。可以在前面用过的 HTML WebView 控件示例的场景 1 中看到一个简单示例。
- **HttpClient** 最强大、高性能且灵活的 HTTP 请求 API 位于 WinRT 的 `Windows.Web.Http` 命名空间中，推荐用于新代码。其主要优势在于性能更好、与浏览器使用相同的缓存、支持更广泛的 HTTP 场景，并允许进行 Cookie 管理、筛选和灵活传输。你还可以创建多个具有不同配置的 HttpClient 实例并同时使用它们。

这里我们将主要关注 `HttpClient`。不过，为了对比，让我们快速看一下 `WinJS.xhr`，以防你在其他代码中遇到它。

注意 如果你对 .NET Framework 有一些经验，请注意 `Windows.Web.Http` 中的 `HttpClient` API 与 .NET 的 `System.Net.Http.HttpClient` API 不同。

## 使用 WinJS.xhr

调用 `WinJS.xhr` 相当容易，正如本章的 SimpleXhr1 示例所演示的那样。这里我们使用 `WinJS.xhr` 从 Windows App Builder 博客检索 RSS 源，注意默认 HTTP 动词是 GET，因此不必显式指定：

```js
WinJS.xhr({ url: "http://blogs.msdn.com/b/windowsappdev/rss.aspx" })
    .done(processPosts, processError, showProgress);
```

也就是说，给 `WinJS.xhr` 一个 URI，它就会返回一个 promise，将结果传递给完成处理程序（本例中为 `processPosts`），如果提供了进度处理程序，它甚至还会调用该处理程序。对于前者，结果包含一个 `responseXML` 属性，这是一个 `DOMParser` 对象。对于后者，事件对象的 `response` 属性包含当前 XML，我们可以轻松用它来显示下载计数：

```js
function showProgress(e) {
    var bytes = Math.floor(e.response.length / 1024);
    document.getElementById("status").innerText = "Downloaded " + bytes + " KB";
}
```

应用的其余部分只是处理响应文本，查找 `item` 元素并显示 `title`、`pubDate` 和 `link` 字段。稍加样式（参见 default.css），并使用 WinJS 排版样式类 `win-type-x-large`（用于 `title`）、`win-type-medium`（用于 `pubDate`）和 `win-type-small`（用于 link），我们就得到一个如图 4-4 所示的快速应用。你可以查看代码了解细节。36

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_190_0.png)

图 4-4 SimpleXhr1 和 SimpleXhr2 应用的输出。

在 SimpleXhr1 中，我也确保为 WinJS.xhr promise 提供了错误处理程序，这样至少可以显示一条简单的消息。

有关 XMLHttpRequest/WinJS.xhr 及相关事项的更完整演示，请参阅“XHR、处理导航错误和 URL 方案”示例以及文档中名为“如何创建混搭”的教程。有关 XMLHttpRequest 和 WinJS.xhr 的更多说明可在附录 C 中找到。

## 使用 Windows.Web.Http.HttpClient

现在让我们看看用 Windows.Web.Http.HttpClient 实现的同一个应用，你可以在配套内容中的 SimpleXhr2 里找到它。就我们的目的而言，`HttpClient.getStringAsync` 方法已经足够：

```javascript
var htc = new Windows.Web.Http.HttpClient();
htc.getStringAsync(new Windows.Foundation.Uri("http://blogs.msdn.com/b/windowsappdev/rss.aspx"))
.done(processPosts, processError, showProgress);
```

此函数将响应正文文本传递给完成处理程序（`processPosts`），因此我们只需创建一个 `DOMParser` 对象来处理 XML 文档。之后，我们得到的内容与从 `WinJS.xhr` 收到的内容相同：

```javascript
var parser = new window.DOMParser();
var xml = parser.parseFromString(bodyText, "text/xml");
```

`HttpClient` 对象提供了许多其他方法，用于发起与 Web 资源的各种 HTTP 交互，如图 4-5 所示。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_191_0.png)

**图 4-5** `HttpClient` 对象中的方法及其关联的 HTTP 流量。请注意，所有流量都通过应用提供的筛选器（或默认筛选器）路由，这允许在 API 下层进行细粒度控制。

在所有情况下，URI 都由 `Windows.Foundation.Uri` 对象表示，正如我们在前面的代码片段中看到的那样。所有特定的 `get*` 方法都会发出 HTTP GET，并以特定形式传递结果：字符串、缓冲区和输入流。所有这些方法（以及 `sendRequestAsync`）都支持进度，进度处理程序会收到一个 `Windows.Web.Http.HttpProgress` 实例，其中包含 `bytesReceived` 等各种属性。

处理字符串很容易，但这些缓冲区和输入流是什么呢？它们是特定的 WinRT 构造，可以馈入其他 API，例如文件 I/O（参见 `Windows.Storage.Streams` 和 `Windows.Storage.StorageFile`）、加密/解密（参见 `Windows.Security.Cryptography`），以及 HTML blob API。例如，可以将 `InputStream` 提供给 `MSApp.createStreamFromInputStream`，从而得到一个 HTML `MSStream` 对象。然后可以将它提供给 `URL.createObjectURL`，其结果可以直接赋给 `img.src` 属性。这样，你就可以轻松发起对图像资源的 HTTP 请求，并在布局中显示结果，而无需在 appdata 中创建中间文件。更多详细信息，请参见第 10 章中的“文件、流、缓冲区和 Blob 问答”。
