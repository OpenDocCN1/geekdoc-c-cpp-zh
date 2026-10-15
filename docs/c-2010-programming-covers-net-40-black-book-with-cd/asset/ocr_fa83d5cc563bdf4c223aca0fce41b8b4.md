# Creating the ConnectionsZone Control in Code

We discussed the working of the ConnectionsZone control in the In Depth section of this chapter. We also discussed how to use the ConnectionsZone class to create the ConnectionsZone control. Now, let's create the ConnectionsZone control with the help of the ConnectionsZone class and specify the various properties of the control. For this, we create an application named ConnectionsZoneApp (also available in the CD). Listing 16.19 shows the complete code for the Default.aspx page of the ConnectionsZoneApp website:

Listing 16.19: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>ConnectionsZone control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label2" runat="server" Font-Bold="True" Font-Underline="True" ForeColor="Navy" Text="ConnectionZone Webpart:"></asp:Label>
<br />
<br />
<asp:Panel ID="Panel1" runat="server" BackColor="#FFE0C0" BorderStyle="Ridge" Height="161px" Width="437px">
<asp:Label ID="Label1" runat="server" Text="Connection Status:" Width="622px" Font-Bold="True" Font-Underline="True" ForeColor="Navy"></asp:Label><br />
&nbsp;<asp:Label ID="Label3" runat="server" Text="Label"></asp:Label>
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<asp:Label ID="Label5" runat="server" Font-Bold="True" Font-Underline="True" ForeColor="Navy" Text="Connection Configuration:"></asp:Label>
<br />
<br />
<asp:Label ID="Label4" runat="server" Text="Label"></asp:Label>&nbsp;
<br />
<asp:Label ID="Label6" runat="server" Text="Label"></asp:Label></asp:Panel>
</div>
</form>
</body>
</html>
```

Listing 16.20 shows the complete code for the code-behind file of the Default.aspx page of the ConnectionsZoneApp website:

Listing 16.20: Showing the Code for the Code-Behind File of the Default.aspx Page

```
using System;
using System.Configuration;
```