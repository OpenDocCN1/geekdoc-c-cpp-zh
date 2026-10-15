```
<asp:MenuItem Text="MenuItem1Leaf" value="MenuItem1Leaf"></asp:MenuItem>
</asp:MenuItem>
<asp:MenuItem Text="MenuItem2" value="MenuItem2">
<asp:MenuItem Text="MenuItem2Leaf" value="MenuItem2Leaf"></asp:MenuItem>
<asp:MenuItem Text="MenuItem2Leaf" value="MenuItem2Leaf"></asp:MenuItem>
</asp:MenuItem>
</Items>
<StaticHoverStyle BackColor="#990000" ForeColor="white" />
</asp:Menu>
</div>
</form>
</body>
</html>
```

The output of the MenuControl application is as shown in Figure 15.17:

![](bbox=[0.22, 0.29, 0.77, 0.605])

Figure 15.17: Showing the Output of the MenuControl Example

# Creating Dynamic Menus

In this section, we are going to use the Menu control with the XML and SiteMapDataSource to create dynamic menus, as we did in the TreeViewControl example earlier. We have created an application named DynamicMenuCS (available on CD-ROM). Add the code shown in Listing 15.11 in the default page of the DynamicMenu application:

Listing 15.11: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>DynamicMenu Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:XmlDataSource ID="XmlDataSource1" runat="server" DataFile="~/Data.xml"></asp:XmlDataSource>
```