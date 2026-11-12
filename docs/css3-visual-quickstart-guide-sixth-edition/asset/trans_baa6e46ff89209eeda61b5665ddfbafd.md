

代码 11.7 已添加到 visual-formatting-properties.css—当应用于代码 11.1 时，此 CSS 为 article 添加投影，为 aside 添加投影和内阴影。它还为画廊图像添加阴影，但由于它们被裁剪，因此不显示。

```
/*** visualformatting-properties.css ***/
header {
 box-shadow: 0 10px 10px
 rgba(0,0,0,.5);
}
article {
 box-shadow: 5px 5px 10px
 rgba(0,0,0,.7); }
aside {
 box-shadow: 1px 1px 5px 1px
 rgba(0,0,0,.25) inset,
 3px 3px 15px
 rgba(0,0,0,.5); }
figure {
 box-shadow: 5px 5px 10px
 rgba(0,0,0,.7); }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_324_0.png)

将代码 11.7 应用于代码 11.1。阴影增加了书页的错觉，赋予它们重量感和厚度感。

- 模糊长度值是正值，用于增加阴影的模糊度并使其扩散。值越高，阴影越大越淡。此值为可选，但未设置时默认为 0。

- 扩展长度值——有时称为收缩——是正值，用于指定阴影渐变的断点。它的效果是在阴影开始渐变之前增加其较暗区域。此值为可选，但未设置时默认为 0。

- 颜色值是第 7 章中概述的任何标准颜色值。此值为可选，但未设置时默认为 transparent，使阴影不可见。

- inset 导致阴影出现在元素边缘内部，创建内阴影。这是可选的。

- 按需要添加更多阴影。3px 3px 15px rgba(0,0,0,.5); 你可以根据需要重复阴影代码任意次，以在元素下方或内部创建多个阴影，每个值列表之间用逗号 (, ) 分隔，并始终记得用分号 (;) 结束 CSS 规则。如果在 x/y 偏移长度值后只包含一个长度值，则将其视为模糊值，而非扩展值。

## 方框“阴影”效果

方框阴影可以实现一些很棒的效果，几乎可以取代 border 和 outline 属性。以下是我创建类的几个示例：

### 框架

框架效果使用扩展设置为 0 的投影来在方框周围创建框架。与 border 相比，它的优势在于可以有多个边框，并且与 outline 属性一样，它不会占用设计中的任何空间。

```
.frame {
    box-shadow: 0 0 0 5px
    hsl(0,100%,0%),
    0 0 0 10px hsl(90,100%,20%),
    0 0 0 15px hsl(180,100%,40%),
    0 0 0 20px hsl(270,100%,80%),
    0 0 0 25px hsl(0,100%,80%),
    0 0 0 30px hsl(90,100%,100%); }
```

### 内嵌框架

与框架效果类似，只是边框位于元素内部。你无法使用 border 属性实现此效果。

```
.insetframe {
background: rgb(53,53,53);
box-shadow: 0 0 0 15px
hsla(0,0%,100%,.5) inset,
0 0 0 10px hsla(0,0%,100%,.5)
inset; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_325_0.png)

使用多个 Box-shadow 创建多边框效果。

![](img/e1ed1e3c1873fa9fc855210fb83699d0_325_1.png)

使用 Box-shadow 在图像内部创建透明边框。

## 代码 11.8 最终的 visualformatting-properties.css

```
/*** visualformatting-properties.css ***/

header, footer {
    position: fixed;
    z-index: 999;
}
header {
    top: 0;
    left: 0;
    box-shadow: 0 10px 10px rgba(0,0,0,.5);
}
footer {
    bottom: 0;
    left: 0;
}
hgroup h2 {
    position: relative;
    top: 15px;
    right: 25px;
}
article {
    box-shadow: 5px 5px 10px rgba(0,0,0,.7);
}
aside {
    position: absolute;
    right: 4%;
    top: 150px;
    opacity: .5;
    clip: rect(30px 230px 60px 10px);
    box-shadow: 1px 1px 5px 1px rgba(0,0,0,.25)
    inset, 3px 3px 15px rgba(0,0,0,.5);
}
aside:hover {
    clip: auto;
    opacity: 1.0;
}
figure {
    box-shadow: 5px 5px 10px rgba(0,0,0,.7);
}
footer nav {
    position: relative;
    top: 20px;
}
strong {
    position: relative;
    top: -.15em;
}
```

## 综合起来

visualformatting-properties.css 的完成代码应类似于代码 11.8。

## 转换和过渡属性

虽然使用 transform 和 transition 属性仍颇具争议，但无需使用 JavaScript 即可将这些更改应用于元素的能力，将对 Web 设计师和开发人员大有裨益。将这些视为时间样式：它们不仅像其他样式一样改变元素的外观，还会随时间和空间改变该元素的外观。

本章介绍的样式极其新颖，至少按 Web 标准来看是这样。虽然 Webkit 已以某种形式拥有它们一段时间，Firefox 和 Opera 也已开始采用它们，但直到最近，许多属性才被添加到 Internet Explorer，并且工作已着手将它们纳入标准 CSS3 规范。我会谨慎对待这些属性，同时确保它们在旧浏览器中能优雅降级，但我迫不及待想看看你如何使用它们。

- 本章内容
- 入门 308
- 转换元素 311
- 元素状态之间的过渡 320
- 综合起来 325

## 入门

本章示例中，我将使用《爱丽丝梦游仙境》第 8 章的文本和图像（代码 12.1A），其中包含我收集到“画廊”中的几幅黑白图形，以便我们可以尝试对其应用转换和过渡。我们将在本章中构建 CSS 文件 transformation-transition-properties.css（代码 12.1B）。首先，添加一些样式来定位我们图形中的图像（ID 为 f1、f2 和 f3）。请参阅本章末尾“综合起来”部分中此 CSS 文件的完成版本。

### 代码 12.1A 第 12 章的 HTML5 代码与上一章类似。它链接到第 5、6、7、8、9、10 和 11 章的最终 CSS，以及本章将构建的名为 transformation-transition-properties.css 的新文件。

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>Alice&#8217;s Adventures In Wonderland | Chapter VIII</title>
<link href=".../css/font-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/text-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/color-background-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/list-table-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/ui-generatedcontent-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/box-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/visualformatting-properties.css" type="text/css" rel="stylesheet" media="all">
<link href=".../css/transformation-transition-properties.css" type="text/css" rel="stylesheet" media="all">
</head>
<body id="chapter8" class="book aaaiw chapter">
<header class="page">
<hgroup>
<h1>Alice&#8217;s Adventures in Wonderland</h1>
<h2>by <cite>Lewis Carroll</cite></h2>
</hgroup>
</header>
<article>
<h2>Chapter VIII</h2>
<span class="chaptertitle">The Queen's Croquet-Ground</span>
</article>

<p>A large rose-tree stood near the entrance of the garden: the roses growing on it were white,
but there were three gardeners at it, busily painting them red. Alice thought this a very curious
thing, and she went nearer to watch them, and just as she came up to them she heard one of them
say <q>look out now, five! Don't go splashing paint over me like that!</q></p>

...

<p>The Cat's head began fading away the moment he was gone, and by the time he had come back with
the Duchess, it had entirely disappeared; so the King and the executioner ran wildly up and down
looking for it, while the rest of the party went back to the game.</p>
<div class="gallery">
<figure id="f1" class="illo bw-illo" style="width: 300px;">
<img src=".../images/illos/p0103-image.png" width="300" height="400" alt="Playing croquet" title="" />
</figure>
<figure id="f2" class="illo bw-illo" style="width: 380px;">
<img src=".../images/illos/p0106-Image.png" width="380" height="179" alt="The Cat" title="" />
</figure>
<figure id="f3" class="illo bw-illo" style="width: 286px;">
<img src=".../images/illos/p0109-Image.png" width="286" height="300" alt="The Executioner" title="" />
</figure>
</div>
</article>
<aside>
<h2>About the Author</h2>
<p><b>Charles Lutwidge Dodgson</b> (7 January 1832 – 14 January 1898), better known by the
pseudonym Lewis Carroll was an English author, mathematician, logician, Anglican deacon and
photographer. His most famous writings are Alice's Adventures in Wonderland and its sequel
Through the Looking-Glass, as well as the poems "The Hunting of the Snark" and "Jabberwocky",
all examples of the genre of literary nonsense. He is noted for his facility at word play,
logic, and fantasy, and there are societies in many parts of the world (including the United
Kingdom, Japan, the United States, and New Zealand) dedicated to the enjoyment and promotion
of his works and the investigation of his life.</p>
</aside>
<footer>
<nav>
<a href=".../AIWL-ch07.html" class="prev">The Mock Turtle's Story</a>
<a href="...toc.html">Table of Contents</a>
<a href=".../AIWL-ch09.html" class="next">Who Stole the Tarts?</a>
</nav>
</footer>
</body>
</html>

