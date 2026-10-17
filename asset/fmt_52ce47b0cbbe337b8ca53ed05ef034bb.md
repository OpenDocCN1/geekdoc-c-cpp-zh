
## 第 4 章：验证器控件

`CustomValidator` 控件与之前的控件一样，使用 `ControlToValidate` 属性将自身与页面上的特定元素关联。你在这里感兴趣的属性是 `ClientValidationFunction` 属性。赋值给此属性的字符串值是当 `CustomValidator` 控件触发时，此验证检查将采用的客户端函数名称。在这种情况下，它是 `validateNumber`：

```
ClientValidationFunction="validateNumber"
```

如果你运行此页面并输入无效内容，结果如图 4-7 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_265_0.png)

图 4-7

### 使用服务器端验证

现在让我们将此验证检查从客户端移动到服务器。`CustomValidator` 控件允许你实现自定义服务器端验证。你会发现，创建服务器端验证与创建客户端验证一样简单。

如果你创建了自己的服务器端验证，可以根据应用程序的需求使其变得复杂。例如，如果你想使用来自 XML 文件、数据库或其他来源的动态值来检查用户输入，则可以使用 `CustomValidator` 进行服务器端验证。

关于使用 `CustomValidator` 控件进行某些自定义服务器端验证的示例，你可以参考创建客户端验证时使用的相同示例。创建一个服务器端检查，确保用户输入的数字能被 5 整除。这在代码列表 4-15 中所示。

#### 代码列表 4-15：使用 CustomValidator 控件执行服务器端验证

```VB
<% Language="VB" %>
<script runat="server">
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.Events)
    If Page.IsValid Then
        Label.Text = "VALID ENTRY!"
    End If
End Sub
```
205

```vb
Sub ValidateNumber(sender As Object, args As ServerValidateEventArgs)
Try
  Dim num As Integer = Integer.Parse(args.Value)
  args.IsValid = ((num mod 5) = 0)
Catch ex As Exception
  args.IsValid = False
End Try
End Sub
```

```html
<script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>CustomValidator</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<p>
Number:
<asp:TextBox ID="Textbox" runat="server"></asp:TextBox>
&nbsp;
<asp:CustomValidator ID="CustomValidator1" runat="server" ControlValidate="Textbox1" Text="Number must be divisible by 5" OnServerValidate="ValidateNumber"></asp:CustomValidator>
</p>
<p>
<asp:Button ID="Button1" OnClick="Button1_Click" runat="server" Text="Button"></asp:Button>
</p>
<p>
<asp:Label ID="Label" runat="server"></asp:Label>
</p>
</div>
</form>
</body>
</html>
```

### C#

```csharp
<@ Page Language="C#" %>
<script runat="server">
protected void Button1_Click(Object sender, EventArgs e) {
  if (Page.IsValid) {
    Label.Text = "VALID ENTRY!";
  }
}
```

```csharp
void ValidateNumber(object source, ServerValidateEventArgs args)
{
  try {
    int num = int.Parse(args.Value);
    args.IsValid = (num%5 == 0);
  }
  catch (Exception ex) {
    args.IsValid = false;
  }
}</script>
```

此示例没有使用客户端 JavaScript 函数，而是包含了一个服务器端函数——`ValidateNumber`。所有构建与 `CustomValidator` 控件协作的函数必须使用 `ServerValidateEventArgs` 对象作为参数，以便为函数传递数据。你实际上是通过 `args.Value` 从表单元素获取值的。然后根据你的验证检查将 `args.IsValid` 属性设置为 True 或 False。从上一个示例中你可以看到，如果数字不能被 5 整除，`args.IsValid` 将被设置为 False，并且在表单元素中输入字符串时会抛出异常。建立自定义函数后，下一步是将其应用于 `CustomValidator` 控件，如下例所示：

```asp
<asp:CustomValidator ID="CustomValidator" Run="server" ControlToValidate="TextBox" Text="Number must be divisible by 5" OnServerValidate="ValidateNumber"></asp:CustomValidator>
```

要在你的服务器端代码中建立 `CustomValidator` 控件与函数之间的关联，使用 `OnServerValidate` 属性。赋值给此属性的值是函数的名称——在这种情况下是 `ValidateNumber`。运行这会导致回传到服务器。页面重新加载并调用验证检查。如下所示：

```vb
If Page.IsValid Then
  Label.Text = "VALID ENTRY!"
```

207

### 同时使用客户端和服务器端验证

正如本章早期所述，当你同时使用客户端和服务器端验证时，必须考虑它们是如何协同工作的。例如，客户端验证为用户提供即时反馈，而服务器端验证在处理之前提供确保数据有效的最终检查。

在许多情况下，你希望同时使用两者以获得最佳用户体验。客户端验证可以帮助用户在出错时修正，而当客户端验证被绕过或失败时，服务器端验证可以保护你的应用程序不受无效数据的影响。

列表 16 显示了同时使用客户端和服务器端验证的示例。

```asp
<asp:CustomValidator ID="CustomValidator" runat="server" ControlValidate="Textbox" Text="Number must be divisible by 5" OnServerValidate="ValidateNumber"></asp:CustomValidator>
```

### ValidationSummary 控件

`ValidationSummary` 控件是一种汇总页面上的验证错误并将其显示在单个位置的控件。当页面上有许多验证控件且你想一次性显示所有错误时，这非常有用。

`ValidationSummary` 控件可以配置为以列表、段落或其他格式显示错误。你还可以自定义 `ValidationSummary` 的头部和页脚。

列表 17 显示了使用 `ValidationSummary` 控件的示例。

```asp
<p><asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
&nbsp;<asp:RequiredFieldValidator ID="RequiredValidator1" runat="server" ErrorMessage="You must enter your first name" ControlToValidate="TextBox1"></asp:RequiredFieldValidator></p>
<p>Last name<asp:TextBox ID="TextBox2" runat="server"></asp:TextBox>
&nbsp;<asp:RequiredFieldValidator ID="RequiredValidator2" runat="server" ErrorMessage="You must enter your last name" ControlToValidate="TextBox2"></asp:RequiredFieldValidator></p>
<asp:Button ID="Button1" OnClick="Button1_Click" runat="server" Text="Submit"></asp:Button>

<asp:ValidationSummary ID="ValidationSummary1" runat="server" HeaderText="You received the following errors:"></asp:ValidationSummary>

<asp:Label ID="Label1" runat="server"></asp:Label>
```

此示例显示了姓和名的用户界面。表单中的每个框都分配了一个 `RequiredFieldValidator`。当页面构建并运行时，如果用户在两个框中都没有输入值就点击提交按钮，将导致触发验证错误。此结果如图 4-8 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_269_0.png)

图 4-8

在表单验证控件的早期示例中，这些验证错误出现在每个文本框旁边。然而，你可以看到 `ValidationSummary` 控件也会以列表的形式在控件的位置显示验证错误。在大多数情况下，你不希望这些错误在页面上为用户出现两次。你可以通过使用验证控件的 `Text` 属性（`ErrorMessage` 属性之外）改变这种行为，正如你一直以来这样做的那样。这种方法在列表 118 中所示。

#### 代码列表 4-18：使用验证控件的 Text 属性

```asp
<asp:RequiredFieldValidator ID="RequiredValidator1"
Runat="server" ErrorMessage="You must enter your first name" Text="*"
ControlToValidate="TextBox1"/></asp:RequiredFieldValidator
```

### 第 4 章：验证字段控件

```asp
<asp:RequiredFieldValidator ID="RequiredFieldValidator"
Runat="server" ErrorMessage="You must enter your first name"
ControlToValidate="Text1"></asp:RequiredValidator>
```

列表 4-18 显示了完成相同任务的两种方法，第二种方案是将默认输出置于 `<asp:RequiredFieldValidator>` 元素的标签之间。对验证控件进行此类更改将产生如图 4-9 所示的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_270_0.png)

为了得到这个结果，请记住 `ValidationSummary` 控件在发生验证错误时会使用验证控件的 `ErrorMessage` 属性来显示验证错误。`Text` 属性由验证控件使用，而 `ValidationSummary` 控件完全不使用。

除了项目列表，还可以使用 `ValidationSummary` 控件的 `DisplayMode` 属性将结果更改为其他类型的格式。该控件具有以下可能的值：

- `BulletList`（项目列表）
- `List`（列表）
- `SingleParagraph`（单段）

你还可以利用对话框将结果缩进显示在 Web 页面。列表 4-19 显示了此行为的示例。

#### 列表 4-19：使用对话框报告验证错误

```asp
<asp:ValidationSummary Id="ValidationSummary" Runat="server"
ShowMessageBox="True" ShowMessage="False"></asp:ValidationSummary>
```

在此段代码中，你看到 `ShowMessage` 属性被设置为 `False` ——这意味着验证错误的列表不会显示在实际 Web 页面上。然而，由于 `MessageBox` 属性被设置为 `True`，你现在会在消息框中收到错误报告，如图 4-10 所示。

### 第 4 章：验证服务器控件

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_271_0.png)

图 4-10

### 关闭客户端验证

由于验证服务器控件会自动为客户端提供客户端验证（如果请求的容器恰当得处理了生成的 JavaScript），你有时需要一种方法来控制这种行为。

关闭这些控件的客户端功能是完全可能的，这样它们就不会独立地向请求者发送客户端功能。例如，你可能希望所有的验证都在服务器上完成，无论请求的容器提供什么功能。你可以采取几种方法来关闭此功能。

第一种是在控件级别上。每个验证服务器控件都有一个 `EnableClientScript` 属性。该属性默认设置为 `True`，但将其设置为 `False` 可以防止控件向客户端发送用于验证的 JavaScript 函数。相反，验证将在服务器上进行。其用法在列表 4-20 所示。

#### 列表 4-20：在验证控件中禁用客户端验证

```asp
<asp:RequiredFieldValidator ID="Requiredvalidator1" Runat="server" Text="" ControlToValidate="TextBox" EnableClientScript="false" />
```

你也可以通过程序移除验证控件的客户端功能（如列表 4-21 所示）。

#### 列表 4-21：通过程序移除客户端功能

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    RequiredFieldvalidator1.EnableClientScript = False
End Sub
```

### 第 4 章：验证服务器控件

```csharp
protected void Page_Load(Object sender, EventArgs e) {
  RequiredFieldValidator1.EnableClientScript = false;
}
```

其他选项是从 `Page_Load` 事件中关闭所有页面的客户端脚本功能。如果你希望动态决定不允许进行客户端验证，这将非常有帮助。这在列表 4-22 中所示。

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    For Each bv In Page.Validators
        bv.EnableClientScript = False
    Next
End Sub
```

```csharp
protected void Page_Load(Object sender, EventArgs e) {
  foreach(BaseValidator bv in Page.Validators)
    bv.EnableClientScript = false;
}
```

### 使用图像和声音提示错误
