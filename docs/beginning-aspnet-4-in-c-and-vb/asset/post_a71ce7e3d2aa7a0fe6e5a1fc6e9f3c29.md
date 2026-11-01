
```
protected void cycleButton_Click(object sender, EventArgs e)
{
    rainbowLabel1.Cycle();
}
```

*code snippet PCS Custom C# WebSite1/Default.aspx.cs*

Now you can view the sample and cycle the colors in the sample text, as shown in Figure 41-4.

![](img/d7d2ffa0a76feaab821930e95daace93_1256_0.png)

FIGURE 41-4

You can do a lot more with custom controls; indeed, the possibilities are practically limitless, but you will have to experiment with these possibilities on your own.

## MASTER PAGES

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

- A <%@ Master %> directive is used instead of a <%@ Page %> directive, although the attributes are the same.
- A ContentPlaceHolder control with an ID of head is placed in the page header.
- A ContentPlaceHolder control with an ID of ContentPlaceHolder1 is placed in the page body.

The ContentPlaceHolder controls are what make master pages so useful. You can have any number of these on a page, and they are used by .aspx pages using the master page to “plug in” content. You can put default content inside a ContentPlaceHolder control, but .aspx pages can override this content.

For an .aspx page to use a master page, you need to modify the <%@ Page %> directive as follows:

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
Inherits="_Default" MasterPageFile="~/MyMasterPage.master"
Title="Page Title" %>
```

Here you have added two new attributes: a MasterPageFile attribute saying which master page to use and a Title attribute that sets the content of the <title> element in the master page.

Or, when you add an .aspx page to a web site that contains master pages, you can choose to select a master page. The Add New Item Wizard contains a “Select master page” check box, and if you select this option, the next page of the wizard gives you a list of master pages to choose from in the web application. The generated code for the page will then include the MasterPageFile attribute as previously described.

The .aspx page doesn’t have to contain any other code, if you want to use the default master page content. Also, you must not include a Form control, because a page may only have one of these and there is one in the master page.

.aspx pages that use a master page can contain no root-level content other than directives, script elements, and Content controls. You can have as many Content controls as you like, where each one inserts content into one of the ContentPlaceHolder controls in the master page. The only thing to look out for is to make sure that the ContentPlaceHolderID attribute of the Content control matches the ID of the ContentPlaceHolder control where you want to insert content. So, to add content into the master page shown earlier, you would simply need the following in the .aspx file:

```
<%@ Page Language="C#" MasterPageFile="~/MyMasterPage.master"
AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="__Default"
Title="Untitled Page" %>

<asp:Content ID="Content1" ContentPlaceHolderID="head" runat="Server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceHolder1"
runat="Server">
Custom content!
</asp:Content>
```

The true power of master pages comes when you surround the ContentPlaceHolder controls in your master pages with other content, such as navigation controls, site logos, and HTML. You can supply multiple ContentPlaceHolder controls for main content, sidebar content, footer text, and so on.

You can omit Content controls on a page if you do not wish to supply content for a specific ContentPlaceHolder. For example, you can remove the Content1 control from the preceding code without affecting the resultant display.

### Accessing Master Page Content from Web Pages

When you add a master page to a web page, you will sometimes need to access the master page from code in your web page. To do this, you can use the Page.Master property, which will return a reference to the master page in the form of a MasterPage object. You can cast this to the type of the master page as defined by the master page file (for the example in the previous section, this class would be called MyMasterPage). After you have this reference, you can access any public members of the master page class.

Also, you can use the MasterPage.FindControl() method to locate controls on the master page by their identifier. This enables you to manipulate control on the master page that is outside of content placeholders.

One typical use of this might be if you define a master page that is used for a standard form, with a submit button. You can locate the submit button in the child page and add an event handler for the submit button in the master page. In this way, you can provide, for example, custom validation logic in response to a form submission.

### Nested Master Pages

The “Select master page” option is also available when you create a new master page. By using this option, you can create a nested master page that is based on a parent master page. For example, you can create a master page called MyNestedMasterPage that uses MyMasterPage as follows:

```aspx
<%@ Master Language="C#" MasterPageFile="~/MyMasterPage.master"
    AutoEventWireup="false" CodeFile="MyNestedMasterPage.master.cs"
    Inherits="MyNestedMasterPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="head" Runat="Server">
    <!--Disabled for child controls.-->
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceHolder1"
    Runat="Server">
    First nested place holder:
    <asp:ContentPlaceHolder ID="NestedContentPlaceHolder1" runat="server">

    </asp:ContentPlaceHolder>
    <br />
    <br />
    Second nested place holder:
    <asp:ContentPlaceHolder ID="NestedContentPlaceHolder2" runat="server">

    </asp:ContentPlaceHolder>
</asp:Content>
```

Pages that use this master page would supply content for NestedContentPlaceHolder1 and NestedContentPlaceHolder2, but would not have direct access to the ContentPlaceHolder controls specified in MyMasterPage. In this example, MyNestedMasterPage fixes the content for the head control and supplies a template for the ContentPlaceHolder1 control.

By creating a family of nested master pages, you can provide alternate layouts for pages while leaving some aspects of the base master pages untouched. For example, the root master page might include navigation and basic layout, and nested master pages could provide layouts with different amounts of columns. You could then use the nested master pages in the pages of your site and quickly switch between these alternate layouts on different pages.

### Master Pages in PCSDemoSite

In PCSDemoSite, the single master page MasterPage.master (the default name for a master page) is used, with code as follows:

```aspx
<%@ Master Language="C#" AutoEventWireup="true"
    CodeFile="MasterPage.master.cs"
    Inherits="MasterPage" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN"
    "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <link rel="stylesheet" href="StyleSheet.css" type="text/css" />
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div id="header">
            <h1><asp:Literal ID="Literal1" runat="server"
                Text="<%$ AppSettings:SiteTitle %>" /></h1>
            <asp:SiteMapPath ID="SiteMapPath1" runat="server"
                CssClass="breadcrumb" />
        </div>
```
