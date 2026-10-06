

![](img/9cd61ac1d4015ed5688d0c411434a660_110_0.png)

# 3. 样式元素的聚焦状态（focus state）。
输入选择器（HTML、类或 ID），
冒号（:），然后输入 focus。

```
input: {...}
```

一旦元素获得焦点
（被点击或轻触），样式就会发生变化，并在元素
失去焦点（称为 blur/模糊）时，样式会恢复到
悬停（hover）或默认样式。

C: 代码 4.7 的结果。这展示了处于四种动态状态下的简单表单。提供这种视觉反馈可以帮助用户知道哪个表单字段已准备就绪，或者他们已经点击了按钮。

# 4. 样式元素的激活状态（active state）。
输入选择器（HTML、类或 ID），
冒号（:），然后输入 active。

```
input:active {...}
```

当用户在元素框内点击时（在第 10 章中解释）

# 5. 样式会根据用户的反应，在必要时应用于元素的
状态。

```
<input type="button"
value="Search">
```

所有使用特定选择器的标签都对其状态进行了样式设置。

> 提示：定义链接和伪类的顺序是有区别的。例如，将 :hover 伪类放在 :visited 伪类之前，会导致链接在被访问后 :hover 无法工作。为了获得最佳效果，请按此顺序定义样式：link（链接）、visited（已访问）、focus（聚焦）和 active（激活）。

> 提示：在更改 :hover 的 s 属性时要谨慎。更改类型、字体大小、字重和其他属性会导致文本比其在布局中保留的空间变大或变小，并强制整个页面重新填充内容，这会非常困扰访问者。

> 提示：在这个示例中，使用 `input` 来显示动态状态。`input` 有一个样式缺点，即所有 input 类型都……在本章的稍后部分，你将看到如何使用标签属性设置样式，这将允许你为文本字段和按钮设置不同的样式。

> 提示：记住伪元素顺序的一种方法是 me LoVe HaTe：Link（链接）、Visited（已访问）、Hover（悬停）、Active（激活）。
> 提示：如果你设置了 :hover，你总是想要设置 :focus。为什么？Hover 仅适用于与元素的非键盘（鼠标）交互。对于仅使用键盘的 Web 用户，:focus 将生效。

# 新 CSS3：使用伪类为特定子元素设置样式 ★

设计师通常希望对另一个元素内部第一个出现的元素应用样式，例如父元素的第一个孩子。

`first-child` 伪元素自 CSS2.22 起已可用；但 CSS3 提供了一系列新的结构伪元素，用于精确设置元素子元素的样式（表 4.4）：

- first-child——如果选择器类型是其父元素的第一个子元素，则设置该第一个实例的外观。
- first-of-type——当元素的选择器类型在父元素中第一次出现时设置其外观。
- nth-child(#)——设置指定子元素的样式。例如，段落的第三个孩子是 `p:nth-child(3)`。
- nth-of-type(#)——设置选择器类型在父元素中特定位置的样式，第七个段落是 `p:nth-of-type(7)`。
- last-of-type(#)——设置选择器类型在父元素中特定位置的样式，但从底部开始。例如，倒数第三个段落是 `p:last-of-type(3)`。
- last-child——如果指示的选择器是父元素的最后一个子元素，则设置其外观。
- last-of-type——设置其父元素中特定选择器类型的最后一个实例的外观。

# 文本装饰：
要不要加下划线

下划线是 Web 上指示超链接的标准方式。然而，许多带有下划线的链接会让页面变成密不透风的线条堆，文本变得难以阅读。此外，如果访问者关闭了下划线，他们就看不到链接，特别是当链接颜色和文本颜色相同时。

CSS 允许你关闭链接下划线，覆盖访问者的偏好。我建议这种做法，并依靠清晰的颜色选择来突出超链接，或者依靠 `border-bottom`（下边框）这种替代下划线方法，这可以让你更好地控制下划线的样式。更多信息请参见第 14 章。

# 为元素的子元素设置样式：

- 1. 根据它们在父元素中的位置对元素设置样式。输入你想设置样式的元素的选择器（HTML、类或 ID）、冒号（:）；以及表 4.4 中的其中一个结构伪元素（代码 4.8）。

```
li:first-child {...}
li:first-of-type {...}
li:nth-of-type(3) {...}
li:nth-last-of-type(2) {...}
li:last-child {...}
li:last-of-type {...}
```

- 2. 如果元素匹配模式，则将对其设置样式。

```
<li...></li>
```

在设置 HTML 时，请记住第 1 步中的选择器。

# 为特定语言设置样式

万维网就是那样，它遍布全球，这意味着任何地方的任何人都可以看到你的页面。这也意味着 Web 页面是用许多语言创建的。

`:lang()` 伪类允许你指定取决于指定语言的样式。

4.8 列表根据位置设置样式。

```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type"
    content="text/html; charset=UTF-8" />
  <title>爱丽丝仙游游</title>
  <style type="text/css" media="all">
    li:first-child { font-size:.85em; }
    li:first-of-type { color: red; }
    li:nth-of-type(3) { font-size:1.5em; }
    li:nth-last-of-type(2) { font-size:2em; }
    li:last-of-type { color: red; }
    li:last-child { font-size:2.5em; }
  </style>
</head>
<body>
  li:Alice</li>
  li:White Rabbit</li>
  li:Mad Hatter</li>
  li:Queen of Hearts</li>
  li:Door Mouse</li>
</body>
</html>
```

# 为特定语言设置样式：

- 1. 根据语言对元素设置样式。输入你想设置样式的元素的选择器（HTML、类或 ID）、冒号（:）、.lang，并在括号内输入你定义的语言代码（代码 4.9）。

```
p:lang(fr)
```

- 2. 如果元素具有匹配的语言，则对其设置样式。根据需要设置标签的语言属性。

```html
<p lang="fr">...</p>
```

代码 4.9 显示法语段落渲染为红色（向法语使用者表示歉意）。

