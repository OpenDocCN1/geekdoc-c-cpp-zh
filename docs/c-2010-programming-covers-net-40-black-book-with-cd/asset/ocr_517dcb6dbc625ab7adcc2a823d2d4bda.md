![](bbox=[0.035, 0.066, 0.92, 0.447])

# Figure 22.30: Displaying EDM of the Publisher Database

3. Replace the code for the Default.aspx page with that given in Listing 22.2 to add the controls required for the application. Listing 22.2 shows the code for the Default.aspx page:

# Listing 22.2: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Entity Framework Application</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
        </div>
        <br />
        Demo showing the use of Entity Framework in database application<br />
        <br />
        ------------------------------------------------------------
        <br />
        <i>Select the Author Name from the Drop - Down list to view the books associated with author<br />
        <br />
        </i><br />
        <i>Author Name</i>
        <asp:DropDownList ID="DropDownList1" runat="server" DataSourceID="AuthorName" DataTextField="FirstName" DataValueField="AuthorID" AutoPostBack="True" Height="20px" Width="80px" onselectedindexchanged="DropDownList1_SelectedIndexChanged">
```