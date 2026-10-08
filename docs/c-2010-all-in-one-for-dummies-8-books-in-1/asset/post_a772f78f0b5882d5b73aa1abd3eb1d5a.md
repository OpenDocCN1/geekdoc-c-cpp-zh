
# 696 Baking Cookies

7. In the body of the if statement, have the FileUpload control help us save the file.

New code is in bold.

```
protected void Button1_Click(object sender, EventArgs e) {
    String localPath = Server.MapPath("~/UploadedFiles/");
    if (FileUpload1.HasFile) {
        try {
            FileUpload1.PostedFile.Save(localPath + FileUpload1.FileName);
        } catch (Exception ex) {
            Response.Write(ex.Message);
        }
    }
}
```

This is a nice feature. In the old days, we needed to wrangle the bytes themselves. Uphill both ways, in the snow.

To build a comprehensive file upload function, you need a little more string programming practices. Like my error handling, for instance? The idea here, though, is that there is a FileUpload control that gives us back-end control.

While we are here, take a look at the HttpFileCollection, which is the System.Web class that gives the FileUpload control its power. The properties of the FileUpload control, like the file's bits, name, and all that, are in the HttpFileCollection. Check it out if you need more fine-grained control than the FileUpload control gives you.

# Baking Cookies

Cookies are the only thing that a Web site can directly save on a client machine without the client's direct permission. It still requires the indirect permission, because a user can disable cookies, thus possibly a cookie be saved without actually asking the user, “Is it okay if I save this?”

Cookies are useful for state management. If you know the ID of the client's shopping cart, for instance, you can save that ID in a cookie, and even if the client goes away for a week and comes back, you will still be able to go back to the business layer and look up the information.

Cookies are stored in a collection — actually a dictionary — keys and values. If you know what you are looking for, you can query the collection for the value you want; if you don't, you can loop through the collection until you find it.

The cookies collection is managed using the Request and Response object based on the HttpRequest and HttpResponse classes we cover earlier in this chapter.

# Coding for client-side storage

To get a cookie, you have to first leave a cookie. In part of the response to a client — after they log in — you want to tell the platform to save information in the Cookies collection.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_722_0.png)

Remember that cookies are plain text — anyone can read them. Never store something that can be used by someone wearing a proverbial black hat. I almost always create a System.Guid (a globally unique identifier) and to track that information that I persist somewhere in my back-end data store.

## Leveraging the .NET Framework

What is even better to store information about the session itself and have an understanding that the information will be removed from the database after some time limit. This prevents the impersonation of the user by someone intercepts the cookie. There are a lot of options, but check out the best practices offered by Microsoft and other organizations before setting your cookie strategy.

If I want to store information about the session in the cookie, and tell the database that my customer is using that session, I generate a Guid and save it in both places. Then I retrieve the cookie at the next request, compare to the available Guides in the cookie collection, and find the user in question.

Here is an example of setting the cookie based on session information:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

namespace Chapter_4
{
    public partial class Cookies : System.Web.UI.Page
    {
        WebUser currentUser = new WebUser();
        List<WebUser> usersInDatabase = new List<WebUser>();
        protected void Page_Load(object sender, EventArgs e)
        {
    }
```

# 698 Baking Cookies

```c
if (!Page.IsPostBack)
{
    //This is a first request, so we need to set the cookie
    Guid sessionGuid = new Guid();
    currentUser.SessionId = sessionGuid;
    //Tell the database about the new user
    usersInDatabase.Add(currentUser);
    //Set the cookie
    Response.Cookies.Add(new HttpCookie("SessionId", sessionGuid.ToString()));
}

//This class would be in the library somewhere,
//not actually in this file.
public class WebUser
{
    public Guid SessionId { get; set; }
}
```

# Wrangling cookies on the server

So now the user has the cookie, and the next request comes in. I need to grab the cookie from the collection and search my known user base to get the information that I need. The boldface in the code indicates the code added:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

namespace Chapter_4
{
    public partial class Classes : System.Web.UI.Page
    {
        WebUser currentUser = new WebUser();
        List<WebUser> usersInDatabase = new List<WebUser>();
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!Page.IsPostBack)
            {
                //This is a first request, so we need to set the cookie
                Guid sessionGuid = new Guid();
                currentUser.SessionId = sessionGuid;
                //Tell the database about the new user
                usersInDatabase.Add(currentUser);
                //Set the cookie
                Response.Cookies.Add(new HttpCookie("SessionId", sessionGuid.ToString()));
            }
            else
            {
        }
    }
}
```

# Tracing with TraceContext 699

```
//The is a postback so we need to get the cookie
string cookieSession = Request.Cookies.Get("SessionId").Value;
Guid sessionGuid = new Guid(cookieSession);
var returningUser = from u in usersInDatabase
where u.SessionId.ToString() == sessionGuid.ToString()
select u
foreach (var user in returningUser)
{
currentUser = user;
}
```

//This class would be in the library somewhere,
//not actually in this file.
public class WebUser{
    public Guid SessionId { get; set; }
}

Book VI
Chapter 4

## .NET Framework:Leveraging the

# How ASP.NET manages cookies

ViewState is the state of the page. In ASP.NET, ViewState is used to maintain the state of the page between postbacks. It is stored in a hidden field on the page.

## Tracing with TraceContext

The Trace class provides all the server processing information about a Web page. It is exposed in the code when you have tracing turned on.

# 700 Tracing with TraceContext

Why not make it easy on yourself later on the road?

If you decide which parts of the application are most likely to have problems while you code, you can insert trace messages as you go. It seems a defeatist attitude, but really I think it is a realistic attitude. Even if it is just caused by bad data in two years, you are probably to spend some time debugging.
