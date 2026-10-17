
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
