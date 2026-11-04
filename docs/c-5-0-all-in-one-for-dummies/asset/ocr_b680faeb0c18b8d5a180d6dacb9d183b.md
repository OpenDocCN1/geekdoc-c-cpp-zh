# 3. Accept the default name, Web.SiteMap.

Visual Studio builds a template site map. Here is the default code:

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
  <siteMapNode url="" title="" description="">
    <siteMapNode url="" title="" description="" />
    <siteMapNode url="" title="" description="" />
  </siteMapNode>
</siteMap>
```

The template file shows you a guideline for adding the navigation of a site. If you have a number of files inside an About section, you make a SiteMapNode of About, and then inside it (before the closing </sitemap-node>), you add the pages in that section, like Contact Us or Our Story.

For this example, though, there are no sectional divisions to the site. There are in Chapter 5. In this current case, you make it flat and play with that.

# 4. Set up the site map for our three-page, flat structure, like this:

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
<siteMapNode>
  <siteMapNode url="" title="" description="" />
  <siteMapNode url="" title="" description="" />
  <siteMapNode url="" title="" description="" />
</siteMapNode>
</siteMap>
```

Note that the SiteMapNode must be two layers deep, by specification.

# 5. Add in the three page names and URLs, like this:

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
<siteMapNode url="Cookies.aspx" title="Cookies" description="Learn all about Cookies" />
<siteMapNode url="Default.aspx" title="Home" description="The main page" />
<siteMapNode url="Request.aspx" title="Request" description="Coding for the Request" />
</siteMapNode>
</siteMap>
```

You need to add the Cookies.aspx file to the project if you aren't working from the book's sample code.

# Navigating a site with SiteMap

With the web.sitemap file installed safely in the application, IIS now has a SiteMap collection that includes the XML file you made right there in