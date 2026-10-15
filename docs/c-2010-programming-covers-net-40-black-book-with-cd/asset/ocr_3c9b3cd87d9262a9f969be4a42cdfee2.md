# Immediate Solutions

# Using the Login and LoginView Controls

You learned about the Login and LoginView controls in detail in the In Depth section of the chapter. Now, let's perform the following steps to implement these controls:

Create a website named LoginandLoginViewControls (also available in the CD).

# NOTE

> The applications in this chapter are created using the Empty Web Site template in the New Web Site dialog box. After creating the application, you need to add the Default.aspx page to the application.

Now, open the Default.aspx file of the LoginandLoginViewControls website and replace the existing code with the code shown in Listing 16.1:

# Listing 16.1: Code of Default.aspx File

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Login and LoginView Controls Example</title>
</head>
<body>
<form id="form1" runat="server">
<h1># 2010 Black Book</h1>
<br />
<asp:LoginView ID="LoginView1" runat="server">
<LoggedInTemplate>
<br />
<font color="navy">welcome!!! You have successfully logged in.</font>
</LoggedInTemplate>
<AnonymousTemplate>
<strong>You are not logged in. Please Login.<br /></strong>
<br />
<asp:Login ID="Login1" runat="server" BackColor="#FFE0C0" BorderColor="ControlText" BorderPadding="4" BorderStyle="Solid" BorderWidth="1px" Font-Names="Garamond" ForeColor="#333333">
<TitleTextStyle BackColor="Maroon" Font-Bold="True" Font-Size="0.9em" ForeColor="White" />
<LoginButtonStyle BackColor="White" BorderColor="#0000C0" BorderStyle="Solid" BorderWidth="1px" Font-Names="Verdana" ForeColor="#284E98" />
<InstructionTextStyle Font-Italic="True" ForeColor="Black" />
</asp:Login>
</AnonymousTemplate>
</asp:LoginView>
<br />&nbsp;
</form>
</body>
</html>
```