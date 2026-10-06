

## 4. 处理 CSS。点击代码字段下方的“Process CSS”按钮。几秒钟后，将出现一个消息列表，显示发现的无效属性。在下方你可以下载或复制你的代码（代码 15.6）。

如果你正在使用 CSS，可能会看到几个无效属性，因为压缩器（Minifier）并不包含这些属性。

## 5. 测试，测试！根据你修改代码的程度，它可能会发生细微变化，也可能变化巨大。无论如何，它已经不同了，行为也可能不同。如果你在使用新的 CSS 代码遇到问题，请尝试使用不同的设置重新压缩。

代码 15.6 修改后的相同 CSS 代码。

```css
/* CSS3 1.3: Wed, 11 Aug 2010
-0500 %/line(margin:0 10px 10px 20px);
article{moz-border-radius:20px;
webkit-border-top-radius:20px;\webkit-
border-radius:transparent-solid;border-top:10px
transparent-solid;border-top-right
radius:20px;float:left;max-height:90px;
width:580px;webkit-height:60px;padding:80px
width:65%;{h2:border-top:2px solid
rgba(142,137,129,5),s} article
avigation2{border-top:none;padding:0}
aside{moz-border-radius-bottom-left:20px 0 20px;
webkit-border-top-left:20px;border-radius:20px
0 20px;margin:10px;overflow:auto;padding
imageurl(../images/border-02.png)
rounded;webkit-border-image:url(../images/
border-02.png) 27 round;border:item double
#8e981;round body,header,page,.footer.
page(margin:0;padding:0)figcaption{display:block
top:2px solid rgba(142,137,129,5)};figure{display:block
padding:10px){moz-border-radius:5px;
webkit-border-radius:5px;border:6px double
rgba(142,137,129,5);border-radius:5px;display
play:block;float:left;margin:0 10px
0;width:300px}footer(clear:both)h1{margin:0
20px 10px 10px%;padding-top:10px}navigation.
global(display:block)navigation.global
l(display:inline;margin-right:10px;padding-
right:10px)
```

## 32 CSS 最佳实践

在本书的后续中，我提供了大量的技巧、建议和提示。我尝试在展示的所有代码中遵循我自己的建议，但创建实用示例的必要性与编码最佳实践的需求必须取得平衡。因此，为了消除任何疑惑，这里是 CSS 的 32 个最重要的最佳实践，并附有交叉引用，显示你可以在哪里找到更多信息。

- 1. 除非值为 0，否则始终为值指定单位。这是一个简单的等：`0px = 0in = 0em = 0cm = 0% = 0mm = 0`。零永远是零，你不需要定义它是哪种 0。参见引言中的“本书中使用的单位”。

- 2. 结构优先，演示在后。有些设计者希望在没有先放置 HTML 结构的情况下就开始设计页面，但这就像试图在一个尚未搭建框架的房子上安装外墙板。参见第 2 章。

- 3. 指定文档类型声明（doctype）。在如今，使用 doctype 是不言而明的，但没有 doctype 的 HTML 文档就像没有封面的书。你不仅不知道里面有什么，整个结构也往往会崩溃。参见第 2 章。

- 4. 所有样式都应该是外部的。为了让网站易于修改，最终样式应*始终*位于外部文件中，而*永远*嵌入或内联。在开发期间，嵌入或内联样式是可以接受的，但在部署之前应全部移动到外部样式表中。参见第 3 章“添加样式”。

- 5. 尽量减少外部样式表的数量。这似乎与之前的陈述矛盾，但每个外部样式表都是对 Web 服务器的调用，每次调用都会减慢页面加载。无论你是使用 `<link>` 还是 `@import` 都是如此。参见第 3 章“添加样式”。

- 6. 将样式链接放在 `<head>` 中，永远放在 `<body>` 中。放置在 `<body>` 文档中的样式会在 Web 页面显示*之后*应用，导致整个文档在应用样式重新渲染时短暂闪烁。这既令人人烦又不美观。参见第 3 章“添加样式”。

