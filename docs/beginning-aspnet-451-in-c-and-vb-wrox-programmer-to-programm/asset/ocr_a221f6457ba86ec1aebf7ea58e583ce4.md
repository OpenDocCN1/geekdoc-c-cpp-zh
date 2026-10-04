Just like a normal ASPX page, a master page can have a Code Behind file, identified by its CodeFile and Inherits attributes:

# VB.NET

```
<@ Master Language="VB" CodeFile="Frontend.master.vb"\nInherits="MasterPages" %>
```

# C#

```
<@ Master Language="C#" AutoEventWire="true" CodeFile="Frontend.master.cs"\nInherits="MasterPages" %>
```

To create regions that content can fill in, you define ContentPlaceHolder controls in your page like this:

```
<asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server"/>
```

You can create as many placeholders as you like, although you usually only need few to create a flexible page layout.

The content pages, which are essentially normal ASPX files, without the code that they're going to take from your master page, are connected to a master page using the MasterPage attribute of the MasterPage directive:

# VB.NET

```
<@ Page Title=" Language="VB" MasterPageFile="~/MasterPages/Frontend.master"\nAutoEventWire="false" CodeFile="Default.aspx.vb" Inherits="_Default %>
```

# C#

```
<@ Page Title=" Language="C#" MasterPageFile="~/MasterPages/Frontend.master"\nAutoEventWire="true" CodeFile="Default.aspx.cs" Inherits="_Default %>
```

The page-specific content is put inside a Content control that points to the ContentPlaceHolder:

```
<asp:Content ID="Content1" ContentPlaceHolderID="ContentPlaceHolder1"\nrunat="Server"/></asp:Content>
```

Note that the ContentPlaceHolderID attribute of the Content control points to the ContentPlaceHolder that is defined in the master page. Right now it points to the default name of ContentPlaceHolder1, but in a later exercise you see how to change this.

At run time, when the page is requested, the markup from the master page and the content page are
merged, and sent to the browser. Figure 6-1 shows a diagram of the master page with just
one ContentPlaceHolder and the content page results in that final page is sent to the browser.

To see this process in action, the following sections guide you through creating master and content
pages.