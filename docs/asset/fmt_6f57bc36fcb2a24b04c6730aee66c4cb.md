
数据驱动的应用程序运行需要极少数组件：模板系统，用于驱动应用程序的数据库，以及基于 `LINQ to SQL` 或 `LINQ to Entities` 等对象模型工作的能力。

此应用程序的目标是让您通过浏览器操作数据库。

![](img/7040c21013b8e6c23c612d6da3599ff8_190_0.png)

图 30

作为一个示例，`DateTime.ascx` 文件，您将获得 30-1 所示的代码。

# 列表 30-1：DateTime.ascx 文件

```asp
<@ Control Language="VB" CodeBehind="DateTime.ascx.vb"
Inherits="DateTimeField" %>

<asp:Literal runat="server" ID="Literal"
Text="<% FieldValueString %> />
```

您可以看到 30-1 中没有多少需要修改的代码。只有一个 `Literal` 控件，别的没有。控件的 `Text` 属性由代码文件中的变量 `FieldValueString` 填充。列表 30-2 展示了该文件。

# 列表 30-2：DateTime.ascx 的代码绑定

```vb
Imports System.ComponentModel.DataAnnotations
Imports System.Web.DynamicData
Imports System.Web

Class DateTimeField
Inherits FieldTemplateUserControl

    Public Overrides Readonly Property DataControl As Control
        Get
            Return Literal
        End Get
    End Property

End Class
```

```csharp
using System;
using System.Collections.Specialized;
using System.ComponentModel.DataAnnotations;
using System.Web.DynamicData;
using System.Web;
using System.Web.UI;
using System.Web.Controls;

public partial class dateTimeField :
    System.Web.DynamicData.FieldTemplateUserControl
{
    public override Control DataControl
        get
        {
            return Literal;
        }
    }
}
```

数据字段模板继承自 `System.Web.DynamicData.FieldTemplateUserControl`，如列表 30-2 所示。该用户控件为您的应用程序提供了数据字段的只读版本。

除了字段 `.ascx` 文件外，除了数据字段的只读版本，还有一个以用户控件形式表示的控件编辑版本。编辑版本的文件名以 `_Edit` 结尾，例如 `DateTime_Edit.ascx` 文件。

列表 30-3 显示了 `DateTime_Edit.ascx` 控件的内容。

# 列表 30-3：DateTime_Edit.ascx 文件

```asp
<asp:Control Language="VB" CodeBehind="DateTime_Edit.ascx.vb"
Inherits="DateTime_Edit.ascx" FieldType="%">

<asp:TextBox ID="TextBox" Text="" run="server" CssClass="DDTextBox">
Text="<asp:FieldEditingString> Columns="20"/></asp:TextBox>

<asp:RequiredFieldValidator run="server" ID="RequiredFieldValidator1"
CssClass="DDControl" ControlToValidate="TextBox"
Display="Dynamic" Enabled="false">
<asp:RegularExpressionValidator run="server" CssClass="DDValidator"
ControlToValidate="TextBox" Display="Dynamic" Enabled="false">
ValidationExpression="Dynamic" CssClass="DDControl" ControlToValidate="TextBox">
<asp:CustomValidator run="server" ID="DateValidator"
CssClass="DDControl" ControlToValidate="TextBox"
Display="Dynamic" EnableClientScript="false"
OnServerValidate="DateValidator_ServerValidate">

<asp:Control Language="C#" CodeBehind="DateTime_Edit.ascx.cs"
Inherits="DateTime_Edit.ascx">
```

```aspasp
<asp:TextBox ID="TextBox" Text="" run="server" CssClass="DDTextBox">
Text="<asp:FieldEditingString> Columns="20"/></asp:TextBox>

<asp:RequiredFieldValidator run="server" ID="RequiredFieldValidator1"
CssClass="DDControl" ControlToValidate="TextBox"
Display="Dynamic" Enabled="false">
<asp:RegularExpressionValidator run="server" CssClass="DDValidator"
ControlToValidate="TextBox" Display="Dynamic" Enabled="false">
ValidationExpression="Dynamic" CssClass="DDControl" ControlToValidate="TextBox">
<asp:CustomValidator run="server" ID="DateValidator"
CssClass="DDControl" ControlToValidate="TextBox"
Display="Dynamic" EnableClientScript="false"
OnServerValidate="DateValidator_ServerValidate">
```

如所示，日期将由 `TextBox` 服务器控件填充。除了这种表示方式外，一系列验证控件会在写入数据库之前对输入进行验证。

列表 30-4 显示了这些面的后台代码（code-behind）。

# 列表 30-4：来自 DateTime_Edit.ascx 文件的后台代码

```vbnet
Imports System.ComponentModel.DataAnnotations
Imports System.Web.DynamicData
Imports System.Web
```

# 1134 | 第 30 章 ASP.NET 动态数据

列表 30-4（续）

```vbnet
Class DateTime_EditField
Inherits FieldTemplateUserControl

    Private Shared DateAttribute As DataTypeAttribute =
    New DataTypeAttribute(DataType, DateTime)

    Public Overrides ReadOnly Property DataControl As Control
    Get
        Return TextBox1
    End Get
End Property

    Protected Sub Page_Load(ByVal sender As Object,ByVal e As EventArgs)
        TextBox1.ToolTip = Column.Description
        SetupValidator(RequiredFieldValidator)
        SetupValidator(RegularExpressionValidator)
        SetupValidator(DynamicValidator)
        SetupCustomValidator(DateValidator)
    End Sub

    Private Sub SetCustomValidator(ByVal validator As CustomValidator)
        If Column.DataTypeAttribute IsNot Nothing Then
            Select Case Column.DataTypeAttribute.DataType
                DataType.Date,
                DataType.DateTime,
                DataType.Time
                    validator.Enabled = True
                    validator.ErrorMessage = Utility.HtmlEncode(
                        Column.DataTypeAttribute.FormatErrorMessage(Column.DisplayName))
            End Select
        Else If Column.ColumnType.Equals(GetType(DateTime)) Then
            validator.Enabled = True
            validator.ErrorMessage = Utility.HtmlEncode(
                DefaultDateAttribute.FormatErrorMessage(Column.DisplayName))
        End If
        End If
    End Sub

    Protected Sub DateValidator_ServerValidate(ByVal source As Object,ByVal args As ServerValidateEventArgs)
        Dim dummyResult As DateTime
        args.IsValid = DateTime.TryParse(args.Value,dummyResult)
    End Sub

    Protected Overrides Sub ExtractValues(ByVal dictionary as Iictionary)
        dictionary(Column.Name) = ConvertEditValue(TextBox1.Text)
    End Sub

End Class
```

```csharp
<# Control Language="C#" CodeFile="DateTime.Edit.ascx.cs" %>
Inherits="DateTime_EditField"

using System;
using System.Collections.Specialized;
using System.ComponentModel.DataAnnotations;
```

```csharp
using System.Web.DynamicData;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
```

```csharp
public partial class DateTimeEditField:
    System.Web.DynamicData.FieldTemplateUserControl {
    private static DataType DefaultAttribute = new DataTypeAttribute(typeof(DateTime));
    protected void Page_Load(object sender, EventArgs e) {
            TextBox1.Tooltip = Column.Description;

            SetupValidator(RequiredValidator());
            SetupValidator(ExpressionValidator());
            SetupValidator(DynamicValidator());
            SetupCustomValidator(CustomValidator());
        }
```

```csharp
private void SetupCustomValidator(CustomValidator validator) {
    if (Column.DataTypeAttribute == null) {
        switch (Column.DataType) {
            case DataType.Date:
            case DataType.DateTime:
            case DataType.Time:
                validator.Enabled = true;
                ErrorMessage = HttpUtility.HtmlEncode(Column.DataTypeAttribute.FormatErrorMessage(Column.DisplayName));
                break;
        }
    } else if (Column.Type.equals(typeof(DateTime))) {
        validator.Enabled = true;
        validator.ErrorMessage = HttpUtility.HtmlEncode(Column.DataTypeAttribute.FormatErrorMessage(Column.DisplayName));
    }
}
```
