
# 712 Securing ASP.NET

For the record, sites without a permission level set default to Full, which is obviously higher than either of those.

# Changing trusts

To change the trust of a class, you want to decorate the class in the ASP.NET application with the hosting permission, like this:

```csharp
using System;
using System.Web;
using System.Security.Permissions;

[NetHostingPermission(SecurityAction.Demand, Level=AspNetPermissionLevel.High)]
public class ApplicationClass
{
    // My Code is here.
}
```

So this code uses the High level. The others are None, Minimal, Low, Medium, and Unrestricted. Table 4-1 shows the general breakdown.

| Table 4-1 | ASP.NET Permission Levels |
|---|---|
| AspHostingPermissionLevel | Description |
| None | Can't get anywhere. Don't ask. |
| Minimal | The code can execute, but it can't DO anything. |
| Low | You have read-only access to some restricted information, like the Request itself. Very rough. |
| Medium | More or less look at anything — database, network, whatever. No write access. |
| High | Read/Write for any managed code, but can't run unmanaged (native) code. |
| Unrestricted | Full run of the box. |

# Fixing problems

The most common problem is the use of None or Minimal as a permission level. I don't even know why Microsoft offers these choices. If you set the class to Minimal, nothing can get to anything so far as I have been able to figure out that. Stick to High for trusted environments, and Medium for shared servers.

# Navigating with Site Maps

A site map is an XML file that assists web design tools in formulating dynamic navigation. There has been a more interesting use for them recently. They are used by search engines for indexing your site better.

![](img/6df7bb88e9302e98442acc219cfbd7fc_738_0.png)

Webmasters.bing.com is a new Microsoft product that makes your suite more available to users of Bing. It uses the site map file to make your site more indexable. Check it out!

Search Engine Optimization (SEO) is a big topic today, and sitemaps can make your life a lot easier. Search engines have set up readers that check for the site map and then use it to walk the file structure and make sure links to the site are accurate.

## Adding a site map

To make a site map, follow these steps:

+   1. Right-click the project and choose Add-> New term.
2. Select Site Map from the context menu, as shown in Figure 4-3.

![](img/6df7bb88e9302e98442acc219cfbd7fc_738_1.png)

**Figure 4-3:** Adding a site map.

![](img/6df7bb88e9302e98442acc219cfbd7fc_738_2.png)

# 714 Navigating with Site Maps

# 3. Accept the default name, Web.SiteMap. Here is the default code:

Visual Studio builds a template site map.

```xml
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode title="" description="" />
  <siteMapNode url title="" description="" />
  <siteMapNode url title="" description="" />
</siteMap>
```

The template file shows you a guideline for the navigation of a site. If you have a number of files inside an About section, you make a SiteMapNode of About, and then inside it (Before the <sitemapnode>), you add the pages in that section, like Contact Us or Our Story.

For this example, though, there are no sectional divisions to the site. There are in Chapter 5. In this current case, you may let it play and flat with

# 4. Set up the site map for our three-page, flat structure, like this:

```xml
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode title="" description="" />
  <siteMapNode url title="" description="" />
  <siteMapNode url title="" description="" />
</siteMap>
```

Note that the SiteMapNode be two layers depth, by specification.

# 5. Add with the three names and URLs, like like this:

```xml
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

# Managing Files 715

memory. If you need to figure out what other pages are related to the page the user is viewing, you can do that. Follow these steps:

+   1. Open up the Default.aspx page in the current project.
2. Drag an empty ListBox control into the page.
3. Go to Code View.

+   4. Loop through the items in the SiteMap collection and add items to the listbox.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // Reference the parent node to get the object model happy.
            string baseNode = SiteMap.CurrentNode.Title;

            // Check to make sure there are subpages.
            if (SiteMap.CurrentNode.HasChildNodes)
            {
                foreach (SiteMapNode sitemapKids in SiteMap.CurrentNode.Children)
                {
                    // Put the name in the listbox.
                    ListBox1.Items.Add(new ListItem(sitemapKids.Title));
                }
            }
        }
    }
}
```

If you get interested, a debugger in the loop and check out SiteMap. The forms contains all the data being sent from the client. The forms collection includes any file being uploaded, using the multipart-data format.

# 741

# 716 Managing Files

ASP.NET uses a two-part plan to get file data to you. Keep in mind, you can do all by hand, but this all goes back to the idea behind ASP.NET. Controls on the front end, System.Web staff on the back end.

I'll start with the Design View. All the user must do is select a local file; the browser handles the encoding. Follow these steps to set up the:

+   1. Create a new web form in the 4 project called FileUpload.aspx.
2. Drag a FileUpload control from the Toolbox to the design surface.
3. Drag a button onto the surface.

The button on the FileUpload control is for selecting an item on your file system. You still need to postback the form.

That gives you a good start. The FileUpload has a text box and a button that gives you access to the local file system. The button provides a submit function.

All the magic happens on the back end for this example. The browser handles the upload for you. The server is your responsibility.

+   4. Double-click the submit button on the design surface to get the Button1_Click event handler.

+   5. Set a path to save the file.

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    string localPath = Server.MapPath("~/UploadedFiles/");
}
```

+   6. Add some code to the handler to check if it is a file in the form. The new code is in:

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    string localPath = Server.MapPath("~/UploadedFiles/");
}
```

+   7. In the body of the if statement, have the FileUpload control help you save the file.

```csharp
string localPath = Server.MapPath("~/UploadedFiles/");
if (FileUpload1.HasFile)
{
    try {
        FileUpload1.PostedFile.SaveAs(localPath + FileUpload1.FileName);
```
