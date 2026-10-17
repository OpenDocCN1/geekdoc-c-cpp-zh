
| :--- | :--- | :--- | :--- |

| article* | 文章内容 | header* | 章节或页面的页眉 |

| aside* | 侧边栏内容 | hgroup* | 分组头部信息 |

| blockquote | 长引用 | hr | 水平线 |

| body | 页面主体 | li | 列表项 |

| br | 换行 | map | 图像地图 |

| button | 按钮 | object | 对象嵌入 |

| canvas* | 绘图区域 | ol | 有序列表 |

| caption | 表格标题 | output* | 表单输出 |

| col | 表格列 | p | 段落 |

| colgroup | 表格列组 | pre | 预格式文本 |

| dd | 定义描述 | progress* | 显示任务消耗的进度 |

| div | 分区 | section* | Web 页面中的章节 |

| dl | 定义列表 | table | 表格 |

| dt | 定义术 | tbody | 表格主体 |

| embed | 外部内容 | textarea | 表单文本输入区域 |

| fieldset | 字段组标签 | tfoot | 表格页脚 |

| figcaption* | 图注 | th | 表格头部 |

| figure* | 分组媒体内容和标题 | thead | 表格头部 |

| footer* | 章节或页面页脚 | tr | 表格行 |

| form | 输入表单 | ul | 无序列表 |

| h1–6 | 标题级别 1–6 | video* | 视频播放器 |

| head | 页面信息 | | |

* HTML5 中新增的

并不是所有的 CSS 定义都能应用到所有的 HTML 元素。特定的 CSS 属性是否可以应用，取决于元素的性质。在大多数情况下，一个属性是否可以应用是显而易见的。

例如，你不会期望缩进段落首行的 `text-indent` 属性应用到如 `<b>` 这样的内联标签；事实上，它是无法应用的。当你在这方面需要帮助时，请查看附录 A 以确定适用于特定 HTML 元素的 CSS 属性。

# HTML5 的演变

HTML5 是 Web 标记的下一步并将取代 XHTML。虽然 XHTML2 开发了近八年，但它在 2009 年被搁置，取而代之的是 HTML5。

为了理解这是如何发生的，让我们回到上世纪末 Web 的黄金时代——确切地说是 1997 年。那还是 Web 1.0 的世界，尽管我们当时还不知道称呼它。互联网泡沫开始膨胀，每个人都在使用 Netscape Navigator 冲浪，直到世界维网联盟（W3C）引入了 HTML 4.0 (HTML4)。

HTML4 是一次巨大的改进，因为它第一次是由标准机构创建的，该机构让每个人都有参与机会，并相信 Web 页面在所有浏览器中的显示应该是相同的。

## 接着是 XHTML

XHTML1（发布于 2001 年）是使用 XML 对 HTML 4.0 的重写，旨在将 XML 的功能引入 Web 开发。XHTML 使用 XML 文档类型。XHTML 采用了与 HTML 相同的所有标签，但代码仍然可以在不支持 XML 的浏览器中运行。

但等等，人们很快发现即使是 XHTML1 也不足以让 Web 演进到二十世纪，开启语义化页面的黄金时代。XHTML2 主要是作为一种过渡技术，将 Web 从其相对静态的“页面”本质演变为一个真正的交互且通用的环境。从一开始开始，事情就出了问题。

## 接着是 HTML5

2003 年 6 月，HTML5 作为 Web 超文本应用小组（WHATWG）诞生了生命，这是一个与 W3C 无关的组织。相反，这个独立的小组对 XHTML 缓慢的速度和方向感到沮丧，开始开发一种新的标准，这种标准将向下兼容，并解决许多实际问题。

在几年里，两种语言并行开发。由于看到 HTML5 的进展比 XHTML 更快，W3C 在 2007 年采纳了它作为新的标准，发布了“发布草案”。

### 2.3 HTML5 与 XHTML5

| | XHTML5 | HTML5 |
|---|---|---|
| 标签大小写 | 小写 | 大写或小写 |
| 闭合标签 | 强制 | 可选 |
| 自闭标签 | 强制 | 可选 |
| MIME 类型 | application/xml 或 application/xhtml+xml | text/html |
| 错误 | 致命 | 不致命 |

## 它是 HTML5 还是 XHTML？

尽管 XHTML 消失了，但统一 XML 和 HTML 的需求并没有消失。因此，如果你了解 XML，学习 HTML5 会与 XHTML 相似。它们处理标签的主要差异见表 2.3。

使用 HTML5 还是 XHTML5 取决你的决定。但诚实说，我喜欢 HTML5 的包容性，这也是我在本书中使用它的原因。

## HTML5 中缺少什么？

HTML5 包含了多项变化。但如果你想开始使用，也需要知道哪些是不可用的。框架标签——`frameset`、`frame`、`noframes`——已被删除，但 `iframe` 仍然可用。大多数演示标签已被删除——如 `basefont`、`big`、`center`、`font`、`s`、`strike`、`tt`、`u`——尽管 `b`（粗体）和 `i`（斜体）仍然保留，关于这一决定存在争议。

此外，与 XHTML 不同，`<img>` 和 `<br>` 等独立标签不需要自闭合。所以，与其使用 `<br />`，回归到了 `<br>`。真的，这难道不简单吗？

## HTML 有什么新？

HTML5 对 Web 页面进行了重要的结构性改变。例如，你可以指定头部、页脚和侧边栏等常见元素。此外，HTML5 原生（即浏览器内置）引入了以前需要插件或脚本的功能，以新元素和 API 的形式出现：

- 元素 元素允许可脚本的位图编辑。

- 文档编辑允许用户直接在 Web 页面上编辑内容。

- Web 表单自校验并包含更多输入类型。

- 拖放允许在无脚本的情况下操作元素。

- 音频和视频播放无需插件即可原生控制媒体文件。

- 新的结构元素消除了使用 `<div>` 标签配合类和 ID 来创建头部和页脚等常见元素的负担。

HTML5 是 Web 设计和开发的舞台。许多浏览器已经开始支持它的部分功能，尽管它还不是一个完整的标准。尽管如此，一个显著（且频繁）的支持反对主义者是 Internet Explorer。然而，微软承诺在 IE 9 中引入 HTML5 支持。

## HTML5 结构是如何工作的？

我告诉你一个小秘密：你今天起就可以使用 HTML5 语法来构建你的 Web 页面，并将其与 CSS3（或旧版本的 CSS）配合。为了理解它是如何工作的，让我们来看看 HTML5 的原理。

HTML5 最显著的变化之一是增加了结构化元素，这将极大地增强 Web 标记背后的语义化哲学。大多数新的结构标签都是自言自足的，但少数需要详细说明：

- `<header>` 可用于页面页头、节头部、文章头部或侧边栏头部。

- `<nav>` 可以独立包含，也可以作为页头和/或页脚的一部分。

- `<section>` 定义页面的主要部分，通常是包含文章（article）的部分。

- `<article>` 是独立的博客文章或博客文章摘要。

- `<figure>` 用于包含嵌入页面中的图像、音频和视频。

- `<dialog>` 代替 `<dl>` 元素来包含对话记录。

- `<aside>` 用于页面上的辅助性内容，如相关链接、次级导航，当然还有广告。

- `<footer>` 与 `<header>` 类似，可以放在其他元素的底部。

遗憾的是，并不是所有的浏览器在没有额外帮助的情况下都能理解 HTML5。

![](img/9cd61ac1d4015ed5688d0c411434a660_49_0.png)

## 2.1 HTML5page.html——展示了一个典型的 HTML5 页面，该页面使用页头、导航、文章和页脚构建布局网格。

## 现在使用 HTML5 结构

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
<meta charset="UTF-8">
<title>HTML5</title>
</head>
<body>
<header>
<nav></nav>
</header>
<section>
<article>
<header></header>
<figure>
<footer></</footer>
</article>
<dialog></dialog>
</section>
<aside></aside>
<footer</footer></footer>
</body>
</html>
```

HTML5 在大多数当前的浏览器中尚未完全实现（可能还需要一段时间时间才能完全普及），但你现在就可以按照一些步骤为未来做准备。

尽管 CSS 可以应用于今天使用的任何 HTML 版本——包括 XHTML 1 和 HTML 4.01——但我将在本书中贯穿使用 HTML5。本书绝不是 HTML 5 的详尽资源。然而，我想向你展示如何设置我将在后续章节中引用的 Web 文档。

## 设置基础 HTML5 文档：

1. 添加 HTML5 文档类型（表 2.4）。注意，新的 `!DOCTYPE HTML` 比今天使用的复杂且难以解析的 HTML 和 XHTML 文档类型（代码 2.1）要简单得多。它仅仅是告诉浏览器使用 HTML。

```html
<!DOCTYPE html>
```

| 标记语言 | Doctype 代码 |
|---|---|
| HTML 4.01 Loose | <!DOCTYPE HTML PUBLIC "-//W3C/DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd" |
| HTML 4.01 Strict | <!DOCTYPE HTML PUBLIC "-//W3C/DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd" |
| HTML 4.01 Frameset | <!DOCTYPE HTML PUBLIC "-//W3C/DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd" |
| XHTML1 Transitional | <!DOCTYPE HTML PUBLIC "-//W3C/DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/xhtml1-transitional.dtd" |
| XHTML1 Strict | <!DOCTYPE HTML PUBLIC "-//W3C/DTD HTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/xhtml1-strict.dtd" |
| XHTML1 Frameset | <!DOCTYPE HTML PUBLIC "-//W3C/DTD HTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/xhtml1-frameset.dtd" |
| HTML5/XHTML5 | <!DOCTYPE html> |

2. 添加 `<html>` 标签，包括预期的语言和语言方向（通常从左到右的文本使用 `ltr`）。

`<html dir="ltr" lang="en-US">...`

`</html>`

3. 在文档中添加 `<head>`，你可以在这里指定关于此文档的信息，包括标题和文本使用的字符集。我建议使用 UTF-8 以获得最佳效果。

`<head>...</head>`

4. 在文档中添加 `<body>`。这是添加所有要显示内容的地方。我建议为你网站中的每个 `body` 元素至少提供一个唯一的类名，以及其他用于标识其在站点中位置的属性。这样做，你可以针对每个页面和每个部分添加样式，而无需包含多个 CSS 文件。

`<body class="section Name page">...`

5. 为你的页面添加 `<header>` 标签。这是你将放置页面页头的地方。

`<header>...</header>`

6. 为你的网站添加 `<nav>` 标签。

`<nav>...</nav>`

## HTML5 何时能就绪？

需要注意的是，广泛采用直到 2012 年尚未完成（当时它还是一个工作草案）。许多浏览器目前支持部分 HTML5 功能。那么，你该怎么办？

虽然 Internet Explorer 不认识 HTML5 标签，但有一个使用 JavaScript 创建元素的局部修复方案（或权宜之计）：

```javascript
document.createElement('header');
```

7. 为你的 Web 页面添加一个或 `<article>` 标签。

`<article>...</article>`

8. 添加 `<aside>` 标签，有时被称为侧边栏。

`<aside>...</aside>`

9. 最后，在页面底部添加 `<footer>` 标签。

`<footer>...</footer>`

## 在 Internet Explorer 中实现 HTML5

为了方便添加这些新标签，请创建一个外部 JavaScript 文件（代码 2.2），并使用 IE 条件（代码 2.3）从你的 HTML 文档中引用它，你将在第 13 节详细探讨。

```javascript
*** CSS Chapter 2 - HTML5forIE.js ***
document.createElement('abbr');
document.createElement('article');
document.createElement('aside');
document.createElement('audio');
document.createElement('bb');
document.createElement('canvas');
document.createElement('center');
document.createElement('datalist');
document.createElement('details');
document.createElement('dialog');
document.createElement('eventsource');
document.createElement('figure');
document.createElement('footer');
document.createElement('header');
document.createElement('group');
document.createElement('mark');
document.createElement('menu');
document.createElement('meter');
document.createElement('nav');
document.createElement('output');
document.createElement('progress');
document.createElement('section');
document.createElement('time');
document.createElement('video');
```

## 为什么要使用 Doctype？

如果不使用 doctype，现代浏览器将被强制进入怪异模式（Quirks Mode）。对于创建新的 Web 页面来说，这是一个糟糕的情况，因为把代码的解释权完全交给了浏览裁量，这会导致大量的显示不一致。

如果不在 Web 页面中包含 doctype，新的浏览器可能无法识别你的所有代码。

## 2.3 HTML5page.html—包含指向代码 2.2 中 JavaScript 的链接

```html
<!DOCTYPE html>
<html lang="ltr" dir="en-US">
<head>
  <meta charset="utf-8">
  <title>HTML5</title>
  <!--if IE -->
  <script src="HTML5forIE.js"
       type="text/javascript"></script>
  <![endif]-->
</head>
<body class="pageName">
  <header></header>
  <nav></nav>
  <article>
    <figure>
      <section></section>
    </figure>
  </article>
  <aside>
    <dialog></dialog>
  </aside>
  <footer></footer>
</body>
</html>
```

> 提示：如果你想把它弄得更花哨一点，可以将代码 2.2 替换为代码 2.4 中的 JavaScript 循环。效果相同，但更加复杂。

> 提示：示例中的文档结构是为了满足你的需求而设计的，但你不需要严格遵守标签放置和嵌套的硬性规定。你可以将导航放在头部、页脚、文章或侧边栏中。同样，图形可以放在侧边栏或头部。之前的示例只是一个基础的 Web 页面结构。

## 2.4 HTML5forIE.js—这与代码 2.2 的相同，但使用了 JavaScript 循环，使得代码更加紧凑。
