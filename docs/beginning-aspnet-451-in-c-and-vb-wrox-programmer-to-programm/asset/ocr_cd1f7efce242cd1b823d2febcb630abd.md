# Exercise 6 Solution

A base page enables you to centralize behavior for all the pages in your site. Instead of recoding the same functionality over and over again in every page, you move this code to the base page so all ASPX pages can use it. When you implement the theme switcher, all you have to do is write some code in the central BasePage class. All pages in your site that inherit from this BasePage class then automatically set the selected theme, without the need for any additional code.

# CHAPTER 7

# Exercise 1 Solution

To change the background color of items in the TreeView control you can use the NodeStyle element as follows:

```
<asp:TreeView ID="TreeView1" runat="server"
    DataSourceID="SiteMapDataSource1" ShowExpandCollapse="False">
    <NodeStyle BackColor="White" />
    ...
</asp:TreeView>
```

Instead of setting the BackColor property (which results in an inline style), you’re better off setting the CssClass property:

```
<NodeStyle CssClass="TreeViewNodeStyle" />
```

You then need to create a separate class in your CSS file:

```
.TreeViewNodeStyle
{
    background-color: White;
}
```

This way, it’s easier to manage the styling from a central location.

# Exercise 2 Solution

To redirect a user to another page programmatically, you can use Response.Redirect, Response.RedirectPermanent, or Server.Transfer. The first two options send a redirect instruction to the browser and are thus considered client-side redirects. Server.Transfer, on the other hand, takes place at the server, enabling you to serve a different page without affecting the user’s address bar.

# Exercise 3 Solution

To display a TreeView that doesn’t have the ability to expand or collapse nodes, you need to set its ShowExpandCollapse property to False.