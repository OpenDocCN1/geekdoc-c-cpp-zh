

管理演示文稿和媒体。虽然这些功能*可以*放在同一应用视图的同一个布局中，但并非必须如此。将它们作为独立视图——这意味着它们运行在不同的线程上，只能通过文件系统共享数据——用户便可以根据需要将它们与其他应用（例如用于客户调研的 Web 浏览器和电子邮件应用）并排放置。

使用多个视图需要注意的是，它们运行在不同的线程上，因此各自拥有独立的脚本上下文。视图之间只能通过`postMessage`调用互相通信（就像我们之前在本地上下文与 Web 上下文之间通信时所用的方式），但也可以通过彼此共享的 appdata 设置和/或文件交换数据。

视图通过`MSApp.createNewView` API 创建。该 API 由应用宿主提供，而不是 WinRT，因为它专用于使用 HTML 和 JavaScript 编写的应用。传递给此方法的唯一参数是一个字符串，其中包含要用于新视图的包内 HTML 页面的`ms-appx` URI（只允许使用`ms-appx` URI，这意味着视图在本地上下文中运行）。当然，该 HTML 文件可以引用自身所需的样式表和脚本（包括 WinJS）。即使视图尚不可见，所有这些内容也会在调用`createNewView`时加载。过程中会触发`DOMContentLoaded`等常见 DOM 事件，你也可以像往常一样使用`WinJS.Application`事件（前提是调用`app.start()`来处理队列中的事件）。

`createNewView`返回的`MSAppView`对象具有唯一的`viewId`属性，可用于标识该视图；它还具有`postMessage`和`close`方法。应用显然会使用后者来关闭视图。在辅助视图中，它会像往常一样通过`window.onmessage`事件接收消息。新视图也可以调用`window.close`来关闭自身，用户还可以通过触摸或鼠标手势，或按 Alt+F4 来关闭视图。要将数据发送回应用，视图会调用`MSApp.getViewOpener`来获取应用主视图的`MSAppView`对象；调用该对象的`postMessage`方法会在主视图中触发`window.onmessage`事件。这些关系如图 8-7 所示。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_424_0.png)

**图 8-7** 主视图通过`MSApp.createNewView`创建辅助视图。辅助视图通过`MSApp.getViewOpener`获取主视图的引用。这两种情况下返回的都是`MSAppView`对象，调用其`postMessage`方法即可向另一个视图发送消息。

先说明一点：如果辅助视图通过`window.close`关闭自身，应用不会收到任何类型的事件。因此，辅助视图通常会使用`postMessage`通知应用自己即将关闭。此时，视图还应订阅`ApplicationView.onconsolidated`事件，以检测用户直接关闭视图的情况，并向应用发送消息。稍后我们会看到一个示例。

现在，创建新视图并不会让它实际显示出来——视图的 HTML、CSS 和 JavaScript 都会加载并运行，但屏幕上不会出现任何内容。要显示视图，需要使用两个 API 之一：`ProjectionManager`或`ApplicationViewSwitcher`，两者都位于`Windows.UI.ViewManagement`中。

`ProjectionManager`适用于全屏场景，并且仅与单个辅助视图配合使用。首先，它的`projectionDisplayAvailable`属性会告知你是否支持投影；配合`projectionDisplayAvailableChanged`事件，你可以用它在应用中启用投影功能。要显示视图，需要将其`viewId`以及主视图的 ID（通过`ApplicationView.getForCurrentView().id`获取）传递给`startProjectingAsync`。之后，可以调用`stopProjectingAsync`关闭视图，调用`swapDisplaysForViewAsync`执行其名称所示的操作。

简单示例请参阅本章配套内容中的 SimpleViewProjection 示例。启动时，它会获取主视图和`ProjectionManager`（js/default.js）：

```javascript
var view = vm.ApplicationView.getForCurrentView();
var projMan = vm.ProjectionManager;
```

示例中的 Start 按钮会根据`ProjectionManager`的状态启用或禁用。

```javascript
btnStart.addEventListener("click", startProjection);
```

```javascript
projMan.onprojectiondisplayavailablechanged = function () {
    checkEnableProjection();
}

function checkEnableProjection() {
    btnStart.disabled = !projMan.projectionDisplayAvailable;
}
```

单击 Start 时，应用会创建视图并开始投影，同时使用两个视图的 ID：

```javascript
viewProjection = MSApp.createNewView("ms-appx:///projection/projection.html");

projMan.startProjectingAsync(viewProjection.viewId, view.id).done(function () {
    // enable/disable buttons
});
```

其他按钮会调用`stopProjectingAsync`和`swapDisplaysForViewAsync`，还有一些代码会根据需要有选择地启用界面。另有一个按钮会通过`postMessage`将当前时间发送到投影视图。

```javascript
function sendMessage() {
    var date = new Date();
    var timeString = date.getHours() + ":" + date.getMinutes() + ":" + date.getSeconds()
        + ":" + date.getMilliseconds();
    var msgObj = { text: timeString };
    viewProjection.postMessage(JSON.stringify(msgObj),
        document.location.protocol + "//" + document.location.host);
}
```

投影页面位于 projection/projection.html，其关联文件包括 .css 和 .js 文件。在激活处理程序中，它会获取打开方视图，并监听 consolidated 事件（js/projection.js）：

```javascript
var opener = MSApp.getViewOpener();

var thisView = Windows.UI.ViewManagement.ApplicationView.getForCurrentView();
thisView.onconsolidated = function () {
    sendCloseMessage();
}
```

其中，sendCloseMessage 是一个只通过`postMessage`发送“close”标记的函数，以便主应用重置其界面。单击投影视图中的 Close 按钮时也会执行同样的操作，随后调用 window.close。

另一个示例请参阅 SDK 中的 Projection 示例。它基本上与上面的简单示例执行相同的操作，只是增加了一些设置视图属性（例如标题）的内容。不过，我没有展示该示例中的代码，因为它将`createNewView`和`getViewOpener`等基本 API 调用深藏在名为 ProjectionView.ViewManager（用于主视图）和 ProjectionView.ViewLifeTimeControl（用于辅助视图）的辅助类中。这些类（位于 js/viewLifetimeControl.js）围绕 consolidated 和可见性变化等各种事件提供了一个小型框架，并在主视图与辅助视图之间建立了消息协议。它还会对辅助视图进行引用计数以控制其生命周期，并确保辅助视图关闭时通知主视图。如果你开始使用多个视图，这类功能确实会派上用场，但作为 API 入门示例，它有点过于复杂了！

SDK 中的 Multiple Views 示例也使用了同一个小型框架，该示例演示了`ApplicationViewSwitcher`类的方法。这些方法的名称都相当冗长：

| 方法 | 说明 |
|---|---|
| switchAsync(id)（3 个重载） | 切换到与当前视图处于同一空间中的指定视图。不过，如果目标视图已显示在屏幕的其他位置，此操作只会将焦点切换到该视图。可以使用`ApplicationViewSwitchingOptions`中的值自定义切换效果：default（标准切换效果）、skipAnimation（不使用切换效果）或 consolidateViews（关闭当前视图）。 |
| tryShowAsStandaloneAsync（3 个重载） | 在当前视图旁显示新视图，并通过`ViewSizePreference`中的选项确定新视图和当前视图的期望状态：default、useLess、useMore、useMinimum、useNone。你可以在示例的场景 1 中试验这些不同选项。 |
| disableShowingMainViewOnActivation | 阻止应用的主视图在后续激活时显示，也就是说，在适合直接激活应用并进入辅助视图时使用此方法。除非调用此方法，否则默认总会显示主视图。示例的场景 2 展示了这一点，实际调用位于 js/default.js 中。 |

