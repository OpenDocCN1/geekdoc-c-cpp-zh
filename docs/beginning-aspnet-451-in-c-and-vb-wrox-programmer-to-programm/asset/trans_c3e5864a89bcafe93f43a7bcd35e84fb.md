

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

表格行（以及许多其他 HTML 元素）有一个 `style` 属性，允许你通过编程更改 CSS。你可能希望使用 `style.background-color` 来更改颜色，但 JavaScript 中不是这样运行的。在该语言中，连字符（-）不是有效的标识符。此外，原始连字符后的每个字母都是大写的。。因此，CSS 中的 `background-color` 在 JavaScript 中变为 `backgroundColor`，`font-family` 变为 `camelFamily`，依此类推。在尝试通过 JavaScript 和 jQuery 动态获取 CSS 信息时，请记住这些命名规则。

# jQuery 杂功能

在进入下一个主题“jQuery 效果”之前，你需要了解 jQuery 中的几个重要函数。首先是 `each`：

`each` 方法对集合进行迭代（或循环）。如果你想对匹配集合应用某些无法通过单个 jQuery 函数设置的行为，这个方法非常棒。`each` 的一个参数是你提供的函数，该函数会在每个项目上执行。接接的 `each` 示例通过遍历匹配集合中的项目并调用 `alert`，弹出每个表格单元格的内容。再次，你可以在匹配的 `jQueryDemos.aspx` 页面中尝试这个：

另外两个重要方法包括 `parent` 和 `prev`。这些方法用于 DOM 遍历，你可以在文档树中“向上”或“向下”移动项目下方、上方或同一层级的元素。
`prev` 方法选择匹配元素的直接相邻元素。要查看它是如何工作的，请看这个：

```
alert($('#DemoTable td:contains("Row 1 Cell 2").prev()[0].innerHTML);
```

你认为这个弹出会显示什么？如果你猜是“Row 1 Cell 1”，那么你对了。`:contains` 选择器根据其包含的文本选择该行第二列的单元格。`prev` 方法返回它的第一个兄弟元素：即左侧的单元格。即使匹配集合只包含一个项目，它也是集合，你仍然需要使用索引如 `[0]` 来引用该项目。
表格单元格随后有一个 `.innerHTML` 属性，返回单元格的内容。

最后，看看 `parent`：
```
alert($('#DemoTable td:contains("Row 1 Cell 2").parent()[0].innerHTML);
```

如果你在演示页面中运行此代码，将得到如图 11-5 所示的结果。

如果你没有看到完全相同的 HTML，请确保以 `alert` 开头的该行是你的 `document ready` 函数内部唯一的行，因为其他示例可能会影响表格的 HTML。

选择器与上一个示例相同。`parent` 函数指向匹配单元格周围的 `<tr>`。弹出 `innerHTML` 会返回该行包含的两个单元格的 HTML。

![](img/9e033e3b9560597824f8b22941d6d8bb_429_0.png)

# 使用 jQuery 常见错误

根据你所使用的 jQuery 功能的复杂性，编写代码可能相当挑战性。你需要注意正确的大小写、括号、括号、逗号等。当你发现 jQuery 代码未运行或出现意料之外的行为时，检查你的代码是否存在以下问题。

# 你的 ID 选择器不起作用

你可能忘记在它前面包含 `#` 符号。`$('DemoTable')` 不会选择 ID 为 `DemoTable` 的表格，而 `$('#DemoTable')` 则会选择。另一种你的 ID 选择器可能不起作用的情况是你写错了大小写。ID 选择器是敏感的，所以 `$('#DemoTable')` 不等于 `('#Demotable')`（注：此处原文可能有误）。

# 即使有井号符号，你的 ID 选择器不起作用

在这种情况下，很可能是客户端元素没有你预期的 ID。也许 ASP.NET 运行时通过在其父元素的 ID 前缀更改了客户端 ID？在这种情况下，尝试将相关控件的 `ClientID` 设置为 `Static`，使其更具可预测性。此外，确保你的代码在 `document ready` 函数内部执行，因为你的目标元素可能尚未可用。

# 你的代码似乎没有运行

检查你的圆括号、大括号和引号。每一对都需要平衡，开启项和结束项的数量相等。

到为止，你解决的问题大多集中在查找页面中的元素以及通过 CSS 更改其外观或执行 JavaScript。然而，jQuery 还带有一系列让页面元素产生动画的技巧。在下一节中，你将看到这些所谓的效果，随后是一个展示它们运行情况的“尝试”练习。

# jQuery 效果

在本章较早的示例中，你看到了 `showUp` 和 `slideDown` 来隐藏和显示元素。但这些只是 jQuery 提供的许多效果和动画方法中的两种。下表列出了你可以使用的最常用的方法。建议使用 `jQueryDemos.aspx` 页面尝试所有示例。

| 方法名称 | 目的 |
| :--- | :--- |
| `show()` | 通过减少高度、宽度和透明度（使其透明）来隐藏或显示匹配元素。两种方法都允许你定义固定速度（slow, normal, fast）或定义以毫秒为单位的数字。 |
| `toggle()` | `toggle` 方法在匹配元素的显示和隐藏之间切换。也就是说，如果它们可见的，就隐藏它们；如果是隐藏的，就显示它们。示例：<br> `$('element').toggle();` |
| `slideDown()` | 与 `hide` 和 `show` 一样，这些方法让匹配元素出现或消失。然而，它们是通过调整高度从当前大小变为零（或反之）来实现。示例：<br> `$('element').slideDown(1000);` |
| `slideUp()` | `slideToggle` 方法让元素向下和向上滑动，这使得通过一个操作即可显示和隐藏元素。示例：<br> `$('element').slideToggle(1000);` |
| `fadeIn()` | 这些方法通过改变透明度让匹配元素可见或不可见。`fadeOut` 将透明度设置为 0，使项目透明，然后将 CSS `display` 设置为 `none`，完全隐藏项目。`fadeTo` 允许你指定一个透明度（0 到 1 之间的数字）来确定元素的透明级别，`fadeIn` 让项目再次出现并将透明度设置为 1。所有三种方法都允许你定义固定速度（slow, normal, fast）或定义以毫秒为单位的动画持续时间。示例：<br> `$('element').fadeOut(1000);` // 1 秒内淡出 <br> `$('element').fadeIn(1000);` // 1 秒内出现 <br> `$('element').fadeOut(1000, 0.5);` // 淡出到半透明 |
| `animate()` | 在内部，`animate` 用于许多动画方法，如 `show` 和 `hide`。然而，它在外部可用，为你动画元素提供极大的灵活性。通过 `animate` 方法，你可以指定一组要动画的属性。考虑这个示例：<br> `$('element').animate({ opacity: 0.4, marginLeft: '50px', fontSize: '50px' }, 1500);` `animate` 方法的第一个参数是一个包含一个或多个你想要动画的属性的对象，每个属性之间用逗号分隔。注意你需要使用 JavaScript 的 `marginLeft` 和 `fontSize`，而不是 CSS 的 `margin-left` 和 `fontSize` 属性。你只能对取数值的属性进行动画。也就是说，你可以使用 `margin`、`fontSize`、`opacity` 等属性，但不能使用 `color` 或 `fontFamily` 等属性。 |

