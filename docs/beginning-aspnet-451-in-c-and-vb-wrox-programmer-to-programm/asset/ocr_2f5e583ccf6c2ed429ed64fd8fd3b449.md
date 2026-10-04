# An Introduction to CSS

# TRY OUT Styling the Planet Wrox Homepage

In this exercise you modify two files. First, you add the basic layout elements to the Default.aspx page to create room for header, a menu, the main content area, a sidebar, and a footer. You modify the styles.css file from the Styles folder to change the size and location of these elements. Finally, you attach the style sheet to the page, the style information is applied when the page is viewed in the designer or in a browser.

+   1. Open the Default.aspx file from the root of your website and, if necessary, switch to Markup View.

+   2. Modify the code within the <form> runat="server"> so it ends up like this:

```
<form id="form" runat="server">
  <div id="PageWrapper">
    <header>Header Goes Here</header>
    <nav>Menu Goes Here</nav>
    <section id="MainContent">
      <h1>Hi visitor and welcome to Planet Wrox</h1>
    </section>
    <aside id="Sidebar">Sidebar Goes Here</aside>
    <footer>Footer Goes Here</footer>
  </div>
</form>
```

Make sure the welcome message you added in the previous chapter ends between the opening and closing tag of the MainContent <section> element. If you were already familiar with versions of HTML before, you might be surprised by the new elements such as header, section, and footer. These elements were introduced in HTML5 to give a better semantic structure to your documents. Refer to Chapter 1 for a quick introduction to HTML5.

+   3. Open the Styles.css file from the Styles folder. If you added some code to this file earlier, remove that code.

+   4. At the top of the CSS file, type the following code that uses an ID selector to select the header element:

```
header
{
}
```

+   5. Position your mouse between the curly braces and type the letter b. This brings you to all properties that start with the letter b, as shown in Figure 3-6.

Next, type the letter c. This list is filtered as you can see in Figure 3-7.
Notice how this filtering is in a pretty smart way. The filter does not limit the list to only those properties that start with c or contains the letters bc (in this case does not exist), but it also supports what is called a title

![](bbox=[0.718, 0.563, 0.952, 0.737])

![](bbox=[0.718, 0.763, 0.952, 0.913])