
```
Windows.Storage.CreationCollisionOption.openIfExists).then(function (folder) {
    return folder.createFileAsync("dynamicPage.html",
        Windows.Storage.CreationCollisionOption.replaceExisting);
}).then(function (file) {
    return Windows.Storage.FileIO.writeTextAsync(file, content);
}).then(function () {
    var webview = document.getElementById("webview");
    webview.navigate("ms-appdata:///local/pages/dynamicPage.html");
}).done(null, function (e) {
    WinJS.log && WinJS.log("failed to create dynamicPage.html, err = " + e.message, "app");
});
```

在这两个示例中，输出（使用包内样式表设置样式）如下，毫不掩饰地展示了我当前已写成的作品：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_181_0.png)

请特别注意，我是在本地 appdata 内的一个子文件夹中创建这个动态页面的。WebView 明确禁止导航到根级 local、roaming 或 temp appdata 文件夹中的页面，以保护其他 appdata 文件和文件夹的安全。也就是说，由于 WebView 运行在 Web 上下文中，可能包含你从 Web 下载的任何不受信任的内容，并且 WebView 允许该内容执行脚本等操作，因此你不希望冒险暴露 appdata 中其他位置的潜在敏感信息。通过强制你将 appdata 内容放在子文件夹中，你必须有意将其他 appdata 存储在同一文件夹中，才能让 WebView 访问它。换句话说，这是一道小小的门槛，让你停下来认真思考自己到底在做什么！

在示例中，我还包含了一个指向包内图像（未显示）的链接，只是为了说明你可以为此使用 ms-appx-web URL：

```
content += "<img src=\"ms-appx-web:///images/logo.png\" />";
```

SDK 的 HTML WebView 控件示例（js/scenario3.js）中的场景 3 也展示了使用 ms-appdata URL 的示例，这里是将包内文件复制到本地 appdata 并导航到该文件。另一个可能的情景是，你通过 HTTP 请求从在线服务下载内容，将其存储在 appdata 文件中，然后导航到它。在这种情况下，你只是在文件夹中构建必要的文件结构，并导航到相应页面。例如，你可以向某个服务发出 HTTP 请求，以获取单个压缩文件中的多媒体内容。然后你可以将该文件解压到 appdata 中；假设根 HTML 页面对其他文件具有相对引用，WebView 就能加载并呈现它。

但如果你想下载单个私有格式文件（如电子书），或者获取一个可能加密的 HTML 页面以及用于媒体资源的单个数据库文件，该怎么办？这正是 navigateToLocalStream 的用途，它允许你将自定义内容处理程序和链接解析器注入渲染过程。此方法接受两个参数：

- 一个内容 URI，通过使用应用定义的内容标识符和要解析的相对引用调用 WebView 的 buildLocalStreamUri 方法创建。
- 一个解析器对象，它实现名为 IUriToStreamResolver 的接口，其唯一方法 UriToStreamAsync 接受相对 URI，并生成一个 WinRT IInputStream，渲染引擎随后可通过它加载媒体。

HTML WebView 控件示例中的场景 4 通过 C# 和 C++ 中由 WinRT 组件实现的解析器对象演示了这一点。（有关这些组件的结构，请参见第 18 章“WinRT 组件”。）下面是调用其中一个解析器的方式：

```
var contentUri = document.getElementById("webview").buildLocalStreamUri("NavigateToStream",
    "simple_example.html");
var uriResolver = new SDK.WebViewSampleCS.StreamUriResolver();
document.getElementById("webview").navigateToLocalStreamUri(contentUri, uriResolver);
```

在这段代码中，contentUri 将是一个 ms-local-stream URI，例如 ms-local-stream//microsoft.sdfsamples.controlswebview.js_4e6176696717465546f53747265616d/simple_example.html。由于它以 ms-local-stream 开头，WebView 将立即调用解析器对象的 UriToStreamAsync，为整个页面生成一个流。因此，如果你有一个指向加密文件的 URI，解析器对象可以执行必要的解密，以获得提供给 WebView 的第一段纯 HTML 流，并可能在此过程中应用 DRM。

当 WebView 渲染该 HTML 并遇到其他相对 URL 时，它会依次为每个相对 URL 调用解析器对象，使该解析器能够从数据库流式传输媒体，或在此过程中执行任何其他必要步骤。

完成所有这些的细节超出了本章范围，因此请再次参考 HTML WebView 控件示例。

## WebView 导航事件

导航到 URI 这一想法当然会让人联想到通用 Web 浏览器；事实上，WebView 相当胜任这种用途，因为它既维护内部导航历史，又会在导航发生时触发事件。

尽管导航历史的内容并未公开，但两个属性和方法足以让你实现前进/后退 UI 按钮来控制 WebView：

- `canGoBack` 和 `canGoForward` 布尔属性，指示 WebView 在其导航历史中的当前位置。
- `goBack` 和 `goForward` 方法，在历史中向后或向前导航 WebView。

当你以任何方式导航 WebView 时，它将触发以下事件：

- `MSWebViewNavigationStarting` 导航已开始。
- `MSWebViewContentLoading` HTML 内容流已提供给 WebView（例如，文件已加载，或解析器对象已提供该流）。
- `MSWebViewDOMContentLoaded` WebView 的 DOM 已构建完成。
- `MSWebViewNavigationCompleted` WebView 的内容已完全加载，包括任何引用的资源。

如果过程中出现问题，WebView 将改为引发 `MSWebViewUnviewableContentIdentified` 事件。还值得一提的是，导航发生时标准 `change` 事件也会触发，但设置其他属性时也会触发该事件，因此它对导航用途不那么有用。

HTML WebView 控件示例中的场景 1（我们之前为 `navigate` 看到过）本质上通过将这些方法和事件连接到几个按钮，为你提供了一个简单的 Web 浏览器。请注意，你访问的网站弹出的任何弹窗都会在应用旁边的浏览器中打开。

**提示** 在 JavaScript 中使用 WebView 时，你会发现该对象没有为这些事件提供等效的 `on*` 属性。这一省略是有意为之，以避免与新兴标准发生潜在的命名冲突。因此，目前你必须使用 `addEventListener` 来连接这些事件。

除了 WebView 主内容的导航/加载事件之外，它还会为该内容中的 `iframe` 元素传递类似事件：`MSWebViewFrameNavigationStarting`、`MSWebViewFrameContentLoading`、`MSWebViewFrameDOMContentLoaded` 和 `MSWebViewFrameNavigationCompleted`，每个事件显然与相关的 WebView 事件含义相同，但还在 `eventArgs.uri` 中包含框架所导航到的 URI。

## 从 WebView 内容调用函数并接收事件

WebView 可以发出的另一个事件是 `MSWebViewScriptNotify`。通过它，WebView 中的 JavaScript 代码可以向其宿主引发自定义事件，类似于我们在 Here My Aml 应用中从 `iframe` 使用 `postMessage` 通知应用位置变化的方式。另一方面，WebView 的 `invokeScriptAsync` 方法为应用提供了一种调用 WebView 内函数的方式。

HTML WebView 控件示例中的场景 5 演示了在 WebView 中调用脚本，其中将 html/script_example.html 的以下内容（此处经过精简）加载到 WebView 中：

```
<!DOCTYPE html><html><head>
<title>Script Example</title>
<script type="text/javascript">
function changeText(text) {
    document.getElementById("myDiv").innerText = text;
}
</script>
</head><body>
<div id="myDiv">Call the changeText function to change this text</div>
</body></html>
```

应用按如下方式调用 changeText：

```
document.getElementById("webview").invokeScriptAsync("changeText", document.getElementById("textInput").value).start();
```

invokeScriptAsync 方法的第二个参数始终是字符串（或将被转换为字符串）。如果你想传递多个参数，请对具有适当命名属性的对象使用 JSON.stringify，并在另一端使用 JSON.parse 解析它。

注意！请注意 invokeScriptAsync 调用末尾附加的至关重要的 start()。实际运行异步调用操作需要它。没有它，你会纳闷为什么调用没有发生！稍后我们将通过另一个示例进一步讨论这一点。

示例中的场景 6 演示了从 WebView 接收事件。事件通过 window.external.notify 方法引发，其唯一参数同样是字符串。在示例中，html/scriptnotify_example.html 页面包含以下 JavaScript：

```
window.external.notify("The current time is " + new Date());
```

应用按如下方式接收它，其中事件参数的 value 属性包含来自 window.external.notify 的参数：

```
document.getElementById("webview").addEventListener("MSWebViewScriptNotify", scriptNotify);

function scriptNotify(e) {
  var outputArea = document.getElementById("outputArea");
  outputArea.value += ("ScriptNotify event received with data:\n" + e.value + "\n\n");
  outputArea.scrollTop = outputArea.scrollHeight;
}
```

要求：MSWebViewScriptNotify 只会从加载了 ms-appx-web、ms-local-stream 和 https 内容的 WebView 中引发，其中 https 还要求清单中有内容 URI 规则，否则该事件将被阻止。如果涉及 URI 解析器，也允许 ms-appdata。请注意，通过 navigateToString 加载的 WebView 没有此要求。
