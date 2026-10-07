
对于有序列表和无序列表，大多数浏览器使用的默认样式是将左侧内边距设置为 40 像素，以便为列表标记提供额外的空间。移除列表标记并不会移除内边距。Allison 建议你通过将导航列表中的左侧内边距大小缩小到 5 像素来找回这段未使用的空间。

# 要更改导航列表中使用的左侧内边距：

- 1. 回到编辑器中的 `tss_styles.css` 文件。
- 2. 在“导航部分”（Navigation Sections）中找到 `nav .ui` 样式规则，并插入样式 `padding-left: 5px;`。

图 2-39 显示了所有导航列表的新样式。

![](img/bf90ebf56b5f948b05e7a26851204c31_158_0.png)

- 3. 保存对文件的更改并在浏览器中重新加载 `tss_home.html` 文件。验证左栏导航列表中的条目是否已向左移动，这是将左侧内边距改为 5 像素的结果。

现在你已经处理了内边距空间，你将检查如何处理外边距（margins）。

## 设置内边距和外边距空间

- 若要设置元素周围四周的内边距空间，使用 `padding: size;`，其中 `size` 是使用 CSS 长度单位之一的内边距大小。
- 若要设置元素周围四周的外边距空间，使用 `margin: size;`。
- 若仅在某侧（上、右、下、左）设置内边距或外边距，在属性 `padding-side: size;` 或 `margin-side: size;` 中包含该边的名称，其中 `size` 为 top、right、bottom 或 left。
- 若要为元素的每侧设置不同的内边距或外边距，输入如 `padding: top right bottom;`、`margin: top right bottom left;` 的条目，其中 top、right、bottom 和 left 是关联大小的各个独立尺寸。

## 设置外边距和边框空间

设置外边距空间的样式与设置内边距空间的样式形式相同。若要设置你的块级元素周围的外边距大小，请使用以下属性之一：

`margin: size;`

或

`margin: top right bottom left;`

各个组组的外边距使用样式属性 `margin-top: size;` `margin-right: size;` `margin-bottom: size;` `margin-left: size;` 设置，其中外边距可以一旦一个 CSS 长度单位之一来表示，或使用关键字 `auto` 让浏览器自动设置外边距。

边框空间的大小使用以下边框宽度属性 `border-width: size;`

或

`border-width: top right bottom left;`
配合属性 `border-top-width`、`border-right-width`、`border-bottom-width` 和 `border-left-width` 来指定各个边框的大小。你将在教程 4 中进行更详细的探索。

首页的导航列表列出了访问 Tri 和 Soccer 网站的页面以及指向外部网站的链接。每个组开头的项目是用类 `newgravity` 创建的。Alison 建议将每组链接上方的外边距增加到 20 像素，以将其与上一组隔开。由于每个组的外边距已经增加，这些组将更容易被识别。

## 要增加顶部外边距：

- 1. 回到编辑器中的 `tss_styles.css` 文件。
- 2. 在“导航样式”（Navigation Styles）部分，直接在 `nav > ul` 选择器的样式规则下方插入以下规则：

```css
nav > ul > li.newgroup {
  margin-top: 20px;
}
```

图 2-40 显示了设置顶部外边距值的样式规则。

![](img/bf90ebf56b5f948b05e7a26851204c31_160_0.png)

- 3. 保存对文件的更改并在浏览器中返回 `tss_home.html` 文件。验证导航列表中的条目现在分为三组：第一组包含来自 Tri and Soccer 的链接；第二组包含指向跑步、自行车和游泳网站的链接；第三组包含指向三项铁锦网站的链接。

Alison 还注意到，首页右栏的区块为客户引用留下了较少的未使用空间。引用块（blockquote）的默认浏览器样式通过将左右外边距设置为 40 像素将引用与周围环境隔开。通过调整此空间以使引用块更易读，你将左/右外边距缩小到 5 像素，同时将上下外边距增加到 20 像素，以区分一个客户引用另一个。

## 要增加引用块周围的外边距空间：

- 1. 回到编辑器中的 `tss_styles.css` 文件。
- 2. 在“侧边栏和引用样式”（Aside and Blockquote Styles）中找到 `aside blockquote` 选择器的样式规则，并在样式规则中插入 `margin: 20px 5px;`。

![](img/bf90eb56b5f948b05e7a26851204c31_158_0.png)

## HTML 146 HTML 和 CSS | 教程 2 开始学习 CSS

Alison 想要修改主页分类列表使用的标记图像。目前，`runicon.png` 图像被用作三个列表项的标记。相反，她希望仅对第一个项目使用 `runicon.png` 图像，将 `bikeicon.png` 图像作为第二个列表项的标记，并将 `swimicon.png` 作为第三也是最后一个项的标记。你可以使用 `first-of-type`、`nth-of-type` 和 `last-of-type` 伪类来将每个项目与相应的 `png` 文件匹配。

- 要对无序列表应用伪类：
  1. 回到编辑器中的 `tss.css` 文件。
  2. 转到样式表底部的 List Styles（列表样式）部分，删除设置列表图像标记的 `@about_tss us` 规则，并将其替换为以下三条样式规则：

```css
@about_tss us li:first-of-type {
  list-style-image: url(runicon.png);
}
@about_tss us li:nth-of-type(2) {
  list-style-image: url(bikeicon.png);
}
@about_tss us li:last-of-type {
  list-style-image: url(swimicon.png);
}
```

图 2-44 显示了在无序列表项在使用伪类的三个选择器及其相关的样式规则。

## 图 2-44 将伪类应用于列表项

| /* List Styles */ | |
|---|---|
| 使用 runicon.png 作为第一个项的标记 | 选中 about_tss 文章中无序列表的第一个项 |
| @about_tss us li:first-of-type { list-style-image: url(runicon.png); } | 选中第二个列表项 |
| 使用 bikeicon.png 图像作为第二个标记 | @about_tss us li:nth-of-type(2) { list-style-image: url(bikeicon.png); } | 选中最后一个列表项 |
| 使用 swimicon.png 图像作为最后一个标记 | @about_tss us li:last-of-type { list-style-image: url(swimicon.png); } |

# 教程 2 开始学习 CSS | HTML 和 CSS

- 3. 保存对文件的更改，然后在浏览器中重新加载 `tss_home.html` 文件。图 2-45 显示了无序列表的新格式，每个列表项都使用了不同的图像标记。

图 2-45 每个项的列表标记图像

## 探索 nth-of-type 伪类

`nth-of-type` 伪类是按循环顺序格式化一组元素的强大工具。循环使用选择器创建：

```css
nth-of-type(an+b)
```

其中 `a` 是循环的长度，`b` 是从循环开始的偏移量，`n` 是计数器，从 0 开始并在每次循环迭代中增加 1。例如，以下样式规则创建了一个周期为 3 的循环，第一个列表项显示为红色，第二个显示为蓝色，第三个显示为绿色，在最后一个项之后，循环重复红-蓝-绿顺序：

```css
nth-of-type(3n+1) {color: red;}
nth-of-type(3n+2) {color: blue;}
nth-of-type(3n+3) {color: green;}
```

当循环长度为 1 时，`nth-of-type` 选择器会在指定的偏移量之后选择元素。以下样式规则将从第 5 个开始的所有列表项文本颜色设置为蓝色：

```css
nth-of-type(n+5) {color: blue;}
```

CSS 还支持 `even`（偶数）和 `odd`（奇数）关键字，以便更紧凑地输入长度为 2 的循环：

```css
nth-of-type(even) {color: red;}
nth-of-type(odd) {color: blue;}
```

对偶数个列表项应用红色字体，对奇数个项应用蓝色字体。

上述相同的方法也可以适用于 `nth-child` 选择器，其重要的区别是 `nth-child` 选择器选择父元素的**任何**子元素，而 `nth-of-type` 选择器只选择特定类型的元素。

## 用于超文本的伪类

另一种类型的伪类是动态伪类，其类可以根据用户的操作更改状态。动态伪类用于超文本链接，例如 `visited` 类，它表示链接的目标已经被用户访问过。图 2-46 描述了这些动态伪类。

图 2-46 动态伪类

| 伪类 | 描述 |
|---|---|
| :link | 链接尚未被访问。 |
| :visited | 链接已被访问过。 |
| :active | 元素正在被点击。 |
| :hover | 鼠标悬停在元素上。 |
| :focus | 元素正在获取焦点。 |

例如，要更改未访问链接的颜色，使用该伪类：

```css
link {
  color: red;
}
```

要更改鼠标悬停时链接的颜色，使用该伪类：

```css
:hover {
  color: blue;
}
```

使用伪类创建超文本

伪类允许你对用户的操作做出响应。例如，伪类允许你根据状态对链接进行样式设置。

`:link`
`:visited`
`:hover`
`:active`

# 教程 2 CSS 入门 | HTML 和 CSS HTML 151

图 2-48 应用于悬停链接的样式

## 伪类 Hover：针对触控设备

该伪类的编写初衷是仅适用于支持鼠标或类似设备的界面。从技术上讲，手机和平板电脑等触控设备并没有悬停事件。然而，当用户最初触摸超文本链接时，设备仍通过短暂应用该样式来支持悬停样式。

许多移动设备使用“双击”响应，因此最初触摸页面元素时会触发悬停样式，然后立即再次点击该页面元素会触发点击事件。这种技术通常用于使用悬停效果来显示隐藏页面对象的网页。在教程 5 中将介绍如何利用这一特性在移动设备上创建隐藏菜单。

随着触控设备重要性的日益增加，一个指导原则是：您应该避免让支持悬停样式成为终端用户的必要条件。然而，效果应该局限于增强用户体验，而不应是其核心组件。

## 伪元素

另一种类型的伪选择器是伪元素，它是一个只存在于渲染页面中的对象。例如，段落（paragraph）是 HTML 文件中被标记的元素，但段落的第一行不是。同样，段落的首字母不是文档元素，但它确实可以被识别为网页中的一个对象。可以使用以下 CSS 选择器选择伪元素

```css
element:pseudo-element
```

其中 `element` 是 HTML 文件中的一个元素，`pseudo-element` 是 CSS 伪元素的名称。图 2-49 描述了 CSS 支持的伪元素。

# HTML 152 HTML 和 CSS | 教程 2 CSS 入门

图 2-49 伪元素

| 伪元素 | 描述 |
| --- | --- |
| :first-letter | 元素文本的首字母 |
| :first-line | 元素文本的第一行 |
| :before | 直接插入在元素之前的内容 |
| :after | 直接插入在元素之后的内容 |

例如，以下样式规则匹配渲染页面中每个段落的第一行，并将该文本转换为大写字母：

```css
p::first-line {text-transform: uppercase;}
```

以下样式规则匹配引用块（blockquote）内每个段落的首字母，并以比周围文字大 250% 的 Times New Roman 字体显示：

```css
blockquote p::first-letter {
  font-family: 'Times New Roman', Times, serif;
  font-size: 250%;
}
```

注意，双冒号 `::` 是 CSS3 中引入的，用于区分伪元素和伪类。旧版浏览器使用冒号 `:` 同时表示伪元素和伪类。

# 使用 CSS 生成内容

另一种伪元素用于为网页生成内容。可以使用 `before` 和 `after` 伪元素在元素之前或之后添加新内容：

```css
element::before {content: text};
element::after {content: text};
```

其中 `text` 是插入到渲染网页中的内容。`content` 属性支持图 2-50 所示的各种类型的文本内容。

图 2-50 content 属性的值

| 值 | 描述 |
| --- | --- |
| none | 将内容设置为空字符串 |
| counter | 显示计数器值 |
| attr(attribute) | 显示选择器的属性值 |
| text | 显示指定的文本 |
| open-quote | 显示起始引号 |
| close-quote | 显示结束引号 |
| no-open-quote | 如果之前指定，则移除起始引号 |
| no-close-quote | 如果之前指定，则移除结束引号 |
| url(url) | 显示来自 url 的媒体内容 |

例如，以下样式规则将 `before` 和 `after` 伪元素与 `hover-class` 类，在每个文本周围插入 "<" 和 "&gt;" 字符：

```css
nav a::before { content: "<"; }
nav a::after { content: "&gt;"; }
```

注意，这些规则也被 `hover-class` 使用，在悬停时插入内容。如果需要插入标记字符，必须插入这些字符的 Unicode 编码。例如，如果使用角括号显示 < 和 >，则需要使用 `\0ab` 和 `\0bb`。在导航中使用这些字符，可以使用以下样式：

```css
nav a::before { content: "\0ab"; }
nav a::after { content: "\0bb"; }
```

除了向元素添加内容外，还可以使用以下代码插入媒体文件（如图像或视频）：

```css
content: url(url);
```

其中 `url` 是媒体文件的位置。例如，当悬停时，以下样式会附加图像文件：

```css
a::after { content: url(uparrow.png); }
```

样式表生成的任何内容都不应该是理解页面的至关重要的材料。相反，生成的内容应该是为了艺术或设计考虑。如果生成的内容对于解释页面至关重要，则应放在 HTML 文件中。

# 显示属性值

`content` 属性可以通过 `attr()` 函数将属性值插入到渲染网页中：

```css
content: attr(attribute)
```

其中 `attribute` 是选中元素的属性。此项应用是添加文本中任何超文本链接的 URL。在接下来，`href` 属性的值附加到带有元素的每个文本处：

```css
a::after {
  content: attr(href)";
}
```

注意圆括号内的 URL。因此，HTML 文档中的超文本链接，如下：

```html
<a href="http://www.triathlon.org">Triathlons</a>
```
