# How to create a web.sitemap file

Before you can use one of the site navigation controls, you must create a web.sitemap file in the application’s root directory. This file uses XML tags to define the hierarchical structure of the pages that make up the application.

As figure 10-2 shows, you can add a web.sitemap file to an application by choosing the Website→Add New Item command and selecting Site Map from the list of templates. Then, you use the Text Editor to edit the contents of this file. The web.sitemap file can contain two types of XML elements: siteMap and siteMapNode.

The siteMap element is the root element for the XML file and should occur only once in the file. You usually don’t need to modify this element.

In contrast, you need to create a siteMapNode element for each page in the web site that you want to include in the navigation controls. In the siteMapNode element, you specify the URL of the page (relative to the application’s root folder); the page title that’s displayed as the link in the menu, tree, or map path; and a description of the page.

To indicate the hierarchy of the pages in the site map, you nest the siteMapNode elements. The file should contain just one top-level siteMapNode element that represents the site’s home page. Then, additional elements can be nested between the start and end tags for the home-page siteMapNode.

An important rule you must follow when you create the sitemap file is that each siteMapNode element must have a unique URL. That means each page in the web site can appear only once in the site map.

Another important point is that you don’t have to include all of the pages in the web site in the sitemap file. Instead, you should only include those pages that you want to make available via the site’s navigation controls. If, for example, the site uses a two-page checkout process, you may not want to include the second check out page in the sitemap file. That way, the user will be able to access the first checkout page from a menu or tree view control, but not the second checkout page.