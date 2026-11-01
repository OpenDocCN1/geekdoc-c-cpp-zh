
they still see the page in the originally requested theme. Another case where output caching can be problematic is when you're using security-related controls such as the LoginView (discussed in the next chapter). These controls can display content based on the currently logged-in user. If that page is cached, other users will see the content that belongs to the first user that requested the page.

One solution to this problem is to not use output caching at the page level and move content that applies to all users to a separate user control, which you then embed in the page as you saw how to do with the Contact Form. For example, a list with news articles or the full list of reviews could be the same for all users. If you move the code for these lists to a user control with output caching enabled, your containing page is still created separately for each user, but the content from the user control is only generated the first time, and then reused for all subsequent requests.

Another solution is to instruct the data source controls to cache data for you, as you see in the next section.

If you're not affected by the drawbacks of output caching (such as when you're not using themes or the security-related controls), output caching is an excellent mechanism to improve the performance of your site.

## Caching with Data Source Controls

The biggest benefit of caching with the data source controls is that they only cache dynamic, database-driven data, and not the entire page. That enables you to keep other parts of the page dynamic, such as a banner module or a personalized greeting welcoming the user. Caching is supported by design on most of the data source controls, except for the SiteMapDataSource, LinqDataSource, and EntityDataSource controls.

Caching with the data source controls is very easy: All you need to do is set the EnableCaching property and then specify a CacheDuration. The following code snippet shows a SqlDataSource control that caches its data for 10 minutes:

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server" CacheDuration="600" EnableCaching="True"></asp:SqlDataSource>
```

What's cool about caching with the data source controls is that they are smart enough to see if you are making updates to the underlying data. So, when you have set up a SqlDataSource control to cache data for the SelectCommand for 20 minutes, but then make a change to the data by using the InsertCommand, UpdateCommand, or DeleteCommand, the cache is invalidated automatically. This only works when you execute the insert, update, or delete command against the exact same SqlDataSource. If you have one page that displays and caches a list with reviews (such as All.aspx, for example) and then have another page that is used to insert a new review (such as AddEditReview.aspx in the Management folder), this won't work. After you have inserted a new review in the Management section of the site, it won't show up in All.aspx until the cache has expired.

Code-free caching with the data source controls is useful in many situations. However, the data source controls cannot be used in every situation. What if you want to cache the results of data you get from a completely different source? What if you want to cache data you receive in a hand-coded page targeting the Entity Framework, or the contents of a text or an XML file that you frequently need to access? For those cases, ASP.NET gives you programmatic access to the cache.

## Programmatic Caching

With programmatic caching, you can store items in the cache through VB.NET or C# code. Obviously, you can also access them again later. To store items, you use the Add or the Insert method or you index the Cache collection directly. The Add method is quite powerful (and complex) and enables you to specify a host of options that determine how long the item is cached, what priority it should have compared to other cached items, and what factors trigger the item's removal from the cache.

The Insert method, on the other hand, is much easier. It has a few short overloads that enable you to specify the cached item and associate it with a specific key. Another overload also enables you to define dependencies that can be used to invalidate a cached item when the original source is changed. This is great for caching files that don't change very often. You can read a file from disk, and store it in the cache with a dependency on the original file. You then keep reading the file from the cache instead of from disk. When the file on disk is changed, the cached item is invalidated automatically and you can read the original source file again and store it in the cache. The following example shows how to modify the ContactForm.ascx user control to store and get the item from the cache until it changes:

```vbnet
If Page.IsValid Then
    Dim mailBody As String = TryCast(Cache("ContactFormMailBody"), String)
    If String.IsNullOrEmpty(mailBody) Then
        Dim fileName As String = Server.MapPath("~/App_Data/ContactForm.txt")
        mailBody = System.IO.File.ReadAllText(fileName)
        Cache.Insert("ContactFormMailBody", mailBody, New CacheDependency(fileName))
    End If
    mailBody = mailBody.Replace("##Name##", Name.Text)
    ...
End If
```

```csharp
if (Page.IsValid)
{
    string mailBody = Cache["ContactFormMailBody"] as string;
    if (string.IsNullOrEmpty(mailBody))
    {
        string fileName = Server.MapPath("~/App_Data/ContactForm.txt");
        mailBody = System.IO.File.ReadAllText(fileName);
        Cache.Insert("ContactFormMailBody", mailBody, new CacheDependency(fileName));
    }
    mailBody = mailBody.Replace("##Name##", Name.Text);
    ...
}
```

Notice how a new CacheDependency (for which you need to bring the System.Web.Caching namespace into scope with an Imports/using statement) is created and passed to the Insert method. This CacheDependency expects the name of the file it is dependent on. As soon as you change the file on disk (using VS or Notepad, for example), ASP.NET removes the item from the cache so it will be read from the original source file again the next time this code is executed.

You remove items from the cache using the Remove method that accepts the key of the cached item. You define this key when inserting the item, using either Add or Insert.

To access the items in the cache, you have a few options available. First of all, you can access the Cache collection directly:

### VB.NET

```
myReview = TryCast(Cache(myKey), Review)
```

### C#

```
Review myReview = Cache[myKey] as Review;
```

Here, the Cache collection is indexed using the key stored in the myKey variable.

Additionally, you can use the Get method that expects the key:

### VB.NET

```
myReview = TryCast(Cache.Get(myKey), Review)
```

### C#

```
Review myReview = Cache.Get(myKey) as Review;
```

Because Get is a method, the C# example now also uses parentheses around the cache key, making both examples look more like each other.

Finally, you can access items in the cache using the Item property that also accepts the key of the cached item.

All three ways to access items in the cache always return an object or Nothing/null when the item cannot be found. That means that if you know the type you are getting back from the cache, you should cast it to the appropriate type using TryCast in VB.NET or the as keyword in C# before you can use its properties. The previous two examples show you how the item from the cache is cast to a strongly typed Review object first.

To give you an idea of how to use the cache programmatically, the next exercise shows you how to insert a review in the cache, so you don't have to get it from the database every time you need it.

## TRY IT OUT Using the Cache API

In this Try It Out exercise you see how to cache a Review instance you get from EF using a LINQ to Entities query so it can be retrieved later by its key (which contains the reviewer's ID),

- 1. Start by adding a new page called ViewDetails.aspx in the Reviews folder of your web application. Make sure it's based on your custom template. There's no need to set an explicit title, because it will be set programmatically. Instead, remove the Title="" attribute from the Page directive. There's a funny and old bug in ASP.NET that causes programmatic modifications to the page's Title not to stick when this attribute is set to an empty string in Markup View.
- 2. In Markup View, add three Label controls to the cpMainContent content placeholder and name the controls as follows:
  - TitleLabel
