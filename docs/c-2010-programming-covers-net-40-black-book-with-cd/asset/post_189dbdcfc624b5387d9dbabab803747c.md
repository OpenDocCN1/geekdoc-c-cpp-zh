
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

Now, add the code in the code-behind file of the Default.aspx page for the DropDownList controls, as shown in Listing 14.23:

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

Now, run the application by pressing the F5 key on the keyboard. The output after selecting a product is as shown in Figure 14.19:

![](img/e073a4882197be4ab61103cbe0bcb394_741_0.png)

Figure 14.19: DropDownList Control at Runtime

## Using the Image Control

When you add an Image control on a Web page, it adds the following code to the source code of the Web page:

```
<asp:Image ID="Image1" runat="server" />
```

Let’s create applications named ImageControl (also available on the CD-ROM). You can add an Image control to a Web page (Default.aspx) either by dragging and dropping it from the Standard tab of the Toolbox or by double-clicking this control in the Toolbox. In this example, we will display the image on the click event of a Button control. To associate an image with an Image control, you just assign the image’s URL to the Image control’s ImageUrl property (if the image file is local to the project, you just set the ImageUrl property to the name of the image file). You can set the image’s width and height with the Width and Height properties, respectively. You can also set the AlternateText property to the text that you want to show in case your image is not visible due to any reason.

Perform the following steps to work with an Image control:

- 1. Place an image in the project folder.
- 2. Add an Image control in the Design view of the Default.aspx file and open the Properties window.
- 3. Click the ellipsis (...) button in front of its ImageUrl property in the Properties window.
- 4. The Select Image dialog box opens, as shown in Figure 5.1.
- 5. Select an image in the Contents of folder pane and click the OK button (Figure 14.20).

Figure 14.20 displays how to select an image with the help of Select Image window:

![](img/e073a4882197be4ab61103cbe0bcb394_742_0.png)

## Figure 14.20: Selecting an Image in the Select Image Dialog Box

Listing 14.24 shows the Default.aspx page for the Image controls:

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

6. Add the code in the code-behind file of the Default.aspx page, as shown in Listing 14.25:

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

7. Run the application by pressing the F5 key on the keyboard. After clicking the Button control, the output is as shown in Figure 14.21:

![](img/e073a4882197be4ab61103cbe0bcb394_743_0.png)

Figure 14.21: Image Control on Clicking the Button Control

## Using the Calendar Control

When you add a Calendar control on a Web page (Default.aspx), it adds the following code to the source code of the Web page:

```
<asp:Calendar ID="Calendar1" runat="server"></asp:Calendar>
```

Let’s create a Web application named CalendarControl (also available on the CD-ROM). First, you have to add one Calendar control to the Web page. In this example, we have also placed one TextBox control on the Web page. In this application, the TextBox control displays the current date on the page load event; when you select any date/month/year, it is displayed in the TextBox control. Listing 14.26 shows the Default.aspx page for the Calendar controls:

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

Now, add the code in the code-behind file of the Default.aspx page for the Calendar controls, as shown in Listing 14.27:

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
