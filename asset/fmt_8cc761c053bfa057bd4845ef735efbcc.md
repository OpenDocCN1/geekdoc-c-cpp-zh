
控件在页面标记部分中的定义现在与实际定义文本框中显示的文本的控件分离，使得定义和编程文本框（或其他任何控件）变得更容易，因为它允许你一次专注于其中一个。你可以在页面的标记部分声明控件及其视觉外观，或从代码块编程其行为。

通常，在标记视图中定义的控件不区分大小写，尽管你可以设置的一些值是区分大小写的。我更喜欢使用 IntelliSense 建议的大写形式。请注意，使用 C#，代码隐藏中使用的属性是区分大小写的。

你将在下一个练习中看到服务器控件如何向客户端发送其底层 HTML。

### 试用 使用服务器控件

在此练习中，你向页面添加一个 `TextBox`、`Label` 和一个 `Button` 控件。当你刷新浏览器时，这些服务器控件将被转换为发送到客户端的 HTML。通过查看浏览器中页面的最终 HTML，你会看到 HTML 与初始 ASP.NET 标记完全不同。

- 1. 在 `Visual Studio` 中打开 `Panel` 项目。
- 2. 在解决方案资源管理器的 `Demos` 文件夹中，创建一个名为 `Demo.aspx` 的新 Web 窗体。选择你的编程语言并确保 Web 窗体使用代码隐藏。
- 3. 切换到设计视图。从工具箱的标准类别中，将 `TextBox`、`Button` 和 `Label` 控件拖到设计表面上，位于为你创建页面时添加的 `<div>` 标签的虚线内。

在 `TextBox` 前面输入 `Your name` 并在 `Button` 和 `Label` 之间添加一行，通过在设计视图中将光标定位在控件之间并按下它们来操作。如果你在控件上定位光标时遇到困难，请将光标放在 `Label` 控件之后，然后按左箭头键。第一次按下时，`Label` 会被选中；第二次按下，即可将光标放置在控件之间。你的设计视图现在应如下图 4-1 所示。

右键单击 `Button` 并选择 `Properties` 以打开属性网格。选中 `Button` 后按 `F4` 也能达到相同效果。窗口如图所示，如图 4-2 所示，可让你更改控件的属性，进而更改其在运行时时的外观和行为。

- 5. 将控件的属性设置为 `Submit Information` 并将其 `ID` 设置为 `SubmitButton`，该 `ID` 将一直找到列表底部并用括号括起来。
- 6. 使用属性网格将 `TextBox` 的 `ID` 改为 `YourName`。
- 7. 使用属性网格清除 `Label` 的属性。你可以在网格中右键单击属性的标签并选择 `Reset`，或者手动删除文本。将其 `ID` 设置为 `Result`。
- 8. 仍在设计视图中，双击 `Button` 控件以让 VS 在页面的代码隐藏中添加一些代码，该代码将在浏览器中单击 `Button` 时触发。你稍后会看到如何通过标记视图来实现这一点。将粗体代码行添加到插入的代码块中：

#### VB.NET

```
Protected Sub SubmitButton_Click(sender As Object,
 e As EventArgs) Handles SubmitButton.Click
Result.Text = "Your name is *" & & YourName.Text;
End Sub
```

#### C#

```
protected void SubmitButton_Click(object sender, EventArgs args)
{
Result.Text = "Your name is *" + YourName.Text;
}
```

请注意，VB.NET 示例中在此处不需要下划线来将代码拆分为两行。在旧版本的 VB.NET 中，下划线是必需的才能将代码拆分为两行。

![](img/9e033e3b9560597824f8b22941d6d8bb_141_0.png)

FIGURE 4-1

![](img/9e033e3b9560597824f8b22941d6d8bb_141_1.png)

FIGURE 4-2

9. 保存对页面的更改并通过按 `Ctrl+F5` 在浏览器中打开它。不要单击按钮，但通过在浏览器中右键单击页面并选择 `View Source` 或 `View Page Source` 来打开页面的源代码。你应该会看到以下 HTML 代码：

```
<div>
Your name <input name="YourName" type="text" id="YourName" />
<input type="submit" name="SubmitButton" value="Submit Information"
id="SubmitButton" />
<br />
<span id="Result">/</span>
</div>
```

10. 切回浏览器，填写姓名文本，然后单击按钮。页面重新加载完成后，使用右键菜单在浏览器中打开页面的源代码。代码现在应如下所示：

```
<div>
Your name <input name="YourName" type="text" value="Imar" id="YourName" />
<input type="submit" name="SubmitButton" value="Submit Information"
id="SubmitButton" />
<br />
<span id="Result">Your name is Imar/</span>
</div>
```

请注意，这两行已更改，现在显示你在文本框中输入的名称。你可以忽略页面的其他 HTML。

## How It Works

如其名所示，ASP.NET 服务器控件驻留在 ASPX 页面上的服务器上，可由 ASP.NET 运行时处理。当你在浏览器中请求页面时，运行时会创建 ASPX 文件的内存表示形式，其中包含你创建的控件。当运行时即将向浏览器发送 HTML 时，它会询问页面中的每个控件其 HTML，该 HTML 会注入到最终响应中。例如，当 `Label` 控件第一次加载时被要求提供其 HTML 时，它返回：

```
<span id="Result">/</span>
```

尽管你使用 `<asp:Label>` 语法定义了 `Label` 控件

当你单击按钮时，控件会触发回发，将页面中控件的信息发送到服务器，在服务器上加载页面。此外，你编写的处理按钮 `Click` 事件的代码也会执行。此代码获取你在文本框中输入的名称并将其分配给 `Label` 控件，如此 C# 示例所示：

```
Result.Text = "Your name is " + YourName.Text;
```

现在不必担心处理 `Click` 事件的代码的语法。在第 5 章中，你将看到这是如何工作的，以及为什么需要此代码。

此时，`Label` 控件包含你在文本框中输入的文本，因此当被要求提供 HTML 时，它现在返回：
```
<span id="Result">Your name is Imar</span>
```

在本章后面讨论 ASP.NET 状态引擎时，你将更深入地了解回发。

## A CLOSER LOOK AT ASP.NET SERVER CONTROLS

由于在构建 ASP.NET Web Forms 页面时大部分时间都在使用服务器控件，因此你需要了解它们的工作细节以及如何使用它们。在下一节中，你将看到如何将控件添加到页面并更改它们在浏览器中的行为。在其后的部分中，你将了解所有服务器控件共有的行为概述。一旦你理解了这种行为，就很容易将这种知识应用到其他新控件，从而能非常快速地掌握它们。

## Defining Controls in Your Pages

如 Try Out 所演示的那样，你可以简单地从工具箱将控件拖到页面的设计表面上。这使得开始时可以轻松地向页面添加一堆控件。然而，由于设计表面的工作方式，很难找到确切想要放置的位置。例如，很难将控件拖到 HTML 元素的开始和结束标签之间。幸运的是，你也可以在标记视图中输入控件的标记，让 IntelliSense 和代码片段帮助你处理不同的标签和属性。你还会发现属性网格在标记视图中也能工作。只需单击标记，属性网格就会更新以反映你单击的标签。这使得在可以看到为你生成的确切标记的同时，更改控件的属性变得容易。`Visual Studio` 允许你直接在标记视图中绑定处理程序（如前练习中使用的 `Click` 事件），而无需切换到设计视图。你还将能够从代码访问控件的 Smart Tasks 面板。本章后面会介绍更多这些功能。

如果你查看页面中某些控件的属性网格，你会注意到其中许多控件具有相似的属性。在下一节中，你将确切地看到这些属性是什么以及它们用于什么。

### Common Properties for All Controls

你在 VS 工具箱中找到的大多数服务器控件共享一些通用行为。这种行为的一部分包括所谓的属性，这些属性定义控件可以包含和公开的内容。你将在下一章了解有关属性和其他行为类型的更多信息。每个服务器控件都有一个 `ID`，用于在页面中唯一标识它，一个 `runat` 属性，始终设置为 `server` 以指示控件应在服务器上处理，以及一个 `ClientID`，其中包含分配给最终 HTML 中元素的客户端 ID 属性。在 ASP.NET 3.5 及更早版本中，此 `ClientID` 始终由你自动生成。然而，在 ASP.NET 4 中引入了新的 `ClientMode` 属性，它使你能够更好地控制客户端元素的 ID。你将在后面的章节中看到这是如何工作的。`runat` 属性在技术上不是服务器控件的属性，但对于标识控件的标记应作为服务器控件处理而不是作为纯文本或 HTML 结束在浏览器中是必要的。

除了这些属性之外，许多服务器控件还共享更多属性，因为它们共享相同的 `Control` 基类。下一章将更深入地介绍基类和继承。下面的表格列出了最常见的共享属性并描述了它们的使用方式。

| PROPERTY | DESCRIPTION |
| --- | --- |
| AccessKey | 使你能够设置一个键，通过按下键盘上的关联键可在客户端访问控件。 |
| BackColor ForeColor | 使你能够更改控件在浏览器中的背景颜色（BackColor）和文本颜色（ForeColor）。 |
| BorderRadius BorderWidth | 在浏览器中更改控件的边框。与你在上一章中看到的 CSS 边框属性的相似性并非巧合。这三个 ASP.NET 属性中的每一个都直接映射到其 CSS 对应项。 |
| CssClass | 使你能够为浏览器中的控件定义 HTML class 属性。此类名称然后指向你在页面或外部 CSS 文件中定义的 CSS 类。 |
| Enabled | 确定用户是否可以在浏览器中与控件交互。例如，对于禁用的文本框（Enabled="False"），你无法更改其文本。 |
| Font | 使你能够定义不同的字体相关设置，例如大小、族以及字体是否应为粗体 |
| Height Width | 确定控件在浏览器中的高度和宽度。 |
| TabIndex | 设置客户端 HTML tabindex 属性，该属性确定用户通过按 Tab 键在页面中移动控件的顺序。 |
| ToolTip | 使你能够为浏览器中的控件设置工具提示。此工具提示以 HTML 中的 title 属性呈现，当用户将鼠标悬停在元素上时显示。 |
| Visible | 确定控件是否发送到浏览器。你应该将其真正视为服务器端可见性设置，因为不可见的控件根本不会发送到浏览器。这意味着它与你在上一章中看到的 CSS display 和 visibility 属性有很大不同，后者会在客户端隐藏元素。 |

## 第4章 使用 ASP.NET 服务器控件

要查看这些属性在浏览器中如何显示，请考虑以下 `TextBox` 服务器控件的标记：

```
<asp:TextBox AccessKey="a" BackColor="Black" ForeColor="White" Font-Size="30px"
BorderColor="Yellow" Border="Dashed" BorderWidth="4" CssClass="TextBox"
Enabled="True" Height="40px" Width="90px" TabIndex="1" ToolTip="Hover text here"
Visible="True" ID="TextBox" runat="server" Text="Hello World">
</asp:TextBox>
```

当你在浏览器中请求此页面时，你将得到以下 HTML：

```
<input name="TextBox" type="text" value="Hello World" id="TextBox1"
tabindex="1" title="Hover text here" class="TextBox" style="color:White;
background-color:Black;border-color:yellow;border-width:4px;
border-style:Dashed;font-size:30px;height:40px;width:200px;">
```

这会产生图 4-3 中显示的文本。

注意服务器端控件属性如何被转换为内联样式并与 style 属性一起使用。

在构建网站时，以这种方式定义 `TextBox` 并不常见。正如你在上一章中学到的那样，你应该尽可能避免内联样式，而选择级联样式表。可以使用以下服务器端控件实现相同的效果：

```
<asp:TextBox ID="TextBox1" AccessKey="a" CssClass="TextBox" TabIndex="1"
ToolTip="Hover text here" runat="server" Text="Hello World">
</asp:TextBox>
```

以及以下 CSS：

```
.TextBox {
background-color: Black;
color: White;
font-size: 30px;
border-color: Yellow;
border-style: Dashed;
border-width: 4px;
height: 40px;
}
```

显然，第二种示例更容易阅读、重用和维护。如果你想要另一个外观完全相同的文本，只需将其 `CssClass` 分配给 `TextBox` 即可。另外，请注意我使用了 `Enabled` 和 `Visible` 属性。两者默认都为 True，因此在控件声明中无需显式声明。

尽管建议使用 CSS 类而不是这些内联样式，但了解服务器端控件属性的工作原理仍然是好的，以防你需要控制它们。如果你以编程方式更改控件的属性（如你将学习的那样），它们仍然会作为样式结束，从而可能覆盖嵌入式或外部样式表中的设置。

![](img/9e033e3b9560597824f8b22941d6d8bb_145_0.png)

图 4-3

## 控件类型

现在你已经看到了所有服务器控件共享的通用行为，是时候查看随 ASP .NET 一起提供的众多控件了。

开箱即用，ASP.NET 4.5.1 附带了大量控件，支持你大部分的 Web 开发需求。为了便于你找到合适的控件，它们已在 VS 工具箱中按控件类别进行了分类（通过按 `Ctrl+Alt+X` 可访问）。图 4-4 显示了工具箱中所有可用的类别。

请注意，根据你的 Visual Studio 版本，工具箱可能还有其他类别。

VS 中的一个便捷功能是在工具箱中搜索。只需在工具箱顶部的搜索框中输入你要查找的控件的几个字母，VS 就会过滤出匹配你条件的列表。

在下面的各节中，你将看到每个类别中的控件以及它们的设计用途。

在讨论各种控件时，你会看到对控件属性的提及。例如，`TextBox` 有一个 `Text` 属性（还有许多其他属性），`ListBox` 有一个 `SelectedIndex` 属性。属性只能以编程方式设置，而不能使用属性网格。有关以编程方式读取和更改控件属性的讨论将在下一章详细讨论。

## 标准控件

标准类别包含几乎任何页面都需要的大多数基本控件。你在本章前面已经见过其中的一些，例如 `TextBox`、`Button` 和 `Label` 控件。图 4-5 显示了标准类别中的所有控件。

其中许多控件不言自明，为了详细描述所有控件，以下各节简要重点介绍了其中一些重要的控件。

### 简单控件

工具箱包含许多简单直接的控件，包括 `TextBox`、`Button`、`Label`、`HyperLink`、`RadioButton` 和 `CheckBox`。它们在工具箱中的图标很好地提示了它们在浏览器中的呈现方式。在本书的其余部分中，你将多次看到这些控件的使用。在 ASP.NET 4.5 中，`TextBox` 控件的 `Text` 模式已扩展以支持新的 HTML5 类型，如 `DateTime`、`Email` 和 `Number`。你将在本书后面看到更多相关内容。

![](img/9e033e3b9560597824f8b22941d6d8bb_146_0.png)

图 4-4

![](img/9e033e3b9560597824f8b22941d6d8bb_146_1.png)

图 4-5

### 列表控件

```
<asp:DropDownList ID="FavoriteLanguage" runat="server">
<asp:ListItem Value="C#">C#</asp:ListItem>
<asp:ListItem Value="Visual Basic">Visual Basic</asp:ListItem>
<asp:ListItem Value="CSS">CSS</asp:ListItem>
</asp:DropDownList>
```
