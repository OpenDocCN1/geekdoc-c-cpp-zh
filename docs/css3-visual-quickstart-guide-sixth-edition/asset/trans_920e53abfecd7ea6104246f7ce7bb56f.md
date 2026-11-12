

## XHTML2 的问题

人们很快意识到，即使是 XHTML1 也不足以让 Web 从其相对静态的“页面”性质演变为真正交互式且通用的应用环境。XHTML2 本应改变这一切。从 2002 年 8 月开始，XHTML 标准的作者们开始打造一种新语言，他们希望这种语言能完全重塑二十一世纪的 Web 标记，带来语义化 Web 页面、交互性、国际化、设备独立性以及人人皆可享用西米布丁的黄金时代！但他们忘了一件事：XHTML2 并未设计为与旧版 Web 标记语言向后兼容。现有浏览器将无法运行这个花哨的全新标记语言。Web 开发者将不得不为旧版浏览器开发一个网站版本，并为 XHTML2 标准开发另一个版本。

## 然后 HTML5 出现了

2003 年 6 月，HTML5 作为 Web Applications 1.0 诞生，由 Web HyperText Application Technology Working Group（WHATWG，Web 超文本应用技术工作组）创建，该组织与 W3C 无关。相反，这个独立小组对 XHTML2 进展缓慢和方向偏差感到沮丧，开始着手制定一个替代标准，该标准将向后兼容，更适合编写应用程序 *和* 页面，并且还将解决 Web 开发者面临的许多实际问题。

几年间，两种语言同时开发。但到了 2007 年，W3C 看到 Web Applications 1.0 的进度已超过 XHTML2，便将其作为新 HTML5 标准的起点，并于 2008 年 1 月 22 日发布了规范的“首份公开工作草案”。为将注意力集中在 HTML5 上，W3C 未续期 XHTML 工作组的章程，XHTML2 也随之消亡。

## 是 HTML5 还是 XHTML5？

尽管 XHTML2 已消失，但统一 XML 和 HTML 的需求依然存在。因此，存在一项并行计划来创建 XHTML5。要明确的是，这 *并非* 一种新的或不同的标记语言；它只是使用 XML 规则编写的 HTML5，与 XHTML 类似。

如果你了解 XHTML，那么学习 XHTML5 应该不难。它们主要在标签处理方式上有所不同。一些最重要的差异列于表 2.3 中。

无论你选择使用 HTML5 还是 XHTML5，由你决定，但两者在现代浏览器中都能正常工作。就我而言，我更喜欢 HTML5 更宽容的特性，并且本书中的代码也都使用它。

| | XHTML5 | HTML5 |
|---|---|---|
| 标签大小写 | 小写 | 大写或小写 |
| 闭合标签 | 必需 | 可选 |
| 自闭合标签 | 必需 | 可选 |
| MIME 类型 | application/xml 或 application/xhtml+xml | text/html |
| 格式正确性错误 | 致命 | 非致命 |

## HTML5 中不再包含的内容

HTML5 包含多项更改。但如果你想立即开始使用它，还需要知道哪些内容 *不再可用*。框架标签——`<frameset>`、`frame`、`noframes`——已被删除，但 `iframe` 仍可用。大多数表现标签已被删除——例如 *basefont*、*big*、*center*、*font*、*s*、*strike*、*tt*、*u*——虽然 *b*（粗体）和 *i*（斜体）仍然保留，但关于该决定仍有争议。

## HTML5 中的新增内容

HTML5 对 Web 页面进行了重要的结构更改。例如，你可以指定页眉、页脚、文章和侧边栏等常见元素。此外，HTML5 原生引入了许多功能（即内置于浏览器的功能），这些功能以前需要以新元素和 API 的形式使用插件和/或脚本：

- Canvas 元素允许脚本化位图编辑。
- 文档编辑允许用户直接在 Web 页面中编辑内容。
- Web 表单支持自动验证并包含更多输入类型。
- 拖放允许在无需脚本的情况下操作元素。
- 音频和视频定时媒体播放可在无需插件的情况下原生控制媒体文件。
- 新的结构元素消除了使用带有类和 ID 的 `<div>` 标签来创建页眉和页脚等常见元素的负担。

## HTML5 结构如何工作？

HTML5 最重要的变化之一是添加了结构元素，这将大大增强 Web 标记背后的语义理念。大多数新结构标签不言自明；但少数几个需要进一步说明：

- `<header>` 可用于页面标题、章节标题、文章标题或侧边栏标题。
- `<hgroup>` 用于对相关的标题元素（h1、h2、h3 等）进行分组，通常作为标题和副标题。
- `<nav>` 可以独立包含，也可以作为页眉和/或页脚的一部分。
- `<section>` 定义页面的主要部分，通常是包含文章的部分。
- `<article>` 是单个博客条目或博客条目摘要。
- `<figure>` 用于包含嵌入页面中的图像、音频和视频。
- `<figcaption>` 包含其所在 figure 标签的标题。
- `<dialog>` 替换 `<dl>` 元素以包含对话记录。
- `<aside>` 用于页面上的支持内容，例如相关链接、次要导航，当然还有广告。
- `<footer>` 与页眉类似，可以放置在其他元素的底部。

不幸的是，并非所有浏览器都能在无需少许帮助的情况下理解 HTML5。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_49_0.png)

A 典型 HTML5 文档的线框图。

## 立即使用 HTML5 结构

我来告诉你一个小秘密：你可以使用 HTML5 语法来构建 Web 页面，并将其与 CSS3（或旧版 CSS）结合使用。HTML5 已在大多数当前浏览器（包括 Internet Explorer）上实现，你应该立即开始使用它。

尽管 CSS 可以应用于当前使用的任何 HTML 版本——包括 XHTML1 和 HTML 4.01——但我将在本书中始终使用 HTML5。本书绝非 HTML5 的详尽资源。不过，我想向你展示如何设置我将在后续章节中引用的基本 Web 文档。

代码 2.1 HTML5page.html——这展示了一个典型的 HTML5 页面，其结构使用了页眉、导航、文章、侧边栏和页脚，用于布局图形。

```
<!DOCTYPE html>
<html dir="ltr" lang="en-US">
<head>
<meta charset="utf-8">
<title>HTML5</title>
</head>
<body>
<header>
<hgroup>
<nav></nav>
</header>
<section>
<article>
</article>
<figure>
<figcaption></figcaption>
</figure>
<footer></footer>
<article>
<dialog></dialog>
</section>
<aside></aside>
<footer></footer>
</body>
</html>
```

## 表 2.4 文档类型

| 标记语言 | Doctype 代码 |
|---|---|
| HTML 4.01 宽松型 | <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"> |
| HTML 4.01 严格型 | <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0//EN" "http://www.w3.org/TR/html4/strict.dtd"> |
| HTML 4.01 框架集 | <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd"> |
| XHTML1 过渡型 | <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"> |
| XHTML1 严格型 | <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> |
| XHTML1 框架集 | <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd"> |
| HTML5/XHTML5 | <!DOCTYPE html> |

## 设置基本 HTML5 文档：

- 1. 添加 HTML5 文档类型（表 2.4）。请注意，HTML5 的新 !DOCTYPE 比当前使用的复杂且难以解读的 HTML 和 XHTML 文档类型（代码 2.1）简单得多。它只是告诉浏览器使用 HTML。
  <!DOCTYPE html>

- 2. 添加 HTML 标签，包括预期语言和语言方向（通常 ltr 表示从左到右的文本）。
  <html dir="ltr" lang="en-US">...
  </html>

- 3. 向文档添加 head，这是你指定有关此文档的信息的地方，包括标题和文本使用的字符集。我建议使用 UTF-8 以获得最佳效果。
  <head>...</head>

- 4. 向文档添加 body。这是添加所有要显示的内容的地方。我建议为网站中的每个 body 元素至少提供一个唯一的类名和其他用于标识其在网站中位置的类名。这样做，你可以按页面和按章节添加样式，而无需包含多个 CSS 文件。
  <body class="section Name - pageName">...</body>

