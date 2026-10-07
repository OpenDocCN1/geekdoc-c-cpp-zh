
你还可以使用 `grid-column` 和 `grid-row` 属性让元素跨越多个单元格。例如，要让标题跨越两列，你会使用：

```css
h1 {
  grid-column: 1 / 3;
}
```

`grid-template-rows` 和 `grid-template-columns` 属性也用于定义网格的大小。例如，要创建一个具有三个不同宽度列的网格，你会使用：

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 2fr;
}
```

`fr` 单位对于创建适应不同屏幕尺寸的响应式布局特别有用。例如，你可以使用 `minmax()` 函数来创建一个灵活的网格：

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```

网格系统是创建复杂且响应式布局的强大工具。通过练习，你将能够创建任何你想象得到的布局。

# 第 3.2 节快速检查

- 1. 固定网格（fixed grid）和流网格（fluid grid）有什么区别？
- 2. 什么是 CSS 网格框架？
- 3. 在提议的网格中，所有的网格行都有类名 `container`。创建一个样式规则，使这些网格行围绕其浮动列展开。
- 4. 在提议的网格中，所有列都有类名 `span-integer`，其中 `integer` 表示列的大小。创建一个样式规则，使每个网格列浮动在左边距。
- 5. 创建一个样式规则，将属于 `span-4` 类的列宽度设置为行宽的 25%。
- 6. 什么是 lorem ipsum？
- 7. 为问题 3 中描述的网格行创建一个样式规则，使其尺寸使用 Border Box 模型进行测量。
- 8. 创建一个样式，为文档中所有的块级引用（block quotes）添加一个 2 像素的绿色虚线边框。
- 9. 使用提议的 CSS 网格规范，为 `body` 元素创建一个网格，该网格具有三行由页面内容自动定义的行以及五列宽度分别为 25%、2.5%、50%、2.5% 和 20% 的列。将 `nav` 元素放在第一列，`article` 元素放在第三列，`aside` 元素放在第五列。

# 第 3.3 节视觉概述

当 `overflow` 设置为 `auto` 时，浏览器会自动为溢出的内容显示滚动条。

`overflow` 属性决定了浏览器如何处理超出元素分配空间的内容。

```css
main {
  overflow: auto;
  position: relative;
  height: 550px;
  width: 100%;
}
```

相对定位（Relative positioning）用于将元素从其在文档流中的默认位置移动。

```css
div#info1 {
  position: absolute;
  top: 28px;
  left: 5%;
}
```

`top` 属性为相对、绝对或固定定位的元素提供坐标。

```css
div#info2 {
  position: absolute;
  top: 185px;
  left: 42%;
}
```

绝对定位（Absolute positioning）用于将元素放置在容器内的指定坐标处。

`left` 属性为定位元素提供坐标。

```css
div#info3 {
  position: absolute;
  top: 135px;
  left: 75%;
}
```

`top` 和 `left` 值可以使用任何 CSS 单位表示，包括像素和百分比，其中百分比代表容器宽度或高度的百分比。

![](img/bf90ebf56b5f948b05e7a26851204c31_241_0.png)

## 使用定位样式的布局

info1 距离 `main` 元素顶部 20 像素，左侧 5%。

info2 距离顶部 155 像素，距离左边缘 42%。

![](img/bf90ebf56b5f948b05e7a26851204c31_242_0.png)

414 Tree Lane, Essex, VT 05452

首页 在线商店 特别优惠 联系我们

关于巧克力

20px

185px

135px

![](img/bf90ebf56b5f948b05e7a26851204c31_242_1.png)

![](img/bf90ebf56b5f948b05e7a26851204c31_242_2.png)

第一盒情人节巧克力是由 Josiah S. Cadbury 于 1868 年创造的。

象牙巧克力占了巧克力产量的 60%。

5%

单块巧克力每年生产约 800 条奶巧克力或黑巧克力。

42%

巧克力副本

Poundaisia © 2017 版权所有

75%

垂直滚动条会自动添加到溢出的内容中。

info3 距离顶部 135 像素，距离左边缘 75%。

# 定位元素

在上一节中，我们开发了一种根据网格的行和列对齐元素的布局。虽然网格布局赋予了页面统一感，但它限制了在不同位置放置元素的自由。在本节中，你将探索如何使用定位“跳出”网格。

## CSS 样式

CSS 支持多个属性将元素放在页面或容器内的特定坐标处。要将元素放在容器内的特定位置，使用以下样式：

```css
position: type;
top: value;
right: value;
bottom: value;
left: value;
```

其中 `type` 表示应用于元素的定位类型，`top`、`right` 和 `left` 属性分别指示元素的顶部、右边缘和左边缘坐标。坐标可以使用任何 CSS 单位或容器的百分比。CSS 支持五定位：`static`（默认）、`relative`、`absolute`、`fixed` 和 `inset`。在 `static` 定位中，元素放置在文档流的自然位置，这基本上与不使用任何定位相同。浏览器在 `static` 定位下会忽略 `top`、`left`、`bottom` 或 `right` 属性的任何值。

## 相对定位

相对定位用于将元素从其在文档流中的正常位置稍微偏移。`top`、`right` 和 `left` 属性表示元素移动到新位置时侧留的额外空间。例如，以下样式规则在元素顶部增加 250 像素的空间，在左侧增加 250 像素（见图 3-4）：

```css
div {
  position: relative;
  top: 250px;
  left: 250px;
}
```

### 教程 3 设计页面布局 | HTML 和 CSS

图 3-46 使用相对定位移动元素

![](img/bf90ebf56b5f948b05e7a26851204c31_244_0.png)

注意，其他元素的布局不受相对定位的影响；它们仍然占据渲染页面上的原始位置，就像对象从未移动过一样。

当设计师想要通过将元素从默认位置稍微移动到符合整体设计的新位置来“调整”页面布局时，有时会使用相对定位。如果没有指定相对定位的 `top`、`right`、`bottom` 或 `left` 值，它们的假设值为 0，元素将完全不移动。

## 绝对定位

绝对定位将元素放在容器内的特定坐标处，其中 `top` 属性指示元素的顶部，`right` 属性设置右边缘，`bottom` 属性设置底部，`left` 属性设置左边缘。

例如，以下样式规则将 `header` 元素放在容器顶部 620 像素，距离左边缘 30 像素（见图 3-47）。

> 要将元素放在容器的右下角，使用 `right` 和 `bottom` 值设置为 0 像素的绝对定位。

```css
header {
  position: absolute;
  top: 620px;
  left: 30px;
}
```

### HTML 2B HTML 和 CSS | 教程 3 设计页面布局

图 3-47 使用绝对定位移动元素

![](img/bf90ebf56b5f948b05e7a26851204c31_245_0.png)

使用绝对定位放置对象时，你使用 `top/left` 坐标或 `bottom/right` 坐标，但你不会同时使用四个坐标，因为那会混淆浏览器。例如，对象不能同时沿左边缘和右边缘定位。

与其他元素浮动时，绝对定位会将元素移出正常的文档流，使后续元素移动到之前由容器占据的空间。这可能导致绝对定位的对象与其他元素重叠。

绝对定位对象的解释是容器的所有边缘。浏览器在对其内部对象进行绝对定位之前，需要“知道”对象的容器在哪里。如果容器是使用设置为 `relative` 或 `absolute` 的定位属性放置的，那么容器值是基于容器边缘的。例如，以下样式规则将 `article` 元素放置在距离容器顶部 50 像素、左边缘 20 像素的坐标处。

> 提示：你可以使用 demo 文件夹中的 `demo_positioning.html` 文件进行定位样式的交互。

```css
section {
  position: relative;
}
article {
  position: absolute;
  top: 50px;
  left: 20px;
}
```

只要你将其设置为 `relative`，就不需要为 `section` 元素定义坐标。

困难始于容器没有设置 `relative` 或 `absolute` 定位。在那种情况下，浏览器没有上下文来使用绝对定位在容器内放置对象。因为浏览器必须在页面元素的层级中向上移动一级，即到达容器的容器。如果该容器是使用 `absolute` 或 `relative` 定位放置的，那么其内部的任何对象

### 教程 3 设计页面布局 | HTML 和 CSS HTML 229

可以使用绝对定位放置。例如，在下面的样式规则中，`article` 元素的位置是从 `body` 元素的边缘计算的，而不是 `section` 元素：

```
body (position: absolute);
```

```
body > section (position: static);
```

```
body > section > article {
position: absolute;
top: 50px;
left: 20px;
}
```

按照这种方式，浏览器将继续向上元素层级查找，直到找到一个使用绝对或相对定位放置的容器，或者到达 `html` 元素。如果到达 `html` 元素，任何绝对定位对象的坐标都是相对于浏览器窗口边缘计算的。图 3-48 显示了根据哪个容器提供 `top` 和 `left` 值的上下文，对象的放置位置。

> 提示
> 如果容器内的对象使用绝对定位放置，容器将发生收陷

图 3-48

# top 和 left 坐标的上下文

![](img/bf90ebf56b5f948b05e7a26851204c31_246_0.png)

因为内部容器没有使用相对或绝对定位放置，上下文会向上层级移动到外部容器

| 相对于内部容器的绝对定位 | 考虑到外部容器的绝对定位 |
| :--- | :--- |

© 2016 Cengage Learning

坐标可以用百分比也可以用像素表示。百分比用于灵活布局，在这种布局中，对象应该相对于其容器的宽度或高度进行定位。因此，下面的样式规则将 `article` 元素放置在其容器左上角下方一半处、右侧 30% 的位置。

```
article {
position: absolute;
top: 50%;
left: 30%;
}
```

### HTML 230 HTML 和 CSS | 教程 3 设计页面布局

当 `article` 的容器宽度或高度变化时，`article` 的位置将自动改变以匹配。

## 固定和继承定位

当你在浏览器窗口中滚动文档时，页面内容随之滚动。如果你想在浏览器窗口内固定一个对象使其不滚动，可以将它的 `position` 属性设置为 `fixed`。例如，下面的样式规则将 `footer` 元素保持在固定位置，距离浏览器窗口底部 10 像素：

```
footer {
  position: fixed;
  bottom: 10px;
}
```

注意，固定对象可能会覆盖其他页面内容，因此在页面设计中应谨慎使用它。
最后，你可以将 `position` 属性设置为 `inherit`，让元素继承其父元素的定位。

![](img/bf90ebf56b5f948b05e7a26851204c31_247_0.png)

## 使用定位样式

Anne 想要为一个包含巧克力信息图的页面设计布局。她勾勒了信息图页的布局，如图 3-49 所示。

### 教程 3 设计页面布局 | HTML 和 CSS HTML 231

图 3-49 巧克力信息图的建议布局

第一盒情人节巧克力是由英国巧克力专家理查德·卡杜里（Richard Cadbury）于 1868 年创造的。

迪迪瓦尔岸占全球可可产量的 40%。

每棵可可树每年大约产生 800 条牛奶巧克力或 400 条黑巧克力。

“chocolate”（巧克力）一词源于阿兹特克单词 "xocolatl"，意思是“苦水”。

顶级巧克力爱好者国家（人均）

最受喜爱的巧克力盒

![](img/bf90ebf56b5f948b05e7a26851204c31_248_0.png)

黑巧克力是最强的抗氧化剂来源之一，其抗氧化剂含量是所谓“超级浆果”的 5 倍以上。

每天吃 80 克优质有机巧克力可以显著减轻压力水平并改善整体健康。

![](img/bf90ebf56b5f948b05e7a26851204c31_248_1.png)

22% 的巧克力消耗发生在晚上 8 点到午夜之间。

© 2016 Cengage Learning

由于文本和插图无法在网格内完美对齐，你将使用 CSS 定位样式来定位每个图形和文本框。Anne 已经创建了页面内容以及格式化信息图外观的样式表。你将编写样式表使用 CSS 定位样式来布局信息图。

### HTML 232 HTML 和 CSS | 教程 3 设计页面布局

要打开信息图文件：

- 使用编辑器打开 **pc_info.txt** 文件。

### HTML 234 HTML 和 CSS | 教程 3 设计页面布局

图 3-51 放置第一个信息框

```css
/* 信息图样式 */
div.infobox {
  position: absolute;
}
/* 第一个信息图 */
div#info1 {
  display: block;
  top: 28px;
  left: 5%;
}
```

使用定位放置每个信息框，将第一个框距离主元素的顶边缘 20 像素，距离左侧 5%。

- 4. 将更改保存到文件并在浏览器中重新加载 pc_info.html 文件。图 3-52 显示了第一个信息框的放置位置。

## 图 3-52 第一个信息框的显示

![](img/bf90ebf56b5f948b05e7a26851204c31_251_0.png)

现在放置第二个和第三个信息框。

## 要放置接下来的两个框：section

- 1. 回到编辑器中的 pc_info.css 文件并进入 Second Infographic 节。
- 2. 添加以下样式规则，将第二个框距离容器顶部 185 像素，距离左侧边缘 42%。

```css
div#info2 {
  display: block;
  top: 185px;
  left: 42%;
}
```

### 教程 3 设计页面布局 | HTML 和 CSS HTML 235

- 3. 在 Third Infographic 节中插入以下样式规则，将第三个框距离顶边缘 135 像素，距离其容器左侧宽度的 75%。

```css
div#info3 {
  display: block;
  top: 135px;
  left: 75%;
}
```

图 3-53 突出了定位第二个和第三个信息框的样式规则。

## 图 3-53 第二个和第三个框的位置

![](img/bf90ebf56b5f948b05e7a26851204c31_252_0.png)
![](img/bf90ebf56b5f948b05e7a26851204c31_252_1.png)

- 4. 将更改保存到文件并在浏览器中重新加载 pc_info.html。图 3-54 显示了前三个信息框的放置位置。

## 图 3-54 前三个框的放置

![](img/bf90ebf56b5f948b05e7a26851204c31_252_2.png)

放置接下来的三个信息框。

## 要放置接下来的三个框：

- 1. 回到编辑器中的 pc_info.css 文件，进入 Fourth Infographic 节，并将第四个框距离顶边缘 510 像素，距离左边缘 8%。

```css
#info4 {
  display: block;
  top: 510px;
  left: 8%;
}
```
- 2. 在 Fifth Infographic 节中添加以下样式规则来定位第五个框：

```css
#info5 {
  display: block;
  top: 800px;
  left: 3%;
}
```
- 3. 在 Sixth Infographic 节中添加以下样式规则来定位第六个框：

```css
#info6 {
  display: block;
  top: 600px;
  left: 48%;
}
```

图 3-55 突出了第四、五和六个信息框的定位样式。

### 教程 3 设计页面布局 | HTML 和 CSS HTML 237

图 3-55

```css
/* 第四个信息图 */
div#info4 {
  display: block;
  top: 510px;
  left: 8%;
}
```
