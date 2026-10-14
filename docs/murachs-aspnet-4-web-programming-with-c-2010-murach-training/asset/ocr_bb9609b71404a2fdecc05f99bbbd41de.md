# # How to nest master pages

In addition to creating content pages from a master page, you can create other master pages. When you nest master pages like this, you can create a *parent master page* that contains the elements used by all the pages in a web site. Then, you can create *child master pages* that add to the contents of the parent master page and that contain the elements used by different sections of the web site.

# ## How to create nested master pages

To create a master page that’s nested within another master page, you use a technique similar to the one in figure 9-2 for creating any master page. After you select the Master Page template and enter the name of the page, however, you check the Select Master Page check box. Then, you’ll be asked to select the master page you want to use as the parent of the child master page.

The code example at the top of figure 9-9 shows the startup.aspx code for a child master page. This page uses a parent master page that’s similar to the one you saw in figure 9-4. The main difference is that I deleted the paragraph at the bottom of the page. As you may recall, this paragraph contained a label that displayed the number of days until Halloween.

Note that this code is almost identical to the code for a content page. The only difference is that it starts with a Master directive instead of a Page directive. Unlike the Master directive for a parent master page, though, the Master directive for a child master page includes MasterPageFile and AutoEventWireup attributes.

# ## How to add content to a child master page

To add content to a child master page, you add elements to the Content controls. This is illustrated in the second code example in figure 9-9. Here, I added div and p elements to the second Content control. The div element contains a ContentPlaceHolder control that can be used by any content page that’s created from this master page. And the p element contains the label that was originally included on the parent master page.

The first Content control contains a link element that identifies the external style sheet that’s used by the page. In addition, it too contains a ContentPlaceHolder control. This control can be used by any content pages to include style and other heading information for the page.

Once you’ve created the parent and child master pages, you can create content pages that use either one of them. If you want a content page to include the label that indicates the number of days until Halloween, for example, you can create a page that uses the child master page. But if you don’t want this label included on a content page, you can create a page that uses the parent master page.