1. Open the master page in Markup View and locate the `MainContent <section>` element. Right after its opening tag, and before the `<asp:ContentPlaceHolder>` tag, press Enter to create some room and drag a `SiteMapPath` from the Toolbox. Right after the `SiteMapPath` add two line breaks (`<br />`). You should end up with code like this:

```
<section id="MainContent">
<asp:SiteMapPath ID="SiteMapPath1" runat="server"></asp:SiteMapPath><br /> </br />
<asp:ContentPlaceHolder ID="cpMainContent" runat="server">
```

2. Save the changes and then request `Default.aspx` in the browser. Note that the page now shows the path from the root of the site (identified by the Home text) to the current page. Click a few of the items in the Menu or TreeView control to navigate around the site and you'll see the breadcrumb change for each page. Figure 7-11 shows the breadcrumb for the All Reviews page in Firefox. The All Reviews page is a subelement of Reviews, which in turn falls under the Home root element.

![](bbox=[0.14, 0.48, 0.9, 0.7])

FIGURE 7-11

When you navigate to one of the subpages, you can click the elements of the path to go up one or more levels. Clicking Reviews in the page shown in Figure 7-11 takes you back to the main Reviews page, and clicking Home takes you back to the root of the site.

3. Using the Theme selector, switch to the other theme. Note that the `SiteMapPath` looks pretty much the same, except for the color of the links, which are defined in the CSS file of each theme.

# How It Works

The `SiteMapPath` renders as a series of `<span>` elements that contain either a link or plaintext. Here's a part of the HTML code for the `SiteMapPath` from Figure 7-11:

```
<span><a title="Home" href="/">Home</a></span>
<span> &gt; </span>
<span><a title="Reviews published on this site" href="/Reviews/Default.aspx">Reviews</a></span>
<span> &gt; </span>
<span>All Reviews</span>
```

The first two menu items (Home and Reviews) are represented by a link (`<a>`) to enable you to navigate to the pages defined in their `href` properties. The final menu item—All Reviews—is just plaintext.