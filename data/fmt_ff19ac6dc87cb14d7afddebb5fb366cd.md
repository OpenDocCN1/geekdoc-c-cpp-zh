
# 第 20 章：ASP.NET AJAX Control Toolkit

在此例中，`MaskedEditExtender` 使用 `TargetControlID` 将自身与 `TextBox` 控件关联。`MaskType` 属性指定了放置在文本框上的掩码或过滤器的类型。可能的值包括：

- None: 不执行任何验证。
- Date: 将进行验证。
- DateTime: 将进行日期和时间验证。
- Number: 将进行数字验证。
- Time: 将进行时间验证

列表 20-20 使用了 `Number`，然后指定了用户需要输入的掩码或模板。这是通过使用 `Mask` 属性实现的。在这种情况下，`Mask` 属性被设置为 `999`。这意味着所有数字的长度都可以为三位。

使用 `999` 作为 `Mask` 属性意味着，当用户在文本框中输入值时，文本框中会出现三个下划线。输入条目的模板如图 20-25 所示。

图 20-25

如果将 `Mask` 属性更改为如下 `99,999.99`：

```assembly
<c:MaskedEditExtender ID="MaskedEditExtender1" runat="server"
TargetControlID="TextBox1" MaskType="Number" Mask="99,999.99">
</c:MaskedEditExtender>
```

那么就会出现框模板，如图 20-26 所示。

图 20-26

从图 20-26 可以看出，模板中存在逗号和句号。当用户输入时，他们不需要重新输入这些值。光标将只需移动到所需的数字部分。

如你看到的 `Mask` 属性值，数字由数字 `9` 表示。在处理其他 `MaskType` 值时，你还需要注意其他的掩码字符。

- `9` — 仅限数字字符
- `L` — 仅限字母
- `$` — 仅限字母或空格
- `C` — 仅限自定义字符（区分大小写）
- `A` — 仅限字母或自定义字符
- `N` — 仅限数字或自定义字符
- `?` — 任意字符

除了字符规范外，模板还使用了分隔符，详见下列表：

- `/` 是日期分隔符
- `:` 是时间分隔符
- `.` 是小数点分隔符
- `,` 是千位分隔符
- `\` 是转义字符
- `{` 是掩码重复的起始分隔符
- `}` 是掩码重复的结束分隔符

使用这些项目中的某些，你可以轻松地更改 `MaskedEditExtender` 来处理 `DateTime` 值：

```assembly
<MaskedEditExtender ID="MaskedEditExtender1" runat="server"
TargetControlID="TextBox1" MaskType="DateTime" Mask="99/99/9999 99:99:99">
</MaskedEditExtender>
```

在文本框中创建的模板如图 20-27 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1010_0.png)

在早期的示例中，验证是通过 `MaskedEditValidator` 控件的实例实现的。

```assembly
<MaskedEditValidator ID="MaskedEditValidator1" runat="server"
ControlToValidate="TextBox1"
IsEmpty="False" EmptyValueMessage="需要三位数字"
Display="Dynamic"></MaskedEditValidator>
```

该控件使用 `ControlToValidate` 属性将自身与 `MaskedEditExtender` 关联，并使用该属性监控表单上的特定控件。默认情况下，`IsValid` 属性设置为 True。将其更改为 False 意味着用户需要在文本框中输入值才能通过验证，而不会收到 `EmptyMessage` 属性中显示的错误消息。触发 `MaskedEdit` 控件的结果如图 20-28 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1010_1.png)

## MaskedEditExtender

在之前的示例中，验证是通过 `MaskedEditValidator` 控件的实例实现的。

通常你想提供一组像复选框那样的单选框，当你有一组复选框时，你希望用户只选择一个。与复选框不同，你希望用户从列表中选择一个。使用 `MaskedEditExtender` 可以实现这一点。列表 20-21 显示了如何操作。

### 列表 20-21：使用复选框的单选框

```assembly
<%@ Page Language="C#" %>
<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="c" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>MaskedEditExtender</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager Id="ScriptManager1" runat="server">
</asp:ScriptManager>
<c:MaskedEditExtender Id="MaskedEditExtender1" runat="server"
TargetControlID="TextBox1" MaskType="Number" Mask="999*">
</c:MaskedEditExtender>
<asp:TextBox Id="TextBox1" runat="server"></asp:TextBox>
<c:MaskedEditValidator Id="MaskedEditValidator1"
runat="server" ControlExtenderID="MaskedEditExtender1"
ControlToValidate="TextBox1" IsValidEmpty="False"
EmptyErrorMessage="需要三位数字!"
Display="Dynamic"
</c:MaskedEditValidator>
</div>
</form>
</body>
</html>
```

## NumericUpDownExtender

`NumericUpDownExtender` 控件允许你在文本框旁边放置向上/下的指示器，使用户轻松控制选择。一个简单的示例如列表 20-22 所示。

### 列表 20-22：使用 NumericUpDownExtender 控件

```assembly
<% Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="c" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>NumericUpDownExtender Control</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager Id="ScriptManager1" runat="server">
</asp:ScriptManager>
<c:NumericUpDownExtender ID="NumericUpDownExtender1" runat="server"
TargetControlID="TextBox1" Width="150"
Maximum="10" Minimum="1">
</c:NumericUpDownExtender>
<asp:TextBox Id="TextBox1" runat="server"></asp:TextBox>
</div>
</form>
</body>
</html>
```

### 列表 20-23：在 NumericUpDownExtender中使用字符代替数字

```xml
<cccl:NumericUpDownExtender ID="NumericUpDownExtender1" runat="server"
TargetControlID="TextBox" Width="150"
RefValues="Blue;Green;Orange;Black;White">
</cccl:NumericUpDownExtender>
```

在这种情况下，单词定义在 `RefValues` 属性中（均用分号分隔）；这将为你带来如图 20-30 所示的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1013_0.png)

## PagingBulletedListExtender

`PagingBulletedListExtender` 控件允许你处理长项目符号列表并轻松地对列表应用字母顺序分页。示例列表 20-24 使用了 Northwind 数据库中的 `Customers` 表。

### 列表 20-24：从 Northwind 数据库对项目符号列表进行分页

```aspnet
@ Page Language="C#" %>
<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="ccx" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>PagingBulletedListExtender Control</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager Id="ScriptManager1" runat="server" />
<ccx:PagingBulletedListExtender
ID="PagingBulletedListExtender1"
runat="server" TargetControlID="BulletedList1">
</ccx:PagingBulletedListExtender>
<asp:DataSource Id="DataSource1" runat="server"
ConnectionString="Data Source=\SQLLEXPRESS;
AttachDbFilename=|DataDirectory\Northwind.MDF;
Integrated Security=True;UserInstance=True"
ProviderName="System.Data.SqlClient"
SelectCommand="SELECT [CompanyName] FROM [Customers]"
</asp:DataSource>
<asp:BulletedList Id="BulletedList1" runat="server"
DataSourceID="DataSource1" DataField="CompanyName"
DataValue="CompanyName">
</asp:BulletedList>
```

```xml
</div>
</form>
</body>
</html>
```

此代码从 Northwind 数据库的 `Customers` 表中提取 `CompanyName` 值，并将值绑定到页面上的 `BulletedList`。运行此页面将得到如图 20-31 所示的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1014_0.png)

图 20-31

从该图中你可以看到页面在客户端是按字母顺序组织。。只有存在对应值的字母才会出现在链接的字母列表中。点击任何字母，都会获得与该字符对应的项目符号列表项。

## PopupControlExtender

`PopupControlExtender` 允许你为页面上的任何控件创建弹出窗口。例如，你可以通过在 `TextBox` 之上创建一个包含 `Calendar` 控件的弹出窗口，来轻松地模拟之前介绍的 `CalendarExtender` 控件。列表 20-25 缺少了这一行为。

### 列表 20-25：使用 PopupControlExtender 创建 CalendarExtender

```vb
<% Page Language="VB" %>
<% Register Assembly="AjaxControlToolkit" 
Namespace="AjaxControlToolkit" TagPrefix="c1" %>
<script runat="server">
    Protected Sub Calendar_SelectionChanged(ByVal sender As Object, 
        ByVal e As System.EventArgs)
        PopupControlExtender.Commit(
            Calendar.SelectedDate.ToShortDateString())
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
```

```xml
<head runat="server">
<title>PopupControlExtender</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager Id="ScriptManager1" runat="server" />
<cccl:PopupControlExtender ID="PopupControlExtender1"
runat="server" TargetControlID="UpdatePanel1" PopupControlID="UpdatePanel1" OffsetY="25" />
<cccl:TextBox ID="TextBox1" runat="server" />
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
<ContentTemplate>
<asp:Calendar ID="Calendar1" runat="server"
BackgroundColor="White" BorderColor="Verdana"
BorderWidth="1px" FontName="Arial" ForeColor="Black"
Height="350px" Format="FullMonth" Width="190px"
OnSelectionChanged="Calendar1_SelectionChanged">
</asp:Calendar>
</ContentTemplate>
</asp:UpdatePanel>
</div>
</form>
</body>
</html>
```

编译并运行代码后，将生成与图 20-33 相同的页面。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1018_0.png)

图 20-33

你可以在顶部的截图可以看到在没有终端用户交互时图像的样式。在这种情况下，图像的右下角有一个黑色正方形（由 CSS 定义）。底部的截图显示了当终端用户抓住手柄并开始更改图像形状时发生的情况。

## RoundedCornersExtender

`RoundedCornersExtender` 控件允许你为页面上的元素添加圆角。与 `ResizableControlExtender` 控件一样，你将感兴趣的元素放在 `Panel` 控件内部。代码列表 20-27 展示了如何对 `Login` 服务器端控件进行操作。

### 代码列表 20-27：对包含 Login 控件的 Panel 控件进行圆角

```
<@ Page Language="C#" %>
<%@ Register Assembly="AjaxControlToolkit" %>
Namespace="AjaxControlToolkit"
TagPrefix="ccl" %>
```

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>RoundedCornersExtender Control</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager Id="ScriptManager1" runat="server">
</asp:ScriptManager>
<ccl:RoundedCornersExtender ID="RoundedCornersExtender"
runat="server" TargetID="Panel1">
<asp:Panel ID="Panel1" runat="server" Width="250px"
HorizontalAlign="Center" BackColor="Orange">
<asp:Login ID="Login1" runat="server">
</asp:Login>
</asp:Panel>
</div>
</form>
</body>
</html>
```
