

增加其大小和加载时间。对于某些功能——例如跟踪客户端所做的更改——这些控件仍需要在按需的基础上将其值存储在 View State 中。

除了 View State，控件还支持 Control State 的概念。控件使用一种机制来跟踪它们绝对需要正确运行的数据。你无法禁用 Control State，但由于 Control State 中只存储了有限量的数据，因此这不是问题。

## 关于 View State 和性能的说明

由于 View State 引擎向页面添加了相当多的信息，因此在不需要时将其关闭通常是个好主意。这样，你可以最小化隐藏的 _VIEWSTATE 字段的大小，这意味着页面更小，在浏览器中加载更快。请注意，当你关闭 View State 时，你仍然会看到隐藏的 _VIEWSTATE 字段，因为 Control State 使用相同的字段来存储其数据。关闭 View State 很简单，你可以在三个不同的位置进行操作：

- 在 Web 级别 — 你可以在站点根目录的 Web.config 文件中通过修改（或添加）<system.web> 下的 <pages> 元素，将 EnableViewState 属性设置为：
```xml
<pages enableViewState="false">
</pages>
```

- 在页面级别 — 在每个页面的顶部，你会找到页面指令，一系列指令，你可以将 EnableViewState 设置为 False：
```vb
<%@ Page Language="VB" AutoEventWireup="False" CodeFile="State.aspx.vb"
Inherits="Demos_State" EnableViewState="False" %>
```

这对于完全不需要 View State 的页面很有用。

- 在控件级别 — 每个 ASP.NET 服务器控件都允许你单独设置 EnableViewState，从而可以选择为某些控件关闭它，而保留其他控件。

一旦你在更高级别（页面或控件级别）关闭了 View State，在更低级别将 EnableViewState 设置为 True 就没有效果了。但是，使用 ViewStateMode 属性你可以按如下方式实现：

- 不要在 Web.config 文件中关闭 View State。
- 在页面级别，将 EnableViewState 设置为 True 并将 ViewStateMode 设置为 Disabled，如下所示：
```vb
<%@ Page Language="C#" EnableViewState="True" ViewStateMode="Disabled" %>
```
这会关闭页面中所有控件的 View State，除了那些通过将 ViewStateMode 设置为 Enabled 来明确启用它的控件。

## 关于使用控件的实用技巧

对于你想要提供 View State 支持的控件，ViewStateMode=Enabled，如下所示：

```
<asp:Label ID="Label1" runat="server" Text="Label" ViewStateMode="Enabled" />
```

如果你想在演示页面中看到这一点，请修改上一个示例中 State.aspx 的指令，将 EnableViewState 设置为 True 并将 ViewStateMode 设置为 Disabled。在页面中创建一个第二个标签并为已启用的标签设置 ViewStateMode：

```
<asp:Label ID="Label1" runat="server" Text="Label" ViewStateMode="Enabled" />
<asp:Label ID="Label2" runat="server" Text="Label" />
```

在 Code-Behind 中，将两个页面的文本设置为今天并设置为第二个标签为：

### VB.NET

```
Label1.Text = DateTime.Now.ToString()
Label2.Text = DateTime.Now.ToString()
```

### C#

```
Label1.Text = DateTime.Now.ToString();
Label2.Text = DateTime.Now.ToString();
```

最后，运行上一个 Try Out 练习的步骤 10 和 11。你会注意到第一个 Label 保持其文本，第二个标签恢复为默认的 Label。

## 关于使用控件的实用技巧

以下列表提供了使用控件的一些实用技巧：

- 花一些时间尝试标准类别中的不同控件。其中许多控件在整本书中都被使用和讨论，了解你应该如何使用它们以及它们如何操作是很有好处的。通过现在在几个示例页面中试验它们，你将在后续章节中再次出现控件时抢占先机。

- 考虑为不需要的控件关闭 View State。在许多情况下，特别是第 13 章及以后讨论的数据驱动控件，禁用 View State 可以显著减小网页的大小，从而缩短加载时间并改善用户体验。

- 在设计一个包含多个控件以接受用户输入的复杂 Web 表单之前，退一步离开电脑，拿出一张纸和一支笔来绘制所需的功能。通过在开始编码之前思考应用程序的（技术）设计，更容易创建一致且深思熟虑的用户界面。如果走错了路，在页面上进行重大更改总是比第一次就（几乎）做对要花费更多时间。

- 尝试 View State 机制以更好地了解其工作原理。创建几个与上次创建的类似的页面。在页面或控件级别关闭 View State，看看页面的行为如何。注意 TextBox 等控件，即使在关闭 View State 的情况下也能保持其值。

## 摘要

本章让你很好地了解了 ASP.NET 服务器控件的大量集合。由于这些控件很重要并且在每个 ASP.NET 应用程序中都使用，了解工具箱中有哪些控件、它们用于什么、它们如何工作以及它们如何维护自己的状态至关重要。

ASP.NET 中最大的发明之一是状态引擎，它使控件能够在回发后保持其状态。状态引擎可以节省大量时间，使你不必在每个网页中编写大量乏味和无聊的代码来复制这种行为。然而，你应该在可能的情况下关闭状态以提高性能。

本章还向你介绍了 Visual Basic 和 C# 中的一些服务器端代码。下一章将让你更好地理解 ASP.NET 页面的编程。你将看到编程语言如何工作，它包含哪些元素，以及如何编写代码以在 ASP.NET 页面中使用。最重要的是，示例以 Visual Basic 和 C# 呈现，因此你不必使用你可能不喜欢的语言。

## 练习

- 1. 使服务器控件能够维护其状态的机制的名称是什么。

- 2. ASP.NET 运行时如何能够在回发之间跟踪控件状态？

- 3. 命名 <asp:DropDownList> 和 <asp:ListBox> 之间的一个区别。

- 4. 当你在浏览器中更改 CheckBox 的选中状态时，需要什么属性才能导致向服务器回发？

- 5. 许多服务器控件有一组共同的属性，影响它们在运行时的外观。命名三个改变样式元素如颜色、边框和大小的属性。

- 6. 而不是设置单个控件属性如 BackColor 和 Foreground，最好设置一个单一的 CSS 相关属性。这个属性的名称是什么，它给你什么好处？

你可以在附录 A 中找到这些练习的答案。

## 本章你学到了什么

| __VIEWSTATE | 用于将状态从服务器传输到客户端并返回的隐藏表单字段。 |
| Container controls | 作为容器服务的服务器控件，通过包装其他内容和控件。 |
| Events tab | 属性网格的一部分，让你为控件事件（如 Button 的 Click）设置。 |
| List controls | 向用户呈现项目列表的服务器控件，例如 DropdownList、CheckboxList 等。 |
| POST and GET methods | 将数据从客户端提交到服务器的不同方法。使用 POST 数据添加到请求的主体中，而使用 GET 数据附加到请求的页面地址。 |
| Postback | 将数据从客户端浏览器发送回服务器的过程。 |
| Server Controls | ASP.NET 的主力，用于在浏览器中构建网页的用户界面。 |
| Smart Tasks panel | 为某些控件出现的动作面板，帮助你完成常见任务。 |
| View State | 使 ASP.NET 控件能够在客户端存储状态的机制。 |

