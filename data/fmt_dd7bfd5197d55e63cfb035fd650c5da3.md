
Vestibulus nisi metus, imperdiet sed, mollis condimentum, nonummy eu.

Duis lobortis felis in est. Nulla eu velit nisi consequat vulputate.

Vestibulum vel metus. /2 Integer ut quam. Ut dignissis, sapien sit amet malesuada aliquam, quam vulputate nibh pulvinar velit at eros. Sed semper lacinia. In. Aliquam ut dolor leo scelerisque. Susppendisse non velisque nec metus. Lorem ipsum dolor sit amet, consectetuer adipicing elit. Praesent pellentesque interdum magna.

## 698 | 第 17 章 使用 ASP.NET 进行 HTML 和 CSS 设计

你可以使用 `position` 属性显式地设置元素的行为。例如，在此处对 div 上设置 `position` 属性，结果如下：

```
<div style="position:relative;"><<b>convallis</b> porttitor.

Vestibulus nisi metus, imperdiet sed, mollis

condimentum, nonummy eu, magna.

</div>
```

Visual Studio 通过为块提供定位线来提供帮助，显示其偏移量是基于块的正常顶部位置计算的，以及相对于正常左侧位置的偏移。Visual Studio 甚至允许你通过选取元素标签并将其拖到设计表面来对块进行定位。

## CSS 定位

CSS 为你提供了三种主要的定位机制：正常（normal）、绝对（absolute）和相对（relative）。每种类型对于你如何在页面中布局元素都提供了不同的益处。每个元素都有自己的 `position` 属性，允许你在页面中使用多种定位方案。

### 正常定位

使用正常定位时，块级元素垂直流向，行内元素从左到右水平流向。这种行为是默认的，当未为 `position` 属性提供值时。图 17-3 展示了四个独立块的布局。

### 相对定位

使用相对定位时，元素最初使用正常布局进行定位。先对框进行定位，然后根据其偏移（top, bottom, left, right）移动框。图 17-14 显示了与上一节相同的内容，但现在第三个框已被样式化为相对定位。Visual Studio 通过为块提供定位线来提供帮助，显示其偏移量是基于块的正常顶部位置计算的，以及相对于正常左侧位置的偏移。Visual Studio 甚至允许你通过选取元素标签并将其拖到设计表面来对块进行定位。

## 700 | 第 17 章 使用 ASP.NET 进行 HTML 和 CSS 设计

当你设计表面上移动位置时，元素的顶部和左侧值会更新。你最终将得到如下所示元素：

```html
<div style="position:relative; top:214px; left:62px; width:239px;height:81px">
  Done et velit a risus <b>convallis</b> porttitor. Vestibum nisi metus, imperdiet sed, mollis condimentum, nonummy eu, magna.
</div>
```

如果你使用相对定位并同时设置左、右偏移，右偏移将被很大程度上忽略。

## 绝对定位

绝对定位的工作与相对定位类似，不同在于元素不是根据其在普通定位方案中的位置来计算偏移，而是根据其最近的定位祖先元素的位置计算偏移。如果没有该元素，则祖先是浏览器窗口本身。

图 17-15 显示了使用绝对定位的块如何在 Visual Studio 表面上显示。如你所见，与上一节所示相对元素的大小不同，这些定位线延伸到了设计表面的边缘。这是因为该块正在使用浏览器窗口来计算其偏移。

![](img/7040c21013b8e6c23c612d6da3599ff8_759_0.png)

图 17-15

与相对块一样，你可以使用元素的标签在页面上定位该元素，Visual Studio 会自动更新偏移值。图 17-15 中的块将输出如下所示的元素：

```html
<div style="position:absolute; top:180px; left:94px; width:239px;height:81px">
  Done et velit a risus <b>convallis</b> porttitor. Vestibum nisi metus, imperdiet sed, mollis condimentum, nonummy eu, magna.
</div>
```

## 浮动元素

另一个选项允许你控制元素位于块的左侧或右侧。`float` 属性允许你在垂直方向上像普通位置中那样浮动元素，但在水平方向上尽可能向左或向右移动。代码列表 17-11 展示了在本节之前示例中使用的相同块进行浮动处理。

代码列表 17-11：将元素向右浮动

```html
<!DOCTYPE html PUBLIC "-//W3//DTD HTML 1.0 Transitional//EN">
"http://www.w3.org/TR/htmlml/html-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <meta id="Head" runat="server">
</head>
<body>
  <form id="form" runat="server">
  <div id="asdas" class="werver">
    <Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  </div>
  <div style="float:right; width:236px;">
    Donec et velit a risus <b>convallis</b> porttitor portittor.
    Vestibulum nisi metus, imperdiet sed, mollis
    condimentum, nonummy eu, magna.
  </div>
  <div>
    Dubois lobortis felis in est. Nulla eu velit ut nisi
    consequat volutpat.
  </div>
  <div>
    Vestibulum metus. Integer ut quam. Ut digniss, diamplin
    sit amet metales massa aliquam, quam vulputate nibh, ut
    put velit lorem at eros. Sed semper lacinia diam. In finibus
    facilisis arcu. Nulla facilis interdum quam Aliquam
    ut id leo scelerisque scallis. Suspendisse non velit.
    Quisque nec metus. Lorem ipsum dolor sit amet, consectetur
    adipiscing elit. Praesent elequent interdum magna.
  </div>
  </form>
</body>
</html>
```

该块已修改，在它的样式中包含了 `float` 属性。完成后，Visual Studio 会正确将元素定位到页面的最右侧，如图 17-16 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_760_0.png)

图 17-16

## 重要的属性

正如你在本章早些部分提到的，浏览器将选择对元素应用最近的样式，这意味着其他已应用样式的属性可能会被覆盖。在 CSS 的许多其他规则中，这一点也不是绝对的。CSS 提供了一种绕过此规则的机制，称为 `!important` 属性。应用了此属性的属性将防止其他 CSS 规则覆盖其值。代码列表 17-8 显示了 `font-family` 属性如何被覆盖。你可以通过修改此示例并在代码列表 17-12 中查看 `!important` 属性是如何工作的。

代码列表 17-12：使用 `important` 属性控制样式覆盖。这在代码列表 17-12 中所示。

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Headt" runat="server">
<style type="text/css">
p{
  font-family: Arial !important;
}
</style>
</head>
<body>
  <form id="form" runat="server">
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
  </form>
</body>
</html>
```

## 在 VISUAL STUDIO 中处理 CSS

当你开始创建样式时，你的应用程序需要能够管理并将这些样式应用到应用程序中的元素。Visual Studio 包含了三个你可以使用的工具来管理样式表、将样式应用于元素，并轻松检查应用于元素的样式属性。

要探索的第一个工具是“管理样式”（Manage Styles）工具窗口，你可以通过“视图”（View）菜单的 CSS 子菜单中打开“管理样式”。该工具窗口如图 17-20 所示，它提供了 Visual Studio 中当前 Web 页面可用所有样式的概览。

如果你检查此工具的内容，你会发现顶部部分包含两个重要的链接：新样式（New Style），它会打开新样式对话框并允许你按照本节所述创建新样式；以及附加样式表（Attach Style Sheet），它允许你将新的样式表导入到 Web 页面中。使用此选项将样式附加到 Web 页面会导致 Visual Studio 在你的网页中插入 `<link>` 标签。

请记住，你必须小心标签和样式块的顺序，以确保样式被正确应用。

窗口的下部分显示类型选择器（type selector）所有可用样式。样式用彩色圆点表示：蓝色表示类型选择器，绿色表示类选择器（Class selectors），红色表示 ID 选择器。页面内显示的样式在彩色圆点周围有一个灰色圆圈。如果你的网页包含多个样式选择器，它们会被分组在一起，以便于确定样式定义的位置。

此外，如图 17-20 所示，工具窗口让你看到通过 CSS 导入附加到 Web 的样式。通过展开图中所示的 `layout.css` 节点，你可以看到该样式中包含的所有样式列表。

最后，工具窗口的底部包含一个预览区域，允许你看到每个样式的实时预览。

## 应用样式工具窗口

在 Visual Studio 中使用 CSS 的第二个工具是应用样式（Apply Styles）工具窗口。通过管理样式工具，应用样式窗口为你提供了一种简单的方法来查看应用程序中可用的 CSS 样式，并将其应用于 Web 页面上的元素。通过工具窗口，你可以将 CSS 文件附加到 Web 页面，使外部 CSS 样式可以应用于或从元素中移除；并对其进行修改。与其他 CSS 工具一样，应用样式窗口根据 CSS 继承顺序显示可用样式，外部样式首先显示，然后是类型选择器部分，最后显示的内联样式也会根据当前选中的元素进行上下文感知，并显示应用程序中应用于该元素类型的样式。样式还根据 CSS 选择器工具进行分组，每个选择器都有不同的视觉指示。

图 17-21 中的工具窗口显示了用于锚点标签的可用样式。工具首先显示附加的 `global.css` 文件中的所有样式、当前页面的样式，最后如果已应用，则显示元素的内联样式。你可以点击这些部分中的任何样式以将其应用到该元素。

应用样式工具还具有正确应用多个类选择器的智能（在点击列表中的类选择器时按住 Ctrl 键），但防止选择会导致无效 CSS 的多个 ID 选择器。该工具也不会让你取消选择类型选择器或内联样式。

![](img/7040c21013b8e6c23c612d6da3599ff8_764_0.png)

- CSS 样式：
- global.css
- layout.css
- html-body
- body
- #global-container
- #Global
- ActionBar
- .Selector
- *Selector*
- #style-class #style-span
- #li-menu = li | span =
- .LeftMenu
- .LeftMenu-child-id
- #RightMenu
- Footer

选中的样式预览：

![](img/7040c21013b8e6c23c612d6da3599ff8_764_1.png)

![](img/7040c21013b8e6c23c612d6da3599ff8_764_2.png)

- CSS 样式：
- global.css
- layout.css
- Footer

- 清除样式
- global.css
- layout.css
- .footerMenu
- .footerImage
- #Menu-lifting

- 当前页面
- .pageFooter

- 上下文选择器
- global.css

- *body
- body

图 17-21

## CSS 属性工具窗口

最后一个工具如图 17-22 所示的 CSS 属性工具窗口。这个实用的工具显示了应用于当前所选元素的所有 CSS 属性。
工具窗口由两个独立部分组成：应用规则（Applied Rules）和 CSS 属性（CSS properties）。

应用规则列表显示了应用于所选元素的所有 CSS 规则。它根据规则的继承链自动排序，从最外层到顶部，再到最内层规则。这意味着包含在外部文件中规则会自动排在列表顶部，而内联样式排在底部。你可以点击列表中的每条规则，并更改 CSS 属性网格中显示的属性。

CSS 属性网格的工作方式类似于 .NET 属性网格，向你显示元素所有可用的 CSS 属性，并显示已设置值的属性。此外，你可以直接从 CSS 属性网格为 CSS 规则设置值。还有一个“摘要”（Summary）按钮，允许你更改 CSS 属性网格的显示，仅显示已设置值的属性。此功能非常有用，因为 HTML 元素可以有大量的 CSS 属性。

由于它还包含了属性继承的概念（这在标准 .NET 对象中通常不可用），CSS 规则列表和 CSS 属性网格的设计旨在帮助你识别特定值定义的位置。当你点击 CSS 规则列表中的每条规则时，CSS 属性网格会更新以反映该规则的属性。你会注意到，某些属性带有删除线（参见图 17-23）。

属性的删除线表示该属性的值被更靠近元素的规则覆盖了。

![](img/7040c21013b8e6c23c612d6da3599ff8_765_0.png)

图 17-22

![](img/7040c21013b8e6c23c612d6da3599ff8_765_1.png)

图 17-23

## 在母页中管理 CSS 链接

在母页中使用 CSS 链接时，管理 CSS 链接可能会变得困难，因为除非给 Link 标签指定一个 ID，否则它无法解析相对 URL。然后，在页面加载（Page Load）时，将链接的 Href 设置为正确的相对 URL。

## 样式化 ASP.NET 控件

由于 ASP.NET 控件只是渲染 HTML 标记，使用 CSS 对它们进行样式化相当简单。事实上，控件使用内联 CSS 样式。你可以通过查看标准的 ASP.NET 控件来看到这种操作。样式化像按钮这样的 ASP.NET 控件的标准方法是提供值。

708 | 第 17 章 使用 ASP.NET 进行 HTML 和 CSS 设计

# 列表 17-13（继续）

```xml
<form id="form" runat="server">
  <asp:Button ID="Button1"
    CssClass="search" runat="server" Text="Button" />
</form>
</body>
</html>
```
