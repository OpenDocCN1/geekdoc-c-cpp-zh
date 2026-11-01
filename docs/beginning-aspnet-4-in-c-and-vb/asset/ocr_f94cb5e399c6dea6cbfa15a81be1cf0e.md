```
protected void cycleButton_Click(object sender, EventArgs e)
{
    rainbowLabel1.Cycle();
}
```

*code snippet PCS Custom C WebSite1/Default.aspx.cs*

Now you can view the sample and cycle the colors in the sample text, as shown in Figure 41-4.

![](bbox=[0.18, 0.32, 0.78, 0.48])

FIGURE 41-4

You can do a lot more with custom controls; indeed, the possibilities are practically limitless, but you will have to experiment with these possibilities on your own.

# MASTER PAGES

Master pages provide an excellent way to make your web sites easier to design. Putting all (or at least most) of your page layout in a single file allows you to concentrate on the more important things for the individual web pages of your site.

Master pages are created in files with the extension .master, and can be added via the Website → Add New Item ... menu item, like any other site content. At first glance, the code generated for a master page is much like that for a standard .aspx page:

```
<%@ Master Language="C#" AutoEventWireup="true"
CodeFile="MyMasterPage.master.cs" Inherits="MyMasterPage" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <asp:ContentPlaceHolder id="head" runat="server">
    </asp:ContentPlaceHolder>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server">
            </asp:ContentPlaceHolder>
        </div>
    </form>
</body>
</html>
```

The differences are:

+   - A <%@ Master %> directive is used instead of a <%@ Page %> directive, although the attributes are the same.
+   - A ContentPlaceHolder control with an ID of head is placed in the page header.
+   - A ContentPlaceHolder control with an ID of ContentPlaceHolder1 is placed in the page body.