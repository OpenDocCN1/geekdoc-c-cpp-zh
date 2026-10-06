

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
```

```css
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
```

```css
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

