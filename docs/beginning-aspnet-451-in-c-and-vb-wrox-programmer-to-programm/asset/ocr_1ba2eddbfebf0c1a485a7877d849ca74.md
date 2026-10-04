page. Note that this is almost the same code you added to Default.aspx in Chapter 3, except for the <asp:ContentPlaceholder> element and the <a> element within the Header <div>. The <a> element takes the user back to the homepage, and will be styled later.

```
<form id="form1" runat="server">
<div id="PageWrapper">
  <header>
    <a href="/">Header Goes Here</a>
  </header>
  <nav>Menu Goes Here</nav>
  <section id="MainContent">
    <asp:ContentPlaceholder ID="cpMainContent" runat="server">
    </asp:ContentPlaceholder>
  </section>
  <aside id="Sidebar">Sidebar Goes Here</aside>
  <footer>Footer Goes Here</footer>
</div>
</form>
```

Make sure that you have the ContentPlaceholder within the MainContent <section> tags. You can drag one from the Toolbox onto or the code directly, using IntelliSense-help hints. In both cases you should give the control an ID of cpMainContent.

+   4. Next, switch your page into Design View and drag Styles.css from the Styles folder in the Solution Explorer onto the master page. As soon as you drop it, VS updates the Design View and shows the layout for the site that you created in Chapter 3. If the design doesn't change, switch to Markup View and ensure there is a <link> tag in the head of the page pointing to your CSS file:

```
<asp:ContentPlaceholder ID="head" runat="server">
</asp:ContentPlaceholder>
<link href="../Styles.css" rel="stylesheet" type="text/css" />
</head>
```

The page should now look like Figure 6-2 in Design View.

![](bbox=[0.165, 0.626, 0.893, 0.816])

Note the area with the purple border around it between the menu and the footer region in Design View. This is the ContentPlaceholder control that is used by the content pages. You see how to use it in the next exercise.