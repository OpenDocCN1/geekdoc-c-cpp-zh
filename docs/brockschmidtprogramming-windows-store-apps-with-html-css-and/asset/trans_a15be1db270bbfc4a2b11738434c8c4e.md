
作为对 webview 这种调用/事件机制的另一个演示，我对本章配套内容中的 HereMyAm4 示例做了一些更改。首先，我用 `x-ms-webview` 替换了之前用来加载地图页面的 iframe。然后，我用 `invokeScriptAsync` 和 `MSWebViewScriptNotify` 替换了用于设置位置和获取图钉移动的 `postMessage` 交互。代码结构基本相同，因为在这种情况下，保留一些通用辅助函数仍然很有用（不过我们不必像使用 `postMessage` 时那样担心设置正确的源字符串）。

我们可以完全删除的一段代码是 html/map.html 中那个将 message 事件内容转换为函数调用的处理程序。这样的代码是不必要的，因为 invokeScriptAsync 会直接调用函数；只需再次注意，参数是作为单个字符串传递的，因此被调用的函数（比如 html/map.html 中的 pinLocation）需要处理这一点。

我们要特别查看的代码是新的 callWebviewScript 辅助函数，它取代了之前的 callIframeScript 函数。下面是新的核心代码：

```javascript
var op = webview.invokeScriptAsync(targetFunction, args);
op.oncomplete = function (args) { /* console output */ };
op.onerror = function (e) { /* console output */ };

//Don't forget this, or the script function won't be called!
op.start();
```

查看这段代码时，你可能会觉得奇怪的是，invokeScriptAsync 的返回值不是 promise，而是一个具有 complete 和 error 事件的 DOM 对象（当然，这些事件可以有多个订阅者）。此外，在你调用这个对象的 start 方法之前，操作实际上不会开始。这是怎么回事呢？嗯，请记住，webview 不是 WinRT 的一部分：它是应用宿主支持的原生 HTML 元素。因此它的行为像其他 HTML 元素和 API（比如 XMLHttpRequest），而不是 WinRT 对象。啊，生活中甜蜜的不一致！

那么，必须单独调用 start 的原因是，你必须确保在操作开始之前将 completed 和 error 处理程序附加到对象上，否则它们不会被调用。

幸运的是，将这样的操作包装在 promise 中并不太难。只需将上面的相同代码结构放入传递给 new WinJS.Promise 的初始化函数中，并在操作的 complete 和 error 事件中调用 complete 和 error 调度器（关于使用 WinJS.Promise，请参阅附录 A“揭秘 Promise”）：

```javascript
return new WinJS.Promise(function (completeDispatch, errorDispatch) {
    var op = webview.invokeScriptAsync(targetFunction, args);

    op.oncomplete = function (args) {
        //Return value from the invoked function (always a string) is in args.target.result
        completeDispatch(args.target.result);
    };

    op.onerror = function (e) {
        errorDispatch(e);
    };

    op.start();
});
```

这之所以可行，是因为 promise 初始化器在调用 start 之前附加了 completed/error 处理程序，而这些处理程序会调用相应的调度器。因此，如果你在 promise 已经完成后调用 then 或 done，它会立即调用你的 completed/error 处理程序。你不会错过任何东西！

对于此操作之外发生的错误（例如 targetFunction 无效），请确保使用 WinJS.ErrorFromName 创建错误对象，并通过使用 WinJS.Promise.wrapError 返回处于错误状态的 promise。你可以在 HereMyAm4（pages/home/home.js）中看到完整代码。

## 捕获 Webview 内容

webview 另一个真正使其与众不同的非常有用的功能是能够捕获其内容，这是使用 iframe 根本无法做到的。这可以通过三种方式实现。

首先是 src 属性。一旦 MSWebViewNavigationCompleted 触发，src 将包含 webview 所看到的内容的 URI。对于 Web 内容，这将是一个 http[s] URI，可以在浏览器中打开。本地内容（从字符串或应用数据文件加载）将以 ms-local-web 开头，可以使用 navigateToLocalStream 将其渲染到另一个 webview 中。请注意，在 MSWebViewNavigationCompleted 之前导航正在进行时，src 属性的状态是不确定的；在这些处理程序中请改用 uri 属性。

其次是 webview 的 captureSelectedContentToDataPackageAsync 方法，它直接反映用户在 webview 中所做的任何选择。数据包是此 API 的一部分，这一事实暗示了它的主要用途：共享契约。从用户的角度来看，你在应用中显示的任何 Web 内容实际上都是应用的一部分。因此，如果他们在那里做出选择并调用“共享”超级按钮，他们会期望共享的是其选中的数据，而此方法让你可以获取该选择的 HTML。当然，只要你想获取所选内容，就可以随时使用它——“共享”超级按钮只是潜在场景之一。

与 invokeScriptAsync 一样，captureSelectedContentToDataPackageAsync 的返回值同样是一个类似 DOM 的对象，具有 start 方法（别忘了调用它！）以及 complete 和 error 事件。如果你想将其包装在 promise 中，可以使用上一节中为 invokeScriptAsync 展示的相同结构。在这种情况下，你在 complete 处理程序中关心的结果（位于其 args.target.result 中）是一个 Windows.ApplicationModel.DataTransfer.DataPackage 对象，与我们在第 2 章中遇到“共享”超级按钮时相同。调用其 getView 方法将生成一个 DataPackageView，其 availableFormats 对象会告诉你它包含什么。然后你可以使用适当的 get* 方法（如 getHtmlFormatAsync）来检索选择数据本身。请注意，如果没有选择，args.target.result 将为 null，因此你需要对此进行防护。那么，下面是本章配套内容中 WebviewExtras 示例的场景 2 中的代码，它将选择从一个 webview 复制到另一个 webview，同时还展示了如何将该操作包装在 promise 中（js/scenario2js）：

~~~javascript
function captureSelection() {
    var source = document.getElementById("webviewSource");

    //wrap the capture method in a promise
    var promise = new WinJS.Promise(function (cd, ed) {
        var op = source.captureSelectedContentToDataPackageAsync();
        op.oncomplete = function (args) { cd(args.target.result); };
        op.onerror = function (e) { ed(e); };
        op.start();
    });

    //Navigate the output webview to the selection, or show an error
    var output = document.getElementById("webviewOutput");

    promise.then(function (dataPackage) {
        if (dataPackage == null) { throw "No selection"; }

        var view = dataPackage.getView();
        return view.getHtmlFormatAsync();
    }).done(function (text) {
        output.navigateToString(text);
    }, function (e) {
        output.navigateToString("Error: " + e.message);
    });
}
~~~

此示例的输出如图 4-3 所示。左侧是一个由 webview 托管的页面（我的博客），右侧是捕获的选择。请注意，捕获的选择是一种 HTML 剪贴板格式，它在来自 webview 的 HTML 之前顶部包含额外信息。如果你只需要提取纯 HTML，则需要剥离此前缀文本，直到 <!DOCTYPE html>。

一般来说，captureSelectedContentToDataPackageAsync 将生成 AnsiText、Text、HTML Format、Rich Text Format 和 msSourceUrl 格式，但不生成位图。为此，你需要使用第三种方法 capturePreviewToBlobAsync，它同样具有 start 方法以及 complete/error 事件。此捕获的结果（位于 complete 处理程序内的 args.target.result 中）是一个 blob 对象，对应 webview 显示区域内包含的任何内容。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_187_0.png)

图 4-3 WebviewExtras 示例的示例输出，显示从 webview 捕获的选择既包含有关该选择的信息，也包含 HTML 本身。
