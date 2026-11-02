
要添加到 DOM 的目标页面内容，以及要从当前页面移除的内容。

基本流程如下，图 3-4 也展示了该流程：

- 1. 创建一个大小合适的 `div`（通常是整个应用窗口）。
- 2. 调用 `WinJS.UI.Pages.render` 将目标 HTML 加载到该元素中（以及该页面唯一引用的任何脚本）。这是一个异步函数，返回一个 promise。稍后我们会看看 `render` 做了什么。
- 3. 当该加载（即渲染）完成时，将第 1 步创建的新元素附加到 DOM。
- 4. 从 DOM 中移除上一页的根元素。如果你在让出 UI 线程之前执行此操作，就永远不会同时看到两个页面显示在屏幕上。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_118_0.png)

**图 3-4** 在单个宿主（通常是 default.html）的上下文中执行页面导航，方法是替换/追加来自 page2.html 的内容并移除 page1.html 中的内容。通常，每个页面占据整个显示区域，但页面控件也可以轻松用于较小区域。

与一般的页面导航一样，你在这里仍可以自由地做任何想做的事，而在 Windows 8 的早期开发者预览版中，你能做的也只有这些！但随着开发者为 Windows 商店构建第一批应用，我们发现大多数人最终都在一遍又一遍地编写几乎相同的样板代码。看到这种模式后，出现了两段标准代码。一个是 WinJS 后退按钮控件 `WinJS.UI.BackButton`，它监听导航事件，并在适当时启用自身。另一个是名为 `PageControlNavigator` 的部件，由 Visual Studio 模板慷慨提供。好耶！

由于 PageControlNavigator 只是模板提供的代码，并不属于 WinJS，因此完全由你控制：你可以随意调整、修改或大改它。²³ 无论如何，由于你可能经常在自己的应用中使用 PageControlNavigator（以及后退按钮），让我们看看它在导航应用模板的上下文中是如何工作的。

**注意** 演示基本页面控件和导航以及处理会话状态的其他示例可在以下 SDK 示例中找到：App activate and suspend using WinJS（在页面控件中使用会话状态对象）、App activated, resume and suspend（前面已描述；展示使用挂起延迟并在终止后重启）以及 Navigation and navigation history（展示页面导航以及跟踪和操作导航历史）。实际上，几乎每个示例都使用页面控件在不同场景之间切换，因此你不缺可供借鉴的示例！

## 导航应用模板、PageControl 结构和 PageControlNavigator

在空白应用模板的基础上更进一步，导航应用模板演示了页面控件的基本用法。（更复杂的模板会进一步扩展导航。）如果在 Visual Studio 或 Blend 中使用此模板创建新项目，你将获得以下内容：

- **default.html** 包含一个容器 `div`，其中有一个 `PageControlNavigator` 控件指向 `pages/home/home.html`，作为应用的主页。
- **js/default.js** 包含应用的基本激活和状态检查点代码。
- **css/default.css** 包含全局样式。
- **pages/home** 包含用于“主页”内容的页面控件，由 `home.html`、`home.js` 和 `home.css` 组成。每个页面控件通常都有自己的标记、脚本和样式文件。请注意，页面控件的 CSS 样式在页面之间导航时会累积。请参阅本章后面的“页面特定样式”。
- **js/navigator.js** 包含 `PageControlNavigator` 类的实现。

要在此结构基础上构建，你可以使用 Visual Studio 中的页面控件项模板向应用添加其他页面。对于每个页面，我建议先在 `pages` 下创建一个特定文件夹，类似于默认项目结构中的 `home`。然后右键单击该文件夹，选择“添加”>“新建项”，再选择“页面控件”。这将在该文件夹中创建名称合适的 `.html`、`.js` 和 `.css` 文件。

现在让我们看看 default.html 的 body 部分（省略标准头部和被注释掉的 AppBar 控件）：

```html
<body>
    <div id="contenthost" data-win-control="Application.PageControlNavigator"
         data-win-options="{home: '/pages/home/home.html'}"></div>
</body>
```

这里我们只有一个名为 contenthost 的容器 div（名称可任意），在其中将 Application.PageControlNavigator 声明为自定义 WinJS 控件。（这就是 data-win-control 和 data-win-options 的用途，我们将在第 5 章看到。）通过它，我们指定一个选项来标识它应加载的第一个页面控件（/pages/home/home.html）。PageControlNavigator 将在激活处理程序对 WinJS.UI.processAll 的调用中实例化。

在 home.html 中，我们有一个页面控件的基本标记。下面是导航应用模板默认提供的主页，它几乎就是你从项模板添加新页面控件时得到的内容（当然，文件名不同）：

```html
<!DOCTYPE html>
<html>
<head>
    <!-- ... typical HTML header and WinJS references omitted -->
    <link href="/css/default.css" rel="stylesheet">
    <link href="/pages/home/home.css" rel="stylesheet">
    <script src="/pages/home/home.js"></script>
</head>
<body>
    <!-- The content that will be loaded and displayed. -->
    <div class="fragment homepage">
        <header aria-label="Header content" role="banner">
            <button data-win-control="WinJS.UI.BackButton"></button>
            <h1 class="titlearea win-type-ellipsis">
                <span class="pagetitle">Welcome to NavApp!</span>
            </h1>
        </header>
        <section aria-label="Main content" role="main">
            <p>Content goes here.</p>
        </section>
    </div>
</body>
</html>
```

带有 *fragment* 和 *homepage* CSS 类的 div 与 header 一起，创建了一个具有标准轮廓的页面，以及一个 WinJS.UI.BackButton 控件，该控件自动绑定键盘、鼠标和触摸事件，并在没有可返回内容时再次保持隐藏。（它是不是很贴心！）你需要做的就是自定义 *h1* 元素内的文本和 *section* 内的内容，或者直接用你想要的标记替换整个部分。（顺便说一句，尽管每个页面控件中都引用了 WinJS 文件，但它们实际上不会重新加载；它们在这里是为了让你能在 Blend 中编辑独立的页面控件。）

提示 看似指向 CSS 和 JavaScript 文件的相对路径，其开头的 / 实际上会创建从包根目录开始的绝对引用。如果省略该 /，有很多时候——尤其是在使用路径控件时——相对路径并不是你所期望的，应用也无法正常工作。一般来说，除非你确实知道自己需要相对路径，否则请使用开头的 /。

实际页面控件的定义在 pages/home/home.js 中；默认情况下，模板只提供最低限度的内容：

```javascript
(function () {
  "use strict";

  WinJS.UI.Pages.define("/pages/home/home.html", {
    // This function is called whenever a user navigates to this page. It
    // populates the page elements with the app's data.
    ready: function (element, options) {
      // TODO: Initialize the page here.
    }
  });
})();
```

最重要的部分是 WinJS.UI.Pages.define，它将基于项目的 URI（页面控件标识符，始终以 / 开头，表示项目根目录）与一个包含页面控件方法的对象关联起来。请注意，define 的特性允许你在多个位置定义页面的不同成员。使用相同 URI 多次调用 WinJS.UI.Pages.define 会向现有定义添加成员，并替换已存在的成员。

提示 请注意，如果 URI 中有拼写错误，导致 define 中的 URI 与页面的实际路径不匹配，页面将不会加载，但不会出现异常或其他可见错误。你会被弄得莫名其妙，不知道哪里出了问题！因此，如果你的页面没有按你预期的方式加载，请仔细检查 URI 和文件路径，确保它们完全匹配。

对于使用页面控件项模板创建的页面，结构中会多出几个方法（省略了一些注释；在此示例中，page2 是在 pages/page2 文件夹中创建的）：

```javascript
(function () {
  "use strict";

  WinJS.UI.Pages.define("/pages/page2/page2.html", {
    ready: function (element, options) {
    },

    unload: function () {
      // TODO: Respond to navigations away from this page.
    }

    updateLayout: function (element) {
      // TODO: Respond to changes in layout.
    },
  });
})();
```
