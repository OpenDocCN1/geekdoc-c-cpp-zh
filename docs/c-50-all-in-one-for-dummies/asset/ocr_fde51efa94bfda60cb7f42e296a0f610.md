# 714 Navigating with Site Maps

# 3. Accept the default name, Web.SiteMap. Here is the default code:

Visual Studio builds a template site map.

```
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode title="" description=" />
  <siteMapNode url title="" description=" />
  <siteMapNode url title="" description=" />
</siteMap>
```

The template file shows you a guideline for the navigation of a site. If you have a number of files inside an About section, you make a SiteMapNode of About, and then inside it (Before the <sitemapnode>), you add the pages in that section, like Contact Us or Our Story.

For this example, though, there are no sectional divisions to the site. There are in Chapter 5. In this current case, you may let it play and flat with

# 4. Set up the site map for our three-page, flat structure, like this:

```
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode title="" description=" />
  <siteMapNode url title="" description=" />
  <siteMapNode url title="" description=" />
</siteMap>
```

Note that the SiteMapNode be two layers depth, by specification.

# 5. Add with the three names and URLs, like like this:

```
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode url="Cookies.aspx" title="Learn all About Cookies" />
  <siteMapNode url="Default.aspx" title="Home" description="The page" />
  <siteMapNode url="Request.aspx" title="Request" description="Coding" />
</siteMap>
```

You need to add the Cookies.aspx file to the project if you aren't working from the book's sample code.

# Navigating a site with SiteMap

With the web.semanticweb file installed safely in the application, IIS now has a SiteMap collection that includes the XML file you made right there