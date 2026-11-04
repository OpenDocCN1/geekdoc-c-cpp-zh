
```csharp
if (!Request.IsAuthenticated) {
    Response.Redirect("login.aspx");
}
```

On the other hand, sometimes you need to tell the user that this isn't the right place to be at all. Especially useful if you have to change the structure of your Web site, RedirectPermanently tells search engine spiders "nope, this isn't here anymore. Go over there and change your index."

For instance, say you have a product line that was moved to a whole new URL. You could check the QueryString for the product line statement, and if you find it, redirect the link permanently.

```csharp
if (Request.QueryString["ProductLineId"] == 4) {
    Response.RedirectPermanently("http://newproduct.com");
}
```

## Changing the request or response directly

Sometimes you just want to change things directly.

Response.Write, Response.WriteFile, and Response.WriteSubstitution all are designed to allow you to do just that. In the old days (before debugging), we had to use Response.Write to put errors into the HTML that we could view with ViewSource. If you are using MVC, there is still a place for that.

In today's development, Response.Write is mostly used to do something that you want to do on every page that meets a certain criteria, no matter who coded it. You can add it to the code-behind of the master page (more on that in Chapter 5) and know that the output stream of the site will be altered directly.

## Securing with ASP.NET

Book III covers security, and there is a whole book on security that you should read — Code Complete by Steve McConnell. I'm only covering security in this chapter because the AspNetHostingPermission is in the System.Web namespace, and I want to give it a little airtime.

ASP.NET security is a complex topic. Because visitors to a Web site are anonymous, bypassing the Windows security system occurs often. That bypassing — called impersonation — allows IIS to do things on behalf of the user even if the user isn't really known to Windows. Remember, just because you have put in a username and password doesn't mean that Windows is okay with your credentials.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_716_0.png)

So ASP.NET Web sites are run most often with whatever permissions the IIS service is running with. Under normal conditions, this service is a fairly restricted account called Network Service. The fact is, however, that you really have no idea what the permissions will be because a hosting company most likely will be managing that. Your users can have administrative permissions for all you know.

You can purposefully restrict the permissions of your users in your code. This prevents someone from finding a way through your code logic to call a method you don't want them to be able to call.

Believe me, it happens.

The general idea is to trust no one, which I harp on in the Security chapter in Book III. You want to pretend that most people who are going to run your code are the enemy. I realize that isn't any fun. But it is necessary today. There are pre-built scripts to break into Web pages — there doesn't even have to be a real person there to bust in.

The MSDN documentation states this:

> "It is recommended that you set the level attribute of the trust configuration element to High for sites that are trusted. For sites that are not trusted, such as a Web server that hosts sites that run code from an external customer, it is recommended that you set the level attribute of the trust configuration element to Medium."

For the record, sites without a permission level set default to Full, which is obviously higher than either of those.

### Changing trusts

To change the trust of a class, you want to decorate the class in the ASP.NET application with the hosting permission, like this:

```csharp
using System;
using System.Web;
using System.Security.Permissions;

[AspNetHostingPermission(SecurityAction.Demand, Level=AspNetHostingPermissionLevel.High)]
public class ApplicationClass
{
    // My Code is here.
}
```

So this code uses the High level. The others are None, Minimal, Low, Medium, and Unrestricted. Table 4-1 shows the general breakdown.

**Table 4-1** ASP.NET Permission Levels

| AspNetHostingPermissionLevel | Description |
| --- | --- |
| None | Can't get anywhere. Don't ask. |
| Minimal | The code can execute but it can't DO anything. |
| Low | You have read-only access to some restricted information, like the Request itself. Very rough. |
| Medium | More or less can look at anything — database, network, whatever. No write access. |
| High | Read/Write for any managed code, but can't run unmanaged (native) code. |
| Unrestricted | Full run of the box. |

### Fixing problems

The most common problem is the use of None or Minimal as a permission level. I don't even know why Microsoft offers these choices. If you set the class to Minimal, nothing can get to anything so far as I have been able to figure out. Stick to High for trusted environments, and Medium for shared servers.

## Navigating with Site Maps

A site map is an XML file that assists Web design tools in formulating dynamic navigation. There has been a more interesting use for them recently, however. They are used by search engines for indexing your site better.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_717_0.png)

Webmasters.bing.com is a new Microsoft product that makes your suite more available to users of Bing. It uses the site map file to make your site more indexable. Check it out!

Search Engine Optimization is a big topic these days, and sitemaps can make your life a lot easier. Search engines have set up readers that check for the site map, and then use it to walk the file structure and make sure the links to the site are accurate.

### Adding a site map

To make a site map, follow these steps:

- 1. Right-click on the project and select Add New ... Item.
- 2. Select Site Map from the context menu, as shown in Figure 4-3.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_718_0.png)

Figure 4-3: Adding a site map.

- 3. Accept the default name, Web.SiteMap.

Visual Studio builds a template site map. Here is the default code:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
    <siteMapNode url="" title="" description="">
        <siteMapNode url="" title="" description="" />
        <siteMapNode url="" title="" description="" />
    </siteMapNode>
</siteMap>
```

The template file shows you a guideline for adding the navigation of a site. If you have a number of files inside an About section, you make a SiteMapNode of About, and then inside it (before the closing </siteMapNode>), you add the pages in that section, like Contact Us or Our Story.

For our example, though, there are no sectional divisions to the site. There are in Chapter 5. In this current case, we make it flat and play with that.

- 4. Set up the site map for our three-page, flat structure, like this:

```xml
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

- 5. Add in the three page names and URLs, like this:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
    <siteMapNode>
        <siteMapNode url="Cookies.aspx" title="Cookies" description="Learn all about Cookies" />
        <siteMapNode url="Default.aspx" title="Home" description="The main page" />
        <siteMapNode url="Request.aspx" title="Request" description="Coding for the Request" />
    </siteMapNode>
</siteMap>
```

### Navigating a site with SiteMap

With the web.sitemap file installed safely in the application, IIS now has a SiteMap collection that includes the XML file we made right there in memory. If you need to figure out what other pages are related to the page the user is viewing, you can do that. Follow these steps:

- 1. Open up the Default.aspx page in the current project.
- 2. Drag an empty ListBox control into the page.
- 3. Go to Code View.
- 4. Loop through the items in the SiteMap collection, and add items to the listbox.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // Reference the parent node to keep the object model happy.
            string baseNode = SiteMap.CurrentNode.Title;

            // Check to make sure there are subpages.
            if (SiteMap.CurrentNode.HasChildNodes)
            {
                foreach (SiteMapNode sitemapKids in SiteMap.CurrentNode.ChildNodes)
                {
                    // Put the node name in the listbox.
                    ListBox1.Items.Add( new ListItem(sitemapKids.Title));
                }
            }
        }
    }
}
```
