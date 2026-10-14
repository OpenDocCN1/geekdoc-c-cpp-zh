# The aspx code for a new child master page that uses a master page like the one in figure 9-4 as its parent

```
<%@ Master Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeFile="ChildMasterPage.master.cs"
    Inherits="ChildMasterPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="head" Runat="Server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="Main" Runat="Server">
</asp:Content>
```

# The aspx code after content has been added to the page

```
<%@ Master Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeFile="ChildMasterPage.master.cs"
    Inherits="ChildMasterPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="HeadContent" Runat="Server">
    <link href="Styles/Child.css" rel="stylesheet" type="text/css" />
    <asp:ContentPlaceHolder ID="HeadContent" runat="server">
    </asp:ContentPlaceHolder>
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" Runat="Server">
    <div id="main">
        <asp:ContentPlaceHolder ID="MainContent" runat="server">
        </asp:ContentPlaceHolder>
    </div>
    <p id="message">
        <asp:Label ID="lblMessage" runat="server"></asp:Label>
    </p>
</asp:Content>
```

# Description

+   - When you create *nested master pages*, the *parent master page* is typically used to provide elements for every page in the web site. Then, different *child master pages* can be used to provide additional elements for different types of pages in the web site.
+   - To create a child master page, use the technique in figure 9-2 for creating a master page, but check the Select Master Page check box and then select the parent master page from the dialog box that’s displayed.
+   - To add content to a child master page, place the content between the start and end tags of the Content elements. Use ContentPlaceHolder controls to identify areas where content can be added in content pages that use the master page.
+   - When you use nested master pages, you can create content pages for the parent master page or any of the child master pages.