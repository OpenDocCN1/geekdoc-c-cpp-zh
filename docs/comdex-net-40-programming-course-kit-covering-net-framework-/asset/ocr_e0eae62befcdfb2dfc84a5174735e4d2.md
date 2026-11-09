Add the code, shown in Listing 8.14, in SkinFile.skin file:

# **Listing 8.14:** Showing the Code for the **SkinFile.skin** File

```
```aspx
<asp:Table runat="server" width="100px" font-bold="False" font-size="Medium"
    forecolor="Green" />

<asp:button runat="server" forecolor="Blue" backcolor="Gray"/>

<asp:textbox runat="server" font-bold="False" font-size="Medium" forecolor="Red"
    backcolor="Silver" font-style="True"/>
```
```

In Listing 8.14, we have specified the style of controls.

+   11. *Right-click* the project name in **Solution Explorer** and select **Add New Item** from the context menu. The **Add New Item** dialog box opens.
+   12. *Select* **Web Form** from the middle pane of the **Add New Item** dialog box.
+   13. *Click* the **Add** button to add the **Default.aspx** page to your project.
+   14. *Replace* the code of the **Default.aspx** page with the code shown in Listing 8.15:

# **Listing 8.15:** Showing the Code for the **Default.aspx** Page of the **StyleSheetThemesAttribute** Application

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
    Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label1" runat="server" BackColor="#666633"
                ForeColor="Yellow"
                Text="Label" Width="200px"></asp:Label> <br />
            <br />
            <asp:Label ID="Label2" runat="server" Text="Enter Name"></asp:Label>
            &nbsp;&nbsp;
            <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>

            <br />
            <br />

            <asp:Label ID="Label3" runat="server" Text="Address"></asp:Label>
            &nbsp;&nbsp;
            <asp:TextBox ID="TextBox2" runat="server"></asp:TextBox>
            <br />
            <br />
                &nbsp;&nbsp;&nbsp;&nbsp;
            <asp:Button ID="Button1" runat="server" Text="Submit" />
        </div>
    </form>
</body>
</html>
```
```

The design of your page is shown in Fig.ASP-8.24: