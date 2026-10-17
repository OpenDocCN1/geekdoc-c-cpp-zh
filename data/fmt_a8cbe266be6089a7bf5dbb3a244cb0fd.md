
```csharp
protected void TextBox1_TextChanged(object sender, EventArgs e)
{
    Label.Text = "This text is different from before";
}
```

如果你在选中 `TextBox` 时查看 Visual Studio 中的属性面板（Properties pane），你将看到 `TextBox` 可用的事件以及你挂钩的事件（参见图 D-2）。

你应该出于以下两个原因考虑 Web Forms 为你做了什么工作：

- 如果是由 Web Forms 自动处理的，那么它在 ASP.NET MVC 中就不会自动处理。
- 你将知道自己错过了什么。你在工作很可能再次需要 Web Forms，并且在构建混合应用程序时，你会感激这些抽象。

### 附录 D：ASP.NET 优于 ASP.NET MVC

属性

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1757_0.png)

图-2

让我们来看看在底层发生了什么以触发 `TextChanged` 事件，并讨论为什么这是如此不寻常。

当列表 D-1 中的页面被渲染时，生成的 HTML 稍微复杂一些，包含了我们在布局页面并未显式创建的字段和标记。

```html
<HEAD><TITLE>Untitled Page</TITLE></HEAD>
<BODY>
<FORM id=form1 name=form action=default.aspx method=post>
<DIV>
<INPUT id="__VIEWSTATE" type=hidden value="wEPDWuJN3gJcmwMjqZGQGO=$.." name="__VIEWSTATE">
</DIV>
<DIV>
<INPUT id=TextBox value="Initial Text" name=TextBox> <INPUT id=Button type=submit value=Button1> <P><span id=Label1></span></P>
</DIV>
<DIV><INPUT id=__VALIDATION type=hidden value="/EWAWkMgKc6QB50lBrBgZm5rGg==" name=__VALIDATION/></FORM></BODY>
```

HTML 的三个方面是 ASP.NET Web Forms 特有的：

- 注意 `<form>` 将“回传”（post back）到 `default.aspx`，而不是另一个页面。虽然 ASP.NET Web Forms 支持跨页面回传的概念，但绝大多数 ASP.NET Web forms 回传到服务器，通过页面向用户交付更改，并启用视图状态（view state）的概念。
- 页面上有一块 `ViewState`，你可以看到它被渲染在一个输入控件中。此时，ASP.NET 并没有维护服务器端状态；`ViewState` 维护的是渲染后的视图。
- 还有另一个名为 `EventValidation` 的隐藏输入控件。这是 ASP.NET 2.0 中添加的功能，用于检查传入的 `POST` 值的有效性。它是可能值的哈希值，旨在防止攻击。

### 附录 D：ASP.NET 优于 ASP.NET MVC

对于一个简单的页面来说，这里有大量的基础设施在运行。然而，请记住 ASP.NET Web Forms 的源头。它正试图抽象掉 HTTP 和大部分 HTML，并提供一个用于处理页面的控制模型，因此它提供了许多复杂的机制来减轻开发者的负担。

### 事件的重要性

Web Forms 最意义的方面是这样一种想法：你的页面将有一个生命周期，并预期事件会被触发，但在这种情况下，ASP.NET 在并不知道 `TextBox` 初始状态的情况下告诉你是某些文本已更改。`TextBox` 控制它自己的状态，它不在服务器上，而是在客户端。这是巨大的。为什么在客户端？因为服务器没有办法知道你是何时将内容交付给浏览器的（如果它曾被提交的话）。你完全可以尝试在服务器上保存状态，但能保持多久呢？如果状态很大，`ViewState` 就派上用场了。初始视图被序列化并固定在你刚刚交付的页面中。当页面被提交时，它会返回到服务器。

## 附录 D：ASP.NET 优于 ASP.NET MVC

客户端。除非你对控制所有的 HTML 标签感兴趣，否则你可以在 Visual Studio 的富节点设计界面上拖放第三方控件，并使用智能标签（SmartTags）和向导与它们进行交互。

## ViewState（视图状态）

`ViewState` 非常强大，但也有它的缺点。由于 `ViewState` 是默认开启的，有时你的 Web Forms 产生的 `ViewState` 会比需要的多。对于复杂的页面和某些控件（例如 `DataGrid`），这会变成一个真正的问题，这些控件虽然异常强大，但极度依赖 `ViewState` 才能发挥功能。

如果你不需要 `TextBox` 抛出 `Changed` 事件，你可以只关闭该控件的 `ViewState`。遗憾的是，开发者很少会针对 `ViewState` 的大小来优化页面，而是选择对默认设置下的臃肿表示抱怨。

## 控制你的尖括号（HTML 标签）

虽然 ASP.NET Web Forms 提供了一套复杂的控件适配器（Control Adapter）模型，允许开发者更改控件渲染自身的方式，但一直有人说，这种抽象对某些开发者来说太复杂。“为什么这些控件就不能让我省心呢？”这句话促使了基于模板的控件开发，例如新的 ASP.NET 3.5 `ListView`。然而，尽管 ASP.NET 取得了一些进展，但在使用 Web Forms 时，你无法对 HTML 拥有绝对控制权。

不同的控件以不同的方式渲染它们的 HTML，当你在这个过程中引入第三方控件时，你可能会感到失望，因为 A 公司的小部件生成的 HTML 标记与公司 B 的有显著差异，导致结果无法协同工作。

## Client IDs（客户端 ID）

ASP.NET 中的某些服务器端控件是命名控制控件，并实现了 `INamingContainer` 接口。该接口的存在是为了让控件为它们的子控件提供这些唯一的命名范围。目标是让这些控件具有唯一的 ID，以免与页面上的其他控件发生冲突。在你的页面变得如此复杂并开始生成如下控件名称之前，这听起来是个好主意：

```
ct100$ContentPlaceholder1$UserControl$TextBox
```
