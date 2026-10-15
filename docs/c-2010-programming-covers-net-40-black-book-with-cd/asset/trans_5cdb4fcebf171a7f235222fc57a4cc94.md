

<head id="Head1" runat="server">
    <title>DropDownList Control </title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
<asp:Label ID="Label1" runat="server" Font-Bold="True" Font-Underline="True" Text="DropDownList Control Example" Font-Size="Medium" ForeColor="Black"></asp:Label>
<br />
<br />
<asp:Label ID="Label2" runat="server" Font-Size="Small" ForeColor="#FF0066" Text="Select the Student Name:"></asp:Label>
<br />
<asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="True" Height="20px" onselectedindexchanged="DropDownList1_SelectedIndexChanged" Width="227px" style="margin-bottom: 0px" DataSourceID="XmlDataSource1" DataTextField="Name" DataValueField="Name" >
</asp:DropDownList>
    <asp:XmlDataSource ID="XmlDataSource1" runat="server" DataFile="~/XMLFile.xml">
    </asp:XmlDataSource>
<br />
<br />
<br />
<br />
<br />
<br />
<asp:Label ID="Label4" runat="server" Font-Size="Small" ForeColor="Red"></asp:Label>
</div>
</form>
</body>
</html>

现在，在 Default.aspx 页面的代码隐藏文件中添加 DropDownList 控件的代码，如 Listing 14.23 所示：

## Listing 14.23: Showing the Code for the Code-Behind File of the Default.aspx Page

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
    }

    protected void DropDownList1_SelectedIndexChanged(object sender, EventArgs e)
    {
        Label4.Text = "You have selected: " + DropDownList1.SelectedItem.Text;
    }
}
```

现在，通过按键盘上的 F5 键运行应用程序。选择产品后的输出如 Figure 14.19 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_741_0.png)

Figure 14.19: DropDownList Control at Runtime

## Using the Image Control

当你在 Web 页面上添加 Image 控件时，它会在 Web 页面的源代码中添加以下代码：

```
<asp:Image ID="Image1" runat="server" />
```

让我们创建一个名为 ImageControl 的应用程序（也可在 CD-ROM 上获得）。你可以通过从工具箱的 Standard 选项卡拖放，或双击工具箱中的此控件，将 Image 控件添加到 Web 页面（Default.aspx）。在本示例中，我们将在 Button 控件的单击事件上显示图像。要将图像与 Image 控件关联，只需将图像的 URL 分配给 Image 控件的 ImageUrl 属性（如果图像文件是项目的本地文件，只需将 ImageUrl 属性设置为图像文件名）。你可以使用 Width 和 Height 属性分别设置图像的宽度和高度。你还可以将 AlternateText 属性设置为在图像因任何原因不可见时要显示的文本。

按照以下步骤操作 Image 控件：

- 1. 在项目文件夹中放置一个图像。
- 2. 在 Default.aspx 文件的设计视图中添加一个 Image 控件并打开属性窗口。
- 3. 在属性窗口中单击其 ImageUrl 属性前面的省略号 (...) 按钮。
- 4. 选择图像对话框打开，如 Figure 5.1 所示。
- 5. 在文件夹内容窗格中选择一个图像并单击确定按钮（Figure 14.20）。

Figure 14.20 显示了如何借助 Select Image 窗口选择图像：

![](img/e073a4882197be4ab61103cbe0bcb394_742_0.png)

## Figure 14.20: Selecting an Image in the Select Image Dialog Box

Listing 14.24 显示了 Image 控件的 Default.aspx 页面：

## Listing 14.24: Showing the Code for the Default.aspx Page

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Image Control Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label1" runat="server" Font-Bold="True" Font-Underline="True"
                Text="Image Control Example"></asp:Label>
            <br />
            <br />
            <br />
            <br />
            <asp:Button ID="Button1" runat="server" BackColor="#000066" Font-Bold="True"
                ForeColor="#66FFFF" Height="51px" OnClick="Button1_Click"
                Text="Click Me to View the Image!" />
            <br />
            <br />
            <asp:Image ID="Image1" runat="server" BorderColor="#660066" Height="300px"
                ImageUrl="~/Tulips.jpg" ToolTip="Image control example" Visible="False"
                Width="300px" />
            &nbsp;
        </div>
    </form>
</body>
</html>
```
```

6. 在 Default.aspx 页面的代码隐藏文件中添加代码，如 Listing 14.25 所示：

## Listing 14.25: Showing the Code for the Code-Behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page {
    protected void Page_Load(object sender, EventArgs e) {
    }
    protected void Button1_Click(object sender, EventArgs e) {
        Image1.Visible = true;
    }
}
```

7. 通过按键盘上的 F5 键运行应用程序。单击 Button 控件后，输出如 Figure 14.21 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_743_0.png)

Figure 14.21: Image Control on Clicking the Button Control

## Using the Calendar Control

当你在 Web 页面（Default.aspx）上添加 Calendar 控件时，它会在 Web 页面的源代码中添加以下代码：

```
<asp:Calendar ID="Calendar1" runat="server"></asp:Calendar>
```

让我们创建一个名为 CalendarControl 的 Web 应用程序（也可在 CD-ROM 上获得）。首先，你必须向 Web 页面添加一个 Calendar 控件。在本示例中，我们还在 Web 页面上放置了一个 TextBox 控件。在此应用程序中，TextBox 控件在页面加载事件上显示当前日期；当你选择任何日期/月份/年份时，它会显示在 TextBox 控件中。Listing 14.26 显示了 Calendar 控件的 Default.aspx 页面：

## Listing 14.26: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Calendar Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="Calendar Control Example" Font-Bold="True" Font-Size="Medium" Font-Underline="True"></asp:Label>
<br />
<br />
<asp:Calendar ID="Calendar1" runat="server" BackColor="#FFFFCC" BorderColor="#FFCC66" BorderWidth="1px" Caption="Select Date and Month:" DayNameFormat="Shortest" Font-Names="Verdana" Font-Size="8pt" ForeColor="#663399" Height="200px" ShowGridLines="True" Width="220px">
<SelectedDayStyle BackColor="#CCCCFF" Font-Bold="True" />
<SelectorStyle BackColor="#FFCC66" />
<OtherMonthDayStyle ForeColor="#CC9966" />
<TodayDayStyle BackColor="#FFCC66" ForeColor="white" />
<NextPrevStyle Font-Size="9pt" ForeColor="#FFFFCC" />
<DayHeaderStyle BackColor="#FFCC66" Font-Bold="True" Height="1px" />
<TitleStyle BackColor="#990000" Font-Bold="True" Font-Size="9pt" ForeColor="#FFFFCC" />
</asp:Calendar>
<br />
<asp:TextBox ID="TextBox1" runat="server" Width="316px"></asp:TextBox>
</div>
</form>
</body>
</html>
```

现在，为 Calendar 控件在 Default.aspx 页面的代码隐藏文件中添加代码，如 Listing 14.27 所示：

## Listing 14.27: Showing the Code for the Code-Behind File of the Default.aspx Page

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
```

