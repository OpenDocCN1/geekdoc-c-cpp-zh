
## &lt;用菜单链接页面&gt;

尽管 Nanonauts 网站现在有四个页面，但除非从主页（`index.html`）开始，否则没有简便方法从一个页面转到另一个页面。因此，我们要为我们创建的所有页面添加链接。这样无论我们位于网站中的哪个位置，都能从一个页面转到另一个页面。目前，我们仅有的链接在 `index.html` 主页上。为此，我们将打开 `index.html` 文件，复制链接的 HTML 代码，然后将其粘贴到其他文件（`about-us.html`、`our-songs.html` 等）中。我们还会添加一个返回主页的链接。

### 复制链接

```html
<body>
<h1>We are the Nanonauts!</h1>
<p>This is our website. Click on a link to visit
a page:</p>
<ul>
<li><a href="about-us.html">About Us</a></li>
<li><a href="our-songs.html">Our Songs</a></li>
<li><a href="see-us-play.html">See Us Play</a></li>
<li><a href="playing-a-concert.html">Playing a
Concert</a></li>
</ul>
</body>
```

- **1.** 在代码编辑器中打开 `index.html`，并选择链接的 HTML 代码。这段代码会高亮显示。
  
  要选择链接的代码：
  - 在 `ul` 开始标签之前单击。按住鼠标或触摸板按钮，然后向下拖动，并在此过程中高亮文本。
  - 到达 `ul` 结束标签时松开按钮。
  - 选中链接后，检查是否包含了 `ul` 元素的全部开始和结束标签。

### 正确

```html
<ul>
<li><a href="about-us.html">About Us</a></li>
<li><a href="our-songs.html">Our Songs</a></li>
<li><a href="see-us-play.html">See Us Play</a></li>
<li><a href="playing-a-concert.html">Playing a Concert</a></li>
</ul>
```

![](img/52e45ce976f775dd17fd84d91912f770_32_0.png)

### 错误

```html
<ul>
<li><a href="about-us.html">About Us</a></li>
<li><a href="our-songs.html">Our Songs</a></li>
<li><a href="see-us-play.html">See Us Play</a></li>
<li><a href="playing-a-concert.html">Playing a
Concert</a></li>
</ul>
```

- **2.** 将链接复制到内存中。你可以使用键盘快捷键来完成此操作——例如 Windows 和 Linux 系统使用 `Ctrl-C`，Mac 使用 `⌘-C`。在编辑器中打开你之前创建的某个网页（在下一页的示例中，我们将使用“Playing a Concert”页面）。
- **3.** 在 **h1** 开始标签之前单击，然后粘贴链接。还要添加一个指向主页的链接。粘贴链接后，在 **`<ul>`** 开始标签之前添加一个 **`<nav>`** 开始标签，并在 **`</ul>`** 结束元素之后添加一个 **`</nav>`** 结束标签。这样就把我们的链接列表放到了一个 **nav**（navigation 的缩写）元素内。这清楚地表明这个列表是特殊的——它是菜单链接列表，而不是页面故事中的列表。

```html
<!DOCTYPE html>
<html>
<head>
<title>Playing a Concert</title>
<link type="text/css" rel="stylesheet" href="css/my-first-stylesheet.css"/>
</head>
<body>
<nav>
<ul>
<li><a href="index.html">Home</a></li>
<li><a href="about-us.html">About Us</a></li>
<li><a href="our-songs.html">Our Songs</a></li>
<li><a href="see-us-play.html">See Us Play</a></li>
<li><a href="playing-a-concert.html">Playing a Concert</a></li>
</ul>
</nav>
<h1>Playing a Concert</h1>
```

- **4.** 保存文件，然后在浏览器中打开它。你可以看到链接出现在 **h1** 元素上方。它们看起来有点奇怪，不过，如果它们像你在大多数网站上看到的顶部菜单栏那样，在顶部排成一行横跨页面，那就更好了。

## 接下来要做的事

首先，尝试做两处更改。

- 在 About Us 链接上方添加一个指向主页的链接。
- 然后将完整的链接集合复制到所有其他页面（主页除外，因为它已经有这些链接了）。

将链接放在 **h1** 元素之前的同一位置。因此，你的所有页面都应该在 **h1** 标题上方有一组指向其他页面的链接。

![](img/52e45ce976f775dd17fd84d91912f770_33_0.png)

## ‹添加菜单›

在页面顶部放一个链接列表看起来有点奇怪。但大多数网站会把这些链接排成菜单栏——看起来会像这样。

- [首页] | [关于我们] | [我们的歌曲] | [观看我们演出] | [演奏音乐会]

但你猜怎么着？仅使用 CSS 就能把链接列表变成菜单。完全不需要更改 HTML 代码。我们将通过把以下代码添加到样式表中来实现。

![](img/52e45ce976f775dd17fd84d91912f770_34_0.png)

这会把链接从列表变成菜单栏：

```css
nav ul {
  list-style-type: none;
  background-color: #B577B5;
  border: 4px solid #111111;
  border-radius: 10px;
  font-family: sans-serif;
  font-weight: bold;
  padding: 16px;
}
nav ul li {
  display: inline;
  border-right: 2px solid #111111;
  padding-right: 8px;
  padding-left: 8px;
}
nav ul li:last-child {
  border-right: none;
}
nav ul li a {
  text-decoration: none;
  color: #111111;
}
```

- [首页]
- [关于我们]
- [我们的歌曲]
- [观看我们演出]
- [演奏音乐会]

- [首页] | [关于我们] | [我们的歌曲] | [观看我们演出] | [演奏音乐会]

### 更复杂的规则！

在我们之前的示例中，规则的花括号外只有一个元素名称。例如，下面有三条声明，它们为一个 h1 元素设置颜色、字体系列和字体大小。

```css
h1 {
  color: #111111;
  font-family: sans-serif;
  font-size: 32px;
}
```

```css
nav ul li {
  display: inline;
  border-right: 2px solid #111111;
  padding-right: 8px;
}
```

但在菜单示例中，花括号外的元素变得稍微复杂一些。我们看到的不再只是一个元素名称，而是几个用空格分隔的元素名称。可以把它想象成一个地址。这个示例适用于位于 `nav` 元素内的 `ul` 内的每一个 `li`。因此，这些规则只应用于 `nav` 元素内的列表项——而不是“普通”列表。要查看每条声明的效果，我们将采用第 28 页提示中描述的相同方法，先添加空规则，然后一次添加一条声明。如果你按下面描述的顺序添加声明，将有助于你理解样式表的工作原理。

### 1.

```css
nav ul {
  list-style-type: none;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

移除 `nav` 元素内列表的项目符号。你可以使用 `list-style-type` 声明更改项目符号的外观，或将其完全移除。

- `list-style-type: none;` 移除项目符号
- `list-style-type: square;` 将其改为方块。

![](img/52e45ce976f775dd17fd84d91912f770_35_0.png)

### 2.

```css
nav ul {
  list-style-type: none;
  background-color: #B577B5;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

将列表（`ul` 元素）的背景颜色更改为较深的紫色（`#B577B5` 是这种颜色的十六进制值）。

![](img/52e45ce976f775dd17fd84d91912f770_35_1.png)

### 3.

```css
nav ul {
  list-style-type: none;
  background-color: #B577B5;
  border: 4px solid #111111;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

为列表添加 4 像素宽的边框。边框是实线，而不是点线或虚线，并且是纯黑色（`#111111` 是这种颜色的十六进制值）。试着更改：

- 边框的像素宽度
- 将边框样式从 **solid** 改为 **dotted** 或 **dashed**
- 将从在线颜色选择器中选择的十六进制值改为你选择的值（见第 31 页）。

![](img/52e45ce976f775dd17fd84d91912f770_35_2.png)

### 4.

```css
nav ul {
  list-style-type: none;
  background-color: #B577B5;
  border: 4px solid #111111;
  border-radius: 10px;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

为边框添加圆角。试着更改 **border-radius** 的值，看看它会有什么效果。试试：

- 5px
- 20px

![](img/52e45ce976f775dd17fd84d91912f770_36_0.png)

### 5.

```css
nav ul {
  list-style-type: none;
  background-color: #B577B5;
  border: 4px solid #111111;
  border-radius: 10px;
  font-family: sans-serif;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

确保字体为 sans-serif。如果你没有指定 **font-family**，它将使用浏览器的默认字体显示。试着将其改为 *cursive* 或 *fantasy*，看看它们的效果。

![](img/52e45ce976f775dd17fd84d91912f770_36_1.png)

### 6.

```css
nav ul {
  list-style-type: none;
  background-color: #B577B5;
  border: 4px solid #111111;
  border-radius: 10px;
  font-family: sans-serif;
  font-weight: bold;
}
nav ul li {
}
nav ul li:last-child {
}
nav ul li a {
}
```

让字体看起来更粗、更深。

![](img/52e45ce976f775dd17fd84d91912f770_36_2.png)

