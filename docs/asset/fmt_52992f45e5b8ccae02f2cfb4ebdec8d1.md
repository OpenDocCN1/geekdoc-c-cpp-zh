
![](img/9cd61acd4015ed5688d0c41134a660_0.png)

> TIP 你可以使用负值将内容向上向左移动，而不是向下向右。

> TIP 绝对定位的子元素与其父元素对齐。

> TIP 如果你对同一个元素设置了 `top`/`left` 和 `bottom`/`right` 位置会怎样？取决于浏览器。Internet Explorer 始终是 `top` 和 `left` 位置。但大多数其他浏览器会扩展没有固定宽度或高度的元素以适应设置的值。

![](img/9cd61acd4015ed5688d0c41134a660_1.png)

> A 将 11.3 应用于代码 11.1。页面开始紧凑。注意粗体文本现在与段落的其他部分对齐。

![](img/9cd61acd4015ed5688d0c41134a660_2.png)

> B 即使滚动时，`footer` 仍然留在屏幕底部。

视觉格式属性 291

# 在 3D 中堆叠对象

尽管屏幕是一个二维区域，但定位元素可以被赋予第三个维度：`z-index`。定位的元素按数字排列，从 0, 1, 2 等开始——取决于它们在 HTML 中出现的顺序。数字较大的元素显示在数字较小的元素。。系统被称为 `z-index`。

`z-index` 相对于其父元素。当元素重叠时，`z-index` 较高的元素将显示在上方。要定义元素的 `z-index`：

- 1. 指定一种定位类型。详情请参阅本章节前面的“设置定位类型”。
- 2. 在你的 CSS 声明列表中添加定位侧边属性。在 CSS 规则中输入 `z-index`，后跟冒号（:）`（代码 11.4）`

`z-index:` 

为元素的偏移输入一个值。你可以输入以下任何值：

- 正数，例如 **10, 100 或更高。**
- 负数，例如 **-1 或 -10。**
- `auto`，如果位置设置为绝对定位，则允许浏览器计算该值；否则，默认值为 `auto`。

> TIP 你不必非包含 `top`、`right`、`bottom` 和 `left` 声明，但如果不包含，它们将被处理为 `auto`。

表 11.4 Z-index 值
| 值 | 兼容性 |
|---|---|
| <positive number> | IE4, F1, S1, C1, O4, CSS2 |
| <negative number> | IE4, F1, S1, C1, O4, CSS2 |
| auto | IE4, F1, S1, C1, O5, CSS2 |
| inherit | IE4, F1, S1, C1, O5, CSS2 |

# 11.4 visual-formatting-properties.css

应用于代码 11.1 时，这段 CSS 将 `footer` 定位在视口的底部（保持在那里）；在屏幕右上角的方便位置定位；并略微偏移了我们的图库图像。它提升了粗体文本，使其基线与周围文本匹配。看起来好多了 A。

```css
*** CSS | 第11 章 |
  visual-formatting-properties.css

aside {
  position: absolute;
  left: 1%;
  top: 120px;
}

strong {
  position: relative;
  top: -15em;
}

footer {
  position: fixed;
  bottom: 0;
  left: 0;
}

ul {
  position: relative;
  top: 10px;
}

div.gallery {
  position: relative;
}

div.gallery figure {
  position: absolute;
}

div.gallery figure.f1 {
  left: 0;
  top: 0;
}

div.gallery figure.f2 {
  left: 150px;
  top: 50px;
}

div.gallery figure.f3 {
  left: 300px;
  top: 100px;
}
```

## 11.5 visualformatting-properties.css

当应用于 11.3 时，此 CSS 隐藏了页头中的导航，因为导航现在已出现在我们的固定页脚中了。别担心，顶部导航将在书的后部分返回。

```css
*** CSS3 VQ5 | Chapter 11 |
visualformatting-properties.css ***
```

```css
header navigation {
visibility: hidden; }
```

```css
aside {
position: absolute;
right: 1px;
top: 120px; }
```

```css
strong {
position: relative;
top: -15em; }
```

```css
footer {
position: fixed;
bottom: 0;
left: 0;
z-index: 99; }
```

```css
footer ul {
position: relative;
top: 10px; }
```

```css
div.gallery {
position: relative; }
```

```css
div.gallery figure {
position: absolute; }
```

```css
div.gallery figure.f1 {
left: 0;
top: 0;
z-index: 3; }
```

```css
div.gallery figure.f2 {
left: 150px;
top: 50px;
z-index: 2; }
```

```css
div.gallery figure.f3 {
left: 300px;
top: 100px;
z-index: 1; }
```

> TIP 尽管这些属性看起来相似，但 `visibility` 与 `display` 不同（第 10 章）。当 `display` 设置为 `none` 时，元素会从文档中移除，不留任何空间。`visibility` 则像包着绷带的隐形人一样预留并显示空区域。

> TIP 通常，`display:none` 用于 JavaScript 效果，例如下拉菜单和弹出文本，在这些元素会交替隐藏和显示。由于此属性会移除元素，它可以防止元素在不需要时干扰页面的布局。

> TIP 我建议在创建打印样式时，使用 `display` 来隐藏元素（如导航）。

> TIP 隐藏元素的一个缺点是 Web 搜索引擎无法看到它们，视障人士使用的屏幕阅读器也无法看到。如果你隐藏了内容，请确保它不是对 SEO 至关重要的内容。

![](img/9cd61ac1d4015ed5688d0c411434a660_318_0.png)

B 11.5 应用于 11.1。页头导航消失了，但并未被遗忘。

## 裁剪元素的可见区域

与设置元素的宽度和高度（这控制元素的尺寸，第 10 章）不同，裁剪一个绝对固定定位的元素指定了该元素内容中有多少部分是可见的（**表 11.6**）。未被指定为可见的部分仍然存在，但观众无法看到它，浏览器将将其视为空区域。

**要定义元素的裁剪区域：**

- 1. 指定位置类型。详情请参阅本章前面的章节“设置定位类型”。
- 2. 在你的声明列表中添加 `clip` 属性。输入 `clip` 属性名，后跟冒号（:），如**代码 11.6** 所示。

```css
clip:
```
- 3. 指定矩形裁剪区域。输入 `rect` 将裁剪形状定义为矩形，打开左括号 `(`、四个用空格分隔的数值、右括号 `)` 和分号（;）。

`rect(50px 250px 250px 50px);` 这些数字分别定义了裁剪区域的顶、右、底和左长度。所有这些值都是距离元素原点（左上角）的距离，而不是距离指定侧边的距离。

每个值可以是长度值或 `auto`，允许浏览器确定裁剪大小（通常为 100 百比）。

| 表 11.6 裁剪值 |
| 值 | 兼容性 |
| :--- | :--- |
| rect <top> <right> <bottom> <left> | IE5,5, FF1, S1, C7, CSS2 |
| auto | IE5,5, FF1, S1, C7, CSS2 |
| inherit | IE5,5, FF1, S1, C7, CSS2 |

![](img/9cd61ac1d4015ed5688d0c411434a660_319_0.png)

> A 中心根据提供给 `clip` 属性的顶、右、底、左值进行裁剪。透明区域将不可见。

## 11.6 visualformatting-properties.css— 当应用于代码 11.1 时，此 CSS 隐藏了画图中图片的边缘，创建了尺寸一致的缩略图 9

```css
*** CSS3 Flex | chapter 11 |
* visualformatting-properties.css* ***

header navigation {
  visibility: hidden;
}

aside {
  position: absolute;
  right: 1%;
  top: 120px;
}

strong {
  position: relative;
  top: -15em;
}

footer {
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 99;
}

ul {
  position: relative;
  top: 10px;
}

div.gallery {
  position: relative;
}

div.gallery figure {
  position: absolute;
  clip: rect(50px 250px 250px 50px);
}

div.gallery figure.f1 {
  left: 0;
  top: 0;
  z-index: 3;
}

div.gallery figure.f2 {
  left: 150px;
  top: 50px;
  z-index: 2;
}

div.gallery figure.f3 {
  left: 300px;
  top: 100px;
  z-index: 1;
}
```

> TIP 元素的边框和内边距被裁剪了，但外边距没有。

> TIP Auto 应该恢复元素的原始状态。然而，Safari 和 Chrome 只会恢复边缘，同时去除轮廓或阴影。

![](img/9cd61ac1d4015ed5688d0c411434a660_320_0.png)

代码 11.6 应用于格式属性。你的画图现在由尺寸一致的缩略图组成。稍后在书中将学习如何让它们完全显示。

## 新 CSS3：设置元素的透明度

最早广泛实现的 CSS3 特性之一是设置 `opacity`，它允许元素从不透明变为透明。然而，不同的浏览器以不同的方式实现。例如，遵循 W3C 语法的浏览器，Internet Explorer 是在其现有的 `filter` 函数基础上构建的。由于 Internet Explorer 代码，你可以将两个声明放在规则中控制其透明度。

![](img/9cd61ac1d4015ed5688d0c411434a660_321_0.png)

> 修改 `opacity` 让你看到下方的元素。

### 表 11.7 透明度值

| 值 | 兼容性 |
| :--- | :--- |
| alpha value | FF1, S1.3, C1, CSS2 |
| inherit | FF1, S1.3, C1, CSS2 |

### 要设置元素的透明度：

- 1. 在你的声明列表中添加 `filter` 属性。为了在 Windows 的 Internet Explorer 中控制透明度，在声明块中输入 filter 名称，后跟冒号（:）（代码 11.7）。

```css
filter:
```
- 2. 为 Internet Explorer 指定透明度。`alpha(opacity=75);` 添加 `alpha()` 代码来定义使用的 filter 值。你不需要更改此代码，除了 alpha 值，范围从 0（完全透明）到 100（完全不透明）。用分号（;）结束声明。
- 3. 在你的 CSS 中添加 `opacity` 属性。要控制元素的透明度，输入 `opacity` 后跟冒号（:）。

```css
opacity:
```

## 11.7 visualformatting-properties.css

当应用于 11.3 时，此 CSS 允许重叠的缩略图显示下层的内容

```css
*** CSS3 V0 | Chapter 11 |
visualformatting-properties.css ***

header navigation {
visibility: hidden; }
```

```css
aside {
position: absolute;
right: 1%;
top: 120px; }
```

```css
strong {
position: relative;
top: -15em; }
```

```css
footer {
position: fixed;
bottom: 0;
left: 0;
z-index: 99; }
```

```css
ul {
position: relative;
top: 10px; }
```

```css
div.gallery {
position: relative; }
```

```css
div.gallery figure {
position: absolute;
clip: rect(50px 250px 250px 50px);
filter: alpha(opacity=0.75);
opacity: .5; }
```

```css
div.gallery figure.f1 {
left: 0;
top: 0;
z-index: 3; }
```

```css
div.gallery figure.f2 {
left: 150px;
top: 50px;
z-index: 2; }
```

```css
div.gallery figure.f3 {
left: 300px;
top: 100px;
z-index: 1; }
```

- 4. 指定透明度。为元素的透明度输入一个 alpha 值，范围从 0.0（完全透明）到 1.0（完全不透明）。

你也可以使用 `inherit` 将元素的透明度设置为与其父元素相同的值。因此，如果父元素的透明度为 0.75，`inherit` 将导致子元素在父元素已设置的 75% 透明度的基础上进一步降低自身的透明度。

> 透明度应用于整个元素及其所有子元素，没有方法在子元素中覆盖。

> 透明度是累积的，因此如果一个透明度为 .5 的元素位于一个透明度为 .5 的元素内部，那么它的累积透明度将为 .25。

![](img/9cd61ac1d4015ed5688d0c411434a660_322_0.png)

代码 11.7 应用于 11.1。缩略图是半透明的。这可以是一个非常有用的效果，特别是当结合悬停时将元素恢复为不透明以指示用户交互。

# CSS3 新特性：设置元素的投影 ★

就像文本投影（第 6 章）一样，你可以为屏幕上任何元素（无论是否定位）的框添加一个外投影或内投影。不过，“投影”一词有点误导性，因为你可以将颜色设置为任何喜欢的颜色——包括浅色——来创建发光效果。

## 如何设置元素投影：

1. 在你的 CSS 规则中添加 `box-shadow` 属性。输入 `box-shadow` 属性名称（包括 Mozilla 和 Webkit 浏览器扩展），加上冒号（;）（代码 11.8）。
```css
-webkit-box-shadow:
-moz-box-shadow:
box-shadow:
```
2. 指定投影偏移、模糊、收缩（choke）和内嵌（inset）。

```
1px 1px 5px 1px rgba(0,0,0,.25)
. inset
```

输入以下关键字或值（表 11.8）来指定如何处理该元素的投影（从右到左）：

- x 和 y 偏移值设置投影相对于元素框的位置。正值使投影向右下方偏移，而负值则使投影向上向左侧移动。这些是必填的。

- 模糊长度是一个正值，会增加投影的模糊度并将其扩散。值越高，投影越大、越稀。。这是可选的，如果未设置，默认值为 0。

![](img/9cd61ac1d4015ed5688d0c411434a660_323_0.png)

> 投影提供了深度感和纹理感。

| 表 11.8 Box-Shadow 值 |
| 值 | 兼容性 |
| :--- | :--- |
| inset | FF3.5, S3, C10.5, CSS3 |
| <x-offset> | FF3.5, S3, C10.5, CSS3 |
| <y-offset> | FF3.5, S3, C10.5, CSS3 |
| <blur> | FF3.5, S3, C10.5, CSS3 |
| <spread> | FF3.5, S3, C10.5, CSS3 |
| <color> | FF3.5, S3, C10.5, CSS3 |

```css
Code 11.8 formatting-properties.css —
当应用到 Code 11.1 时，此 CSS 为文章添加了投影，并在侧边添加了外内外投影。它还为图库图像添加了投影，但由于它们被裁剪了，所以没有显示 ①
```

```css
*** CSS3 W5 | Chapter 11 |
```
