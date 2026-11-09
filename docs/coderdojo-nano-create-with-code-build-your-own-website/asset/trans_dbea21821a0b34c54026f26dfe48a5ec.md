
- 3. 完成更改后，在浏览器中刷新网页。注意，更改后的菜单项不再可点击。单独添加 **class** 属性并没有产生任何效果。试着刷新菜单，它看起来还是一样。但是，添加 **class** 属性可以让你在 **my-first-stylesheet.css** 文件中选中该链接，并将其颜色改为灰色，以暗示它不可点击。方法如下：

```css
nav li a {
  text-decoration: none;
}
nav li.selected {
  color: #606060;
}
```

- 4. 刷新后，你会看到选中的链接变为灰色。你所做的是添加了一条新规则，它仅适用于具有 **selected** 的 **class** 属性的 **li** 元素。注意 CSS 文件中的语法——在规则中不是指定 **li**，而是指定 **li.selected**。

### 忍者提示

![](img/52e45ce976f775dd17fd84d91912f770_57_0.png)

> `nav li.selected` 的意思是“nav 元素内 class 为 selected 的 li 元素”

- 5. 最后，通过向 CSS 添加一条新规则，让链接在鼠标悬停时显示下划线。这条规则定义了当光标悬停在元素上时会发生什么。

```css
nav li a:hover {
  text-decoration: underline;
}
```

选择器中的 **:hover** 部分称为**伪类**。伪类会在某些特殊情况下改变元素的外观。以下伪类可用于设置链接样式：

- `unvisited` — 设置在你访问链接目标之前链接应如何显示。
- `visited` — 设置在你访问链接目标之后链接应如何显示。
- `hover` — 设置当光标悬停在元素上时应发生什么。
- `active` — 设置当你在释放鼠标按钮之前点击链接时应发生什么。

因此，一组链接格式规则可能如下所示：

```css
a:link {
  color: blue;
}
a:visited {
  color: purple;
}
a:hover {
  text-decoration: underline;
}
a:active {
  text-decoration: underline;
  background-color: black;
  color: white;
}
```

## 完成！

### 接下来要做的事

- 尝试各种链接格式设置选项。
- 对示例中的规则做一些更改，看看它对你的网站有什么影响。

## CSS 盒模型

使用样式表为页面设置样式时，理解 CSS 工作原理有一个秘诀——**CSS 盒模型**。盒模型的工作原理是想象每个 HTML 元素都位于一个盒子中。这个盒子包含三个区域：

- padding（内边距）
- border（边框）
- margin（外边距）——此盒子与下一个盒子之间的间距

如下图所示。

![](img/52e45ce976f775dd17fd84d91912f770_58_0.png)

![](img/52e45ce976f775dd17fd84d91912f770_58_1.png)

使用 CSS，你可以分别更改盒子的每一个部分。例如，只需调整内边距和间距属性，就能大幅改变标题和段落的外观。

除了更改盒子各部分的大小，你还可以更改盒子不同部分的颜色。你在网页上看到的许多出色视觉效果都是通过这种方式创建的。

![](img/52e45ce976f775dd17fd84d91912f770_59_0.png)

### 认识 NanoNauts！

你还可以通过设置盒子的宽度或高度来更改其整体大小。用于包含单个单词或短语（例如 **em** 或 **strong**）的元素称为**内联元素**。对于内联元素，盒子会贴合单词或短语。用于包含整个段落的元素称为**块级元素**。对于块级元素，盒子通常会横跨页面的整个宽度。

![](img/52e45ce976f775dd17fd84d91912f770_59_1.png)

这些**盒子**是围绕**内联**元素绘制的。

- 这个盒子是围绕一个块级元素绘制的。

下表显示了哪些常见元素通常是块级元素，哪些通常是内联元素：

| 内联 | 块级 |
|---|---|
| a | h1 到 h6 |
| em | p |
| strong | ul, ol |
|  | li |

我们说“通常”是内联或“通常”是块级，是因为如有需要，你可以在样式表中更改这一点。我们在前面菜单格式示例的第 8 步（见第 38 页）就这样做了：当时我们更改了菜单内的 **li** 元素，使它们并排显示，而不是一个在另一个上方。我们通过将 **display** 属性设置为 **inline** 来实现这一点，如下所示：

```css
nav li {
  display: inline;
}
```

## 为网站添加吉他调音器

### 嵌入 Scratch 项目

在意识到嵌入视频和地图有多么容易之后，Holly 想知道她是否能在网站中嵌入一个吉他调音器。但她从哪里弄到一个呢？然后她想起，她的姐姐一直在 CoderDojo 使用 Scratch 编程语言学习制作游戏。她去了 Scratch 网站，搜索“guitar tuner”。结果有很多。

她找到了一个喜欢的，但看不到任何嵌入选项！幸运的是，她的姐姐来救场了——Holly 必须先登录 Scratch 网站，Embed 按钮才会出现在游戏底部的信息栏中。她最喜欢的吉他调音器有以下嵌入代码：

```html
<iframe allowtransparency="true" width="485" height="402" src="//scratch.mit.edu/projects/embed/16403918/?autostart=false" frameborder="0" allowfullscreen></iframe>
```

请注意，只有你的网页在线时，调音器才会显示出来。有关如何让页面上线的更多信息，请参见第 90 页。

![](img/52e45ce976f775dd17fd84d91912f770_60_0.png)

![](img/52e45ce976f775dd17fd84d91912f770_60_1.png)

### 要记住的术语

![](img/52e45ce976f775dd17fd84d91912f770_60_2.png)

**iframe** ——你可能已经注意到，YouTube 视频和 Google 地图也都使用了 `iframe` 元素。iframe 允许你将另一个网站的内容嵌入到你的网页中。你可以通过在 iframe 的 `src` 属性中输入 URL 来指定在哪里找到该内容。

## JAVASCRIPT

![](img/52e45ce976f775dd17fd84d91912f770_61_0.png)

在开发网站时，你迟早会遇到 **JavaScript**。**JavaScript** 是一种编程语言，可让你为页面添加各种特殊效果和功能，比如游戏、图表和动画。本书没有足够的篇幅向你展示 **JavaScript** 能做的所有事情，但下面这个例子可以让你了解你能做的一些事情。我们将使用一个简单的函数来将一张图片替换为另一张。

图像交换器背后的 JavaScript 被嵌入在页面中。之所以称为嵌入，是因为实际的 JavaScript 位于页面 body 内的 **script** 元素中。（如果你愿意，也可以将 JavaScript 放入单独的文件中。有关这一点以及 JavaScript 一般信息的更多内容，请参见 scholastic.com/coder-dojo/javascript。）

```html
<!DOCTYPE HTML>
<html>
<head>
<link type="text/css" rel="stylesheet" href="css/full-style.css"/>
</head>
<body>
<p>
<img id="display-image" onclick="swapImage()" src="images/01.png" width="180" height="180"/>
</p>
<p>Click the image to change it!</p>
<script>
function swapImage() {
  var imageDisplayed = document.getElementById('display-image');
  if (imageDisplayed.src.match("images/01.png")) {
    imageDisplayed.src = "images/02.png";
  }
  else {
    imageDisplayed.src = "images/01.png";
  }
}
</script>
</body>
</html>
```

如果我们查看上面的代码，可以看到 **img** 元素有一个名为 **onclick** 的属性，其值为 **swapImage()**。

![](img/52e45ce976f775dd17fd84d91912f770_62_0.png)

`onclick` 属性的用途是包含一个函数的名称，当图像被点击时将调用该函数。函数是我们给执行有用任务的某些代码起的名称。在本例中，`swapImage()` 函数包含在 `script` 元素内。该函数会启动一系列按如下方式发生的过程：

- 1. 当图像被点击时，`swapImage()` 函数会运行。

```html
<img id="display-image" onclick="swapImage()" src="images/01.png" width="180" height="180">
```

- 2. 这使图像（通过其 `id` 为 `display-image` 来标识）作为名为 `imageDisplayed` 的变量（`var`）可供脚本使用。（`id` 属性允许你为元素指定唯一的标识名称。）

```javascript
var imageDisplayed = document.getElementById('display-image');
```

- 3. 如果 `imageDisplayed` 变量的源（`src`）当前设置为 `images/01.png`，那么函数会将其更改为 `images/02.png`。

```javascript
if (imageDisplayed.src.match("images/01.png")) {
  imageDisplayed.src = "images/02.png";
}
```

- 4. 但是，如果 `imageDisplayed` 变量的源（`src`）当前设置为 `images/02.png`，则会将其更改为 `images/01.png`。

```javascript
else {
  imageDisplayed.src = "images/01.png";
}
```

