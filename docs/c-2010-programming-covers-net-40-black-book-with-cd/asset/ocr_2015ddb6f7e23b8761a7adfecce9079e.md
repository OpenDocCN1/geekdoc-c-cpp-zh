# Creating SiteMapPath

We have aforementioned in the In Depth section of this chapter, that the SiteMapPath control can be automatically configured to the SiteMapDataSource control, which, in turn, can read the Web.sitemap file to display the data on the application. We have created an application named SiteMapPathControl. You can find this application on the CD-ROM as SiteMapPathControlCS.

To create Web.sitemap in the SiteMapPathControl application, right-click the Project name. A context menu appears. Select the Add New Item option from the context menu. The Add New Item dialog box appears, shown earlier in Figure 15.14. Select Site Map from the options available. This will create a new Web.sitemap file in the project.

The Web.sitemap file consists of navigational details for an application. You can set the title, URL, and other information for each page by using the Web.sitemap file. Add the code shown in Listing 15.14 in the Web.sitemap file:

# Listing 15.14: Showing the Code for the Web.sitemap File

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
  <siteMapNode url="default.aspx" title="Home Page" description="" >
    <siteMapNode url="page1.aspx" title="Section 1" description="" />
    <siteMapNode url="page2.aspx" title="Section 2" description="" />
  </siteMapNode>
</siteMap>
```

You also need to add the code shown in Listing 15.15 in the Default.aspx page of this application:

# Listing 15.15: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>SiteMapPath Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="SiteMapDataSource Example"/><br />
<asp:SiteMapPath ID="SiteMapPath1" runat="server" Font-Names="Verdana" Font-Size="0.8em" PathSeparator=" : " PathDirection="CurrentToRoot">
<PathSeparatorStyle Font-Bold="True" ForeColor="#5D7B9D" />
<CurrentNodeStyle ForeColor="#333333" />
<NodeStyle Font-Bold="True" ForeColor="#7C6F57" />
<RootNodeStyle Font-Bold="True" ForeColor="#5D7B9D" />
</asp:SiteMapPath>
<br />
<br />
<asp:HyperLink ID="HyperLink1" runat="server" NavigateUrl="~/Page1.aspx">Go to Page 1</asp:HyperLink>
<asp:HyperLink ID="HyperLink2" runat="server" NavigateUrl="~/Page2.aspx">Go to Page 2</asp:HyperLink><br />
</div>
</form>
</body>
</html>
```