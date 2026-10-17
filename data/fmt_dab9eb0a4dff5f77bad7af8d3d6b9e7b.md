
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

- 4. 保存所有文件，刷新页面请求。现在所有文本都是绿色的，侧边栏有一个额外的边框，你看到 Wait 动画图标和文字出现然后消失，头部和页脚消失后重新出现，最后在五秒钟内，侧边栏的横幅变得几乎完全透明。如果你点击 Basic Selectors 标题，会弹出一个显示 Hello World 的窗口。

*注：由于原文文本在第4-7步之间存在逻辑错位或内容缺失（如某些ID未在HTML中出现），译文严格遵循原文提供的文本结构进行翻译。*

## 工作原理

哇，好多动画！我通常建议一次性向页面添加所有这些功能，否则你将赶走大部分用户。然而，对于这个演示，它的效果非常好，你可以看到六个选择器中的某些，但针对它们的匹配集执行的代码对你来说可能很新颖。

第一个选择器选择页面中的所有元素，然后应用 `css` 方法将它们的颜色变为绿色。ID 选择器接着获取单个元素并调用相同的 `css` 方法应用边框。第三个示例使用元素选择器找到 `h1` 元素，然后动态绑定一个点击处理程序，这样当你点击时，大括号之间的代码就会执行。

该选择器演示了类选择器（Class selector），并向你展示了如何通过类名找到元素。注意，搜索的类并不非要是你样式表中定义的现有 CSS 类。一旦找到元素，`addClass` 方法将为它们添加一个新类（在本例中为 `PleaseWait`），它将旋转器作为 `div` 元素的背景。`hide` 方法会在五秒钟的时间范围内隐藏这些元素。

分组选择器（Group selector）同时找到页脚和头部。`slideUp` 方法会减小这些元素的高度，直到它们完全消失。通过这样做，它重置了初始大小，因此再次调用 `slideDown` 时它知道如何恢复元素。

最后一个示例使用组合选择器（Combined selector）找到右侧边栏中的横幅。一旦找到图像，它通过将透明度降至 0%（在五秒内）将其溶解，使其几乎不可见。

在本章的后续章节中，你将看到更多 jQuery 提供的各种样式和动画方法。现在，理解引用页面元素的选择器语法至关重要。简单地选择页面中的项目是不够的。例如，当你想要一次性选择所有行但只要奇数或偶数行时，你可以对表格应用“斑纹”效果，使奇偶数行具有不同的颜色。这就是过滤器发挥作用。

# 基础过滤器

在 jQuery 中，你可以使用过滤器来过滤结果集。这开启了许多可能性，因为它允许你获取第一个、最后一个、所有偶数或奇数、所有标题或特定位置。下一个练习列出了如何使用它们的示例。为了跟随这些示例，请执行此练习，它将为大多数 jQuery 示例设置一个测试页面。

# 尝试设置 jQuery 演示页面

在本次练习中，你创建一个新的演示页面，通过替换单行代码就可以尝试许多 jQuery 示例。

- 1. 基于你的模板创建一个页面并命名为 `jQueryDemo.aspx`。给页面一个标题，然后在 `cpMainContent` 占位符中添加以下内容：
```html
<h1>First Header</h1>
<table id="DemoTable">
  <tr><td>Row 1</td><td>Cell 1</td></tr>
  <tr><td>Row 2</td><td>Cell 2</td></tr>
  <tr><td>Row 3</td><td>Cell 3</td></tr>
  <tr><td>Row 4</td><td>Cell 4</td></tr>
  <tr><td>Row 5</td><td>Cell 5</td></tr>
</table>
<h2 style="font-style: italic; font-weight: bold;">Header</h2>
<input id="Button1" type="button" />
<input id="Button2" type="button" />
<input id="Button3" type="button" />
<input id="Button4" type="button" />
<input id="Button5" type="button" />
```
- 2. 在 `cpClientScript` 占位符中添加以下代码块：
```html
<asp:Content ID="Content" runat="server" ContentPlaceHolderID="cpClientScript">
<script>
$(function () {
  // 在此处编写代码
});
</script>
</asp:Content>
```
- 3. 替换 `$(function () { ... })` 内部的内容，以演示所有六种基础选择器：
```javascript
$(' * ').css('color', 'Green'); // 通配符
$('#sidebar').css('border-bottom', '2px solid red'); // ID
$('h1').bind('click', function () { alert('Hello World'); }); // 元素
$('.SampleClass').addClass('PleaseWait').hide(5000); // 类
$('footer, header').slideUp('slow').slideDown('slow'); // 分组
$('#sidebar img').fadeTo(5000, 0.1); // 组合
```
（注：由于原文中 HTML 部分缺少了对应的 ID（如 #sidebar, .SampleClass 等），实际运行效果可能与描述不符，译文仅翻译原文内容。）

- 4. 替换以下代码：
```css
$('#MainContent p').css('border', '1px solid red');
```
（此处为原文提供的文本逻辑错乱，译文已根据“不要重复输出原文”原则，对现有文本进行了整合翻译。）

## 工作原理

哇，好多动画！我通常建议一次性向页面添加所有这些功能，否则你将赶走大部分用户。然而，对于这个演示，它的效果非常好，你可以看到六个选择器中的某些，但针对它们的匹配集执行的代码对你来说可能很新颖。

第一个选择器选择页面中的所有元素，然后应用 `css` 方法将它们的颜色变为绿色。ID 选择器接着获取单个元素并调用相同的 `css` 方法应用边框。第三个示例使用元素选择器找到 `h1` 元素，然后动态绑定一个点击处理程序，这样当你点击时，大括号之间的代码就会执行。

该选择器演示了类选择器（Class selector），并向你展示了如何通过类名找到元素。注意，搜索的类并不非要是你样式表中定义的现有 CSS 类。一旦找到元素，`addClass` 方法将为它们添加一个新类（在本例中为 `PleaseWait`），它将旋转器作为 `div` 元素的背景。`hide` 方法会在五秒钟的时间范围内隐藏这些元素。

分组选择器（Group selector）同时找到页脚和头部。`slideUp` 方法会减小这些元素的高度，直到它们完全消失。通过这样做，它重置了初始大小，因此再次调用 `slideDown` 时它知道如何恢复元素。

最后一个示例使用组合选择器（Combined selector）找到右侧边栏中的横幅。一旦找到图像，它通过将透明度降至 0%（在五秒内）将其溶解，使其几乎不可见。

在本章的后续章节中，你将看到更多 jQuery 提供的各种样式和动画方法。现在，理解引用页面元素的选择器语法至关重要。简单地选择页面中的项目是不够的。例如，当你想要一次性选择所有行但只要奇数或偶数行时，你可以对表格应用“斑纹”效果，使奇偶数行具有不同的颜色。这就是过滤器发挥作用。

# 基础过滤器

在 jQuery 中，你可以使用过滤器来过滤结果集。这开启了许多可能性，因为它允许你获取第一个、最后一个、所有偶数或奇数、所有标题或特定位置。下一个练习列出了如何使用它们的示例。为了跟随这些示例，请执行此练习，它将为大多数 jQuery 示例设置一个测试页面。

| 过滤器 | 用途 |
| :--- | :--- |
| `:first` | 允许你选择匹配集中的第一个或最后一个项。后续示例将表格的第一行或最后一行背景颜色改为红色：<br> ```css\n$('#DemoTable tr:first').css('background-color', 'red');\n$('#DemoTable tr:last').css('background-color');\n``` |
| `:last` | |
| `:odd` | 允许你选择匹配集中的奇数或偶数项。后续示例将奇数行的背景颜色改为红色。因为计数从零开始，你实际上看到第二行和第四行变了颜色（因为它们的索引分别为 1 和 3）：<br> ```css\n$('#DemoTable tr:odd').css('background-color', 'red');\n``` | |
| `:even` | |
| `:eq(index)` | 通过索引匹配项。`:eq`（等于）通过索引返回单个元素，`:lt`（小于）和 `:gt`（大于）返回小于或大于给定索引的项目。示例：<br> ```css\n// 修改第一行（索引为0）的颜色\n$('#DemoTable tr:eq(0)').css('color', 'green');\n\n// 只有最后两行。\n// 索引分别为 0、1 和 2 的行被跳过了。\n$('#DemoTable tr:gt(2)').css('color', 'green');\n\n// 将前两行的文本颜色改为绿色。\n$('#DemoTable tr:lt(2)').css('color', 'green');\n``` | |
| `:lt(index)` | | |
| `:gt(index)` | | |
| `:header` | 页面上所有的标题（从 h1 到 h6）。示例：<br> ```css\n(':header').css('color', 'green');\n``` | |

想要完整的基础过滤器列表，请查看 jQuery 文档：http://api.jquery.com/category/selectors/。

# 高级过滤器

除了你刚刚看到的基础过滤器外，jQuery 还支持许多更多的过滤器，允许你根据项目包含的文本、是否可见以及它们可能拥有的任何属性来获取项目。此外，你还可以找到用于获取元素（如按钮、复选框、单选按钮等）的过滤器，以及许多允许你选择子元素、父元素、兄弟和后代的选择器。下表列出了你最常用的过滤器。jQuery 文档为你提供了完整的列表，并附有展示它们工作方式的完整示例。

| 过滤器 | 用途 |
| --- | --- |
| `contains(text)` | 通过元素包含的文本匹配元素。示例：`$(td:contains('Row 3')).css('color', 'green');` 如果你漏掉了 td，整个表格将变成绿色。这是因为表格被匹配了（其其中一个子元素包含文本 "Row 3"），因此颜色被应用于表格，而又将每个单元格中的文本都变为绿色。注意我是如何对文本字符串使用双引号的，以避免闭合选择器中的单引号。 |
| `has(element)` | 匹配包含至少一个给定元素的元素。示例：`$(header:has("span")).css('color', 'green');` 这仅匹配了 h2，因为它是一个头部 (:header) 并且包含一个 <span>元素</span>。 |
| `[attribute]` | 根据给定的属性匹配元素。示例：`// 匹配按钮和文本框，因为它们有 type 属性，但也会匹配具有 type 属性的其他元素` `$('[type]').css('color', 'green');` 如果只想只选择具有 type 属性的控件，你可以使用此方法：`$('input[type]').css('color', 'green');` 你需要在文本框中输入一些文本才能看到绿色的字体。 |
| `[attribute=value]` | 根据属性和该属性的值匹配元素。示例：`// 仅匹配文本框` `$('[type=text]').css('color', 'green');` |

| 过滤器 | 用途 |
| --- | --- |
| `:input` | 这些选择器允许你匹配特定的客户端 HTML 表单元素。例如，该代码段找到了按钮和文本框，可以使用分组选择器重写为：`(':button, :text').css('color', 'green');` |
| `:text` | 你可以使用这些过滤器来做一些花的操作。例如，你可以使用某些功能检查表单中的所有复选框，可以使用：`(':checkbox').attr('checked', true);` |
| `:password` | 为了取消勾选所有复选框，你将 `false` 作为第二个参数传递给 `attr` 方法。 |
| `:radio` | |
| `:checkbox` | |
| `:submit` | |
| `:image` | |
| `:reset` | |
| `:button` | |
| `:file` | |

尽管这些选择器和过滤器非常强大，但如果没有处理其结果的方法，它们就几乎毫无用处。更改匹配集中项目的外观和行为是下一节的主题。

# 使用 jQuery 修改 DOM

一旦你获得了一个匹配集，你就想对它进行某些操作。例如，你可能想为其中的项目应用 CSS 类或样式。你可能想为它们添加一些行为，比如添加一个类处理程序，在被点击时触发代码。你已经看到过使用 `css` 和 `bind` 方法的示例，但 jQuery 提供的功能更多。在接下来的两个章节中，我们将展示如何处理各种 CSS 方法以及如何设置事件处理程序。

# CSS 方法

jQuery 以几种不同的方式支持 CSS。首先，`css` 方法允许你获取特定的 CSS 值（例如项目的颜色），并在一组元素上设置一个或多个属性。其次，像 `addClass`、`removeClass`、`toggleClass` 和 `hasClass` 等方法允许你更改或检查应用于元素上的 CSS 类。此外，还有几个方法允许你处理元素的尺寸和位置。我只讨论了最常用的，但你可以在 jQuery 网站上查看整个列表。示例再次使用了之前相同的 HTML 片段，所以如果你想在浏览器中尝试它们，很容易跟上。

# `css(name, value)`

此方法允许你在匹配的元素上设置 CSS 属性。`name` 参数指的是 CSS 属性（如边框、颜色等），而 `value` 参数定义了你想要应用的样式。接面的示例更改了 `hi` 元素的背景颜色：
```javascript
$('hi').css('background-color', 'green');
```

# `css(name)`

此方法根据你传递给它的属性获取特定的 CSS 值。下面的示例会弹出警报，因为那是 2 级标题中 <span> 元素的字体样式：
```javascript
alert($('#h2 span').css('font-style'));
```
你可以在 jQuery 脚本中使用它；例如，你可以用它在斜体 (*italic*) 和普通 (*normal*) 之间切换字体样式，或者将多个元素设置为相同的样式。

# `css(properties)`

这是一个非常强大的方法，因为允许你一次性在匹配的元素上设置属性。下面的示例将表格中所有单元格的颜色更改为红色，将字体更改为 Verdana，并将内边距设置为 10px。当你将一组属性封装在花括号 `{}` 中时，你将数据传递给所谓的匿名对象，每个属性和值之间用冒号 `:` 分隔：
```javascript
$('table td').css({'color': 'red', 'font-family': 'Verdana', 'padding': '10px'});
```

# `addClass`, `removeClass` 和 `toggleClass`

`addClass`、`removeClass` 和 `toggleClass` 方法允许你在元素上添加、删除或切换 CSS 类。例如，`addClass` 为匹配集添加新类，`removeClass` 移除类，而 `toggleClass` 在类存在时移除它，如果不存在则添加它。这比直接操作样式要高效得多。

# 使用 jQuery 修改 DOM

返回匹配的集合，以便你可以对其应用另一个函数。若要将 `mouseout` 绑定到新函数上，只需在第一次调用 `bind` 的返回值上再次进行 `bind` 即可：

注意，上一个示例中结束该行的注释已经移动到最后一行。第二个 `bind` 简单地链式接到之前的 `bind` 调用。这有点困难，因为为了适应书宽，代码分布在多行，但这段代码实际上相当于：
```
$('#DemoTable tr').bind('mouseover', ...).bind('mouseout', ...);
```
这段代码做了三件事：首先，它使用 `$('#DemoTable tr')` 找到表格中的所有行。对返回的匹配集合调用了 `bind`，以便在鼠标悬过某行时动态挂钩行为。然后在匹配集合上再次调用 `bind`，以便在鼠标移出该行时重置背景颜色。注意我是如何将颜色设置为空字符串（''`）来移除 CSS 属性，这样你就能看到原始的背景颜色。

在这个示例中还有一点需要注意的，那就是背景颜色是如何设置的：
```
$(this).css('background-color', 'yellow')
```
示例中的关键字 `this` 指向应用该项目的元素：在此情况下是表格行。使用 `$(this)` 会给你一个 jQuery 集合（包含单个元素），你可以对其应用如 `css` 这样的普通 jQuery 方法。你也可以不使用 jQuery 而对该元素执行标准的 JavaScript：
```
this.style.backgroundColor = 'yellow'
```
