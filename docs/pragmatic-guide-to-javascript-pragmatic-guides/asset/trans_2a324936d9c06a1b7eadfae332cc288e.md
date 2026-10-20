

## 13 制作低调的弹出窗口

无论你使用的是“真正的”弹出窗口（独立窗口）还是伪弹出窗口（当前页面上的元素，样式模拟窗口外观），问题都一样：对于无法打开窗口（或不想打开窗口）的用户，你如何提供对这些内容的访问？想想禁用窗口打开、屏幕阅读器、搜索引擎等等。

唯一的方法就是：让链接真实地指向弹出窗口的内容，然后在此基础上渐进增强。

如果你的内容旨在作为伪弹出窗口（可能也通过 Ajax 加载）中显示的 HTML 片段，你需要确保能够将内容独立提供，无论是否有包含文档标记。这样，用户通过普通链接访问，作为独立文档时，也能获得不错的体验。

这里的核心做法是：原生地链接到目标内容（`href=`，或许再加 `target="_blank"`），然后使用 JavaScript 挂钩这些链接，让它们变得更酷。自己编写打开窗口的代码相当简单——关键是内置的 `window.open()` 方法。

如果你要添加伪弹出窗口或灯箱，务必使用一个优秀的现有库，避免跨浏览器问题和定位算法带来的无尽痛苦。这里有几个参考：

- Scripty2 的 UI¹⁴
- jQuery UI¹⁵
- Dijit（基于 Dojo）¹⁶
- YUI 的 Overlay 模块¹⁷
- Ext.Window¹⁸

还要记住，小型的弹出内容可能适合使用点击触发的富工具提示，而不是一个完整的弹出区域。在这种情况下，可以查看工具提示库和模块。

14. http://github.com/madroobby/scripty2
15. http://jqueryui.com/
16. http://dojotoolkit.org/projects/dijit
17. http://developer.yahoo.com/yui/3/overlay/
18. http://www.extjs.com/deploy/dev/docs/?class=Ext.Window

### 标记用于渐进增强。

下载 ui/popups/index.html

```
<p>
  The great thing about <a class="popup" target="_blank" href="http://pragprog.com/titles/pg_js">Pocket Guide to JavaScript</a>
  is that it focuses on a bunch of specific, useful tasks.</p>
```

### 编写一个简单的 window.open() 脚本。

下载 ui/popups/popups.js

```
var POPUP_FEATURES = 'status=yes,resizable=yes,scrollbars=yes,' +
'width=800,height=500,left=100,top=100';

function hookPopupLink(e) {
  var trigger = e.findElement('a.popup');
  if (!trigger) return;
  e.stop(); trigger.blur();
  var wndName = trigger.readAttribute('target') ||
    ('wnd' + trigger.identify());
  window.open(trigger.href, wndName, POPUP_FEATURES).focus();
}

document.observe('click', hookPopupLink);
```

### 相关任务

- 任务 12，制作优雅的工具提示，第 44 页
- 任务 15，创建灯箱效果，第 50 页

## 14 预加载图像

当你的页面提供用户交互来更改所显示的图像（例如提供缩放、特写、正面/背面视图，或其他任何方式）时，你不会希望用户因为突然需要的图像需要瞬间加载而看到短暂的空白屏幕。你可能想要预加载这些图像。

本质上，只有三种预加载图像的方式：

- *使用 JavaScript，通过动态创建的 Image 对象并设置适当的 src 属性*：这样做可以让你检测预加载的图像确实已加载。
- *使用 CSS，隐藏预加载的图像*：这归结为使用隐藏的 <img> 标签来预加载图像。你可以隐藏 <img> 标签本身，或者隐藏一个共同的容器（我更喜欢这种方式）。
- *使用 CSS 精灵*：当你想要预加载诸如悬停效果或一组相关图像（例如背景、边框和角落）时，这绝对应该是首选方法。¹⁹

CSS 方法相当直接，但它不像 JavaScript 方法那样提供那么多的潜在控制。对面页面上的标记和脚本假设，带有 `rel="preloadZoom"` 属性的图像标签具有一个使用相同 URI 并带有 `_closeup` 名称后缀的特写版本，用于悬停特写预加载。

这种情况通常更适合使用 JavaScript 选项而不是 CSS 选项。由于悬停效果依赖于 JavaScript，我们也应该在 JavaScript 中预加载。（如果没有 JavaScript，我们就不会预加载那些以后无法显示的内容。）此外，在 JavaScript 中预加载可以避免标记/样式膨胀。

使用 JavaScript，我们可以避免暂时空白/不完整渲染的风险，只在我们确定图像已预加载时才切换显示。非精灵的 CSS 方法存在切换到一个尚未加载完成的图像的风险（虽然风险确实很低）。

对于快速加载图像的更高级技术，请查看 Steve Souder 于 2009 年 5 月做的演示：14 rules for faster-loading images.²⁰

19. 查看开创性的 http://www.alistapart.com/articles/sprites 以及更新的 http://css-tricks.com/css-sprites/。Steve Souders 还维护着 SpriteMe 工具：http://spriteme.org/。
20. http://stevesouders.com/docs/wordcamp-20090530.ppt

### 标记用于预加载。

下载 ui/preloading/index.html

```
<ul id="products">
  <li><h2><a href="http://pragprog.com/titles/cppsu">
    <img rel="preloadZoom" src="cppsu.jpg" alt="" />
    <span>Prototype and script.aculo.us</span>
  </a></h2></li>
  <li><h2><a href="http://pragprog.com/titles/vsscala">
    <img rel="preloadZoom" src="vsscala.jpg" alt="" />
    <span>Programming Scala</span>
  </a></h2></li>
</ul>
```

### 脚本预加载。

下载 ui/preloading/preloading.js

```
function preloadImages() {
  $$('img[rel="preloadZoom"]').each(function(img) {
    var pimg = new Image();
    pimg.src = img.src.replace(/\(\.\w+)$/, '_closeup$1');
  });
}

document.observe('dom:loaded', preloadImages);
```

### 悬停切换到（理想情况下已预加载的）图像。

下载 ui/preloading/preloading.js

```
function togglePreloaded(e) {
  var trigger = e.findElement('img[rel="preloadZoom"]');
  if (!trigger) return;
  if (e.type == 'mouseover') {
    trigger.src = trigger.src.replace(/\(\.\w+)$/, '_closeup$1');
  } else {
    trigger.src = trigger.src.replace('_closeup', '');
  }
}

document.observe('mouseover', togglePreloaded).
  observe('mouseout', togglePreloaded);
```

## 15 创建灯箱效果

灯箱效果是指将某些内容调出显示，同时用遮罩层将页面其余部分变暗并阻止鼠标操作。大多数情况下，灯箱界面居中显示在页面上。灯箱通常用于展示图像，并通过页面上的链接文本或链接缩略图启动。

![](img/544d515106a3758d5f58491594755dce_49_0.png)

在这本书的示例中，我们使用 Janis Skarnelis 编写的 FancyBox jQuery 插件，将缩略图以灯箱形式展示为更大的版本。它不唐突，相当轻量，易于直接使用，开箱即用且外观华丽。不过，如果你愿意，也可以查看本书演示页面底部的替代方案。

FancyBox 不仅限于图像内容——它可以调出任何内容，包括 `<iframe>` 之类的东西。当链接的目标 URI 既不“看起来像图像文件”也不使用 iframe 时，它默认为即时 Ajax 加载。因此，例如，较大的图像可以通过无扩展名的 URL 按需加载。

与大多数 UI 相关的库一样，FancyBox 需要加载至少一个脚本和一个 CSS 文件。它假设其图像位于样式表所在的文件夹中，避免了乏味的 CSS 调整。FancyBox 对图像 URL 没有要求。

要让链接变为灯箱效果，我们只需获取它们并调用它们的 `fancybox()` 方法，如对面页面所示。它可以在没有任何选项的情况下工作，但也提供了许多可能的调整。我非常喜欢看到缩略图放大到更大版本，所以我这样设置了。

### 加载 FancyBox。

下载 ui/lightbox/index.html

```
<link rel="stylesheet" type="text/css"
    href="vendor/fancybox/jquery.fancybox-1.2.6.css" />
<script type="text/javascript" src="vendor/jquery-1.3.2.min.js"></script>
<script type="text/javascript"
    src="vendor/fancybox/jquery.fancybox-1.2.6.pack.js"></script>
```

### 链接到单个图像。

下载 ui/lightbox/index.html

```
<a href="beach_normal.jpg" title="A gorgeous beach">
    <img src="beach.jpg" alt="Beach" />
</a>
```

### 将图像作为可浏览的组进行链接。

下载 ui/lightbox/index.html

```
<li>
    <a href="beach_normal.jpg" rel="demo" title="A gorgeous beach">
        <img src="beach.jpg" alt="Beach" />
    </a>
</li>
<li>
    <a href="feline_normal.jpg" rel="demo" title="A cute cub">
        <img src="feline.jpg" alt="Feline" />
    </a>
</li>
```

### 初始化 FancyBox（并加入一些自定义设置）。

下载 ui/lightbox/lightbox.js

```
$(function() {
    $('#thumbnails a').fancybox({
        zoomSpeedIn: 300, zoomOpacity: true, overlayColor: '#000',
        overlayOpacity: 0.6
    });
});
```

### 相关任务

- 任务 12，制作优雅的工具提示，第 44 页
- 任务 13，制作低调的弹出窗口，第 46 页

