To access the items in the cache, you have a few options available. First of all, you can access the Cache collection directly:

# VB.NET

```
myReview = TryCast (Cache (myKey), Review)
```

# C#

```
myReview = Cache[myKey] as Review;
```

Here, the Cache collection is indexed using the key template in the myKey variable.
Additionally, you can use the Get method that expects the key:

# VB.NET

```
myReview = TryCast (Cache.Get (myKey), Review)
```

# C#

```
myReview = Cache.Get (myKey) as Review;
```

Because get is cached, the C# example now uses parentheses around the Item property that also accepts the key of the cached item.
both examples look like each other.

Finally, you can access items in the cache using the Item property that also accepts the key of the cached item.
All ways to access items in the cache always return an object or Nothing/null when the item cannot be found. That means if you know the type you are getting back from the cache, you should cast it to the appropriate type using TryCast in VB.NET or the as keyword in C# before you can use its properties. The two examples show you how the item from the cache is cast to a strongly typed Review object first.

To give an idea of how to use the cache programmatically, the next exercise shows how to insert a review in the cache, so you don't have to get it from the database every time you need it.

# TRY OUT Using the Cache API

In This Out exercise you use to get a Review instance from EF using LINQ to Entities so it can be retrieved later by its key (which contains the review's ID).

+   Start by adding a new page ViewData.aspx in the Reviews folder of your web application. Make sure it's based on your custom template. There's no need to set an explicit title, because it will be set programmatically. Instead, remove the Title=" attribute from the Page directive. There's a funny and old bug in ASP.NET that causes programmatic modifications to the page's Title not to stick when this attribute is set to an empty string.
2. In Markup View, add three Label controls to the cpMainContent content placeholder and name the controls as:

+   * TitleLabel
* SummaryLabel
* BodyLabel