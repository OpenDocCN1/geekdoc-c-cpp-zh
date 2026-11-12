

## HTML5 何时可用？

需要注意的是，许多人担心 HTML5 仍然是“工作草案”。最终的“建议标准”要到 2022 年才会完成。（是的，那是十年后的事。）怀疑论者举手投降，认为 HTML5 要过一段时间才会相关。但这个日期非常具有误导性。

目前所有新浏览器都支持重要的 HTML5 属性。2022 年的日期遥遥无期，但那是 *所有* 浏览器都将适配 *所有* HTML5 属性的时候。

从实际角度来看，HTML5 已经到来，并在未来几年内使用量将不断增长，直到成为该领域的主流。

如果你准备好使用它，HTML5 已经准备好迎接黄金时段。

- 5. 为你的页面添加 header 标签。这与步骤 3 中的 head 标签 *不* 相同。这是你放置所有在网页标题中显示的内容的地方。你也可以在此处包含导航，或单独包含，具体取决于你的设计需求。

  <header>...</header>

- 6. 添加导航标签，并包含指向网站顶级页面的链接。

  <nav>...</nav>

- 7. 添加一个或多个 article 标签，它们将包含页面上的重要内容。许多网络浏览器和 RSS 新闻阅读器现在允许用户专注于文章，以获取页面的主要内容。图片和章节非常适合放在这里。

  <article>...</article>

- 8. 添加 aside 标签，这是放置文章补充内容的地方。这有时也被称为侧边栏或导轨，具体取决于你与谁交谈。它可以包含你想要的任何内容，但我喜欢在此处放置评论和对话。

  <aside>...</aside>

- 9. 最后，在页面底部添加 footer 标签。这通常包括冗余的顶级导航、版权和其他小字条款。

  <footer>...</footer>

就是这样。你已经准备好开始使用 HTML5 标签了。大胆去做吧。哦，等等，没错：它在除 Internet Explorer 之外的所有东西上都能工作，*但* Internet Explorer 恰好占据了当今使用的浏览器的大多数。那么，你该怎么办？

## 让 HTML5 在旧版 Internet Explorer 中工作

虽然 Internet Explorer 不认识 HTML5 标签，但有一个部分修复（或凑合的补丁）涉及使用 JavaScript 来创建 HTML5 元素：

```
document.createElement('header');
```

被称为“HTML5 Shiv”，这将“教会” Internet Explorer 6（及更高版本）这些元素存在，并且应该被视为 HTML 标签。你可以为需要的每个 HTML5 元素添加一行这样的 JavaScript。

为了简化添加这些新标签，创建一个外部 JavaScript 文件（Code 2.2），并使用 IE 条件注释（Code 2.3）从你的 HTML 文档链接到它，你将在第 13 章中详细探讨这一点。

### Code 2.2 HTML5forIE.js—这为 Internet Explorer 缺少的每个 HTML5 标签添加一个空白 HTML 标签。

```
/*** CSS VQS - Chapter 2 - HTML5forIE.js ***/
document.createElement('abbr');
document.createElement('article');
document.createElement('aside');
document.createElement('audio');
document.createElement('bb');
document.createElement('canvas');
document.createElement('datagrid');
document.createElement('datalist');
document.createElement('details');
document.createElement('dialog');
document.createElement('eventsource');
document.createElement('figure');
document.createElement('footer');
document.createElement('header');
document.createElement('hgroup');
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

### 为何要使用文档类型？

如果不使用文档类型，现代浏览器将被迫进入怪异模式。如果你正在创建新网页，这是一种糟糕的情况，因为它将代码的解释完全留给浏览器自行决定，这可能导致大量显示不一致。

如果你在网页中不包含文档类型，较新的浏览器可能无法识别你的所有代码。

### Code 2.3 HTML5page.html—这包含指向 Code 2.2 中 JavaScript 的链接。

```
<!DOCTYPE html>
<html dir="ltr" lang="en-US">
<head>
<meta charset="utf-8">
<title>HTML5</title>
<![if IE ]>
<script src="script/HTML5forIE.js"
type="text/javascript"></script>
<![endif]>
</head>
<body class="pageName">
<header></header>
<nav></nav>
<article>
<figure></figure>
<section></section>
</article>
<aside>
<dialog></dialog>
</aside>
<footer></footer>
</body>
</html>
```

如果你想要花哨一点，用 Code 2.4 中显示的 JavaScript 循环替换 Code 2.2。这有相同的效果，但代码更紧凑。

> **提示** 本示例中的文档已按我的需求构建，但你无需为标签位置和嵌套遵循死板的规则。你可以将导航放在 header、footer、article 或 aside 中。同样，图片可以放在 aside 或 head 中。前面的示例只是一个基本的常见网页结构。

### Code 2.4 HTML5forIE.js—这与 Code 2.2 完成相同的工作，但使用 JavaScript 循环，使代码更紧凑。

```
/*** CSS VQS - Chapter 2 - HTML5forIE.js ***/
/*@cc_on
if(!@_@) return;
var e = "abbr,article,aside,audio,bb,canvas,
datagrid,datalist,details,dialog,
eventsource,figure,footer,header,hgroup,
mark,menu,meter,nav,output,progress,
section,time,video".split(',');
for(var i=0;i<e.length;i++)
  document.createElement(e[i]);
*/
```

## CSS 基础

![](img/e1ed1e3c1873fa9fc855210fb83699d0_56_0.png)

CSS 让你控制文档外观的所有元素——字体、文本、颜色、背景、大小、边框、间距、定位、视觉效果、表格和列表。它甚至允许你使用过渡和变换来控制元素的空间和时间样式。然而，使用 CSS 进行样式设置的真正威力在于，你可以通过仅更改几行 CSS 代码来改变网站上每个页面的外观。

通过娴熟运用 CSS，你可以从一个简单的网页开始，添加视觉设计和交互，并将其转变为网状环境。

### 本章内容

- 基本 CSS 选择器 36
- 内联：为 HTML 标签添加样式 37
- 嵌入：为网页添加样式 40
- 外部：为网站添加样式 43
- (重)定义 HTML 标签 50
- 定义可重用类 53
- 定义唯一 ID 57
- 定义通用样式 61
- 分组：定义使用相同样式的元素 64
- 向 CSS 添加注释 67

### 基本 CSS 选择器

CSS 通过使用 CSS _规则_ 来定义网页上元素的样式。规则通过 _选择器_ 应用，选择器有四种基本类型：HTML 选择器用于引用特定标签；类选择器单独应用于元素；ID 选择器应用于页面上的单个元素；通用选择器应用于页面上的所有元素（表 3.1）。你将不断使用这四种基本选择器，它们是最佳的起点。在第 4 章中，你将学习使用其他选择器来创建更具选择性的样式。

| Format | Selector Name | What Elements Are Styled |
| :--- | :--- | :--- |
| a | HTML | All specified HTML tags |
| .myClass | Class | Any HTML tag where class is applied |
| a.myClass | Dependent class | Specified HTML tag where class is applied |
| #myID | ID | Any HTML tag where ID is applied |
| a#myID | Dependent ID | Specified HTML tag where ID is applied |
| * | Universal | All HTML tags |

```
<h1 style="color: red;">...</h1>
```

直接在 HTML 标签中定义样式的一般语法。

### 内联：为 HTML 标签添加样式

虽然使用 CSS 意味着你不必单独设置每个标签的外观，但你仍然有自由在单个标签内使用内联样式 A 来设置样式。

当你在 head 或外部样式表中为页面设置了样式，并且需要逐个案例地覆盖这些样式时，这很有用。但是，你应该只将其作为最后的手段。因为内联样式在层叠顺序中具有最高优先级，几乎不可能被覆盖。（参见“为何你绝对、绝对不应该在最终网站中使用内联样式……大部分情况”。）

