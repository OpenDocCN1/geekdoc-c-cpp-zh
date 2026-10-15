# Using the Label Control

When you add a Label control on a Web page, the following code is added to the source code of the Web page:

```
<asp:Label ID="Label1" runat="server" Text="Label1"></asp:Label>
```

Now, let's create a Web application named LabelControl (also available in CD-ROM) to show the working of the Label control. You can add a Label control to a Web page either by dragging and dropping it from the Standard tab of the Toolbox or by double-clicking it in the Toolbox. In these applications, we are setting the Text and BackColor properties of a Label control at the Page_Load event. Listing 14.5 shows the code of Default.aspx page for the Label controls:

# Listing 14.5: Showing the Code of the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Label Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="Example showing some of the properties of the Label Control" Font-Bold="True" Font-Underline="True"></asp:Label>
<br />
<br />
<asp:Label ID="Label3" runat="server"></asp:Label>
<br />
<br />
<asp:Label ID="Label4" runat="server"></asp:Label>
<br />
</div>
</form>
</body>
</html>
```

Now, add the code, shown in Listing 14.6, in the code-behind file of the Default.aspx page:

# Listing 14.6: Showing the Code of the Code-behind File of the Default.aspx Page

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
        Label3.Text = "Welcome to the world of ASP.NET 4.0";
        Label4.Text = "I have Olive Color";
        Label4.BackColor = System.Drawing.Color.Olive;
    }
}
```