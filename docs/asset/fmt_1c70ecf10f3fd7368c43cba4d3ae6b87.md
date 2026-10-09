
查看表单上的 `CompareValidator` 控件，你可以看到它与 `RequiredFieldValidator` 控件相似。`CompareValidator` 控件有一个名为 `ControlToValidate` 的属性，它将自己与页面上的其中一个表单元素关联。在这种情况下，页面上页面只需要一个 `CompareValidator` 控件，因为只需要进行一次比较。在这个示例中，你正在对 `TextBox2` 的值和 `TextBox1` 的值进行比较。因此，你使用了 `ControlToCompare` 属性。该特定值将与 `TextBox2` 进行比较。在这种情况下，该值是 `TextBox1`。

就是这么简单。如果用户提交表单后，两个文本框的内容不匹配，`CompareValidator` 控件的 `Text` 属性值将显示在浏览器中。该示例如图 4-2 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_256_0.png)

图 4-2

## 与常量进行验证

除了可以与其他控件验证值之外，你还可以使用 `CompareValidator` 控件与特定数据类型进行比较。例如，假设你的注册表单上有一个文本框询问用户的年龄。在大多数情况下，你希望得到一个真实的数字，而不是像 `aa` 或 `bb` 这样的值。列表 4-9 显示了如何确保获取的是一个真实的数字。

### 列表 4-9：使用 CompareValidator 对常量进行验证

```html

年龄:

<asp:TextBox Id="TextBox" Runat="server" MaxLength="3"></asp:TextBox>

<asp:CompareValidator Id="CompareValidator1" Runat="server"

Text="You must enter a number"

ControlToValidate="TextBox" Type="Integer"

Operator="DataTypeCheck"/></asp:CompareValidator>

```

在这个示例中，要求用户在文本框中输入数字。如果他试图通过输入包含数字以外任何内容的错误值来绕过验证，页面将被标记为无效，并且 `CompareValidator` 控件将显示 `Text` 属性的值。

要指定你在这些比较中要使用的数据类型，只需使用 `Type` 属性。`Type` 属性接受以下值：

- Currency（货币）
- Date（日期）
- Double（双精度浮）
- Integer（整数）
- String（字符串）

你不仅可以确保输入的内容是特定数据类型，还可以确保与特定常量比较时输入的内容是有效的。例如，你可以确保表单元素中输入的内容大于、小于、等于、大于等于或小于。

### 列表 4-10：使用 CompareValidator 进行比较

```html

年龄:

<asp:TextBox Id="TextBox" Runat="server"></asp:TextBox>

<asp:CompareValidator ID="CompareValidator" Runat="server"

ControlToValidate="TextBox" Type="Integer"

Operator="GreaterThan" ControlToCompare="TextBox1"

Text="You must be greater than"></asp:CompareValidator>

```

在这种情况下，`CompareValidator` 控件将自己与文本框关联，如果用户输入的值不小于 18，则页面无效。`Operator` 属性可以取以下值之一：

- Equal（等于）
- NotEqual（不等于）
- GreaterThan（大于）
- GreaterEqual（大于等于）
- LessThan（小于）
- LessEqual（小于等于）
- DataTypeCheck（数据类型检查）

### 列表 4-11：使用 RangeValidator 测试范围值

```html

年龄:

<asp:TextBox ID="TextBox1" Runat="server"></asp:TextBox>

<asp:RangeValidator ID="RangeValidator" Runat="server"

ControlToValidate="TextBox" Type="Integer"

Text="You must be between 30 and 40"

MaximumValue="40" MinimumValue="30"></asp:RangeValidator>

```

在这个示例中，要求用户在文本框中输入数字。如果他试图通过输入包含数字以外任何内容的错误值来绕过验证，页面将被标记为无效，`RangeValidator` 控件将显示 `Text` 属性的值。

# 第 4 章：验证器控件

`RangeValidator` 控件不仅用于验证数字（尽管它经常这样使用）。它还可以用于验证字符串范围以及其他项目，包括日期。默认情况下，任何验证控件的 `Type` 属性都设置为 `String`。你可以使用 `RangeValidator` 控件确保输入另一个控件（例如日历控件）的内容在日期范围内。

例如，假设你正在构建一个询问客户到达日的 Web 表单，到达日期需要在当前日期的两周。你可以轻松地使用 `RangeValidator` 控件测试这些场景。

由于要检查的日期是动态生成的，你在 `Page_Load` 事件中通过代码分配 `MaximumValue` 和 `MinimumValue` 属性。在设计器中，你的示例页面看起来像图 4-4。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_259_0.png)

这种思路是，最终用户从日历控件中选择一个日期，这将填充文本框控件。然后，当最终用户点击表单按钮时，如果选择的日期无效，他将收到通知。如果选择的日期有效，该日期将通过页面上的 `Label` 控件呈现。该代码见列表 4-12。

### 列表 4-12：使用 RangeValidator 测试日期值

```vb

<%@ Page Language="VB" %>

```

```vb

<script runat="server">

Protected Sub Page_Load(ByVal sender As Object, ByVal As System.EventArgs)

    RangeValidator1.MinimumValue = DateTime.Now.ToShortString()

    RangeValidator1.MaxValue = DateTime.Now.AddDays(14).ToShortString()

End Sub

</script>

```

```vb

Textbox1.Text = Calendar.SelectedDate.ToShortString()

End Sub

```

```vb

Protected Sub Button1_Click(ByVal sender As Object,

ByVal e As System.EventArgs)

If Page.IsValid Then

Label1.Text = "You are set to arrive on: " & Textbox1.Text

End If

```

```vb

End Sub

}

</script>

```

```html

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">

<title>日期验证检查</title>

</head>

<body>

<form id="form" runat="server">

到达日期：

<asp:TextBox ID="TextBox" runat="server"></asp:TextBox>&nbsp;

<asp:RangeValidator ID="RangeValidator" runat="server"

Text="You must select a date within the next two weeks.",

ControlToValidate="TextBox" Type="Date"></asp:RangeValidator><br />

选择您的到达日期: <br />

<asp:Calendar ID="Calendar" runat="server"

OnSelectionChanged="Calendar_SelectionChanged"></asp:Calendar>

&nbsp;

<br />

<asp:Button ID="Button" runat="server" Text="Button"

OnClick="Button1_Click" />

<br />

<br />

<asp:Label ID="Label" runat="server"></asp:Label>

</form>

</body>

</html>

```

# 第 4 章：验证服务器控件

```vb

Textbox1.Text = Calendar.SelectedDate.ToShortString()

End Sub

```

```vb

Protected Sub Button1_Click(ByVal sender As Object,

ByVal e As System.EventArgs)

If Page.IsValid Then

Label1.Text = "You are set to arrive on: " & Textbox1.Text

End If

```

```vb

End Sub

}

</script>

```

# C#

```csharp

<@ Page Language="C#" %>

<script runat="server">

protected void Page_Load(object sender, EventArgs e)

{

RangeValidator1.MinimumValue = DateTime.Now.ToShortString();

RangeValidator1.MaximumValue =

    DateTime.Now.AddDays(14).ToShortString();

}

protected void Calendar_SelectionChanged(object sender, EventArgs e)

{

Textbox1.Text = Calendar.SelectedDate.ToShortString();

}

```

```csharp

protected void Button1_Click(object sender, EventArgs e)

{

    if (Page.IsValid)

    {

        Label1.Text = "You are set to arrive on: " + TextBox1.Text.ToString();

    }

}

</script>

```

从这段代码中，你可以看到当页面加载时，`MinimumValue` 和 `MaximumValue` 属性被赋值了一个动态值。在这种情况下，`MinimumValue` 获取了 `DateTime.Now.ToShortString()`，而 `MaximumValue` 获取了 14 天后的日期。

在用户选择日期后，通过 `Calendar_Changed` 事件将选定的日期填充到 `TextBox` 控件中。选择日期并点击页面上的按钮后，会触发 `Button1_Click` 事件，并使用 `Page.IsValid` 属性对页面进行验证。如果页面无效，将得到图 4-5 所示的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_261_0.png)

图 4-5

# ExpressionValidator 服务器控件

这意味着你可以定义一个结构，如果用户的输入结构与你定义的结构匹配，则将根据该结构对输入进行验证。例如，你可以定义用户输入的结构必须是电子邮件地址或 Internet URL 格式；如果不符合此定义，则该页面被视为无效。列表 14-13 展示了如何通过确保输入为电子邮件地址格式来验证输入文本框的内容。

201

www.it-ebooks.info

# 列表 4-13：确保文本框值为电子邮件地址

```html

电子邮箱：

<asp:TextBox ID="Textbox1" Runat="server"></asp:TextBox>

&amp;

<asp:RegularExpressionValidator ID="RegularValidator1"

Runat="server" ControlTo="Textbox1"

Text="You must enter an email address"

ValidationExpression="^([-a-zA-Z0-9\%&'*+/=?^_`{|}~]+\.)+[a-zA-Z0-9-]+\.[a-zA-Z]{2,4}$"

</asp:RegularExpressionValidator>

```

与其他验证控件一样，`ControlToValidate` 属性将其自身绑定到 `TextBox` 控件，并包含一个 `Text` 属性，在验证失败时将错误消息推送到屏幕上。该验证的独特属性是 `ValidationExpression` 属性。该属性接收一个字符串值，即你想要应用于输入值的正则表达式。

Visual Studio 2008 通过使用表达式编辑器（Expression Editor）使得使用正则表达式变得稍微容易。该编辑器提供了几个你可能想要应用于 `ExpressionValidator` 的正则表达式。要实现此，请从设计视图（Design view）操作你的页面。在 Visual Studio 的属性窗口中，点击 `ValidationExpression` 旁边的按钮启动表达式编辑器。该编辑器如图 4-6 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_262_0.png)

此外，你还可以找到电子邮件地址、Internet URL、邮政编码、电话号码和社会号码等的正则表达式。除了使用表达式编辑器帮助处理这些复杂的表达式字符串外，你也可以从网站 `regexlib.com` 找到它们的很好的集合。

# CustomValidator 服务器控件

到为止，你已经看到了许多可供使用的验证控件。在很多情况下，验证控件解决了你想应用于表单的许多验证规则。

然而，有时这些控件中没有一个能满足你的需求，你必须超出它们提供的范围。这时 `CustomValidator` 就派上用场了。`CustomValidator` 允许你构建自己的客户端或服务器端验证，这些验证可以轻松地应用于你的表单。这样做意味着你可以对数据层中执行的值或计算（例如，在数据库中）进行验证检查，或者确保用户的输入符合某些算术运算（例如，判断一个数字是偶数还是奇数）。你可以通过 `CustomValidator` 实现这一点。

# 使用客户端验证

`CustomValidator` 控件的一个非常有价值的功能是它能够轻松地提供客户端验证。许多开发者在他们的应用程序中使用了一套属于自己的 JavaScript 函数集合，而使用 `CustomValidator` 控件是实现这些函数的一种简单方法。

例如，看一个要求用户输入数字的简单表单。该表单使用 `CustomValidator` 控件对输入进行客户端验证，以提供的数字能被 5 整除。这在 4-14 中所示。

# 列表 4-14：使用 CustomValidator 进行客户端验证

```vb

<%@ Page Language="VB" %>

<script runat="server">

Protected Sub Button_Click(ByVal sender As Object, ByVal e As System.EventArgs)

        Label.Text = "VALID NUMBER!"

    End Sub

</script>

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">

<title>CustomValidator</title>

    <script type="javascript">

        function validateNumber(oSrc, args) {

            args.IsValid = (args.Value % 5 == 0);

        }

    </script>

</head>

<body>

    <form id="form1" runat="server">

        <div>

            <p>

                <asp:TextBox ID="TextBox1" Runat="server"></asp:TextBox>

                &nbsp;

                <asp:CustomValidator ID="CustomValidator1"

                Runat="server" ControlToValidate="TextBox1"

                Text="Number must be divisible by 5"

                ClientValidationFunction="validateNumber"

                </asp:CustomValidator>

            </p>

            <p>

                <asp:Button ID="Button1" OnClick="Button1_Click"

                Runat="server" Text="Button"></asp:Button>

            </p>

            <p>

                <asp:Label ID="Label1" Runat="server"></asp:Label>

            </p>

        </div>

    </form>

</body>

</html>
