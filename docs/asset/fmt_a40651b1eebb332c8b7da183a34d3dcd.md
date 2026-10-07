
```csharp
@ Page Language="C#" %>
<script runat="server">

protected void Button_Click(Object sender, EventArgs e) {
  Label.Text = "有效数字";
}
</script>
```

查看此 Web 表单，有几件事正在发生。这是一个简单的表单，只有一个需要用户输入的单文本框。用户点击按钮触发 `Button_Click` 事件，该事件反过来填充页面上的 `Label` 控件。只有在执行了所有验证检查且用户输入通过测试时，它才会执行此简单操作。

一个与众之处是在 `<head>` 部分中包含的 `<script>` 块。这是自定义验证器（Custom Validator）。Visual Studio 2010 对处理此类结构非常友好，特别是当你在页面的设计视图（Design view）和代码视图（Code view）之间切换时——这是 Visual Studio 在 2008 年之前非常困难的。

```javascript
<script type="javascript">
function validateNumber(o, args) {
  args.IsValid = (args.Value % 5 == 0);
}
</script>
```

第二个 `<script>` 部分是你希望让 `CustomValidator` 控件使用的客户端 JavaScript，以便它对输入到文本框中的信息进行验证检查。你将使用的 JavaScript 函数将使用 `args.IsValid` 属性，并根据验证检查的结果将其设置为 true 或 false。在这种情况下，会检查用户输入（`args.Value`）是否能被 5 整除。返回的布尔值随后赋值给 `args.IsValid` 属性，该属性由 `CustomValidator` 控件使用。

`CustomValidator` 控件与其他控件一样，使用 `ControlToValidate` 属性将其与页面上的特定元素关联。你感兴趣的属性是 `ClientValidationFunction` 属性。你提供的字符串值是你希望在 `CustomValidator` 控件被触发时让验证检查采用的客户端函数名称。在这种情况下，它是 `validateNumber`。

```
ClientValidationFunction=validateNumber
```

如果你使用无效输入运行此页面，产生的结果将如图 4-7 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_233_0.png)

图 4-7

# 使用服务器端验证

现在让我们将相同的验证检查从客户端移动到服务器端。`CustomValidator` 控件允许你让自定义服务器端验证成为现实。你会发现，创建服务器端验证与创建客户端验证一样简单。

如果你创建了自己的服务器端验证，可以使它们变得与你的应用程序要求一样复杂。例如，使用 `CustomValidator` 进行服务器端验证，如果你想检查用户输入相对于来自 XML 文件、数据库或其他地方的动态值，可以这样做。

关于使用 `CustomValidator` 控件进行某些服务器端验证的示例，你可以配合创建客户端验证时使用相同的示例。现在，创建一个服务器端检查，确保用户输入能被 5 整除，如列表 4-15 所示。

> 列表 4-15：使用 CustomValidator 控件执行服务器端验证

```vb
<%@ Language="VB" %>
<script runat="server">
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    If Page.IsValid Then
        Label1.Text = "输入有效!"
    End If
Sub

Sub ValidateNumber(sender As Object, args As ServerEventArgs)
    Try
        dim num As Integer = Integer.Parse(args.Value)
        args.IsValid = ((num mod 5) = 0)
    Catch ex As Exception
        args.IsValid = False
    End Try
End Sub
</script>
```

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>CustomValidator</title>
</head>
<body>
  <div
  <form id="form" runat="server">
    <p>
      数字:
      <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
      &nbsp;
      <asp:CustomValidator ID="CustomValidator1" runat="server" ControlToValidate="TextBox1"
Text="数字必须能被5整除"
ClientValidationFunction="validateNumber">
</asp:CustomValidator>
    </p>
    <p>
      <asp:Button ID="Button" OnClick="Button_Click" runat="server" Text="按钮"></asp:Button>
    </p>
    <p>
      <asp:Label ID="Label" runat="server"></asp:Label>
    </p>
  </div>
</form>
</body>
</html>
```

```csharp
@ Page Language="C#" %>
<script runat="server">
protected void Button1_Click(Object sender, EventArgs e) {
  if (Page.IsValid) {
    Label1.Text = "输入有效!";
  }
}

void ValidateNumber(object source, ServerEventArgs args) {
  try {
    int num = Integer.Parse(args.Value);
    args.IsValid = (num % 5) == 0;
  } catch (Exception ex) {
    args.IsValid = false;
  }
}
</script>
```
*(注：由于原文提供的文本在后半部分代码块非常混乱（包含了 C#, VB, 和 HTML 的混合），根据“代码块不需要翻译”的原则，我将保留了所有原始代码结构，仅翻译了其周围的说明性文字。)*

*(注：由于原文格式混乱，我已在翻译中尽可能修正了逻辑的对应关系。)*

默认情况下，ValidationSummary 控件以项目列表的形式显示验证错误列表，如列表 4-17 所示。

### 列表 4-17：ValidationSummary 控件的部分页面示例

```xml

<p>First name

  <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>

  &amp;&nbsp;

  <asp:RequiredFieldValidator ID="RequiredFieldValidator1"

    runat="server" ErrorMessage="You must enter your first name"

    ControlToValidate="TextBox1"/></asp:RequiredFieldValidator>

</p>

<p>Last name

  <asp:TextBox ID="TextBox2" runat="server"></asp:TextBox>

  &amp;&nbsp;

  <asp:RequiredFieldValidator ID="RequiredFieldValidator2"

    runat="server" ErrorMessage="You must enter your last name"

    ControlToValidate="TextBox2"/></asp:RequiredFieldValidator>

</p>

<p><asp:Button ID="Button1" OnClick="Button1_Click" runat="server"

    Text="Submit"/></asp:Button></p>

<p><asp:ValidationSummary ID="ValidationSummary1" runat="server"

    HeaderTexts="You received the following errors:"/></asp:ValidationSummary></p>

<p><asp:Label ID="Label1" runat="server"/></asp:Label></p>

```

此示例显示了姓和名的用户端。表单中的每个文本框都有一个关联的 RequiredFieldValidator 控件。当页面生成并运行时，用户在两个文本框中未输入任何值的情况下点击 Submit 按钮，将触发验证错误。图 4-8 显示了此情况。

![](img/7040c21013b8e6c23c612d6da3599ff8_236_0.png)

图 4-8

## 第 4 章服务器端验证控件

与之前表单上验证控件的示例一样，验证错误会出现在每个框附近。然而，你可以看到 ValidationSummary 控件也会在 Web 表单上验证控件的位置以项目列表的形式显示验证错误。在大多数情况下，你不希望这些错误在页面上为用户出现两次。你可能在本章中已经过过过，你可以通过使用验证控件的 Text 属性以及 ErrorMessage 属性来更改这种行为。列表 4-18 显示了这种方法。

### 列表 4-18：使用验证控件的 Text 属性

```xml

<asp:RequiredFieldValidator Id=RequiredFieldValidator

runat="server" ErrorMessage="You must enter your first name" ControlToValidate="TextBox"></asp:RequiredFieldValidator>

<asp:RequiredFieldValidator Id=RequiredFieldValidator

runat="server" ErrorMessage="You must enter your first name" ControlToValidate="TextBox"></asp:RequiredFieldValidator>

```

列表 4-18 显示了完成相同任务的两种方法。第一种是使用 Text 属性，第二种是将提供的输出放在 `<asp:RequiredFieldValidator>` 标签之间。对验证控件进行此类更改所产生的结果如图 4-9 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_237_0.png)

图 4-9

要实现这一点，只需记住 ValidationSummary 控件在发生验证错误时，使用验证控件的 ErrorMessage 属性来显示这些错误。Text 属性由验证控件使用，ValidationSummary 控件完全不利用。

除了项目列表外，你还可以使用 ValidationSummary 控件的 DisplayMode 属性将结果显示为其他类型的格式。此控件具有以下可能的值：

- BulletList
- RichList
- SingleParagraph

你还可以利用对话框而不是向 Web 显示结果。列表 4-19 显示了这种行为。

### 列表 4-19：使用对话框报告错误

```xml

<asp:ValidationSummary ID="ValidationSummary1" runat="server"

ShowMessageBox="true" ShowSummary="false"></asp:ValidationSummary>

```

从代码可以看出，ShowSummary 属性被设置为 False，这意味着页面上没有显示验证错误列表。但是，由于 MessageBox 属性被设置为 True，你现在会在对话框中报告这些错误，如图 4-10 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_238_0.png)

图 4-10

## 关闭客户端验证

由于验证控件会自动为客户端提供验证（如果浏览器可以正确处理），你有时可能想要控制这种行为。关闭这些控件的客户端功能以便它们独立地向请求者发送验证。例如，你可能希望在服务器上进行所有验证。第一个选项是在控件级别。每个验证控件都有一个 EnableScript 属性。该属性默认设置为 True，但将其设置为 False 可以防止控件在客户端发送验证。列表 4-20 显示了该属性的使用。

### 列表 20：在验证控件中禁用客户端验证

```xml

<asp:RequiredFieldValidator ID="RequiredValidator1" runat="server"

Text="" ControlToValidate="TextBox1" EnableScript="false" />

```

你还可以通过编程移除验证控件的客户端功能（列表 21 所示）。

```vb

Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)

    RequiredValidator1.EnableScript = False

End Sub

```

```csharp

protected void Page_Load(Object sender, EventArgs e) {

    RequiredValidator1.EnableScript = false;

}

```

另一个选项是从 Page_Load 事件关闭页面上所有验证的客户端脚本功能。如果你想动态地不允许客户端验证，这种方法可能有用。列表 4-22 显示了此选项。

```vb

Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)

    For Each ev As BaseValidator In Page.Validators

        ev.EnableScript = False

    Next

End Sub

```

```csharp

protected void Page_Load(Object sender, EventArgs e) {

    foreach(BaseValidator bv in Page.Validators) {

        bv.EnableScript = false;

    }

}

```

## 使用图像和声音提示错误

到为止，你一直在显示来自验证控件的错误提示消息。在大多数情况下，你会这样做——显示一些文本消息以通知用户他们在表单输入的内容未通过你的验证规则。

关于验证控件的一个有趣提示是，你不局限于文本——你可以使用图像和声音进行错误提示。

要使用图像错误，你将使用任何验证控件的 Text 属性。只需将适当的 HTML 作为属性的值，如列表 4-23 所示。

### 列表 23：使用图像提示错误

```xml

<asp:RequiredFieldValidator ID="RequiredValidator" ImageUrl="error.gif"

runat="server"

ControlToValidate="TextBox1"></asp:RequiredFieldValidator>

```

从此示例可以看出，输出到 Web 页面的不是文本，Text 属性的值是一个 HTML 字符串。这段 HTML 用于显示图像。请注意单引号和双引号的使用，这样当浏览器生成页面时就不会出现任何错误。此示例产生与图 4-11 类似的结果。

## 使用验证组

![](img/7040c21013b8e6c23c612d6da3599ff8_240_0.png)

图 4-11

你可以创建的另一个花样是在用户出错时添加声音提示。你可以采用显示图像错误提示相同的方法。列表 4-24 显示了此的示例。

### 列表 24：使用声音提示错误

```xml

<asp:RequiredFieldValidator ID="RequiredFieldValidator1"

runat="server" bgsoundsrc="C:\Windows\Media\tada.wav"

ControlToValidate="TextBox1" EnableClientScript="false">

</asp:RequiredFieldValidator>
