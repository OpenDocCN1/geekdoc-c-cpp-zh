

| 章节 | 标题 | 评级 |
|---|---|---|
| I. | 掉进兔子洞 | ♥ |
| II. | 泪水池 | ♥♥ |
| III. | 核心竞选赛与长故事 | |
| IV. | 兔子派出小比尔 | ♥♥ |
| V. | 毛毛虫的忠告 | ♥♥♥ |
| VI. | 猪与胡椒 | ♥ |
| VII. | 疯狂茶会 | ♥♥♥♥ |
| VIII. | 女王的槌球场 | ♥♥ |
| IX. | 假海龟的故事 | |
| X. | 龙虾四对舞 | ♥ |
| XI. | 谁偷了馅饼？ | ♥♥♥ |
| XII. | 爱丽丝的证词 | ♥♥ |

代码 8.8 应用于代码 8.1：使用分离设置，您可以设置边框间距。

> 显示的结果在不同浏览器之间可能会有所不同，除非您使用 CSS 设置边框样式。
> 如果合并的边框不共享相同的边框厚度，则会显示较厚的边框并使用其样式。
> 如果边框厚度相同但样式不同，则使用左侧数据单元格的边框样式。

## 处理空表格单元格

如果表格数据单元格没有数据（甚至没有空格或非断行空格），它将简单地以列和行的默认宽度和高度显示为一个空白框。

empty-cells 属性（表 8.9）允许您指定该空数据单元格（最重要的是，其边框）的呈现方式。

### 隐藏空表格数据单元格：

- 1. 将 empty-cells 属性添加到表格元素的 CSS 规则中。键入 empty-cells，后跟冒号 (:)（代码 8.9）。
- 2. 指定应如何处理空表格单元格。
- hide;

键入以下之一以指定单元格的处理方式：

- 显示将强制空数据单元格显示其背景和边框。
- 隐藏将在数据单元格的位置留出一个视觉间隙。

| 值 | |
|---|---|
| 显示 | |
| 隐藏 | |
| 继承 | |

代码 8.9. 添加到 list-table-properties.css——empty-cells 属性允许您显示（默认）或隐藏空表格数据单元格

```css
/*** list-table-properties.css ***/
table {
  empty-cells: hide;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_253_0.png)

代码 8.9 应用于代码 8.1：空表格数据单元格已被隐藏，因此其边框和背景颜色不显示，在表格中留出一个空白间隙。

| 值 |
|---|
| 顶部 |
| 底部 |
| 继承 |

代码 8.10 添加到 list-table-properties.css —— caption-side 属性允许您指定标题应出现在表格上方（top）还是下方（bottom）。

```css
/* *** list-table-properties.css ***/
table {
  caption-side: bottom;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_254_0.png)

标题被强制放置在表格底部，而不是其自然位置顶部。

## 设置表格标题的位置

<caption> 标签允许您在表格中嵌入标识文本。您可以在标签中设置 align 属性以定义标题相对于表格的位置，但此方法正在被弃用，转而使用 CSS caption-side 属性（表 8.10），它起到相同的作用。

### 设置标题相对于其表格的位置：

- 1. 将 caption-side 属性添加到您的 CSS 中。键入 caption-side，后跟冒号 (:)（代码 8.10）。caption-side:
- 2. 键入一个关键字，指示您希望标题出现在表格的哪一侧：top 或 bottom。bottom;

## 综合运用

代码 8.11 显示了 list-table-properties.css 的最终版本，在可能的地方使用了列表简写属性。caption-side 属性允许您指定标题应出现在表格上方（top）还是下方（bottom） A。

## 代码 8.11 最终的 list-table-properties.css

```css
/*** list-table-properties.css ***/

ul {
    list-style: circle inside; }
ol.list {
    list-style: none url(../Images/chrome/
        bullet-01.png) inside; }

table {
    table-layout: auto;
    border-spacing: 8px;
    border-collapse: separate;
    empty-cells: hide;
    caption-side: top;
    width: 75%;
    margin: 40px auto; }

tr {
    font-size: 1.25em; }

td {
    vertical-align: top;
    padding: .5em;
    background-color: rgba(200, 200, 180,.25);
    border: 1px solid rgb(200, 200, 180); }

table caption {
    font: normal 3em "TitleCopy", Corbel,
        "Helvetica", Arial, sans-serif; }

table thead {
    font-size: 1em;
    font-style: normal;
    font-variant: small-caps;
    text-shadow: 0px 1px 1px
        rgba(255,255,255,.6), 0px -1px 1px
        rgba(0,0,0,.6); }

article {
    padding: 100px 20px; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_255_0.png)

目录的最终外观。

## 用户界面和生成内容属性

用户界面在大部分情况下无法由 CSS 控制。它取决于正在使用的特定操作系统和浏览器。滚动条等对象不在您的控制范围内。但是，CSS 确实提供了一些对鼠标指针外观和引用样式的控制。

此外，CSS 包含几个属性，允许您为特定实例指定要放置在页面上的内容（生成的内容）。例如，您可能希望所有章节标题前都包含“Chapter”一词。虽然您通常希望将所有网页内容直接放入 HTML 代码中，但偶尔您会发现让某些冗余内容为您生成或将其定制为特定语言很有用。

| 本章内容 | |
|---|---|
| 入门 | 236 |
| 更改鼠标指针外观 | 238 |
| 使用 CSS 添加内容 | 240 |
| 教会浏览器计数 | 242 |
| 指定引用样式 | 244 |
| 综合运用 | 246 |

## 入门

对于本章，我们将使用《爱丽丝梦游仙境》中的第 5 章内容（代码 9.1）。HTML 导入了第 5、6、7 和 8 章的最终 CSS，以及您将在本章中构建的新文件 ui-generatedcontent-properties.css。我还将段落内的所有引号标记转换为使用 «q» 标签，允许我们为不同语言指定引用样式。从技术上讲，这是除块引用外的所有引用都应该加标签的方式，但很少看到它们被使用。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_257_0.png)

本章网页在添加任何生成内容之前的样子。

### 代码 9.1 本章示例中使用的 HTML5 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Alice&#8217;s Adventures In Wonderland | Chapter V</title>
<link href="../css/font-properties.css" type="text/css" rel="stylesheet" media="all">
<link href="../css/text-properties.css" type="text/css" rel="stylesheet" media="all">
<link href="../css/color-background-properties.css" type="text/css" rel="stylesheet" media="all">
<link href="../css/list-table-properties.css" type="text/css" rel="stylesheet" media="all">
<link href="../css/ch09/01a.css" type="text/css" rel="stylesheet" media="all">
</head>
<body id="chapter5" class="book aaiw chapter">
<header class="page">
<hgroup>
<h1>Alice&#8217;s Adventures in Wonderland</h1>
<h2>By <cite>Lewis Carroll</cite></h2>
</hgroup>
</header>
<article>
<h2>CHAPTER V</h2>
<span class="chaptertitle">Advice from a Caterpillar</span>
<p>
The Caterpillar and Alice looked at each other for some time in silence: at last the Caterpillar
took the hookah out of its mouth, and addressed her in a languid, sleepy voice.</p>
<p><q>Who are you?</q> said the Caterpillar.</p>
<p>This was not an encouraging opening for
a conversation. Alice replied, rather shyly, <q>I hardly know, sir, just at present&mdash;at least
I know who I <em>was</em> when I got up this morning, but I think I must have been changed
several times since then.</q></p>
<p>What do you mean by that?</p>
<p>said the Caterpillar sternly. <q>Explain yourself!</q></p>
</article>
<footer>
<a href="...AIWL-ch04.html" class="prev">The Rabbit sends in a little Bill</a>
<a href="...toc.html">Table of Contents</a>
<a href="...AIWL-ch06.html" class="next">Pig and Pepper</a>
</footer>
</body>
</html>

