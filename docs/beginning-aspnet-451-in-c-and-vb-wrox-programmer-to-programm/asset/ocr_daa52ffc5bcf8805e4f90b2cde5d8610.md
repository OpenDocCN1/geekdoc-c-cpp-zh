+   5. In Markup View, drag the file modernizr-2.7.1.js from the Scripts folder into the <head> section of the Master Page below the CSS file. Then manually remove the two leading periods of the src attribute, like this:

```
<script src="Scripts/modernizr-2.7.1.js"></script>
```

+   6. You can save and close the master page because you're done with it now.

# How It Works

Within VS, master pages behave like normal pages. You can add HTML and server controls to them, and you can manage the page both in Markup and Design View. The big difference is, of course, that a master page isn't a page itself; it serves as a template for pages in your site. You needed to change the path to the script file by removing the two leading periods. This causes the browser to download the file from the Scripts folder in the root of the site, no matter where the page that uses this master page is located. ASP.NET manages for CSS files automatically, but not for script files. In the next chapter you will learn more about how file paths are handled.

In the next section we show how to use this master page as the template for a content page.

# Creating Content Pages

A master page is useless without a content page that uses it. Generally, you'll have a few master pages, whereas you can have many content pages in your site. To base a content page on a master page, check the Select Master Page option at the bottom right of the Add New Item dialog box when you add a new Web Form to your site. Alternatively, you can set the MasterFile attribute on the page directly in the Markup View of the page. You will see this Page directive earlier in this chapter when master and content pages were introduced.

Content pages can only contain content controls that map to a ContentHolder control in the master declarations. These controls in turn can contain standard markup like HTML and server controls. Because the markup in a content page needs to be wrapped with <asp:Content> tags, it's not easy to import an existing ASPX page into a content page. The easiest thing to do is copy the code you want to keep to the clipboard, delete the old page, and add a new page to the master page. Once the page is added, you can paste the markup within the <asp:Content> tags. You see how this works in the following exercise.

> TRY IT OUT Adding a Content Page

In this Try Out we show how to add a content page to the site that is based on the master page we created earlier. Once the page is added, you add content to the <asp:Content> regions.

+   1. In previous examples you added standard ASPX pages to your project, which should now be "updated" to make use of the new master page. If you want to keep the welcome text you added to Default.aspx copy all the HTML between the MainContent <section> tags to the clipboard (that is, the <h1> and the two <p> elements that you created earlier) and then delete