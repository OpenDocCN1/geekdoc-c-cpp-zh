

## 适应环境

断点最容易被视为小、中、大屏幕尺寸。起初，你可能希望为每个断点创建完全不同的样式表并分别应用。然而，事实是大多数样式在不同样式表之间是相同的，因此最简单的做法是将通用样式放在 small 中，然后使用 medium 和 large 样式表来覆盖那些需要调整设计规模的样式。

然而，在这些断点之间，不同设备的尺寸各不相同，因此你的样式应使用相对长度，以确保它们能够拉伸以适应 A。这被称为自适应设计。

- small.css (Code 14.8): 应用于所有设备。包含应用于设计的所有通用样式，并带有小型设备的布局 B。

- medium.css (Code 14.9): 应用于平板电脑和计算机屏幕。包含用于为中等屏幕尺寸调整设计规模的覆盖样式 C。

A 0–739 像素是小范围。740–979 像素是中范围。980 及以上是大范围。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_387_0.png)

B 小。Code 14.8 应用于 Code 14.12。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_387_1.png)

C 中。Code 14.9 应用于 Code 14.12。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_387_2.png)

Code 14.8 small.css 包含网站中使用的所有默认样式，以及用于较小屏幕的布局样式。为节省空间，我使用 @import 添加了第 5–10 章的样式，将其他文件引入此文件中，但通常不推荐此技术（有关详细信息，请参见第 3 章）。

```css
/*** small.css - Default Styles ***/

@import url("../css/font-properties.css");
@import url("../css/text-properties.css");
@import url("../css/color-background-properties.css");
@import url("../css/list-table-properties.css");
@import url("../css/ui-generatedcontent-properties.css");

h1 {
    font-size: 3em; }

p {
    width: 94%; }

nav.toc {
    color: rgba(255,255,255,.75);
    margin: 0;
    padding: 0;
    width: 93%; }

nav.toc ol, nav.toc ul, nav.toc li {
    background: rgba(0,0,.5);
    border-bottom: 1px solid rgb(153,153,153);
    list-style: none;
    margin: 0 0 -4%;
    padding: .5em 5%;
    width: 100%; }

aside {
    padding: 5%;
    width: 91%; }
```

Code 14.9 medium.css 为中型设备提供自适应样式，在此情况下意味着更改标题大小。

```css
/*** Medium Device Styles ***/

h1 { font-size: 4em; }
```

- large.css (Code 14.10): 应用于计算机屏幕。包含用于为较大屏幕尺寸调整设计规模的覆盖样式 D。

- print.css (Code 14.11): 应用于打印设计 E。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_389_0.png)

D 大。Code 14.10 应用于 Code 14.12。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_389_1.png)

E 打印。Code 14.11 应用于 Code 14.12。

Code 14.10 large.css 为较大设备包含自适应样式。由于第 11–13 章是在考虑大屏幕的情况下构建的，我将这些样式导入 large。

```css
/* *** Large Device Styles ***/
@import url(".../css/box-properties.css");
@import url(".../css/visual-formatting-properties.css");
@import url(".../css/transformation-transition-properties.css");
@import url(".../css/design-interface.css");

h1 {
    font-size: 5em;
}
nav.toc {
    color: rgba(0,0,0,.75);
}
```

Code 14.11 print.css 包含一些简单样式，以使页面更适合打印，如第 3 章所示。

```css
/* *** For Print ***/

body {
    padding: 1em;
    color: rgb(0,0,0);
    background: white url(../chapters/alice23a.gif) no-repeat 0 0;
    padding: 200px 0 0 175px;
}

header.page, article {
    margin: 1em 0;
    background: none;
}

h1, h2, h3 { color: black; }
h2.chaptertitle { color: red; }
h2 cite { color: black; }

p { font: normal 12pt/2 Constantia, palatino, times, "times new roman", serif;
    text-indent: 3em; }

nav { display: none; }
```

## 使用 CSS 媒体查询设置简单的响应式设计：

- 1. 添加视口元标签 (Code 14.12):

```html
<meta name="viewport"
    content="width=device-width,
    initial-scale=1,
    maximum-scale=1,
    minimum-scale=1,
    user-scalable=no">
```

这为响应式设置了文件，确保设计适当地缩放到用户的设备，并防止用户放大，因为设计已经为最佳适配进行了缩放，放大可能会引起问题和烦恼。如果您担心一些用户会想要放大，可以改为将 user-scalable 设置为 yes。

- 2. 添加指向 small.css 的链接

```html
<link type="text/css"
    rel="stylesheet" media="all"
    href="css/small.css" />
```

此文件包含应应用于任何环境的基础级和默认样式，以及使设计最佳适配较小移动设备（如智能手机）的样式。

- 3. 添加一个条件链接，以涵盖较旧版本的 IE（不包括移动版本，移动版本获取 CSS 的小版本），加载 large.css:

```html
<!--[if (lt IE 9)&(IEMobile)]>
    ...<![endif]-->
```

由于旧版 Internet Explorer 无法使用媒体查询，我们希望确保它们的样式是为计算机屏幕设计的。

## Code 14.12 显示页面所有结构的最终 HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1,
user-scalable=no">
<title>Alice's Adventures In Wonderland | Chapter X</title>
<link type="text/css" rel="stylesheet" media="all" href="../css/cssreset.css" />
<!--[if lte IE 8]>
<script type="text/javascript" src="../script/HTML5forIE.js"></script>
<![endif]-->
<!--[if IE ]>
<style type="text/css" media="all">
@import url("../css/ie-fix.css");
</style>
<![endif]-->
<link type="text/css" rel="stylesheet" media="all" href="../css/small.css" />
<!--[if (lt IE 9)&(IEMobile)]>
<style type="text/css" media="all">
@import url("../css/medium.css");
@import url("../css/large.css");
</style>
<![endif]-->
<!--[if gte IE 9]><!-->
<style type="text/css" media="screen and (min-width: 740px) and (min-device-width: 740px),
(max-device-width: 800px) and (min-width: 740px) and (orientation:landscape)">
@import url("../css/medium.css");
</style>
<!--<![endif]-->
<!--[if gte IE 9]><!-->
<style type="text/css" media="screen and (min-width: 980px) and (min-device-width: 980px)">
@import url("../css/medium.css");
@import url("../css/large.css");
</style>
<!--<![endif]-->
<link type="text/css" rel="stylesheet" media="print" href="../css/print.css" />
</head>
<body id="chapter0" class="book aaiw chapter">
<header class="page">
<hgroup>
<h1>Alice's Adventures in Wonderland</h1>
<h2>By <cite>Lewis Carroll</cite></h2>
</hgroup>
</header>
<section>
<nav class="toc">
<ul class="menu">
<li><h2>Table of Contents</h2></li>
<ol class="drop">
<li><a href="drop">Down the Rabbit-hole</a></li>
<li><a href="AAA1M1-c02.html">The Pool of Tears</a></li>
<li><a href="AAA1M1-c03.html">A Caucus-race and a Long Tale</a></li>
<li><a href="AAA1M1-c04.html">The Rabbit sends in a Little Bill</a></li>
<li><a href="AAA1M1-c05.html">Advice from a Caterpillar</a></li>
<li><a href="AAA1M1-c06.html">Pig and Pepper</a></li>
<li><a href="AAA1M1-c07.html">A Mad Tea-party</a></li>
<li><a href="AAA1M1-c08.html">The Queen's Croquet-ground</a></li>
<li><a href="AAA1M1-c09.html">The Mock Turtle's Story</a></li>
<li><a href="AAA1M1-c010.html">The Lobster Quadrille</a></li>
<li><a href="AAA1M1-c011.html">Who Stole the Tarts?</a></li>
<li><a href="AAA1M1-c012.html">Alice's Evidence</a></li>
</ol>
</nav>
</article>
<h2>Chapter X</h2>
<span class="chaptertitle">The Lobster Quadrille</span>
</h2>
<p>The Mock Turtle sighed deeply, and drew the back of one flipper across his eyes. He looked at Alice, and tried to speak, but, for a minute or two, sobs choked his voice. "Same as if he had a bone in his throat," said the Gryphon: and it set to work shaking him and punching him in the back. At last the Mock Turtle recovered his voice, and, with tears running down his cheeks, went on again:</p>
...
<aside>
<h2>About the Author</h2>
<p><a href="">Charles Lutwidge Dodgson</a> (7 January 1832 - 14 January 1898), better known by the pseudonym Lewis Carroll was an English author, mathematician, logician, Anglican deacon and photographer. His most famous writings are Alice's Adventures in Wonderland and its sequel Through the Looking-Glass, as well as the poems "The Hunting of the Snark" and "Jabberwocky," all examples of the genre of literary nonsense. He is noted for his facility at word play, logic, and fantasy, and there are societies in many parts of the world (including the United Kingdom, Japan, the United States, and New Zealand) dedicated to the enjoyment and promotion of his works and the investigation of his life.</p>
</aside>
</footer>
<footer>
Illustrator: Arthur Rackham
</footer>
</body>
</html>
```

