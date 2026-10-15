# Listing 36.26: Showing the Code for the Login.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Login.aspx.cs" Inherits="Login" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>The Login Page</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<strong><span style="color: #000099; text-decoration: underline">Enter your information</span></strong><br />
<br />
<table style="border-left-color: black; border-bottom-color: black; border-top-style: solid; border-top-color: black; border-right-style: solid; border-left-style: solid; border-right-color: black; border-bottom-style: solid" bgcolor="#ffcc99" id="TABLE1">
<tr>
<td style="width: 100px; height: 21px">
<strong><span style="text-decoration: underline">User Name:</span></strong></td>
<td style="width: 100px; height: 21px">
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox></td>
</tr>
<tr>
<td style="width: 100px">
<strong><span style="text-decoration: underline">Password:</span></strong></td>
<td style="width: 100px">
<asp:TextBox ID="TextBox2" runat="server" TextMode="Password" Width="151px"></asp:TextBox></td>
</tr>
<tr>
<td style="width: 100px"></td>
<td style="width: 100px">
<asp:Button ID="Button1" runat="server" Text="Validate" OnClick="Button1_Click" /></td>
</tr>
</table>
<asp:Label ID="Label1" runat="server"></asp:Label>
</div>
</form>
</body>
</html>
```

6. Add the code in the code-behind file of the Login.aspx page. Listing 36.27 shows the code for the code behind file of the Login.aspx page to validate and retrieve a user:

# Listing 36.27: Showing the Code for the Code-Behind File of the Login.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Web.Security;
public partial class Login : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        MembershipCreateStatus status;
```