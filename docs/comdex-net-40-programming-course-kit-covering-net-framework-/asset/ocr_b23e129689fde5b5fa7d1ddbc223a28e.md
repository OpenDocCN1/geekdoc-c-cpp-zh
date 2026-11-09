+   16. Select the **MasterPage** option from the Contents of folder pane (Fig.ASP-8.7).
+   17. Click the **OK** button, as shown in Fig.ASP-8.7:

![](bbox=[0.334, 0.175, 0.689, 0.343])

Fig.ASP-8.7

The **Default.aspx** page is added in the **Solution Explorer** window.

+   18. Replace the code of the **Default.aspx** page with the code shown in Listing 8.2:

# Listing 8.2: Showing the Code for the Default.aspx Page

```
```aspx
<%@ Page Title="" Language="C#" MasterPageFile="~/Master.master"
    AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="Default" %>
<asp:Content ID="Content1" ContentPlaceHolderID="ContentPlaceHolder1"
    Runat="Server">
    Enter your name in the text box<br />
    <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox><br />
    <br />
    <asp:Button ID="Button1" runat="server" Text="Click to submit"
    OnClick="Button1_Click" />
    <br />
    <asp:Label ID="Label1" runat="server" Text="Label"></asp:Label>
</asp:Content>
```
```

In Listing 8.2, we have used the **MasterPageFile** attribute of the @Page directive to inherit the layout of the master page.

+   19. Select the **Design** tab to view the design page of the **Default.aspx** page. The layout you have defined in the master page has been incorporated in the content page (**Default.aspx**), as shown in Fig.ASP-8.8.

![](bbox=[0.357, 0.632, 0.666, 0.846])

Fig.ASP-8.8