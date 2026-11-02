

`getAsync` 方法会创建一个通用 HTTP GET 请求。它的 `message` 参数是一个 `HttpRequestMessage` 对象，在其中你可以构造所需的任何类型的请求，设置 `requestUri`、`headers`、`transportInformation`<sup>37</sup>，以及你想传递给筛选器、也可能传递给服务器的其他任意 `properties`。`getAsync` 的完成处理程序将接收一个 `HttpResponseMessage` 对象，稍后我们就会看到。

**处理异常！** 在处理 HTTP 请求时，处理异常非常重要，也就是说，要为 `getAsync` 之类的方法提供错误处理程序。已发现，由 HTTP 请求引发的未处理异常是应用突然终止的主要原因之一！

对于其他 HTTP 操作，你可以在图 4-5 中看到 `putAsync`、`postAsync` 和 `deleteAsync`，以及完全通用的 `sendRequestAsync`。对于后者，它的 `message` 参数同样是 `getAsync` 所用的 `HttpRequestMessage`，只是在这里你还可以设置将要使用的 HTTP `method`（这是一个 `HttpMethod` 对象，也允许附加选项）。就 `deleteAsync` 而言，它完全根据 URI 参数工作。

在 put 和 post 的情况下，方法的参数是 URI 和 `content`，后者是一个通过 `HttpContent` 接口的方法和属性提供相关数据的对象（见图 4-5 左下角）。并不要求你从头创建此类对象（尽管你可以这样做）——WinRT 提供了名为 `HttpBufferContent`、`HttpStringContent`、`HttpStreamContent`、`HttpMultipartContent`、`HttpMultipartFormDataContent` 和 `HttpFormUrlEncodedContent` 的内置实现。

然后，你从 `getAsync`、`sendRequestAsync` 以及 delete、put 和 post 方法得到的是一个 `HttpResponseMessage` 对象。在这里，你会找到你所期望的所有内容：

- `statusCode`、`reasonPhrase`，以及一些用于处理错误的辅助方法——即 `EnsureSuccessStatusCode`（在未收到特定代码时抛出异常）和 `isSuccessStatusCode`（检查 200–299 范围）。
- 一个 `headers` 集合（类型为 `HttpResponseHeaderCollection`），它又会引出许多其他次级类。
- 原始 `requestMessage`（一个 `HttpRequestMessage`）。
- `source`，一个来自 `HttpResponseMessageSource` 的值，它告诉你数据是通过网络接收的，还是从缓存加载的。
- 响应 `content`，一个与之前一样具有 `HttpContent` 接口的对象。通过它，你可以将响应数据获取为字符串、缓冲区、输入流和内存中数组（`bufferAllAsync`）。

<sup>37</sup> 此只读属性用于 SSL 连接的证书，并包含 SSL 协商的结果；请参阅 `HttpTransportInformation`。要设置客户端证书，`HttpBaseProtocolFilter` 上有一个属性。

因此，很明显，HttpClient 对象确实让你能够完全控制需要向服务发出的任何类型的 HTTP 请求，包括接下来两节中所述的缓存控制和 Cookie 管理等附加能力。同样明显的是，HttpClient 在某种程度上仍然是一个低层 API。因此，对于你将使用的任何给定 Web 服务，我非常建议创建一个层或库，用来封装对该 API 的请求，以及将响应转换为应用其余部分要处理的数据的过程。这样，你还可以让应用的其余部分与后端细节隔离开来，使后端能够按需更改而不会破坏应用。如果你希望整合 Windows.Web.Http API 的附加功能（例如筛选、缓存控制和 Cookie 管理），这也会很有帮助。

我很想先谈谈 Cookie（正餐前先吃甜点总是很不错的），但这都属于筛选的一部分。筛选是一种机制，通过它你可以控制 HttpClient 如何管理其请求和响应。筛选器要么是按需配置的默认 `HttpBaseProtocolFilter` 类（位于 `Windows.Web.Http.Filters` 命名空间中）的实例，要么是派生类的实例。你将这个筛选器对象传递给 `HttpClient` 构造函数；如果未提供筛选器，它将默认使用 `HttpBaseProtocolFilter`。不过，要进行缓存控制之类的操作，你需要直接创建 `HttpBaseProtocolFilter` 的实例、设置属性，然后用它创建 `HttpClient`。

提示：完全允许甚至鼓励在需要为不同服务使用不同筛选器和配置时创建多个 HttpClient 实例。这样做没有任何代价，而且可以极大简化编程模型。

筛选器本质上是一个黑盒，它接收 HTTP 请求并生成 HTTP 响应——关于它在整个流程中的位置，请再次参考图 4-5。在筛选器内部，你可以处理凭据、代理、证书和重定向等细节，也可以实现重试机制、缓存、日志记录等。这样可以把所有这些细节集中放在 HttpClient API 下层的一个位置，使你不必在 HttpClient 调用周围的代码中费心处理它们。

在缓存控制方面，筛选器包含一个 `cacheControl` 属性，可以将其设置为 `HttpCacheControl` 类的实例。该对象有两个属性：`readBehavior` 和 `writeBehavior`，它们决定缓存如何应用于经过此筛选器的请求。对于读取，`readBehavior` 设置为 `HttpCacheReadBehavior` 枚举中的值：`default`（像 Web 浏览器一样工作）、`mostRecent`（与服务器进行 if-modified-since 交换）和 `onlyFromCache`（供离线使用）。对于写入，`writeBehavior` 可以是 `HttpCacheWriteBehavior` 中的值，该枚举支持 `default` 和 `noCache`。

管理 Cookie 也发生在筛选器层面。默认情况下——通过 `HttpBaseProtocolFilter`——`HttpClient` 会自动读取传入的 set-cookie 标头，按需保存生成的 Cookie，然后酌情将 Cookie 添加到传出标头中。要访问这些 Cookie，请使用 `HttpBaseProtocolFilter` 的实例创建 `HttpClient`。然后可以访问筛选器的 `cookieManager` 属性（这听起来是个不错的差事）。该属性是 `HttpCookieManager` 的实例，有三个方法：`getCookies`、`setCookie` 和 `deleteCookie`。它们允许你检查要为请求发送的特定 Cookie，或出于隐私考虑删除特定 Cookie。

Cookie 行为通常遵循与浏览器相同的模式。Cookie 是否会跨应用会话持久存在取决于常规 Cookie 规则：Cookie 必须标记为持久，并受常规的每应用限制等约束。另请注意，出于正常的安全原因，Cookie 在应用之间是隔离的，即使这些应用使用相同的在线资源。

有关 HttpClient 的更多思考，请参阅 Windows App Builder 博客上的《更新 JavaScript 应用以使用新的 Windows Web HTTP API》。随后可以在 Windows SDK 的 HttpClient 示例中找到该 API 的演示，包括筛选。以下是其场景演示内容的简要概述：

- **场景 1–3** 针对文本（带缓存控制）、流和 XML 列表的 GET 请求。
- **场景 4–7** 针对文本、流、多部分 MIME 表单和带进度的流的 POST 请求。
- **场景 8–10** 获取、设置和删除 Cookie。
- **场景 11** 一个按流量计费的连接筛选器，在筛选器层面实现成本感知。
- **场景 12** 一个重试筛选器，可自动处理带有 Reply-After 标头的 503 错误。

要运行此示例，你必须先设置一个本地主机服务器，以及一个数据文件和一个上传目标页面。为此，请确保你的计算机上安装了 Internet Information Services，如下文“侧栏：使用本地主机”所述。然后，在管理员命令提示符中，导航到示例的 Server 文件夹并运行命令 powershell -file setupserver.ps1。这会在本地主机（c:\inetpub\wwwroot）上安装示例所需的服务器端文件。

## 侧栏：使用本地主机

本地主机是一个在你本地计算机上运行的服务器进程，使得调试客户端-服务器交互的两端成为可能。为此，你可以使用 Apache 之类的服务器，也可以使用 Windows 内置并与 Visual Studio 工具集成的解决方案：Internet Information Services (IIS)。

要在 Windows 中启用 IIS，请转到“控制面板”>“程序和功能”>“启用或关闭 Windows 功能”。如下所示，在顶层勾选“Internet Information Services”复选框，以安装核心功能：

