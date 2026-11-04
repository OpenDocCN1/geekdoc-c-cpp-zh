but we could be reading from a Web service, a database, or even calculating the values. Images can be listed from a directory. Text could be generated and read into a table. The options are endless.

# Panels and multiviews

Managing all these text blocks and images can be rough. ASP.NET provides a number of tools that help, including the two following tools.

+   - **Panels** are just divs that you can manage in code-behind. Just like the text and images we added earlier, panels can be named and controlled in C#. The server will process changes before it sends the HTML to the browser. This helps to break the content into manageable groups.
+   - **Multiviews** are essentially containers that hold a lot of panels. You can use them for wizards and tag groupings. They help to manage the panels, which help manage the content. For more information, search MSDN for ASP.NET Multiview.

From the client's perspective, panels and multiviews are effectively the same structure, but they provide developers with a few options. For instance, the multiview shows one view only of itself by default, whereas you have to hide panels that are not in use.

# Tables

Tables work like other Web controls. In HTML, you have the basic <table>, <tr>, and <td> tags. In ASP.NET there is a Table control, with TableRows and TableCells. If you add an ASP.NET table, it looks like this:

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Tables.aspx.cs" Inherits="Chapter3.Tables" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Table ID="Table1" runat="server">
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
<asp:TableRow runat="server">
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
<asp:TableCell runat="server"></asp:TableCell>
</asp:TableRow>
</asp:Table>
</form>
</body>
```