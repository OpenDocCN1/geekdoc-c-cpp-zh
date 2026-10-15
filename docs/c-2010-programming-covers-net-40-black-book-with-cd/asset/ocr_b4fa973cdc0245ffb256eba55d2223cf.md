5. Open the Default.aspx page and replace its existing code with the code shown in Listing 18.29:

# Listing 18.29: Code of the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<asp:ScriptManager ID="ScriptManager1" runat="server">
<Services>
<asp:ServiceReference Path="~/webservice.asmx" />
</Services>
</asp:ScriptManager>
<div style="border-style: double; background-color: Gray; font-size: large; width:350px;">
<asp:Label ID="Label1" runat="server"></asp:Label>
<div>
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
<ContentTemplate>
<div style="border-style: dotted; background-color: Silver; font-size: larger; width: 300px;">
<asp:Label ID="Label2" runat="server"></asp:Label>
<asp:Button ID="Button1" runat="server" Text="Partial Update" />
</div>
<br />
</ContentTemplate>
</asp:UpdatePanel>
<asp:Button ID="Button2" runat="server" Text="Full Update" />
</div>
</div>
</form>
</body>
</html>
```

6. Open the code-behind file of the Default.aspx page and replace its existing code with the code shown in Listing 18.30:

# Listing 18.30: Code of the Code-Behind File of the Default.aspx Page

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
        WebService ts = new WebService();
        Label1.Text = ts.GetServerTime().ToString();
        Label2.Text = ts.GetServerTime().ToString();
    }
}
```

In Listing 18.30, you can see that we have created an object of the WebService Web service with the name ts. Through the ts object, we are able to access the GetServerTime method of the WebService Web service.

7. Now, make the Default.aspx page your start-up page, right-click the Default.aspx page, and select the Set As Start Page option from the context menu.

8. Press the F5 key on the keyboard to execute the application. The output of the Web application appears (Figure 18.32).