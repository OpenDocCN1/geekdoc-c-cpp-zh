

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_177_0.png)

此类经纪能力需要内容 URI 规则，因为加载到 iFrame 中的 Web 内容很容易提供导航到其他任意页面的途径，而这些页面可能具有恶意性。如果没有为目标页面设置内容 URI 规则，iFrame 将根本不会导航到该页面。

在某些应用设计中，你可能需要从应用中的 Web 内容页面导航到本地上下文页面。例如，你可能会在服务器上托管一个页面，使其能够确保其他服务器端内容完全安全（也就是说，不将这些内容带到客户端）。当然，你可以将该页面托管在 iframe 中，但如果出于某种原因需要直接导航到它，那么可能需要导航回本地上下文页面。你可以通过在本地页面的代码中调用超级机密函数 `MSApp.addPublicLocalApplicationUri` 来启用此功能（实际上，该函数有完整的文档说明），并为每个需要的特定 URI 进行调用。[集成 Web 服务中的内容和控件示例](https://example.org)中的场景 6 就给出了一个示例。首先，它在 Web 上下文中包含一个 iframe（http://addPublicLocalUri.html）：

```
~~~html
<iframe src="ms-appx-web:///navigateToLocal.html"></iframe>
~~~
```

然后，该页面包含一个用于导航到本地上下文页面的 `<a href>`，该本地页面会调用 WinRT API，以便进行充分演示；请参阅项目根目录中的 navigateToLocal.html：

```
~~~html
<a href="ms-appx:///callWinRT.html">Navigate to ms-appx:///callWinRT.html</a>
~~~
```

为了使其正常工作，我们随后必须从本地上下文页面调用 `addPublicLocalApplicationUri`，并指定受信任的目标（js/addPublicLocalUri.js）：

```
~~~javascript
MSApp.addPublicLocalApplicationUri("callWinRT.html");
~~~
```

通常，最好在调用中包含 `ms-appx:///` 前缀，以提高清晰度：

```
~~~javascript
MSApp.addPublicLocalApplicationUri("ms-appx:///callWinRT.html");
~~~
```

请注意，虽然该方法表面上并不显得强大，但实际上它的权限非常大。由于 Web 上下文可以托管任何远程页面，因此当 URI 包含查询参数时尤其要谨慎。例如，不要允许网站导航到类似 `ms-appx:///delete.html?file=superimportant.doc` 的地址，然后盲目接受这些参数！简而言之，始终应将此类 URI 参数（以及标头中的任何信息）视为不受信任的内容。

## `<x-ms-webview>` 元素

每当你希望在应用上下文中显示某个任意 HTML 页面——特别是显示应用包之外的页面时，`x-ms-webview` 元素就是你的最佳选择。<sup>35</sup> 这是一个能够被渲染引擎识别的原生 HTML 元素，其基本工作方式类似于 Web 浏览器的核心（但不包含导航、收藏夹等外围功能）。加载到 WebView 中的任何内容都会在 Web 上下文中运行，因此它可以用于任意 URI，但使用 `ms-appx` 架构的 URI 除外。它还支持 `ms-appdata` URI 和字符串字面量渲染，这意味着你可以轻松显示动态生成的 HTML/CSS/JavaScript，以及下载并存储在本地的内容。这还包括自行解析链接的能力，例如图像存储在数据库中而不是作为独立文件存储时。WebView 内容同样始终在 Web 上下文中运行（无法访问 WinRT）；就应用商店认证而言，目前对脚本等内容的使用没有限制。而且，WebView 甚至支持其他功能，例如将其内容渲染到流中，以便据此创建位图。下面就来看看这一切是如何工作的！

**这个奇怪的名称是怎么回事？** 你可能已经在想，为什么 WebView 使用这个奇怪的 `x-ms-webview` 标签。这样做是为了避免将来与新兴标准发生冲突；届时，带有供应商前缀的实现可能会变成 `ms-webview`。

由于 WebView 和其他 HTML 元素一样都是 HTML 元素，因此你可以随意使用 CSS 设置其样式、对元素进行动画处理，等等。它的 JavaScript 对象还具有与其他 HTML 元素共享的完整属性、方法和事件集合，同时也有一些自身独有的成员。不过请注意，WebView 没有也不支持任何属于自身的子内容，因此 `innerHTML` 和 `childNodes` 等属性为空，对它们进行设置也不会产生任何效果。

WebView 最简单的使用场景（我之所以这样称呼它，是因为每次都输入这个奇怪的元素名称实在令人厌烦）就是通过其 `src` 属性让它指向某个 URI。[集成 Web 服务中的内容和控件示例（html/webContent.html）](html/webContent.html)的场景 1 中就有一个例子，结果如图 4-2 所示：

```
```
<x-ms-webview id="webContentHolder"
src="http://www.microsoft.com/presspass/press/NewsArchive.mspx?cmbContentType=PressRelease">
</x-ms-webview>
```
```

该示例允许你选择不同的链接，然后只需再次设置其 `src` 属性，这些链接就会在 WebView 中呈现。

35 WebView 元素的加入是 Windows 8.1 的重要改进之一。在 Windows 8 中，使用 HTML、CSS 和 JavaScript 编写的应用只能使用 `iframe` 元素。然而，`iframe` 无法处理包含阻止框架代码的网页，无法加载本地（appdata）页面，并且存在一些细微的安全问题。因此，Windows 8.1 为大多数用途提供了原生的 `x-ms-webview` HTML 元素，同时将 `iframe` 限制为仅使用包内的 ms-appx[-web] 和 https URI。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_179_0.png)

**图 4-2** 显示 WebView；WebView 是应用布局中与其他 HTML 元素一样的元素。WebView 在 Web 上下文中运行，并允许在其自身内容中进行导航。

单击 WebView 内的链接会导航到相应页面。在许多实时网页中，如果你在调试器中运行应用，可能会看到 JavaScript 异常。这些异常不会终止整个应用，因此可以安全地忽略，或不进行处理。事实上，在调试器之外，用户永远不会看到这些异常——WebView 会忽略它们。

正如本例所示，设置 `src` 属性是将内容加载到 WebView 的一种方式。WebView 对象还支持另外四种方法：

- `navigate` 将 WebView 导航到受支持的 URI（[http[s]、ms-appx-web 和 ms-appdata）。该页面可以包含对其他 URI 的引用，但 `ms-appx` 除外。
- `navigateWithHttpRequestMethod` 将 WebView 导航到受支持的 URI，并允许设置 HTTP 谓词和标头。
- `navigateToString` 将 HTML 字符串字面量渲染到 WebView 中。引用同样可以指向受支持的 URI，但 `ms-appx` 除外。
- `navigateToLocalStreamUri` 使用应用提供的对象解析相对 URI，并可能解密页面内容，然后导航到本地 appdata 中的页面。

HTML WebView 控件示例中提供了上述大多数方法的示例。SDK 示例的场景 1 展示了 `navigate`：首先创建一个空的 WebView，然后使用 URI 字符串调用 `navigate`（`js/1_NavToUrl.js`）：

```
var webviewControl = document.getElementById("webview");
webviewControl.navigate("http://go.microsoft.com/fwlink/?linkId=294155");
```

通过 navigateWithHttpRequestMessage 进行导航会稍微复杂一些。虽然示例中没有包含相关代码，但你可以在 App Builders Blog 的《Blending Apps and Sites with the HTML x-ms-webview》中找到相关代码：

```
//The site to which we navigate
var siteUrl = new Windows.Foundation.Uri("http://www.msn.com");

//Specify the type of request (get)
var httpRequestMessage = new
Windows.Web.Http.HttpRequestMessage(Windows.Web.Http.HttpMethod.get, siteUrl);

// Append headers to request the server to check against the cache
httpRequestMessage.headers.append("Cache-Control", "no-cache");
httpRequestMessage.headers.append("Pragma", "no-cache");

// Navigate the WebView with the request info
webview.navigateWithHttpRequestMessage(httpRequestMessage);
```

SDK 示例的场景 2 展示了 `navigateToString`：将包内的 HTML 文件加载到字符串变量中，这与使用相同的 ms-appx-web URI 调用 navigate 类似。当然，如果内容已经存在于 HTML 文件中，直接使用 navigate 即可！因此，navigateToString 更常用于动态生成的内容。例如，假设我创建如下字符串，你会注意到其中包含对包内样式表的引用。本例位于本章配套内容中的 WebviewExtras 示例的场景 1（js/scenario1.js）：

```
var baseURI = "http://www.kraigbrockschmidt.com/images/";

var content = "<!doctype HTML><head><style>";
//Refer to an in-package stylesheets (or one in ms-appdata:/// or http[s]://)
content +=
"<head><link rel='stylesheet' href='ms-appx-web:///css/localstyles.css' /></head>";
content += "<html><body><h1>Dynamically-created page</h1>";
content += "<p>This document contains its own styles as well as a remote image references.</p>"
content += "<img src='" + baseURI + "Cover_ProgrammingWin8.jpg' />" + space;
content += "<img src='" + baseURI + "Cover_MysticMicrosoft.jpg' />" + space;
content += "<img src='" + baseURI + "Cover_FindingFocus.jpg' />" + space;
content += "<img src='" + baseURI + "Cover_HarmoniumHandbook2.jpg' />"
content += "</body></html>";
```

这样，我们就可以直接加载这个字符串：

```
var webview = document.getElementById("webview");
webview.navigateToString(content);
```

同样，我们也可以轻松地将这段文本写入应用的 appdata 中的文件，然后使用带有 ms-appdata URI 的 navigate（同样位于 js/scenario1.js）：

```
var local = Windows.Storage.ApplicationData.current.localFolder;

local.createFolderAsync("pages",
