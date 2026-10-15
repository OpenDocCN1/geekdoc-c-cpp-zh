

现在，按 F5 键运行应用程序。输出显示在图 14.3 中：

![](img/e073a4882197be4ab61103cbe0bcb394_721_0.png)

## 使用 HyperLink 控件

当你向 Web 页面（Default.aspx）添加 HyperLink 控件时，它会在 Web 页面的源代码中添加以下代码：

```
<asp:HyperLink ID="HyperLink1" runat="server">HyperLink</asp:HyperLink>
```

让我们创建一个名为 HyperLinkControl 的 Web 应用程序（也可在 CD-ROM 上获得）。在此示例中，我们已将 Hyperlink 控件的 NavigateUrl 属性设置为 http://www.google.co.in Web 页面。清单 14.7 显示了 HyperLink 控件的 Default.aspx 页面：

### 清单 14.7：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>HyperLink Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Font-Bold="True" Font-Size="Medium" Font-Underline="True" ForeColor="Black" Text="HyperLink Control Example"><br />
<br />
<br />
<asp:HyperLink ID="HyperLink1" runat="server" Font-Size="Small" ForeColor="Blue" Target="_blank" NavigateUrl="http://www.google.co.in">Click me to move to the google website</asp:HyperLink>
<br />
</div>
</form>
</body>
</html>
```

现在，按键盘上的 F5 键运行应用程序。点击 Click me to move to the Google website 链接后的输出如图所示 14.4：

![](img/e073a4882197be4ab61103cbe0bcb394_722_0.png)

## 使用 HiddenField 控件

当你在 Web 页面上添加 HiddenField 控件时，以下代码将被添加到 Web 页面的源代码中：

```
<asp:HiddenField ID="HiddenField1" runat="server" />
```

现在，让我们创建一个名为 HiddenFieldControl 的 Web 应用程序（也可在 CD-ROM 中获得）以显示 HiddenField 控件的工作原理。你可以通过从工具箱的标准选项卡拖放 HiddenField 控件或在工具箱中双击它来向 Web 页面添加 HiddenField 控件。当你点击这些应用程序中的 Button 控件时，它会在 Label 控件中显示 HiddenField 控件中存储的值。清单 14.8 显示了 HiddenField 控件的 Default.aspx 页面的代码：

### 清单 14.8：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
    Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Hidden Field Control Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label1" runat="server"
                Text="HiddenField Control showing value on Button click" Font-Bold="True"
                Font-Underline="True"></asp:Label>
            <br />
            <br />
            <br />
            <br />
            <asp:Button ID="Button1" runat="server" Text="Click Me!" Font-
                Bold="True" OnClick="Button1_Click"
                />
        </div>
    </form>
</body>
</html>
```

<br />
<asp:Label ID="Label2" runat="server"></asp:Label>
<br />
<br />
<br />
<br />
</div>
</form>
</body>
</html>

现在，在 Default.aspx 页面的代码隐藏文件中添加清单 14.9 中显示的代码，用于 HiddenField 控件：

### 清单 14.9：显示 Default.aspx 页面的代码隐藏文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        HiddenField1.Value = "Welcome to the World of ASP.NET 4.0";
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        Label2.Text = HiddenField1.Value;
    }
}
```

现在，按 F5 键运行应用程序。输出显示在图 14.5 中：

![](img/e073a4882197be4ab61103cbe0bcb394_723_0.png)

### 图 14.5：在 Button 点击事件上显示 HiddenField 控件的值

## 使用 FileUpload 控件

当你在 Web 页面上添加 FileUpload 控件时，以下代码将被添加到 Web 页面的源代码中：

```
<asp:FileUpload ID="FileUpload1" runat="server" />
```

现在，让我们创建一个名为 FileUploadControl 的 Web 应用程序（也可在 CD-ROM 中获得）以显示 FileUpload 控件的工作原理。你可以通过从工具箱的标准选项卡拖放 FileUpload 控件或在工具箱的标准选项卡中双击它来向 Web 页面添加 FileUpload 控件。在此情况下，我们使用 FileUpload 控件浏览文件并使用 SaveAs() 方法在点击事件上将其上传到服务器。清单 14.10 显示了 FileUpload 控件的 Default.aspx 页面的代码：

### 清单 14.10：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>File Upload Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label2" runat="server" Font-Bold="True" Font-Underline="True" Text="FileUpload Control Example"></asp:Label>
<br />
<br />
<br />
&nbsp;<asp:Label ID="Label1" runat="server" Text="Please select a file to Upload:"></asp:Label>
<asp:FileUpload ID="FileUpload1" runat="server" />
<br />
<br />
&nbsp;<br />
<asp:Button ID="Button1" runat="server" Font-Bold="True" Font-Underline="False" Text="Click to Upload" Height="26px" onclick="Button1_Click" Width="144px" />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<asp:Label ID="Label3" runat="server"></asp:Label>
</div>
</form>
</body>
</html>
```

现在，在 Default.aspx 页面的代码隐藏文件中添加清单 14.11 中显示的代码，用于 FileUpload 控件：

### 清单 14.11：显示 Default.aspx 页面代码隐藏文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    if (!Page.IsPostBack) Label3.Text = "";
}
protected void Button1_Click(object sender, EventArgs e)
{
    if (FileUpload1.HasFile)
    {
        FileUpload1.SaveAs("D:/" + FileUpload1.FileName);
        Label3.Text = "File " + FileUpload1.FileName + " is Uploaded";
    }
    else
        Label3.Text = "No uploaded file";
}
```

现在，按 F5 键运行应用程序。输出显示在图 14.6 中：

![](img/e073a4882197be4ab61103cbe0bcb394_725_0.png)

图 14.6：使用 FileUpload 控件将文件上传到服务器

NOTE
点击 Button 控件后，FileUpload 控件中显示已上传文件路径的文本框会变为空。

## 使用 CheckBox 控件

当你在 Web 页面（Default.aspx）上添加 CheckBox 控件时，它会在 Web 页面的源代码中添加以下代码：

```
<asp:CheckBox ID="CheckBox1" runat="server" />
```

让我们创建一个名为 CheckBoxControl 的 Web 应用程序（也可在 CD-ROM 上获得）。在此示例中，我们在 Web 页面上放置了五个 CheckBox 控件显示汽车名称。附加到 CheckBox 控件的项目在你选择该项目时出现在 ListBox 控件中，并在你清除 CheckBox 控件时从 ListBox 控件中移除。清单 14.12 显示了 CheckBox 控件的 Default.aspx 页面：

### 清单 14.12：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
