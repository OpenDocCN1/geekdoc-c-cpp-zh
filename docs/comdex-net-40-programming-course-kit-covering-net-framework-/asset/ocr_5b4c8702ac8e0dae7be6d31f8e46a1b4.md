+   17. Right-click the application name in the **Solution Explorer** window and select the **Add Service Reference** option from the context menu. The **Add Service Reference** dialog box opens (Fig.ASP-10.39). Click the **Discover** button (Fig.ASP-10.39).

+   18. A list of available WCF service references is displayed in the **Address** text box (Fig.ASP-10.40). Click the **Go** button (Fig.ASP-10.40).

![](bbox=[0.194, 0.215, 0.499, 0.409])

![](bbox=[0.521, 0.215, 0.831, 0.409])

+   19. The **NORTHWINDEntities** service reference is displayed (Fig.ASP-10.41). *Write* a name for the service reference in the **Namespace** text box, which in this case is **ServiceReference1**, as shown in Fig.ASP-10.41.

+   20. *Click* the **OK** button to add the service reference to the application, as shown in Fig.ASP-10.41:

![](bbox=[0.356, 0.494, 0.665, 0.686])

Now, you need to create a client that can consume the data services.

+   21. *Write* the code, shown in Listing 10.7, in the **Default.aspx** file:

# **Listing 10.7:** Code for the **Default.aspx** File

```
```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <asp:GridView ID="GridView1" runat="server" BackColor="White"
        BorderColor="#CC9966" BorderStyle="None" BorderWidth="1px"
        CellPadding="4">
        <FooterStyle BackColor="#FFFFCC" ForeColor="#330099" />
        <HeaderStyle BackColor="#990000" Font-Bold="True" ForeColor="#FFFFCC" />
```
```