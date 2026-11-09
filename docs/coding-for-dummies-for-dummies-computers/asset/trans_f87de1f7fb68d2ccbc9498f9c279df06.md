
`title` 属性提供关于元素的提示信息，当鼠标光标悬停在受影响的文本上时会出现（换句话说，就是一个 `tooltip`）。在本例中，单词 USA 使用 `<h1>` 标签被样式化为标题，并将 `title` 属性设置为 "United States of America"。那么在浏览器中，当你将鼠标光标放在单词 USA 上时，文本 United States of America 会显示为工具提示。（见图 4-3。）

![](img/5a907eb39993e80f28c82efc2e4632b3_60_0.png)

图 4-3：带有 `title` 属性的标题具有工具提示。

`hidden` 属性表示该元素不相关，因此浏览器不会渲染任何带有此属性的元素。在本例中，单词 New York City 永远不会出现在浏览器窗口中，因为 `hidden` 属性位于开头的 `<h1>` 标签中。更实际地说，`hidden` 属性通常用于对用户隐藏字段，以便他们无法编辑这些字段。例如，一个 RSVP 网站可能希望包含日期和时间字段，但将其对用户视图隐藏。

`hidden` 属性是 HTML5 中的新属性，这意味着它可能在某些较旧的浏览器上不起作用。

你不必一次只使用一个属性。你可以在开头的 HTML 标签中包含多个属性，如下所示：

```html
<h1 title="United States of America" lang="en">USA</h1>
```

在本例中，我使用了 `title` 属性和 `lang` 属性，将其设置为 `"en"`，以指定该元素的内容为英语。

包含多个属性时，请用单个空格分隔每个属性。

## 第二部分：构建静默且可交互的网页

使用属性时请牢记以下规则：

- 如果使用属性，请始终将属性包含在开头的 HTML 标签中。
- 多个属性可以修饰单个元素。
- 如果属性有值，则使用等号（=）并将值括在引号中。

### 让 head、title 和 body 高于其余部分

HTML 文件以特定方式构建，以便浏览器能够正确解释文件的信息。每个 HTML 文件都有相同的五个元素：其中四个元素的开始标签和结束标签只出现一次且仅出现一次，另一个元素出现一次且不需要结束标签。它们如下：

- `<!DOCTYPE html>` 必须首先出现在你的 HTML 文件中，并且只出现一次。此标签让浏览器知道你正在使用哪个版本的 HTML。在本例中，它是最新版本 HTML5。此元素不需要结束标签。对于 HTML4 网站，HTML 文件的第一行会写成 `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">`。

![](img/5a907eb39993e80f28c82efc2e4632b3_61_0.png)

- `html` 表示 HTML 文档的根或开头。`<html>` 标签之后首先是开始和结束的 `<head>` 标签，然后是开始和结束的 `<body>` 标签。
- `head` 包含其他元素，这些元素指定页面的通用信息，包括标题。
- `title` 定义浏览器标题栏或页面标签中的标题。像 Google 这样的搜索引擎使用 `title` 在搜索结果中对网站进行排名。
- `body` 包含 HTML 文档的主要内容。在开始和结束 body 标签之间列出的文本、图像和其他内容由浏览器显示。

下面是一个具有这五个标签的结构正确的 HTML 文件示例（见图 4-4）：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Favorite Movie Quotes</title>
</head>
<body>
    <h1>"I'm going to make him an offer he can't refuse"</h1>
<h1>"Houston, we have a problem"</h1>
<h1>"May the Force be with you"</h1>
<h1>"You talking to me?"</h1>
</body>
</html>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_62_0.png)

**图 4-4：** 使用基本 HTML 元素创建的网页。

![](img/5a907eb39993e80f28c82efc2e4632b3_62_1.png)

强烈建议使用空格来缩进和分隔标签。它可以帮助你和其他人阅读和理解你的代码。然而，这些空格只为你和其他阅读代码的人服务。你的浏览器不会在意。就浏览器而言，你可以将所有标签放在一行中运行。（不过，不要这样做。下一个阅读你代码的人会非常不高兴。）HTML 确实会识别并显示开始和结束 HTML 标签之间文本中的第一个空白字符。

![](img/5a907eb39993e80f28c82efc2e4632b3_62_2.png)

我们的示例有许多 h1 标签，但只有一个开始和结束的 html、head、title 和 body 标签。

## 熟悉常见的 HTML 任务和标签

你的浏览器可以解释一百多个 HTML 标签，但大多数网站只使用少数几个标签来完成浏览器内的大部分工作。为了理解这一点，让我们做一个小练习：想一想你最喜欢的新闻网站。想到了吗？现在连接到互联网，打开浏览器，输入该网站的地址。带上这本书，慢慢来——我可以等！

如果你现在无法访问互联网，可以看看图 4-5 中来自我最喜欢的新闻网站 *《纽约时报》* 的一篇文章。

![](img/5a907eb39993e80f28c82efc2e4632b3_63_0.png)

*图 4-5：一篇《纽约时报》文章，包含标题、段落、超链接和图像。*

仔细看看你屏幕上的新闻网站（或者看看我的）。四个 HTML 元素用于创建页面的大部分内容：

- **标题：** 标题以粗体显示，并且字体大小比周围文本更大。
- **段落：** 每个故事都组织成段落，段落之间用空白分隔。
- **超链接：** 网站的主页和文章页面有指向其他故事的链接，以及在 Facebook、Twitter 和 Google+ 等社交网络上分享故事的链接。
- **图像：** 作者在故事中放置图像，但也会寻找图标和徽标等网站图像。

在接下来的章节中，我将解释如何编写代码来创建这些常见的 HTML 功能。

### 编写标题

使用标题来描述页面的某个部分。HTML 有六级标题（见图 4-6）：

- h1，用于最重要的标题
- h2，用于副标题
- h3 到 h6，用于不太重要的标题

浏览器渲染 h1 标题的字体大小大于 h2 的字体大小，而 h2 的字体大小又大于 h3 的字体大小。标题以开始标题标签、标题文本和结束标题标签组成，如下所示：

`<h1>Heading text here</h1>`

以下是一些展示各种标题的额外代码示例：

```html
<h1>Heading 1: "I'm going to make him an offer he can't refuse"</h1>
<h2>Heading 2: "Houston, we have a problem"</h2>
<h3>Heading 3: "May the Force be with you"</h3>
<h4>Heading 4: "You talking to me?"</h4>
<h5>Heading 5: "I'll be back"</h5>
<h6>Heading 6: "My precious"</h6>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_64_0.png)

图 4-6：使用 h1 到 h6 元素创建的标题。

> 打开什么就要关闭什么。对于标题，记得包含结束标题标签，例如 `</h1>`。

![](img/5a907eb39993e80f28c82efc2e4632b3_65_0.png)

### 在段落中组织文本

要以段落显示文本，你可以使用 p 元素：在段落前放置开始 `<p>` 标签，在其后放置结束标签。p 元素接收文本，并在结束标签后插入换行。

要在任何元素后插入单个换行，请使用 `<br>` 标签。`<br>` 标签是自闭合的，因此不需要结束标签，也不使用 `</br>`。

段落以开始段落标签、段落文本和结束段落标签组成：

```html
<p>Paragraph text here</p>
```

一些额外的段落编码示例（见图 4-7）：

```html
<p>Armstrong: Okay. I’m going to step off the LM now.</p>
<p>Armstrong: That’s one small step for man; one giant leap for mankind.</p>
<p>Armstrong: Yes, the surface is fine and powdery. I can kick it up loosely
             with my toe. It does adhere in fine layers, like powdered
             charcoal, to the sole and sides of my boots.</p>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_65_1.png)

**图 4-7：** 使用 p 元素在段落中显示的文本。

### 链接到你的（心中）内容

超链接是 HTML 最有价值的功能之一。包含指向其他来源的超链接引用的网页允许读者只需点击一下即可访问这些来源，这是相对于印刷页面的巨大优势。

