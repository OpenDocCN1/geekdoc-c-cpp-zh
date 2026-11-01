
| 属性 | 描述 | 示例 |
|---|---|---|
| font-family<br>font-size<br>font-style<br>font-weight | 更改页面上所用字体的外观。 | font-family: Arial;<br>font-size: 18px;<br>font-style: italic;<br>font-weight: bold; |
| height<br>width | 设置页面中元素的高度或宽度。 | height: 100px;<br>width: 200px; |
| margin<br>padding | 设置元素内部（padding）和外部（margin）的空白量。 | padding: 0;<br>margin: 20px; |
| visibility | 控制元素在页面中是否可见。不可见元素仍然占据屏幕空间；只是你看不到它们。 | visibility: hidden;<br>这会使元素不可见。但是，它仍然占据页面中原来的空间。就好像元素仍在原地，但完全透明。 |

幸运的是，VS 提供了许多 CSS 工具，帮助你找到合适的属性，因此你不必全部记住它们。

> *注意 本文所描述的 CSS 选择器和属性只是其中一部分，CSS 中还有更多。有关 CSS 的更多详细信息，请查阅 VS 的 IntelliSense 列表，或查看 www.w3schools.com/cssref。*

要使属性发挥作用，你需要为其赋予一个值，这个值回答了第三个问题：你希望所选元素的部分呈现什么外观？

## 值

与属性一样，值的种类也很多。你可以使用的值取决于属性。例如，color 属性接受表示颜色的值。这个值可以是命名颜色（如 white）、表示红、绿、蓝（RGB）分量的十六进制数（如 #FF0000），也可以使用 CSS 的 rgb 表示法来设置。以下示例在功能上完全等价，都将 h1 元素的颜色设置为红色：

```
h1
{
  color: Red;
}
h1
{
  color: #FF0000;
}
h1
{
  color: rgb(100%, 0%, 0%);
}
```

你还可以使用 rgba 表示法来指定颜色的透明度，其中第四个参数是介于 0（完全透明）和 1（不透明）之间的小数，如下所示：

```
color: rgba(255, 0, 0, 0.50);
```

使用命名颜色可以提高 CSS 代码的可读性，但由于命名颜色的列表相对较短，你常常需要使用十六进制表示法来获得所需的精确颜色。本章稍后将介绍如何使用内置的颜色选择器来创建你需要的精确颜色。

还可以使用许多其他值，包括尺寸单位（px、em 等）、字体族、图像（采用 url(SomeImage.jpg) 的形式），或所谓的枚举，如 border-style，它允许你设置边框样式，例如 solid（实线）、dashed（虚线）、double（双线）等。

## 使用简写

许多 CSS 属性既支持简写形式，也支持更展开的形式。以 border 属性为例，你可以用最简短的形式设置 border 属性，如下所示：

```
border: 1px solid Black;
```

这个 border 属性会为 HTML 元素的四边都应用边框。边框大小为 1px，样式为 solid（其他选项包括 dashed、dotted 和 double），边框颜色设置为 Black。

这是一种快速将 HTML 元素四边边框设置为相同值的简便方法。但是，如果你想对各个边框及其属性进行更多控制，可以使用展开的版本：

```
border-top-width: 1px;
border-top-style: solid;
border-top-color: Black;
border-right-width: 1px;
border-right-style: solid;
border-right-color: Black;
border-bottom-width: 1px;
border-bottom-style: solid;
border-bottom-color: Black;
border-left-width: 1px;
border-left-style: solid;
border-left-color: Black;
```

这个长版本产生的效果完全相同：四边都是 1 像素厚的黑色实线边框。在大多数情况下，你应该优先使用简写形式而不是展开形式，因为它更易于阅读和维护。但是，如果你需要完全控制边框——例如，你希望 HTML 元素的左侧和顶部为 2 像素虚线边框，右侧和底部为绿色实线边框——那么了解可以单独设置四个方向的每个边框属性是很有用的。你还可以混合使用这些选项。以下示例先将四边边框设置为 1 像素黑色实线，然后仅覆盖左边框的颜色：

```
border: 1px solid Black;
border-left-color: Blue;
```

其他支持简写形式的 CSS 属性包括 font、background、list-style、margin 和 padding。如果你不确定某个属性是否支持简写形式，可以在 CSS 文件或 `<style>` 块中输入属性时按 Ctrl+Space，查看弹出的 IntelliSense 列表。

尽管有时编写 CSS 似乎需要反复试验，并希望能得到正确结果，但实际上 CSS 背后有一个相当精确的模型，用于决定页面中元素的布局方式。这个模型称为 CSS 盒模型（CSS Box Model）。

## CSS 盒模型

CSS 盒模型描述了三个重要的 CSS 属性如何应用到 HTML 元素上：padding（内边距）、border（边框）和 margin（外边距）。图 3-4 展示了盒模型的图形表示。

![](img/eadab2ccd79b253c01a3fdff2321202d_123_0.png)

图 3-4

中间是一个具有特定高度和宽度的 HTML 元素，例如 `<p>` 或 `<div>`。紧挨着它的是 padding（内边距），即元素边框内包围元素的空白区域。在 padding 之后紧跟着的是 border（边框），最后在外部是 margin（外边距），它定义了元素（包括其内边距和边框）与其周围元素之间的空间。一个元素的三个外部属性——padding、border 和 margin——加起来就是该元素在页面中占据的空间。为了理解其工作原理，请看下面的 CSS 和 HTML：

```
.MyDiv
{
    width: 200px;
    padding: 10px;
    border: 2px solid Black;
}
...
<div class="MyDiv">Element</div>
```

这会在浏览器中渲染一个矩形，`<div>` 元素周围环绕着 2 像素宽的黑色边框，如图 3-5 所示。

![](img/eadab2ccd79b253c01a3fdff2321202d_123_1.png)

图 3-5

在继续阅读之前，请尝试回答这个问题：`<div>` 元素下方的箭头有多宽？

如果你猜的是 224 像素，那么你答对了。箭头的宽度是三个值之和：元素本身的宽度（200 像素），加上元素两侧内边距的宽度（2 × 10 像素），再加上两侧边框的宽度（2 × 2 像素），总宽度为 224 像素。因此，如果你希望整个盒子的宽度为 200 像素，则需要将 MyDiv 选择器的 width 属性设置为 176px。在元素边框之外，margin 还会进一步影响该元素与其周围元素之间的间距。

该示例只展示了对宽度的影响，但同样的原理也适用于元素的高度。在布局页面时，请牢记这个盒模型。当元素的最终宽度或高度超出你的预期时，请检查 CSS 样式表中的 width、height、padding、border 和 margin 属性。

在下一个练习中，你将修改上一章创建的网站主页。你将添加网站的基本布局，然后使用样式表对其进行样式化。在第 6 章中，当该页面升级为母版页时，你会再次用到它。

## 试一试：为 Planet Wrox 主页设置样式

在本练习中，你将修改两个文件。首先，向 Default.aspx 页面添加基本布局元素，为页眉、菜单、主内容区域、侧边栏和页脚创建空间。然后，修改 Styles 文件夹中的 Styles.css 文件，以更改这些元素的尺寸和位置。最后，将样式表附加到页面，以便在设计器或浏览器中查看页面时应用样式信息。

1. 打开网站根目录下的 Default.aspx 文件，如有必要，切换到标记视图。

2. 修改 `<form>` 元素内的代码，使其最终如下所示：

```
<form id="form1" runat="server">
  <div id="PageWrapper">
    <header>Header Goes Here</header>
    <nav>Menu Goes Here</nav>
    <section id="MainContent">
      <h1>Hi there visitor and welcome to Planet Wrox</h1>
    ...
    </section>
    <aside id="Sidebar">Sidebar Goes Here</aside>
    <footer>Footer Goes Here</footer>
  </div>
</form>
```

确保上一章添加的欢迎消息位于 MainContent `<section>` 元素的开始和结束标签之间。如果你已经熟悉 HTML5 之前的 HTML 版本，可能会对 `header`、`section` 和 `footer` 等新元素感到有些惊讶。这些元素是在 HTML5 中引入的，目的是为文档提供更好的语义结构。有关 HTML5 的快速介绍，请参阅第 1 章。

3. 打开 Styles 文件夹中的 Styles.css 文件。如果你之前向此文件添加过一些代码，请先删除这些代码。

