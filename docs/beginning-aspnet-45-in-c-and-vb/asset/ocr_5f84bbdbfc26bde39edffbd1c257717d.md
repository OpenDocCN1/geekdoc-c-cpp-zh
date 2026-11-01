Note the area with the purple border around it between the menu and the footer region in your Design View. This is the ContentPlaceHolder control that is used by the content pages. You see how to use it in the next exercise.

5. Drag the file modernizr-2.6.2.js from the Scripts folder into the <head> section of the Master Page below the CSS file. Then manually replace the two leading periods with a slash, like this:

```
<script src="/Scripts/modernizr-2.6.2.js"></script>
```

6. You can save and close the master page because you're done with it for now.

# How It Works

Within VS, master pages behave like normal pages. You can add HTML and server controls to them, and you can manage the page both in Markup and Design View. The big difference is, of course, that a master page isn't a true page itself; it only serves as a template for other pages in your site.

In the next section you see how to use this master page as the template for a content page.

# Creating Content Pages

A master page is useless without a content page that uses it. Generally, you'll have only a few master pages, whereas you can have many content pages in your site. To base a content page on a master page, check the Select Master Page option at the bottom right of the Add New Item dialog box when you add a new Web Form to your site. Alternatively, you can set the MasterPageFile attribute on the page directly in the Markup View of the page. You saw this @ Page directive earlier in this chapter when master and content pages were introduced.

Content pages can only directly contain Content controls that each map to a ContentPlaceHolder control in the master page. These content controls in turn can contain standard markup like HTML and server control declarations. Because the entire markup in a content page needs to be wrapped by <asp:Content> tags, it's not easy to turn an existing ASPX page into a content page. Usually the easiest thing to do is copy the content you want to keep to the clipboard, delete the old page, and then add a new page based on the master page to the website. Once the page is added, you can paste the markup within the <asp:Content> tags. You see how this works in the following exercise.

# TRY IT OUT Adding a Content Page

In this Try It Out you see how to add a content page to the site that is based on the master page you created earlier. Once the page is added, you add content to the <asp:Content> regions.

+   1. In previous exercises you added standard ASPX pages to your project, which should now be "upgraded" to make use of the new master page. If you want to keep the welcome text you added to Default.aspx earlier, copy all the HTML between the MainContent <section> tags to the clipboard (that is, the <h1> and the two <p> elements that you created earlier) and then delete the Default.aspx page from the Solution Explorer. Next, right-click the website in the Solution Explorer and choose Add ▸ Add New Item. Select the correct programming language, click Web