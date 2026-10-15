2. Add the following controls to the Default.aspx page to design the interface of the UsingSimpleInterestWebService Web application:

+   - Five Label Controls—Set the Text property of four Label controls to Principal, Rate, Duration, and Simple Interest, respectively. Clear the Text property of the fifth Label control.

+   - Four Text Box Controls—Set the ID properties of the Text Box controls to txtPrincipal, txtRate, txtDuration, and txtSimpleInterest, respectively.

+   - A Button Control—Set this control’s Text property to CalculateSimpleInterest.

3. Now add the code, shown in Listing 18.13, in the Default.aspx page of the UsingSimpleInterestWebService Web application:

# Listing 18.13: Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<strong><span style="text-decoration: underline"><em>Calculate Simple Interest using the Web Service<br /></em></span></strong>
<br />
<asp:Label ID="Label1" runat="server" Text="Principal" Width="66px"></asp:Label>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<asp:TextBox ID="txtPrincipal" runat="server"></asp:TextBox><br />
<asp:Label ID="Label2" runat="server" Text="Rate" Width="63px"></asp:Label>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<asp:TextBox ID="txtRate" runat="server"></asp:TextBox><br />
<br />
<asp:Label ID="Label3" runat="server" Text="Duration" Width="63px"></asp:Label>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<asp:TextBox ID="txtDuration" runat="server"></asp:TextBox>
<br />
<br />
<asp:Label ID="Label4" runat="server" Text="Simple Interest" Width="105px"></asp:Label>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<asp:TextBox ID="txtSimpleInterest" runat="server"></asp:TextBox><br />
<br />
<asp:Label ID="Label5" runat="server" Width="66px"></asp:Label>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<asp:Button ID="Button1" runat="server" Text="Calculate Simple Interest" Width="220px" onclick="Button1_Click" />
</div>
</form>
</body>
</html>
```

4. Right-click the UsingSimpleInterestWebService Web application in Solution Explorer and select the Add Web Reference option from the context menu to display the Add Web Reference dialog box (Figure 18.19).