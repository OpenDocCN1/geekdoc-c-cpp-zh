Subsequent requests to the same page result in the same HTML sent. This means the page is not processed by the server again, and no custom code in the Code Behind will fire. The exact HTML from the first request is simply returned on each subsequent request.

Enabling output caching is extremely simple; just add an OutputCache directive below your Page directive, as shown in bold this C# Page directive (you use the same code if you're using VB.NET, but @ Page may look slightly different):

```
<@ Page File Title="Site" Language="C#"
MasterFile="~/Pages/Frontend.master" AutoEventWire="true"
CodeFile="Default.aspx" Inherits="_Default %>
<@ OutputCache Duration="60" VaryPathParam="None">
```

The Duration is the number of seconds you want to cache the page before ASP.NET creates a new copy of it. In the preceding example, the page is cached for a moment.
The None value in the VaryPathParam tells .NET to cache a single version of the page, no matter what query string values you pass to it. Although this is fine for static pages like the About page in the Planet Wrox site, this is typically not an ideal solution for dynamic pages. Imagine a page that shows the details for a review over the query that is being passed to the page. The first time you request the page you may browse to browse to:

```
http://localhost:12345/Reviews/Viewdetails.aspx?id=23
```

ASP.NET generates a page showing review 23 and then returns the output of the page. What happens when you request this?

```
http://localhost:12345/Reviews/ViewDetails.aspx?id=33
```

Instead of seeing the review with an ID of 33, you end up with the review with an ID of 23! To overcome this problem, ASP.NET enables you to cache specific versions of the query string. For an example, you can instruct it to cache the page by setting the VaryPathParam attribute of a directive to a comma-separated list of possible query string or values. ASP.NET will cache a copy of the page for each unique combination of the fields it finds. As, consider a page that contains the ID of the review in the query string and then displays it. To cache a copy for each unique review, you add Id to the VaryPathParam attribute like this:

```
<@ OutputCache Duration="60" VaryPathParam="Id"
```

For a page showing the details of a specific review, this is perfect. For each unique review, ASP.NET keeps a cached copy. This means that the database will only be hit when the review is not present in the cache.
One the problems with output caching is that it's an all-or-nothing scenario. Although it's easy to cache different pages, you'll need to write code to handle other issues dealing with them. When a page is requested and cached for the first time, the user's theme is taken into account. If subsequent users have a different theme they still see the page in the originally requested theme. Another case where output caching can be problematic when you're using query-related controls such as the Login(discussed in the next chapter). These controls can display content based on the currently logged-in user. If that is cached, other users will see the content that belongs to the first user that requested the page.