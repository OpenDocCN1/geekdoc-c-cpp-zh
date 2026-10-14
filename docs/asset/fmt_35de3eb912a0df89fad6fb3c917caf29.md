
## 如何使用按钮、链接按钮和图像按钮

图 6-5 展示了三种按钮控件。这些控件仅在向用户显示的方式上有所不同。这由本图顶部显示的三个按钮所说明。如您所见，按钮在矩形区域内显示文本。链接按钮显示看起来像超链接的文本。而图像按钮显示图像。

本图还展示了所说明的三个按钮的 asp 标签。对于按钮和链接按钮，`Text`属性提供控件显示的文本。对于图像按钮，`ImageUrl`属性提供按钮上显示的图像的 URL 地址。在某些情况下，浏览器可能无法显示图像。因此，您还应编码 `AlternateText`属性，以便在浏览器无法显示图像时提供显示的文本。

当用户单击其中一个按钮控件时，ASP.NET 会引发两个事件：`Click`和`Command`。您可以在本图中看到按钮控件 `Click`事件的事件处理程序。请注意，此事件处理程序接收两个参数。`sender`参数表示被单击的控件。由于此参数的类型为`object`，如果您想访问控件的属性和方法，则需要将其转换为按钮控件。例如，如果您编写一个处理多个按钮的处理方法，您可能希望这样做。然后，您可以使用控件的`ID`属性来确定单击了哪个按钮。然而，更简单的方法是使用`Command`事件。您将在图 6-7 中了解如何使用此事件。

传递给`Click`事件的事件处理程序的第二个参数`e`包含特定于事件的信息。您最有可能使用此参数与图像按钮控件，以确定用户在图像上单击的位置。您将在下一图中了解更多相关信息。

当然，`Click`和`Command`事件处理程序仅在页面发布回自身时执行。但是，如果为`PostBackUrl`属性指定了值，则会执行并显示指定 URL 处的页面。这是您在第 3 章中了解的跨页发布功能。

顺便说一下，从本章及本书的这一点开始，图表通常会展示所使用的控件的 asp 元素。通过研究这些控件的代码，您可以快速了解其属性是如何设置的。请记住，通常您通过使用设计器将控件添加到表单，并通过使用属性窗口设置控件的属性。然后，aspx 文件中 asp 元素的代码会自动生成。

### 浏览器中的一个按钮、一个链接按钮和一个图像按钮

![](img/c024ccf88e28c30c07dd410d4342288f_236_0.png)

### 三个按钮的 asp 标签

```aspx
<asp:Button ID="btnAdd" runat="server" Text="Add to Cart"
    OnClick="btnAdd_Click" />

&nbsp;&nbsp;&nbsp;&nbsp;

<asp:LinkButton ID="lbtnCheckOut" runat="server"
    PostBackUrl="~/CheckOut1.aspx">Check Out</asp:LinkButton>

&nbsp;&nbsp;&nbsp;&nbsp;

<asp:ImageButton ID="ibtnCart" runat="server" AlternateText="Cart"
    ImageUrl="~/Images/Cart.gif" PostBackUrl="~/Cart.aspx" />
```

### 常用按钮属性

| Attribute | Description |
|---|---|
| `Text` | （仅 `Button` 和 `LinkButton` 控件）按钮显示的文本。对于 `LinkButton` 控件，文本可以作为开始和结束标签之间的内容编码，也可作为 `Text` 属性的值。 |
| `ImageUrl` | （仅 `ImageButton` 控件）按钮要显示的图像。 |
| `AlternateText` | （仅 `ImageButton` 控件）如果浏览器无法显示图像时要显示的文本。 |
| `CausesValidation` | 确定单击按钮时是否执行页面验证。默认值为 `True`。 |
| `CommandName` | 单击按钮时传递给 `Command` 事件的字符串值。 |
| `CommandArgument` | 单击按钮时传递给 `Command` 事件的字符串值。 |
| `PostBackUrl` | 当用户单击按钮时应请求的页面的 URL。 |

### 按钮控件 Click 事件的事件处理程序

```csharp
protected void btnAccept_Click(object sender, EventArgs e)
{
    this.AddInvoice();
    Response.Redirect("Confirmation.aspx");
}
```

### Description

- 当用户单击 *button*、*link button* 或 *image button* 时，`PostBackUrl` 属性指定的页面将被加载并执行。如果未包含此属性，则页面将回发到服务器并引发 `Click` 和 `Command` 事件。您可以为这两个事件中的一个或两个编码事件处理程序。
- 两个参数传递给 `Click` 事件处理程序：`sender` 和 `e`。`Sender` 是用户单击的控件，`e` 包含特定于事件的信息。您可以使用 `e` 参数与图像按钮控件一起确定用户在图像中单击的位置。有关更多信息，请参阅图 6-6。
- 有关为 `Command` 事件编码事件处理程序的信息，请参阅图 6-7。

*Figure 6-5 How to work with buttons, link buttons, and image buttons*

## 如何使用图像按钮控件的 `e` 参数

*of an image button control*

在某些情况下，当用户单击图像按钮时执行的处理将取决于用户在按钮内单击的位置。为说明这一点，请考虑图 6-6 顶部所示的图像按钮，它代表四个导航按钮。 （此图像使用标准图标表示 First (<<)、Previous (<)、Next (>) 和 Last (>>)）。此图像按钮可用于让用户在网站的某个部分中导航页面或在数据表的不同行之间导航。

要处理此类图像按钮，您可以使用传递给按钮`Click`事件处理程序的`e`参数的`X`和`Y`属性。这些属性指示用户单击的`x`和`y`坐标。此图中显示的事件处理程序说明了其工作原理。

在此示例中，使用`if`语句确定`X`属性的值。如果它在 0 到 23 之间，则表示用户单击了 << 图标。然后，事件处理程序执行`GoToFirstRow`方法。如果它在 24 到 47 之间，则表示用户单击了 < 图标，并执行`GoToPreviousRow`方法。如果它在 48 到 71 之间，则表示用户单击了 > 图标，并执行`GoToNextRow`方法。最后，如果它在 72 到 95 之间，则表示用户单击了 >> 图标，并执行`GoToLastRow`方法。请注意，在此示例中不需要检查`y`坐标。这是因为所有图标的`y`坐标范围相同。

### 用于图像按钮控件的图像

![](img/c024ccf88e28c30c07dd410d4342288f_238_0.png)

### 控件的 asp 标签

```aspx
<asp:ImageButton ID="ibtnNavigate" runat="server"
                 ImageUrl="~/Images/navbuttons.gif" Height="24px" Width="96px"
                 OnClick="ibtnNavigate_Click" />
```

### 控件 Click 事件的事件处理程序

```csharp
protected void ibtnNavigate_Click(object sender, ImageClickEventArgs e)
{
    if (e.X >= 0 && e.X <= 23)
        this.GoToFirstRow();
    else if (e.X >= 24 && e.X <= 47)
        this.GoToPreviousRow();
    else if (e.X >= 48 && e.X <= 71)
        this.GoToNextRow();
    else if (e.X >= 72 && e.X <= 95)
        this.GoToLastRow();
}
```

### ImageClickEventArgs 类的属性

| Property | Description |
|---|---|
| `x` | 表示用户单击图像按钮的 `x` 坐标的整数。 |
| `y` | 表示用户单击图像按钮的 `y` 坐标的整数。 |

### Description

- 当用户单击`ImageButton`控件时，ASP.NET 会调用控件的`Click`事件处理程序，并将用户单击图像的`x`和`y`坐标作为`e`参数的属性传递。
- 传递给图像按钮`Click`事件处理程序的`e`参数是`ImageClickEventArgs`对象。此对象包含属性，可让您检索用户在图像上单击的`x`和`y`坐标。您可以使用这些属性来确定执行的处理。

## 如何使用 `Command` 事件

图 6-7 显示了如何使用`Command`事件通过单个事件处理程序处理一组按钮控件。与`Click`事件一样，此事件接收`sender`参数和`e`参数。在此情况下，`e`参数表示`CommandEventArgs`对象。

`CommandEventArgs`类的两个属性显示在此图中。您可以使用这些属性获取控件的`CommandName`和`CommandArgument`属性。当您创建按钮控件时，可以将`CommandName`和`CommandArgument`属性设置为任何字符串值。然后，您可以在`Command`事件处理程序中检查它们，以确定应用程序在用户单击按钮时应如何响应。

此图中的示例说明了其工作原理。第一个示例显示了四个按钮控件的 asp 标签。请注意，为每个控件分配了不同的`CommandName`值。但是，相同的事件处理程序被命名为`OnCommand`属性上。那样，同一个事件处理程序将处理全部四个控件的`Command`事件。虽然您也可以为每个控件分配`CommandArgument`值，但在这里不是必需的。

第二个示例显示了一个处理全部四个控件的`Command`事件的事件处理程序。为此，它使用`switch`语句测试`e`参数的`CommandName`属性的值。由于此值指示单击的控件，因此可用于根据单击的按钮确定要调用哪个方法。这是另一种执行您在图 6-6 中看到的处理的方法，该处理使用了图像按钮控件。

### 使用 CommandName 属性的四个按钮控件

```aspx
<asp:Button ID="btnFirst" runat="server" Text="<<" Width="25px"
    CommandName="First" OnCommand="NavigationButtons_Command" />
<asp:Button ID="btnPrevious" runat="server" Text="<" Width="25px"
    CommandName="Previous" OnCommand="NavigationButtons_Command" />
<asp:Button ID="btnNext" runat="server" Text=">" Width="25px"
    CommandName="Next" OnCommand="NavigationButtons_Command" />
<asp:Button ID="btnLast" runat="server" Text=">>" Width="25px"
    CommandName="Last" OnCommand="NavigationButtons_Command" />
```

### 按钮的 Command 事件的事件处理程序

```csharp
protected void NavigationButtons_Command(object sender, CommandEventArgs e)
{
    switch (e.CommandName)
    {
        case "First":
            this.GoToFirstRow();
            break;
        case "Previous":
            this.GoToPreviousRow();
            break;
        case "Next":
            this.GoToNextRow();
            break;
        case "Last":
            this.GoToLastRow();
            break;
    }
}
```

### CommandEventArgs 类的属性

| Property | Description |
|---|---|
| `CommandName` | 为生成 `Command` 事件的控件的 `CommandName` 属性指定的值。 |
| `CommandArgument` | 为生成 `Command` 事件的控件的 `CommandArgument` 属性指定的值。 |

### Description

- 每当用户单击按钮控件时都会引发`Command`事件。当您希望为执行相关功能的按钮组编码单个事件处理程序时，它可用作`Click`事件的替代方案。
- 传递给`Command`事件处理程序的`e`参数是`CommandEventArgs`对象。此对象包含属性，可让您检索控件的`CommandName`和`CommandArgument`属性的值。您可以使用这些值来确定哪个控件引发了`Command`事件。

### Note

- 如果您为`Click`事件和`Command`事件都编码事件处理程序，则`Click`事件处理程序将先执行。

*Figure 6-7 How to use the Command event*

## 如何使用文本框、标签、复选框和单选按钮

在开发 Web 表单时，你会经常使用两种控件：文本框和标签。正如你所知，文本框让你可以接受用户的输入，而标签让你可以向用户显示信息。由于你已经掌握了使用这些控件的基本技能，下面介绍的主题将介绍一些额外的技能。之后，你将学习如何使用复选框和单选按钮让用户从一个或多个选项中进行选择。

### 如何使用文本框和标签

在图 6-8 的顶部，你可以看到包含一个文本框和一个标签的网页的一部分。与迄今为止你所看到的文本框不同，这里显示的文本框允许用户输入多行文本。为此，该文本框的`TextMode`属性从默认的`SingleLine`改为`MultiLine`。此外，为了指示一次可以在文本框中显示的行数，`Rows`属性被设置为 5。你可以在该控件的 asp 标签中看到这些属性。

另一个可用于多行文本框的属性是`Wrap`。默认情况下，该属性设置为`True`，这意味着当文本到达文本框末尾时会自动换行。如果你将此属性设置为`False`，用户必须按 Enter 键才能开始新的一行文本。

除了`SingleLine`和`MultiLine`之外，你还可以将`TextMode`属性设置为`Password`。然后，用户输入的字符会被屏蔽，因此不会显示。由于 ASP.NET 提供了可用于接受用户名称和密码的`Login`控件，因此你不太可能使用文本框来接受密码。

尽管大多数文本框用于接受用户的输入，但你偶尔可能需要限制用户向文本框中输入数据。为此，你可以将控件的`ReadOnly`属性设置为`True`。然后，用户可以看到控件中的文本，但无法更改它。

你可以使用`MaxLength`属性指定可以输入到文本框中的最大字符数。如果用户输入的数据将存储在数据库表的列中，这尤其有用。然后，你可以将输入限制为该列允许的字符数。

尽管在设计视图中调整大小时文本框的宽度会自动设置，但你也可以使用`Columns`属性设置宽度。该属性以字符为单位指定文本框的宽度。需要注意的是，宽度是近似的，因为它基于所使用字体的字符平均宽度。

请记住，你还可以使用 CSS 指定控件的一些属性，例如`Width`。在本章中，不过，我会在 aspx 代码中显示这些属性，只要有助于你理解控件的工作方式。

图 6-8 中的标签控件也与迄今为止你所看到的不同之处在于它由两行文本组成。为此，分配给标签的`Text`属性的文本包含 HTML。你将在一分钟后看到分配此值的代码。

在继续之前，我想提醒你，通常你只使用标签来显示从一次页面执行到下一次页面执行会发生变化的文本。要包含不发生变化的文本，你可以使用文字文本。这就是我在示例中输入文本“Enter your question:”的方式。

### 如何使用复选框和单选按钮

除了将文本输入到表单中之外，你可能还想让用户从一个或多个选项中进行选择。为此，你可以使用复选框或单选按钮。这两种控件的主要区别在于，组中的单选按钮是互斥的，而复选框则独立运行。换句话说，如果用户在组中选择了一个单选按钮，则同一组中的所有其他单选按钮都会自动关闭。相比之下，当用户选择一个复选框时，它不会影响其他复选框。

图 6-9 显示了包含四个复选框控件和一组两个单选按钮控件的网页的一部分。第一个复选框让用户表明他是否希望被添加到邮件列表中。其他复选框让用户选择他希望被联系的内容。单选按钮让用户选择他希望被联系的方式。

要创建一组单选按钮，只需为组中每个单选按钮的`GroupName`属性指定相同的名称即可。如果你想在单个表单上创建两个或多个单选按钮组，只需为每个组使用不同的组名即可。请注意，如果你没有为单选按钮指定组名，则该按钮将不属于任何组。相反，它将独立于表单上的任何其他单选按钮进行处理。

如果你开发过 Windows 应用程序，你会意识到这与 Windows 单选按钮的工作方式相反。在 Windows 应用程序中，表单上未专门包含在组中的任何单选按钮都被视为同一组的一部分。因此，如果表单只有一个单选按钮组，你可以让它们默认为同一组。然而，由于 Web Server 单选按钮控件并非如此工作，因此你几乎总是为它们指定组名。
