

最后，如果出于某种原因你需要知道 Flyout 何时加载完成，请在 `document.body` 上监听 `DOMNodeInserted` 事件：

```js
document.body.addEventListener("DOMNodeInserted", insertionHandler, false);
```

## Flyout 示例

Flyout 控件与其他 WinJS 控件一样，通过 `data-win-control` 和 `data-win-options` 属性创建，并由 `WinJS.UI.process/processAll` 处理。内容相对固定的 Flyout 通常会在标记中声明，这样你就可以对 Flyout 内元素的特定属性使用数据绑定。而对那些内容高度动态的 Flyout，可以直接通过代码使用 `new WinJS.UI.Flyout(<element>, <options>)` 创建，而且你当然可以随时更改其子元素。它们都只是 DOM 的一部分！（我是不是又在重复自己？）

就像我前面说过的（显然我又在重复），`Flyout` 控件可以包含任意 HTML，并一如既往地使用 CSS 设置样式。示例中场景 1 的 Flyout 在 `html/confirm-action.html` 中如下所示（略有删减）：

```html
<div id="confirmFlyout" data-win-control="WinJS.UI.Flyout" aria-label="{Confirm purchase flyout}">
    <div>Your account will be charged $252.</div>
    <button id="confirmButton">Complete Order</button>
</div>
```

场景 2 中的登录 Flyout 与此类似，它甚至使用了一个 HTML 表单，将 Login 按钮与 Enter 键关联起来（`html/collect-information.html`）：

```html
<div id="loginFlyout" data-win-control="WinJS.UI.Flyout" aria-label="{Login flyout}">
    <form onsubmit="return false;">
        <p>
            <label for="username">Username: <br /></label>
            <span id="userNameError" class="error"></span>
            <input type="text" id="username" />
        </p>
        <p>
            <label for="password">Password: <br /></label>
            <span id="passwordError" class="error"></span>
            <input type="password" id="password" />
        </p>
        <button id="submitLoginButton">Login</button>
    </form>
</div>
```

Flyout 通过调用它的 `show` 方法显示。例如，在场景 1 中，按钮的 `click` 事件被连接到 `showConfirmFlyout` 函数（`js/confirm-action.js`），并将 Buy 按钮作为锚点元素传入。处理 Complete Order 按钮只需要通过附加到该元素上的 `click` 处理程序，在这里我们要确保调用 `hide` 以编程方式关闭 Flyout。最后，使用 `afterHide` 事件来检测 Flyout 是否已关闭：

```javascript
var bought;

var page = WinJS.UI.Pages.define("/html/confirm-action.html", {
    ready: function (element, options) {
        document.getElementById("buyButton").addEventListener("click",
            showConfirmFlyout, false);
        document.getElementById("confirmButton").addEventListener("click",
            confirmOrder, false);
        document.getElementById("confirmFlyout").addEventListener("afterhide",
            onDismiss, false);
    }
});

function showConfirmFlyout() {
    bought = false;
    var buyButton = document.getElementById("buyButton");
    document.getElementById("confirmFlyout").winControl.show(buyButton);
}

// When the Buy button is pressed, hide the flyout since the user is done with it.
function confirmOrder() {
    bought = true;
    document.getElementById("confirmFlyout").winControl.hide();
}

// On dismiss of the flyout, determine if it closed because the user pressed the buy button.
// If not, then the flyout was light dismissed.
function onDismiss() {
    if (!bought) {
        // (Sample displays a dismissal message on the canvas)
    }
}
```

**提示** 若要在 Flyout 中创建默认按钮，请使用 <input type="submit"> 元素。但要确保在 Flyout 未显示时，它不会抢走其他按钮的 Enter 键行为。

场景 2 中登录控件的处理方式基本相同，只是额外添加了一些代码，以确保同时提供用户名和密码。如果没有输入完整，Login 按钮的处理程序会显示内联错误，并将焦点设置到相应的输入字段：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_494_0.png)

由于场景 2 的 Flyout 稍大一些，在 1366x768 的显示环境中（例如模拟器），`auto` 作为默认的 `placement` 值会让 Flyout 出现在触发它的按钮下方。该按钮上方没有足够的空间。因此，可以尝试在调用 `show` 时把 `placement` 设置为 `top`：

```javascript
function showLoginFlyout() {
    // ...
    document.getElementById("loginFlyout").winControl.show(loginButton, "top");
}
```

然后你会看到，由于整体控件元素太短，Flyout 出现了滚动条：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_494_1.png)

我前面用过的那个词是什么来着？"lock"？

继续往下，场景 3 同样在标记中声明了一个 Flyout，其中包含一些 `label`、`select` 和 `input` 控件。不过，它在 JavaScript 中监听后者的 change 事件，并将新的值应用到应用画布上的输出元素：

```javascript
var page = WinJS.UI.Pages.define("/html/change-settings.html", {
    ready: function (element, options) {
        // ...
        document.getElementById("textColor").addEventListener("change", changeColor, false);
        document.getElementById("textSize").addEventListener("change", changeSize, false);
    }
});
// Change the text color
function changeColor() {
    document.getElementById("outputText").style.color =
        document.getElementById("colorColor").value;
}

// Change the text size
function changeSize() {
    document.getElementById("outputText").style.fontSize =
        document.getElementById("textSize").value + "pt";
}
```

如果这个 Flyout 有一个 Apply 按钮，而不是立即应用更改，那么它的 click 处理程序可以获取当前的选项和滑块值，并像 `changeColor` 和 `changeSize` 那样使用它们。

最后，在场景 4 中，我们看到一个带标题的 Flyout。这里的标题只是标记中一段较大的文本；Flyout 控件本身并没有单独的标题概念。

```html
<div id="moreInfoFlyout" data-win-control="WinJS.UI.Flyout" aria-label="More info flyout">
    <div class="win-type-x-large">Lorem Ipsum</div>
    <div>
        Lorem Ipsum is text used as a placeholder by designers...
    </div>
</div>
```

最后一个示例的重点在于说明：与传统的桌面对话框不同，Flyout 通常不需要标题，因为它已经在应用内部拥有了上下文。桌面应用中的对话框需要标题，是因为标题会与其它应用一起出现在任务切换界面中。

**提示** 如果你发现 Flyout 触发的 beforeShow、aftershow、beforehide 或 afterhide 事件被传播到了包含它的应用栏或导航栏（它们使用相同的事件名称），请在 Flyout 的处理程序中调用 `eventArgs.stopPropagation()`。

## 菜单与菜单命令

`WinJS.UI.Menu` 控件与更通用的 Flyout 之间的区别在于：菜单要求其所有子元素都是 `WinJS.UI.MenuCommand` 对象，这类似于应用栏的标准命令布局要求使用 AppBarCommand 对象（如果声明了其他内容，则不会实例化）。菜单控件与其他 Flyout 之间的其他共同特征包括：

- show 和 hide 方法。
- `getCommandById`、`showCommands`、`hideCommands` 和 `showOnlyCommands`，以及 `commands` 属性，这意味着你可以使用与应用栏部分中“Showing, Hiding, Enabling, and Updating Commands”讨论过的相同策略来管理命令，包括使用 JSON 数组而不是离散元素来指定命令。
- `beforeshow`、`aftershow`、`beforehide` 和 `afterhide` 事件。
- `anchor`、`alignment` 和 `placement` 属性。

菜单的外观还有两种样式，即 `win-menu` 和 `win-command`，正如我们所见，它们可用于为整个菜单以及单个文本命令创建更具体的选择器。

`MenuCommand` 对象与 `AppBarCommand` 对象也非常相似。二者共享许多相同的属性：`id`、`label`、`type`（字符串：`button`、`toggle`、`flyout` 或 `separator`）、`disabled`、`extraClass`、`flyout`、`hidden`、`onclick` 和 `selected`。菜单命令没有图标、分区和工具提示，但你可以从 `type` 中看出，菜单项可以是按钮（包括纯文本项）、可勾选项、分隔符，也可以是另一个 Flyout。在后一种情况下，二级菜单会替换一级菜单，而不是并排显示。说实话，我还没在实际应用里见过使用二级菜单的，不过控件确实支持这种用法！

我们已经看到了如何从应用栏命令使用 Flyout 菜单，这包含在 HTML Flyout 控件示例的场景 6 中（请参阅前面的“Command Menus”部分）。另一个主要用途是提供类似从头元素下拉的菜单，这包含在场景 5 中。这里（请参阅 `html/header-menu.html`）的标准设计是，在页头末尾放置一个向下箭头符号（`&#xe099`）：

~~~html
<header aria-label="Header content" role="banner">
    <button class="win-backbutton" aria-label="Back"></button>
    <div class="titlearea win-type-ellipsis">
        <button class="titlecontainer">
            <h1>
                <span class="pagetitle">Music</span>
                <span class="chevron win-type-x-large">&#xe099</span>
            </h1>
        </button>
    </div>
</header>
~~~

请注意，整个页头都包裹在一个按钮中，因此它的 `click` 处理程序可以通过 `show` 显示菜单：

~~~javascript
document.querySelector(".titlearea").addEventListener("click", showHeaderMenu, false);
~~~

~~~javascript
function showHeaderMenu() {
    var title = document.querySelector("header .titlearea");
    var menu = document.getElementById("headerMenu").winControl;
    menu.anchor = title;
    menu.placement = "bottom";
    menu.alignment = "left";
    menu.show();
}
~~~

当你点击页头的任意位置时，Flyout（在 `html/header-menu.html` 中定义为 `headerMenu`）就会出现，而不只是在箭头处点击，因为那只是页头文本中的一个字符：

