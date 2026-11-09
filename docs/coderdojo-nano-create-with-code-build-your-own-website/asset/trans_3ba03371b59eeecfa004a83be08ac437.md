

## 9.

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
}
nav ul li:last-child {
}
nav ul li a {
}
```

在每条菜单项的右侧添加一条 2 像素宽的分隔线。你可以通过修改 `px` 前面的数字让线条变粗或变细。注意，这条声明是如何将边框的三个独立属性——粗细、线型和颜色——结合在一起的。

![](img/52e45ce976f775dd17fd84d91912f770_38_0.png)

## 10.

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
}
nav ul li a {
}
```

在每条菜单项与其右侧的分隔线之间添加一些额外的间距。

![](img/52e45ce976f775dd17fd84d91912f770_38_1.png)

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
}
```

移除最后一条分隔线。如你所见，我们再次引入了一条新规则。这条规则以 **nav ul li:last-child** 开头。规则中包含的 **last-child** 条件意味着它只适用于 **nav** 元素内 **ul** 元素中的最后一个 li 元素。

![](img/52e45ce976f775dd17fd84d91912f770_39_0.png)

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
}
```

移除菜单项的下划线。在网页中，链接带下划线很有用，但在顶部菜单中却不好看。我们可以将 **text-decoration** 的值设为 **none** 来移除下划线。规则中的 **nav ul li a** 部分表示它适用于 **nav** 元素内 **ul** 元素中 **li** 元素里的 **a** 元素。

![](img/52e45ce976f775dd17fd84d91912f770_39_1.png)

```css
nav ul {
  list-style-type: none;
  background-color: #B577B5;
  border: 4px solid #111111;
  border-radius: 12px;
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

确保链接为黑色。为了完善我们的菜单，我们将链接改为黑色，使其与菜单栏的其他配色方案融为一体。

## 音乐会演出

登台开一场音乐会会非常有趣！也可能非常吓人！有时两种感觉同时出现。

所以，我们整理了一份打造精彩音乐会的顶级贴士清单。

### 写下演出曲目单

曲目单就是按演出顺序列出的所有歌曲清单。

给每个人都复印一份。

把它打印得大大的！这样即使它掉在地上、跑到你脚边，或者现场灯光不太好，你也能看得清。

### 记得带好备用件

有些乐器的部件如果磨损或损坏，就需要更换。例如：

- 吉他弦
- 萨克斯管或单簧管的簧片
- 鼓槌

![](img/52e45ce976f775dd17fd84d91912f770_40_0.png)

![](img/52e45ce976f775dd17fd84d91912f770_40_1.png)

## 格式化页面的特定部分

你可能还记得，添加菜单时，我们用 **nav** 元素将它包起来——就像这样：

```html
<nav>
  <ul>
  </ul>
</nav>
```

这样做既让代码更容易阅读，也让我们可以在样式表中添加只适用于菜单的规则。

右侧的这条规则只会改变 **nav** 元素内 **ul** 元素的背景颜色。

```css
nav ul {
  background-color: #B577B5;
}
```

这个列表将会有紫色背景：

```html
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
```

但这个列表不会呈现紫色背景：

```html
<body>
<ul>
<li><a href="index.html">Home</a></li>
<li><a href="about-us.html">About Us</a></li>
<li><a href="our-songs.html">Our Songs</a></li>
<li><a href="see-us-play.html">See Us Play</a></li>
<li><a href="playing-a-concert.html">Playing a Concert</a></li>
</ul>
```

如果你添加下面这条规则，它就会改变两个列表的背景颜色。

```css
ul {
  background-color: #B577B5;
}
```

另外请注意，你可以为元素创建规则，让它们只在位于其他元素内部时才生效。

因此，右侧的规则**仅**适用于 **nav** 元素内的 **ul** 元素内部的 **li** 元素。稍后，在设计更加复杂的页面时，我们会用到这一技术（它的正式名称是**上下文选择**）。

```css
nav ul li {
  display: inline;
  border-right: 2px solid #111111;
  padding-right: 8px;
}
```

## 我很特别！使用 `class` 属性

另一种标识具有特殊含义、并需要以特定方式设置样式的元素的方法，是使用 **class** 属性。

### 让我们看看这是如何工作的……

Nanonauts 乐队决定在某些页面中加入给音乐人的“小贴士”。他们希望这些贴士能从页面其他内容中脱颖而出——就像这样：

![](img/52e45ce976f775dd17fd84d91912f770_42_0.png)

> **小贴士：** 如果你弹错了一个音符或出了差错，不要停下来——假装你本来就想这么弹！

他们做的第一件事，就是在 HTML 页面中，给包含贴士的 `<p>` 元素添加一个 `class` 属性。就像这样：

```html
<p class="top-tip">If you hit a wrong note or make a mistake, don't stop playing - just keep going and look as though you meant it!</p>
```

然后，Nanonauts 使用样式表以特殊方式为贴士设置格式，使它们脱颖而出。下面就是他们用来格式化小贴士的规则：

```css
p.top-tip {
  border: 4px solid #EA6E8E;
  border-radius: 10px;
  padding: 16px;
  background-color: #C5E8FB;
}
p.top-tip:before {
  color: black;
  content: "TOP TIP: ";
  font-weight: bold;
}
```

### 接下来要做的事

![](img/52e45ce976f775dd17fd84d91912f770_42_1.png)

- 看看你能不能给自己的页面添加一些小贴士。
  - 你能弄清楚 `p.top-tip:before` 规则的作用吗？
    - 提示：试着把 `content: "Top Tip: "` 改成 `content: "Mega Tip! "`。
  - 你能只让“Top Tip:”这几个词显示为橙色吗？
  - 如果你把边框从 `solid` 改成 `dashed`，会发生什么？

### 更多线上内容

![](img/52e45ce976f775dd17fd84d91912f770_42_2.png)

如果你想让网页看起来非常精美，能够分辨出页面的各个部分就很重要。`class` 属性隐藏着一个秘密，它可以让你为一个元素应用多条格式化规则。点击这里了解 `class` 属性：scholastic.com/coder-dojo/class

## 需要记住的词汇

![](img/52e45ce976f775dd17fd84d91912f770_43_0.png)

**class 属性**——我们已经知道了什么是属性。大多数属性只能用于特定元素，但 **class** 属性很特殊，因为它可以应用于任何 HTML 元素。例如：

```html
<p class="top-tip">
<h3 class="author">
<table class="football-league-table">
<li class="selected-menu-item">
```

你可以使用 **class** 属性来标识特定元素的含义，然后只对带有该 class 的元素应用特殊样式。

### 解锁徽章

## 真优雅！

![](img/52e45ce976f775dd17fd84d91912f770_43_1.png)

