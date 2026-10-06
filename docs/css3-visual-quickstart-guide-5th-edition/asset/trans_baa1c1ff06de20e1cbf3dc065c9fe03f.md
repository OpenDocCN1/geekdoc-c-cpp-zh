

# 控制溢出内容

当元素被裁剪，或者父元素的宽度和高度小于显示所有内容所需的区域时，部分内容将无法显示。`overflow` 属性允许你指定如何处理这些内容。

CSS3 新特性 ★ 使用 `overflow-x` 和/或 `overflow-y` 可以独立地控制宽度或高度的溢出。

# 定义溢出控制：

+   1. 输入 `overflow`、`overflow-x` 或 `overflow-y` 属性名，后跟一个冒号（:）（见代码 10.4）。

overflow:

![](img/9cd61ac1d4015ed5688d0c411434a660_277_0.png)

该元素在给定区域内无法显示的溢出区域（水平方向或垂直方向）。

代码 10.4 `ui-properties.css`——当应用于 101 ，，`overflow` 属性会自动添加滚动条，但仅在需要时添加，以确保内容始终可访问。

```css
*** CSS3 V5 | Chapter 10 |
box-properties.css ***

nav.global {
  display: block;
}

nav.global li {
  display: inline;
}

article {
  max-width: 980px;
  min-width: 660px;
}

figure {
  display: block;
  width: 300px;
}

figcaption {
  display: block;
}

aside {
  display: block;
  width: 200px;
  height: 400px;
  overflow: auto;
}

footer {
  width: 100%;
}
```

![](img/9cd61ac1d4015ed5688d0c411434a660_277_1.png)

代码 10.4 应用于代码 101：区域的高度被限制为 400px，但内容超过了该区域的范围，因此会自动了垂直滚动条。

# 表 10.4 溢出值

| 值 | 兼容性 |
| --- | --- |
| visible | IE4, FF1, S1, C1, O4, CSS51 |
| hidden | IE4, FF1, S1, C1, O4, CSS51 |
| scroll | IE4, FF1, S1, C1, O4, CSS51 |
| auto | IE4, FF1, S1, C1, O4, CSS51 |

# 表 10.5 Overflow-x 和 Overflow-y 值

| 值 | 兼容性 |
| --- | --- |
| visible | IE5, FF1.5, S3, C2, O9.5, CSS33 |
| hidden | IE5, FF1.5, S3, C2, O9.5, CSS33 |
| scroll | IE5, FF1.5, S3, C2, O9.5, CSS33 |
| auto | IE5, FF1.5, S3, C2, O9.5, CSS33 |

+   2. 添加一个关键字来告诉浏览器如何处理裁剪部分的溢出。
auto;

使用以下关键字之一（见表 10.4 和表 10.5）：
* **visible** 强制显示元素的裁剪部分，本质上是指令浏览器忽略裁剪，使内容流到盒子之外。
* **hidden** 隐藏溢出部分并防止滚动条出现。

![](img/9cd61ac1d4015ed5688d0c411434a660_278_0.png)

> 毛毛虫和爱丽丝沉默地对视了一会儿：最后毛毛虫从嘴里拿出烟斗，用一种懒散、睡睡的声音对她说道。

Visible 会覆盖元素的高度，强制显示所有内容。

![](img/9cd61ac1d4015ed5688d0c411434a660_278_1.png)

> 毛毛虫和爱丽丝沉默地对视了一会儿：最后毛毛虫

Hidden 会裁剪元素，但没有提供访问元素其余内容的方法。

+   scroll 在可见区域周围设置滚动条，允许访问者滚动元素的内容。当你设置此值时，即使不需要，也会为滚动条预留空间。

+   auto 允许浏览器决定是否需要显示滚动条。

通常情况下，auto 是溢出的首选，因为它只在需要时显示滚动条，并在没有内容可滚动时隐藏滚动条控件。

`overflow` 属性也用于定义如何处理溢出的裁剪。

![](img/9cd61ac1d4015ed5688d0c411434a660_279_0.png)

+   scroll 同时放置水平和垂直滚动条以访问元素中的额外内容。然而，即使不需要，也会添加占位滚动条。

![](img/9cd61ac1d4015ed5688d0c411434a660_279_1.png)

+   Auto 通常认为是最佳选项，因为它只在需要时显示滚动条。

# 即将推出：文本溢出

虽然可以设置溢出，但它是非常有用的。最常见的方法是使用省略号（...）来处理溢出的文本。CSS3 允许你精确地控制溢出文本。

# 浮动元素

虽然能够设置浮动是有用的，但有时你可能会发现需要覆盖浮动属性以防止包裹。类似于 HTML 标签的 `clear` 属性，CSS `clear` 属性允许你指定清除元素的左侧、右侧还是两侧（见表 10.7）。

浮动元素可能会产生奇怪的后果。解决这些问题将在第 13 章“修复浮动”中讨论。

> TIP 在第 13 章，你将学习如何使用浮动属性来替换表格布局。

# 清除浮动元素

有时，你可能会发现需要覆盖浮动属性以防止包裹。类似于 HTML 标签的 `clear` 属性，CSS `clear` 属性允许你指定清除元素的左侧、右侧还是两侧（见表 10.7）。

10.6 `ui-properties.css`——当应用于 101，，footer 被告诉不要浮动

# 防止元素浮动：

```css
*** CSS3 V5 | Chapter 10 |
box-properties.css ***

nav.global {
  display: block;
}

nav.global li {
  display: inline;
}

article {
  max-width: 980px;
  min-width: 660px;
  float: left;
}

figure {
  display: block;
  width: 300px;
  float: left;
}

figcaption {
  display: block;
}

aside {
  display: block;
  width: 200px;
  height: 400px;
  overflow: auto;
  float: right;
}

footer {
  width: 100%;
  clear: both;
}
```

