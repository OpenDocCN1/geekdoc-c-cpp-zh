
通常，两个或三个值代表 X、Y、Z 轴。如果只包含一个值，则假设应用于所有轴。

# 2D 变换

许多浏览器（包括 Mozilla、Webkit 和 Opera）实现了变换。

目前最稳定且广泛支持的变换是二维的，但这是一个很好的起点。

![](img/9cd61ac1d4015ed5688d0c411434a660_331_0.png)

原始

![](img/9cd61ac1d4015ed5688d0c411434a660_331_1.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_2.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_3.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_4.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_5.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_6.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_7.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_8.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_9.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_10.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_331_11.png)

# 表 12.3 变换源关键字 (Transform-Origin)

| Value |
| --- |
| left (左) |
| right (右) |
| top (上) |
| bottom (下) |
| center (中) |

+ 3. 根据需要添加更多变换。
`transform: scale(.75) rotate(3deg);`
你可以包含由空格分隔的多个变换值。
4. 如果不是不是元素的中心，则指定变换源。
`-webkit-transform-origin: 0, 25%;`
`-moz-transform-origin: 0, 25%;`
`-o-transform-origin: 0, 25%`
`transform-origin: 0, 25%;`

# 浏览器扩展会消失吗？

是的，浏览器扩展最终会消失。在浏览器实现了属性的标准 W3C 语法后，通常会在后续两个版本中支持该扩展，尽管这绝不是一条硬性规定。这就是为什么——如果已经定义了标准的 CSS 语法，最好将其放在浏览器扩展属性列表的底部，以确保在支持的情况下使用的是该版本。

默认情况下，所有变换都使用元素的中心作为原点。因此，旋转变换将围绕元素的中间旋转。
要更改此设置，请添加 `transform()` 属性，并以百分比或关键字指定原点 X 和 Y 位置的值（表 12.2）。如果你只指定一个值，则该值将同时用于 X 和 Y。正值将原点向元素的左上方移动，而负值则将原点向中心点的右下方移动。

# 3D 变换

在本书期间，3D 过渡仅在 Safari 和 Chrome 中支持，尽管随着 Firefox 新版本的发布，这种情况可能会发生快速变化。因此，我不建议使用 3D 过渡，除非你确定使用的浏览器是支持这些属性的——例如，在 iOS 应用程序或为 iPhone、iPod touch 或 iPad 创建的页面中。尽管如此，由于这是 W3C 正在开发的标准，你也应该包含标准的 CSS3 语法以确保未来的兼容性。

变换与过渡属性 311

# 在三维空间中变换元素

+ 1. 在你的 CSS 声明中添加 `transform-style` 属性并指定样式。
`-webkit-transform-style: flat;`
`transform-style: flat;`
为被变换的元素添加 `transform-style`（代码 12.3），这允许你指定哪些子元素应该相对于父元素平铺（flat），或者在各自的 3D 空间中单独变换（表 12.4）。

+ 2. 在你的 CSS 声明中添加 `perspective` 属性并指定透视值。
`-webkit-perspective: 500;`
`perspective: 500;`
透视的工作原理与本章描述的 `transform()` 值类似，但它用于为子元素应用透视（表 12.5）。

代码 12.3 transform-properties.css——当应用于代码 12.1 时，它用仅限 Webkit 的 3D 变换替换了代码 12.2 中的变换样式。其他浏览器看起来仍然如下所示：

```css
*** CSS VS | 第 12 章 | transform-properties.css ***

aside;

-webkit-transform: rotate(-2deg);

-moz-transform: rotate(-2deg);

-o-transform: rotate(-2deg);

transform: rotate(-2deg);

div.gallery figure {

width:;

-webkit-transform-origin: left 25%;

-moz-transform-origin: left 25%;

-o-transform-origin: left 25%;

transform-origin: left 25%;

-webkit-transform-style: flat;

transform-style: flat;

-webkit-perspective: 5000;

perspective: 5000;

-webkit-perspective-origin: 25% 25%;

perspective-origin: 25% 25%;

-webkit-backface-visibility: visible;

backface-visibility: visible;

}
```

```css
#f1
-webkit-transform: perspective(250) scale3d(75,5,1) rotate3d(5,4,2,-10);
-moz-transform: scale(.75) rotate(10deg);
-o-transform: scale(.75) rotate(10deg);
transform: scale(.75) rotate(10deg);
```

```css
#f2
-webkit-transform: perspective(250) scale3d(5,7,1.5) rotate3d(3,-10,8,-18);
-moz-transform: scale(.75) rotate(-8deg);
```

| Value | Compatibility |
| --- | --- |
| flat | S3.1, C5, CSS3 |
| preserve-3d | S3.1, C5, CSS3 |

| Value | Compatibility |
| --- | --- |
| <number> | S3.1, C5, CSS3 |
| none | S3.1, C5, CSS3 |

# 代码 12.3 继续

```css
-o-transform: scale(.75) rotate(-8deg);
transform: scale(.75) rotate(-8deg);
```

```css
#f3 {
  -webkit-transform: perspective(250) scale3d(1,5,7) rotate3d(3,6,10,20deg);
  -moz-transform: scale(.75) rotate(3deg);
  -o-transform: scale(.75) rotate(3deg);
  transform: scale(.75) rotate(3deg);
}
```

```css
#f1:hover, #f2:hover, #f3:hover {
  opacity: 1;
  -webkit-transform: rotate(0);
  -moz-transform: rotate(0);
  -o-transform: rotate(0);
  transform: rotate(0);
  cursor: pointer;
  clip: auto;
  z-index: 9999;
}
```

3. 在你的 CSS 声明中添加 `perspective-origin` 属性或两个值。

`-webkit-perspective-origin: 25%;`
`perspective-origin: 25%;`

添加一个或两个值的透视源。

4. 在你的 CSS 声明中添加 `backface-visibility` 属性。
`-webkit-backface-visibility: visible;`
`backface-visibility: visible;`

添加一个或两个值的透视源来定义原点（表 12.6）。

| Value | Compatibility |
| --- | --- |
| <number> | S3.1, C5, CSS3 |
| none | S3.1, C5, CSS3 |

| Value | Compatibility |
| --- | --- |
| visible | S3.1, C5, CSS3 |
| hidden | S3.1, C5, CSS3 |

# CSS3 新特性：在元素状态之间添加过渡 ★

尽管人们期望屏幕上会有变化和移动，但 CSS 和 HTML 很少有允许你设计交互的控制手段，而现有的手段到为止都是二元化的：

- 链接要么是一种颜色，要么是另一种颜色。
- 文本框要么是某种尺寸，要么是另一种。
- 照片要么是透明的，要么是不透明的。

过去，从一个状态到另一个状态没有任何中间过程。没有过渡效果。
这导致大多数网页在视觉上非常突兀，元素的移动和变化方式非常不优雅。

我们需要一种快速简便的方法来为页面添加简单的过渡效果，这正是 CSS 过渡（CSS transitions）大显身场的地方。

## 什么可以过渡？

几乎任何具有颜色、长度或位置组件的 CSS 属性——包括许多新的 CSS3 属性——都可以设置过渡，使其随时间推移从一种样式变为另一种样式。

表 12.9 显示了可用的 CSS 属性列表以及可以过渡的值。唯一的例外是盒投影（box-shadows）。

要发生过渡，元素必须发生状态变化，即使用第 3 章讨论的链接伪类或动态伪类。过渡的实现原理是在一段时间内改变不同元素状态之间的样式。例如，元素默认状态的颜色值在显示为悬停（hover）状态的颜色值之前，会经过光谱中的中间色值。

![](img/9cd61ac1d4015ed5688d0c411434a660_339_0.png)

> 过渡就像电影中的几帧，随着时间逐渐变化，而不是瞬间完成。

# 表 12.9 带有过渡效果的 CSS 属性

| CSS 属性 | 可过渡类型 | CSS 属性 | 可过渡类型 |
| :--- | :--- | :--- | :--- |
| background-color | 颜色 | margin-right | 长度 |
| background-image | 仅渐变 | margin-top | 长度 |
| background-position | 百比、长度 | max-height | 长度、百分比 |
| border-bottom-color | 颜色 | max-width | 长度、百分比 |
| border-bottom-width | 长度 | min-height | 长度、百分比 |
| border-color | 颜色 | min-width | 长度、百分比 |
| border-left-color | 颜色 | opacity | 数字 |
| border-left-width | 长度 | outline-color | 颜色 |
| border-right-color | 颜色 | outline-offset | 整数 |
| border-right-width | 长度 | outline-width | 长度 |
| border-spacing | 长度 | padding-bottom | 长度 |
| border-top-color | 颜色 | padding-left | 长度 |
| border-top-width | 长度 | padding-right | 长度 |
| border-width | 长度 | padding-top | 长度 |
| bottom | 长度、百分比 | right | 长度、百分比 |
| color | 颜色 | text-indent | 长度、百分比 |
| crop | 矩形 | text-shadow | 投影 |
| font-size | 长度、百分比 | top | 长度、百分比 |
| font-weight | 数字 | transform | 数字、角度、宽度 |
| grid-* | 各种 | vertical-align | 关键字、长度、百分比 |
| height | 长度、百分比 | visibility | 可性 |
| left | 长度、百分比 | width | 长度、百分比 |
| letter-spacing | 长度 | word-spacing | 长度、百分比 |
| line-height | 数字、百分比 | z-index | 整数 |
| margin-bottom | 长度 | zoom | 数字 |
| margin-left | 长度 | | |

*表 12.9

# 代码 12.4 续

```css
-o-transform: scale(.75) rotate(10deg);
transform: scale(.75) rotate(10deg);
#f2 {
  -webkit-transform: perspective(250)
  scale3d(5,75,1.5) rotate3d(-3,10,-8,18deg);
  -moz-transform: scale(.75) rotate(-8deg);
  -o-transform: scale(.75) rotate(-8deg);
  transform: scale(.75) rotate(-8deg);
}
#f3 {
  -webkit-transform: perspective(250)
  scale3d(1,5,5) rotate3d(3,6,10,20deg);
  -moz-transform: scale(.75) rotate(3deg);
  -o-transform: scale(.75) rotate(3deg);
  transform: scale(.75) rotate(3deg);
}
#f1:hover, #f2:hover, #f3:hover {
  opacity: 1;
  -webkit-transform: rotate(0);
  -moz-transform: rotate(0);
  -o-transform: rotate(0);
transform: rotate(0);
  cursor: pointer;
  clip: auto;
  z-index: 9999;
}
```
