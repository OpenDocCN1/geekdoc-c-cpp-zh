
场景 5（pages/verticallayout.html）接着再进一步，通过将 Hub 控件切换为垂直方向来处理 320px 的窄视图（并在 pages/verticallayout.css 中使用适当的样式）。处于垂直方向时，Hub 只是将各个节垂直排列，示例在此状态下也处理语义缩放。为了说明这一切，图 8-13 展示了应用 500px 宽的视图（此时仍使用水平方向），然后是 320px 的窄视图，最后是窄视图的缩小视图。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_440_0.png)

图 8-13 场景 5 在 500px 宽（左）、320px 宽且采用垂直 Hub 布局（中），以及 320px 宽且使用垂直 ListView 的缩小视图（右）。

处理这一点所需的唯一一段代码是 `updateHubLayout` 函数，它在 `window.onresize` 时被调用（pages/verticallayout.js；该函数的参数分别是 Hub 和缩小后的 ListView 控件）：

```javascript
function updateHubLayout(hub, listview) {
    if (document.body.clientWidth < 500) {
        if (hub.orientation !== WinJS.UI.Orientation.vertical) {
            hub.orientation = WinJS.UI.Orientation.vertical;
            listview.layout = new WinJS.UI.ListLayout();
        }
    }
    else {
        if (hub.orientation !== WinJS.UI.Orientation.horizontal) {
            hub.orientation = WinJS.UI.Orientation.horizontal;
            listview.layout = new WinJS.UI.GridLayout();
        }
    }
}
```

这里的代码会在窗口宽度低于 500px 时更改方向。在许多情况下，你可能希望在宽高比变为纵向时进行切换，这只需将 `if` 语句改为与 `document.body.clientHeight` 比较，并将 CSS 媒体查询改为检查方向变化而不是宽度即可：

```javascript
// pages/verticallayout.js
if (document.body.clientWidth < document.body.clientHeight)
```

```css
/* pages/verticallayout.css */
/* Original was @media (min-width: 320px) and (max-width:499px) */
@media (orientation: portrait)
```

## Hub 控件样式

为 Hub 控件设置样式，就是为其各个部分设置样式，正如我们在前面章节中对 ListView、FlipView 和 ItemContainer 控件所看到的那样。为了清晰地展示 `div` 结构，类似下面这样的标记：

```html
<div data-win-control="WinJS.UI.Hub">
    <div class="hero" data-win-control="WinJS.UI.HubSection"
        data-win-options="{header: 'Hero'}"></div>
    <div class="section1" data-win-control="WinJS.UI.HubSection"
        data-win-options="{header: 'Images', isHeaderStatic: true}"></div>
</div>
```

会变成更深的 `div` 层级，并分配各种 `win-hub-*` 类（以及一些其他元素）：

```html
<!-- The root element (win-vertical if vertically oriented) -->
<div class="win-hub win-horizontal">
    <!-- The panning region with snap points for the sections -->
    <div class="win-hub-viewport">
        <!-- The container for sections -->
        <div class="win-hub-surface">
            <!-- hero section -->
            <div class="hero win-hub-section">
                <!-- header -->
                <div class="win-hub-section-header">
                    <button class="win-hub-section-header-tabstop
                        win-hub-section-header-interactive"></button>
                    <h2 class="win-hub-section-header-content">Hero</h2>
                    <span class="win-hub-section-header-chevron"></span>
                </div>
                <!-- content -->
                <div class="win-hub-section-content">
                </div>
            </div>

            <!-- section1 -->
            <div class="section1 win-hub-section">
                <!-- same structure for header and content but without
                     win-hub-section-header-interactive for non-invocable header -->
            </div>
        </div>
    </div>
</div>
```

最常见的需要与默认样式不同地设置样式的类会是 `win-hub-section`、`win-hub-section-header` 和 `win-hub-section-content`，用于更改外边距和/或内边距。`win-hub-section-header-tabstop` 类标识标题中的按钮元素，无论它是否可交互。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_442_0.png)

由于 `win-hub-surface` 的背景默认是透明的，你可以在 `win-hub-viewport` 上设置背景颜色使其透出，也可以使用一张会固定在各节后面的背景图像。通常你会使用低对比度的图像（如“开始”屏幕上的那些），以免分散对内容其余部分的注意力。

除此之外，各节中的内容当然完全由你掌控，因此你可以按自己的意愿为所有这些内容设置样式。

## 使用 CSS 网格

从第 2 章开始，我们就已经将 CSS 网格用于许多目的。就个人而言，我喜欢网格模型，因为它能如此轻松地实现元素的相对放置，并轻松缩放到不同的屏幕尺寸。

由于本书的重点是 Windows 平台的特定内容，我将把全部细节留给 W3C 规范 http://www.w3.org/TR/css3-grid-layout/ 和 http://dev.w3.org/csswg/css3-grid-align/ 来解释。这些规范是理解行和列如何确定大小的重要参考资料，尤其是当一些行列声明为固定大小、一些根据内容确定大小、另一些声明为填充剩余空间时。其中的细微差别很多！

由于在撰写本文时这些规范本身仍处于草案阶段，因此最好确切了解 Store 应用所使用的 HTML/CSS 引擎实际支持这些规范的哪些部分。

对于包含网格的元素，支持的样式很简单。首先使用 `-ms-grid` 和 `-ms-inline-grid` 显示模型（`display:` 样式）。我们稍后会再讨论 `-ms-inline-grid`。

其次，在网格元素上使用 `-ms-grid-columns` 和 `-ms-grid-rows` 来定义其排列方式。如果未指定，默认是一列一行。支持诸如 `-ms-grid-columns: (1fr)[3];` 这样的重复语法，当你有一系列重复的行或列（出现在括号内）时，它最有用。作为示例，以下所有写法都是等效的：

```
    -ms-grid-rows:10px 10px 10px 20px 10px 20px 10px;
    -ms-grid-rows:(10px)[3] (20px 10px)[2];
    -ms-grid-rows:(10px)[3] (20px 10px) 20px 10px;
    -ms-grid-rows:(10px)[2] (10px 20px)[2] 10px;
```

如何定义行和列才是真正有趣的部分，因为你可以使用以下值将一些设为固定、一些设为灵活，还有一些根据内容确定大小。再次说明，关于涉及 `max-content`、`min-content`、`minmax`、`auto` 和 `fit-content` 说明符，以及以 `px`、`em`、`%` 和 `fr` 为单位指定的值的细微差别，请参阅规范。Windows Store 应用还可以使用 `vh`（视口高度）和 `vw`（视口宽度）作为单位。

现在在网格内部，子元素使用以下样式被放置在特定的行和列中，并具有特定的对齐、跨行/列和分层特性：

- `-ms-grid-column` 标识子元素在网格中的列（从 1 开始计数）。
- `-ms-grid-row` 标识子元素在网格中的行（从 1 开始计数）。
- `-ms-grid-column-align` 和 `-ms-grid-row-align` 指定子元素在网格单元格中的放置位置。允许的值为 `start`、`end`、`center` 和 `stretch`（默认）。
- `-ms-grid-column-span` 和 `-ms-grid-row-span` 表示子元素跨一行或多行/列。
- `-ms-grid-layer` 控制网格项如何重叠。这类似于用于定位元素的 `z-index` 样式。由于网格子元素不是直接用 CSS 定位，而是根据网格进行定位，因此 `-ms-grid-layer` 允许单独控制。

务必注意，行和列样式是从 1 开始计数的，而不是从 0 开始。真的要重新调整你面向 JavaScript 的思维来记住这一点，因为如果你在从 0 开始的数组中跟踪子元素，就需要做一点转换。

另外，在 JavaScript 中将这些 `-ms-grid*` 样式作为属性引用时，去掉连字符并改为驼峰式，如 `msGrid`、`msGridColumns`、`msGridRowAlign`、`msGridLayer` 等。
