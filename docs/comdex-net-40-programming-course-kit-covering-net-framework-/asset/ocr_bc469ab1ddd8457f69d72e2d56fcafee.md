```
```aspx
<asp:ContentPlaceHolder ID="ChildPage" runat="server">
</asp:ContentPlaceHolder>
```
```

In Listing 8.5, we have created a child master page, **Child.master**, by inheriting it from the **Parent.master** page using the `MasterPageFile="~/Parent.master"` attribute of the **@ Master** directive. The **Child.master** master page displays the message, **This is Child Master Page.**

+   20. *Right-click* the project in **Solution Explorer** and select **Add New Item** from the context menu. The **Add New Item** dialog box opens.
+   21. Select the **Web Form** option from the middle pane of the **Add New Item** dialog box.
+   22. Select the **Select master page** check box.
+   23. *Click* the **Add** button. The **Select a Master Page** dialog box opens.
+   24. Select the **Child.master** from the **Contents of folder** pane and click the **OK** button. The **Default.aspx** page is added to the **Solution Explorer** window.
+   25. *Replace* the code of the **Default.aspx** page with the code shown in Listing 8.6.

**Listing 8.6:** Showing the Code for the **Default.aspx** Page

```
```aspx
<%@ Page Title="" Language="C#" MasterPageFile="~/Child.master"
    AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!-- Add content controls here -->
<asp:Content ID="Content1" ContentPlaceHolderID="ChildPage" Runat="Server">
    Enter your name in the text box<br />
    <br />
    <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox><br />
    <br />
    <asp:Button ID="Button1" runat="server" Text="Click to Submit"
        OnClick="Button1_Click" />
    <br />
    <asp:Label ID="Label1" runat="server" Text="Label"></asp:Label>
</asp:Content>
```
```

In Listing 8.6, we have used the **MasterPageFile** attribute of the **@Page** directive to inherit the **Child.master** page, which itself is inherited from the **Parent.master** master page. Now, the **Default.aspx** page inherits the layout of both the master pages, **Parent.master** and **Child.master**. This shows a nested master page hierarchy.

+   26. Select the **Design** tab to view the design of the **Default.aspx** page, as shown in Fig.ASP-8.14:

![](bbox=[0.34, 0.605, 0.684, 0.859])