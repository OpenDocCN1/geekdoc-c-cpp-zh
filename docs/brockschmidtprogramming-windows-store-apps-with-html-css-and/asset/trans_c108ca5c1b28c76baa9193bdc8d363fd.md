
| 属性 | 类型 | 描述 |
|---|---|---|
| `previousExecutionState` | `ApplicationExecutionState` | 此激活之前应用的状态。值为 `notRunning`、`running`、`suspended`、`terminated` 和 `closedByUser`。处理 `terminated` 情况最常见，因为在这种情况下，你希望恢复之前保存的会话状态（参见“应用生命周期转换事件”）。 |
| `splashScreen` | `SplashScreen` | 包含一个 `onDismissed` 事件，用于系统启动屏幕被关闭时，以及一个 `imageLocation` 属性（`Windows.Foundation.Rect`），其中带有启动屏幕图像显示位置的坐标。关于其用法，请参见附录 B“WinJS 附加内容”中的“扩展启动屏幕”。 |

其他属性为激活提供相关数据。例如，`launch` 提供来自辅助磁贴的 `title` 和 `arguments`（见第 16 章）。`search` 类型（第二常用的类型）提供 `queryText` 和 `language`，`protocol` 类型提供 `uri`，等等。我们将看到如何在适当的上下文中使用其中许多属性，有时它们适用于与 `default.html` 完全不同的页面。模板中包含的内容（以及我们已为像 Here My Am! 这样的应用使用的内容）主要用于处理从应用磁贴正常启动或在 Visual Studio 调试器中启动的情况。

## WinJS.Application 事件

`WinJS.Application` 并不仅仅关注激活——它的用途是集中来自多个不同来源的事件，并将它们转换为自身的事件。同样，这使应用能够从单一来源监听事件（既可以通过 `addEventListener(<events>)` 或 `on<event>` 属性分配处理程序；两者都受支持）。以下是这些事件及其触发时机的完整说明（如果事件已排队，则会在你调用 `WinJS.Application.start` 期间触发）：

- `loaded` 在本地和 Web 上下文中为 `DOMContentLoaded` 排队。[^19] 它在 `activated` 之前触发。
- `activated` 在本地上下文中为 `Windows.UI.WebUI.WebUIApplication.onactivated` 排队（该事件在 `window.onload` 之后触发）。在 WinRT 不适用的 Web 上下文中，它改为排队给 `DOMContentLoaded`（其中启动类型将为 `launch`，并且 `previousExecutionState` 被设置为 `notRunning`）。
- `ready` 在 `loaded` 和 `activated` 之后排队。这是激活序列中的最后一个。
- `error` 如果在调度另一个事件时发生异常，则触发。（如果错误未在此处处理，则会传递给 `window.onerror`。）
- `checkpoint` 当应用应保存其从之前的 `terminated` 状态重新启动所需的会话状态时触发。它响应文档的 `beforeunload` 事件和 `Windows.UI.WebUI.WebUIApplication.onsuspending` 两者而触发。
- `unload` 在 `checkpoint` 事件触发后，也会为 `beforeunload` 触发。
- `settings` 响应 `Windows.UI.ApplicationSettings.SettingsPane.oncommandsrequested` 而触发。（见第 10 章“状态的故事，第 1 部分”。）

[^19]: 还有 `WinJS.Utilities._ready`，通过它可以专门为 `DOMContentLoaded` 设置回调。事实上，这在 WinJS 内部用于保证对 `WinJS.UI.processAll` 的任何调用都在 `DOMContentLoaded` 之后处理。

我认为你通常会发现 `WinJS.Application` 是应用中的一个有用工具，并且它还提供了一些更多功能，如 `WinJS.Application` 页面上所述。例如，它提供 `local`、`temp`、`roaming` 和 `sessionState` 属性，这些属性有助于管理状态。我们已经在第 2 章中稍微了解了 `local`；稍后在第 10 章中我们将看到更多内容。

其他部分是 `queueEvent` 和 `stop` 方法。`queueEvent` 方法将事件放入队列，在现有队列清空后，该事件将被分派给你在 `WinJS.Application` 对象上设置的任何监听器。事件仅通过字符串标识，因此你可以用任意名称排队事件，并在应用的其他任何地方用相同名称调用 `WinJS.Application.addEventListener`。这使得集中自定义事件变得容易，你可以在启动期间和执行过程中的其他时间点调用这些事件，而无需为此创建单独的全局函数。它还是一种强大的手段，通过它，分别定义的独立组件可以引发事件，这些事件会被聚合到单个处理程序中。（有关使用 `queueEvent` 的示例，请参见 `App model sample` 的场景 2。）

至于 `stop`，它用于帮助进行单元测试，以便你可以模拟不同的激活序列，而无需重新启动应用，也无需在应用重新启动时以某种方式重新创建一组特定条件。当你调用 `stop` 时，WinJS 会移除其监听器，清空任何现有事件队列，并清空 `sessionState` 对象，但应用继续运行。然后，你可以调用 `queueEvent` 用你喜欢的任何事件填充队列，然后再次调用 `start` 来处理该队列。此过程可以根据需要重复任意多次。

## 激活延迟与 setPromise

如前文“激活事件序列”所述，一旦你从 `WebUIApplication.onactivated`（或 `WinJS.Application.onactivated`）的处理程序返回，Windows 就会假定你的主页已准备好，并且可以关闭默认启动屏幕。对于 `WebUIApplication.onsuspending`（进而 `WinJS.Application.oncheckpoint`）也是如此：Windows 假定一旦处理程序返回，就可以挂起应用。更一般地说，`WinJS.Application` 假定一旦你从当前事件返回，它就可以处理队列中的下一个事件。

如果你的处理程序需要执行一个或多个异步操作（例如 HTTP 请求），而这些操作的响应对于你的主页至关重要，那么情况就会变得棘手。由于这些操作在其他线程上运行，你最终会在操作仍处于待处理状态时从处理程序返回，这可能导致主页在尚未准备好之前就显示，或者应用在尚未完成状态保存之前就被挂起。这可不是你希望发生的情况！（当然，你可以发出其他次要请求，在这种情况下，它们在主页启动后完成是没问题的——始终避免因为非必要事项而阻塞主页。）

因此，你需要一种方法来告诉 Windows 和 WinJS 推迟它们的默认行为，直到你最关键的异步工作完成。WinRT 中为此提供的机制称为延迟（deferral），而我们在 WinJS 中看到的 setPromise 方法与之相关联。

在 WinRT 层面，传给 WebUIApplication.onactivated 的 args 包含一个名为 getDeferral 的小方法（严格来说是 `Windows.UI.WebUI.ActivatedOperation.getDeferral()`）。此函数返回一个 deferral 对象，该对象包含一个 complete 方法。通过调用 getDeferral()，你告诉 Windows 保持系统启动屏幕显示，直到你调用 complete（受下文“优化启动时间”中所述的 15 秒超时限制）。代码如下：

```javascript
// In the activated handler
var activatedDeferral = Windows.UI.WebUI.ActivatedOperation.getDeferral();

someOperationAsync().done(function () {
    // After initialization is complete
    activatedDeferral.complete();
});
```

同样的机制也用于 WinRT 的其他地方。你会发现 WebUIApplication.onsuspending 的 args 也有一个 getDeferral 方法，因此你可以将挂起推迟到异步操作完成之后。我们在第 2 章中看到的用于处理“共享”超级按钮的 DataTransferManager.ondatarequested 事件也是如此。在使用“搜索”超级按钮、打印、后台任务、Play To 和状态管理时，你也会遇到 deferral，我们将在后续章节中看到。简而言之，只要事件处理程序中可能需要执行异步工作，你就会发现 getDeferral。

在 WinJS 内部，每当 WinJS 为 WinRT 事件提供包装器时（例如 WinJS.Application.onactivated），它还会将 deferral 机制包装成一个单独的 setPromise 方法，你可以在传递给相关事件处理程序的 args 对象上找到该方法。由于在这些事件处理程序中执行异步操作时需要 deferral，并且由于 JavaScript 中的异步操作始终用 promise 表示，因此 WinJS 提供一种通用方式将 deferral 与 promise 的完成关联起来是合理的。这正是 setPromise 所做的。

事实上，无论你是否需要，WinJS 都会自动请求一个 deferral。如果你向 setPromise 提供一个 promise，WinJS 将为其附加一个完成处理程序，并在适当的时候调用 deferral 的 complete。否则，WinJS 将在你的事件处理程序返回时调用 complete。

你可以在传递给 WinJS.Application 的 loaded、activated、ready、checkpoint 和 unload 事件的 args 上找到 setPromise。同样，setPromise 既会推迟 Windows 对 WinRT 事件的默认行为，也会告诉 WinJS.Application 推迟处理其队列中的下一个事件。例如，这允许你将 activated 事件延迟到 loaded 中的异步操作完成之后。

现在我们可以看看之前看到的激活代码中 setPromise 的用途：

```javascript
var app = WinJS.Application;

app.onactivated = function (args) {
    if (args.detail.kind === activation.ActivationKind.launch) {
```
