# The aspx code for a new page that uses the master page in figure 9-4

```
<%@ Page Language="C#" MasterPageFile="~/Site.master" AutoEventWireup="true" CodeFile="Order.aspx.cs" Inherits="Order" Title="Untitled Page" %>

<asp:Content ID="Content1" ContentPlaceHolderID="HeadContent" runat="Server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="Server">
</asp:Content>
```

# Two ways to create a new content page

+   - Choose the Website→Add New Item command. Then, select the Web Form template, enter the name for the form, check the Select Master Page check box, and click Add. When the Select a Master Page dialog box appears, select the master page you want and click OK.
+   - Select the master page in the Solution Explorer, then choose the Website→Add Content Page command.

# How to convert a regular ASP.NET page to a content page

+   - First, add a MasterPageFile attribute to the Page directive that specifies the URL of the master page. Next, replace the div element that contains the actual content of the page with an ASP.NET Content element like the second one shown above. Then, if the head element contains other elements used by the page, replace the head element with a Content element like the first one shown above. Last, delete everything that’s outside the Content elements except for the Page directive.

# Two other ways to specify the master page

# In the web.config file

```
<system.web>
  <pages masterPageFile="Site.master" />
</system.web>
```

# In the Page_PreInit method

```
protected void Page_PreInit(object sender, EventArgs e)
{
    MasterPageFile = "Site.master";
}
```

# Description

+   - The Page directive in the aspx code for a content page includes a MasterPageFile attribute that specifies the name of the master page.
+   - The aspx code for a content page includes Content elements that indicate the IDs of the content placeholders where the content for the page should be placed. Any content you create for the page should be coded between the start and end tags for these elements.
+   - You can also specify the master page in the web.config file or in the Page_PreInit method. However, the Web Forms Designer doesn’t support either of these techniques, so you won’t be able to view the content page in Design view.