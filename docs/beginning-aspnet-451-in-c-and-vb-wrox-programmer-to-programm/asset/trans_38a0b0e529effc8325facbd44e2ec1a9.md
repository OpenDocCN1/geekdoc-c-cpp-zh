

# CSS 简介 | 75

使用命名颜色可以提高 CSS 代码的可读性，但由于你只能从相对较短的命名颜色列表中选择，通常需要使用十六进制表示法来获得你想要的确切颜色。本章后面你将看到如何使用内置的颜色选择器来创建所需的确切颜色。

还有许多其他值也是可能的，包括尺寸单位（px、em 等）、字体族、图像（形式为 url(SomeImage.jpg)），以及所谓的枚举，如 border-style，它使你能够设置诸如 solid、dashed 和 double 之类的边框样式。

## 使用简写

许多 CSS 属性都允许你使用简写版本而不是更展开的版本。例如 border 属性。在最简形式中，你可以这样设置 border 属性：

```
border: 1px solid Black;
```

此 border 属性将边框应用于 HTML 元素的四个边。边框大小为 1px，样式为 solid（其他选项包括 dashed、dotted 和 double），边框颜色设置为 Black。

这样可以轻松地快速将 HTML 的四个边框都设置为相同的值。然而，如果你想控制各个边框及其属性，可以使用展开版本：

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

这个较长的版本创建的效果与在所有四个边上都有 1px 厚的实线边框完全相同。在大多数情况下，你应该优先使用简写表示法而不是其展开形式，它更容易阅读和维护。然而，如果你需要对边框进行绝对控制——例如，如果你想要顶部和左侧有 2 像素的虚线边框，而右侧和底部为绿色实线边框——知道你可以单独设置所有方向的每个边框属性是很有用的。你也可以混合使用这些选项。

```
border: 1px solid Black;
border-left-color: Blue;
```

支持简写的其他 CSS 属性包括 font、background、list-style、margin 和 padding。如果你不确定某个属性是否支持简写，在 CSS 文件或 <style> 块中输入属性时按 Ctrl+Space 会出现 IntelliSense 弹出列表。

虽然有时看起来你需要通过反复试验来使用 CSS，并希望得到正确的结果，但在 CSS 背后有一个相当准确的模型来确定元素在页面上应如何布局。这个模型被称为 CSS 盒模型。

## CSS 盒模型

CSS 盒模型描述了应用于 HTML 元素的三个重要 CSS 属性：padding、border 和 margin。图 3-4 显示了盒模型的图形表示。

中间是一个 HTML 元素，如 <p> 或 <div>，具有一定的高度和宽度。紧靠外部的是 **padding**；空白环绕元素内部的边框。padding 之后可以看到 border，最后在最外部的是 *margin*，它定义了元素（包括其 padding 和 border）与其周围元素之间的空间。元素的三个外部属性——padding、border 和 margin——之和构成了元素在页面上占用的空间。要了解其工作原理，请考虑以下 CSS 和 HTML：

```
.MyDiv {
  width: 200px;
  padding: 10px;
  border: 2px solid Black;
}

<div class="MyDiv">Element</div>
```

这将在浏览器中渲染一个矩形，<div> 元素周围环绕着 2 像素的边框，如图 3-5 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_113_0.png)

继续之前，请尝试回答这个问题：<div> 元素下方箭头的宽度是多少？

如果你猜测是 224 像素，你是正确的。箭头的宽度是三个值的总和：元素的宽度（200 像素），加上两侧的 padding 宽度（两边各 10 像素），加上两侧的 border 宽度（两边各 2 像素），总宽度为 224 像素。因此，如果你希望该框宽为 200 像素，你需要将 .MyDiv 选择器的 width 属性设置为 176px。边框外部，margin 还可能进一步影响该元素与其周围元素之间的间隙。

示例展示了对宽度的效果。在布局页面时请牢记这个盒模型。当元素比预期更宽时，请检查 CSS 样式中的 width、height、padding、border 和 margin 属性。

在下一个练习中，你将修改上一章中创建的网站主页。你为网站添加基本布局，然后使用样式表对其进行样式设置。在第 6 章中，你将再次使用此页面将其升级为主页。

![](img/9e033e3b9560597824f8b22941d6d8bb_113_1.png)

# CSS 简介

## 试用 为 Planet Wrox 主页设置样式

在此练习中，你将修改两个文件。首先，你在 Default.aspx 页面中添加基本布局元素，为页眉、菜单、主要内容区域、侧边栏和页脚腾出空间。你修改 Styles 文件夹中的 styles.css 文件以更改这些元素的大小和位置。最后，你将样式表附加到页面上，样式信息在设计器或浏览器中查看页面时会被应用。

- 1. 打开网站根目录中的 Default.aspx 文件，如果需要，切换到标记视图。

- 2. 修改 <form> runat="server"> 内的代码，使其最终如下所示：

```
<form id="form" runat="server">
  <div id="PageWrapper">
    <header>Header Goes Here</header>
    <nav>Menu Goes Here</nav>
    <section id="MainContent">
      <h1>Hi visitor and welcome to Planet Wrox</h1>
    </section>
    <aside id="Sidebar">Sidebar Goes Here</aside>
    <footer>Footer Goes Here</footer>
  </div>
</form>
```

确保你在上一章中添加的欢迎信息位于 MainContent <section> 元素的开始和结束标签之间。如果你之前熟悉 HTML 的版本，你可能会对 header、section 和 footer 等新元素感到惊讶。这些元素是在 HTML5 中引入的，目的是为文档提供更好的语义结构。有关 HTML5 的快速介绍，请参阅第 1 章。

- 3. 打开 Styles 文件夹中的 Styles.css 文件。如果你在该文件中添加了一些代码，请删除该代码。

- 4. 在 CSS 文件顶部，输入以下使用 ID 选择器选择 header 元素的代码：

```
header
{
}
```

- 5. 将鼠标定位在花括号之间并输入字母 b。这会将你带到所有以字母 b 开头的属性，如图 3-6 所示。

接下来，输入字母 c。此列表会被过滤，如图 3-7 所示。
注意这种过滤方式非常智能。过滤器不会将列表限制为仅以 c 开头或包含字母 bc 的属性（在这种情况下不存在），但它还支持所谓的标题
case 搜索，这意味着它列出属性中每个单词都以你搜索的字母开头的项目。在这种情况下，bc 匹配 background-clip、background-color 等项目，同样的规则适用于所有其他 CSS 属性。例如，td 会给出 text-decoration，bbw 会给出 border-bottom-width，等等。这使得只需几个击键就能非常轻松地编写 CSS。

注意列表中某些项目具有剪刀图标而不是标准属性图标。剪刀表示可通过按两次 Tab 键展开的代码片段。这样会在文件中插入浏览器特定的 CSS，用于尚未被所有浏览器实现的 CSS 属性。

继续此练习，选择列表中的 background-color。你可以双击该值，按 Enter 或 Tab，VS 会为你补全该属性。接下来，输入一种颜色、冒号，然后是井号（#）后跟 cocococo（代表银色）。用分号结束该行。你的最终代码可能如下所示：

```
header {
  background-color: #C0C0C0;
}
```

- 6. 通过添加 width 和 height 属性来完成 header 元素的代码块，如下所示：
{
  background-color: #C0C0C0;
  width: 844px;
  height: 86px;
}

- 7. 通过创建以下规则来完成 CSS 文件。充分利用 Visual Studio 的 IntelliSense 和标题搜索功能，以最大限度地减少编写此代码所需的击键次数。

```
* {
  font-family: Arial;
}
h1 {
  font-size: 20px;
}
#PageWrapper {
  width: 844px;
  margin: auto;
}
nav {
  width: 844px;
}
```

