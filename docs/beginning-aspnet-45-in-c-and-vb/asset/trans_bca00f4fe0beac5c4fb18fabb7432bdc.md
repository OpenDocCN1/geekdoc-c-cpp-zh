
在 VS 中创建的新页面（或你在第 6 章中学到的母版页）已包含 `<form>` 元素，因此你无需自行添加。最后，重要的是要理解 ASP.NET Web Form 默认情况下始终提交回自身。在其他 Web 环境中，如经典 ASP 和 PHP，设置页面的 `action` 属性指向另一个处理用户提交数据的页面是很常见的。然而，对于 ASP.NET 页面，你会发现即使在代码中显式设置 `action` 属性，ASP.NET 运行时也会将其还原为当前页面的名称。

> **注意** ASP.NET 支持一项称为跨页回发的功能，可让你从一个页面提交到另一个页面。要了解更多关于此概念的信息，请在 MSDN 网站上搜索 Cross Page Postbacks 或购买 Wrox 出版的 Professional ASP.NET 4.5 一书。

下一个要查看的是 ASP.NET 的 View State 功能，它使用隐藏的 `__VIEWSTATE` 字段实现，你可以在以下代码片段的 HTML 源中看到它以粗体显示：

```html
<form method="post" action="State.aspx" id="form1">
...
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="IXcrUZS1B9YmtdoSL5cn2+Vrx5oW3k2kAwoRXGsE3P0/W016/upieH7Nhtlfhyr99U0IRKmJyYk4PdH5B9ZRucaJ0xPkwCyR0NB1K3kidqR5eAVX86Dq0f1584e5B0f3F1P4O3Y+ZqD7q2pA==" />
</div>
```

虽然乍一看文本似乎只包含随机字符，但它实际上包含有用信息。为了保护存储在此字段中的信息，ASP.NET 已将前述字符串中的页面状态进行了转换。如果能够查看字段的值内部，你会发现 `Label1` 控件的值为当前日期和时间。

当你的 ASP.NET 页面加载时，ASP.NET 运行时会用有关页面的信息填充此隐藏字段。例如，当你通过单击 Set Date 按钮触发回发时，它会添加 `Label1` 控件的 `Text` 属性的值。同样，它还包含 `Calendar` 控件的所选日期。当页面随后通过回发提交回来时，此隐藏 `__VIEWSTATE` 字段中的值会随请求一起发送。然后，当 ASP.NET 在服务器上创建新页面时，`__VIEWSTATE` 字段中的信息会被读取并应用到页面中的控件。这样，像 `Label` 这样的控件即使在页面已回发到服务器后也能保持其文本。

不过 `TextBox` 不需要 View State。它能够保持其值，是因为浏览器在每次回发时都会将其提交到服务器。

重申一下，以下是前面 Try It Out 中发生的过程概述。

- 1. 你通过在 VS 中打开它在浏览器中请求了该页面。
- 2. 浏览器通过请求从服务器获取了该页面。
- 3. ASP.NET 运行时从磁盘读取页面，对其进行处理，并将生成的 HTML 发送到浏览器。此时，所有控件都被设置为页面标记中定义其默认值。例如，`Label` 控件的 `Text` 被设置为 `Label`。
- 4. 页面在浏览器中显示后，你单击了 Set Date 按钮。这导致向服务器回发。
- 5. 在服务器上，页面再次被重建，与第 3 步描述的首次加载时类似。此时，所有控件都包含其默认值。因此，Label1 控件的 Text 属性再次被设置为 Label。默认值设置后不久，运行时会为在 View State 中找到的控件覆盖这些默认值。然而，由于这是第一次回发，且 Label 控件的 Text 属性尚未更改，其值不存在于 View State 中。因此 Text 属性仅包含默认单词 Label。
- 6. 在处理同一请求的同时，ASP.NET 运行时执行了 SetDate_Click 中的代码。如你所见，此代码将 Label 控件的 Text 属性更改为当前日期和时间。ASP.NET 运行时检测到此更改并将该新值也存储在 View State 中，以便在后续回发中保持可用。
- 7. 接下来，你输入了一些文本并单击了 Plain Postback 按钮。与其他按钮一样，这也导致回发发生。页面再次构建，所有默认值都被设置。这再次意味着 Label1 控件的 Text 属性仅包含单词 Label。然而，在此之后不久，在同一处理周期中，ASP.NET 运行时会处理 View State，还原在隐藏的 __VIEWSTATE 字段中找到的控件值。在此示例中，它找到了带有当前日期和时间的 Text 属性，并再次将其分配给 Label 控件。由于 Plain Postback 按钮不再更改 Label 的文本，Text 属性不会更改；它包含来自上一次回发的日期和时间。TextBox 控件的 Text 属性由提交到服务器的值设置；也就是说，此控件不使用 View State 来维护其值。最后，整个页面被发送到浏览器，其中标签正确显示其先前的值。
- 8. 最后，你通过将 EnableViewState 设置为 False 关闭了 Label 和 TextBox 控件的 View State。关闭此设置后，ASP.NET 运行时不再跟踪 Label 控件。因此，当你单击 Plain Postback 按钮时，ASP.NET 运行时在 View State 中找不到有关标签的任何信息，最终导致标签显示其自己的默认文本：单词 Label。

## 并非所有控件都依赖 View State

你必须理解，并非所有控件始终都依赖 View State。一些控件能够维护自身的部分状态，正如你在前面的练习中看到的 TextBox 控件一样。这些控件包括但不限于 TextBox、CheckBox、RadioButton 和 DropDownList 控件。它们能够保持其值，是因为它们在浏览器中呈现为标准的 HTML 表单控件。例如，TextBox 服务器控件在浏览器中最终如下所示：

```
<input name="TextBox1" type="text" value="Initial Text" id="TextBox1" />
```

当包含此类 TextBox 的页面回发时，浏览器也会将控件的值发送回服务器。然后 ASP.NET 运行时只需查看该值即可再次预填充文本框，而无需从 View State 获取值。显然，这比也将值存储在 View State 中更高效。如果是这样，该值将被发送到服务器两次：一次在文本框中，一次在 View State 中。特别是对于大值，这可能会迅速增加页面的大小，从而增加其加载时间。对于某些功能——例如跟踪客户端所做的更改——这些控件仍需要在 View State 中存储其值，并且按需进行。

除 View State 外，控件还支持 Control State 概念。控件使用该机制来跟踪它们正确运行绝对需要的数据。你无法禁用 Control State，但由于 Control State 中只存储有限量的数据，因此这不是问题。

## 关于 View State 和性能的说明

由于 View State 引擎向页面添加了相当多的信息，因此在不需要时将其关闭通常是个好主意。这样，你可以最小化隐藏的 __VIEWSTATE 字段的大小，这意味着页面变得更小，从而在浏览器中加载更快。请注意，当你关闭 View State 时，你仍然会看到隐藏的 __VIEWSTATE 字段，因为 Control State 使用同一字段来存储其数据。关闭 View State 很简单，你可以在三个不同的位置执行此操作：

- 在网站级别——你可以在站点的根目录中的 Web.config 文件中通过修改 <system.web> 下的 <pages> 元素，将 enableViewState 属性设置为 false 来执行此操作：
- 在页面级别——在每个页面的顶部，你会找到页面指令，一系列指示 ASP.NET 运行时页面应如何行为的指令。在页面指令中你可以将 EnableViewState 设置为 False：
- 此选项适用于你确定完全不需要 View State 的页面。
- 在控件级别——每个 ASP.NET 服务器控件都允许你单独设置 EnableViewState，从而可以选择为某些控件关闭它，同时为其他控件保留开启状态。

```
<pages enableViewState="false">
...
</pages>
```

```
<%@ Page Language="VB" AutoEventWireup="False" CodeFile="State.aspx.vb"
Inherits="Demos__State" EnableViewState="False" %>
```

一旦你在更高级别（Web.config 或页面级别）关闭了 View State，在较低级别（页面或特定控件）再次将 EnableViewState 设置为 True 将不起作用。然而，使用 ViewStateMode 属性你仍可以按如下方式实现此目的：

- 不要在 Web.config 文件中关闭 View State。
- 在页面级别，将 EnableViewState 设置为 True 并将 ViewStateMode 设置为 Disabled 如下所示：

```
<%@ Page Language="C#" ... EnableViewState="True" ViewStateMode="Disabled" %>
```

这会为页面中的所有控件关闭 View State，除了那些通过将 ViewStateMode 设置为 Enabled 明确再次启用它的控件。
