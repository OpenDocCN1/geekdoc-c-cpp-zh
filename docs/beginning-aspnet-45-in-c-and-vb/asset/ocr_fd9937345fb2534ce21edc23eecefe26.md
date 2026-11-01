You remove items from the cache using the Remove method that accepts the key of the cached item. You define this key when inserting the item, using either Add or Insert.

To access the items in the cache, you have a few options available. First of all, you can access the Cache collection directly:

# VB.NET

```
myReview = TryCast(Cache(myKey), Review)
```

# C#

```
Review myReview = Cache[myKey] as Review;
```

Here, the Cache collection is indexed using the key stored in the myKey variable.

Additionally, you can use the Get method that expects the key:

# VB.NET

```
myReview = TryCast(Cache.Get(myKey), Review)
```

# C#

```
myReview = Cache.Get(myKey) as Review;
```

Because Get is a method, the C# example now also uses parentheses around the cache key, making both examples look more like each other.

Finally, you can access items in the cache using the Item property that also accepts the key of the cached item.

All three ways to access items in the cache always return an object or Nothing/null when the item cannot be found. That means that if you know the type you are getting back from the cache, you should cast it to the appropriate type using TryCast in VB.NET or the as keyword in C# before you can use its properties. The previous two examples show you how the item from the cache is cast to a strongly typed Review object first.

To give you an idea of how to use the cache programmatically, the next exercise shows you how to insert a review in the cache, so you don't have to get it from the database every time you need it.

# TRY IT OUT Using the Cache API

In this Try It Out exercise you see how to cache a Review instance you get from EF using a LINQ to Entities query so it can be retrieved later by its key (which contains the reviewer's ID),

+   1. Start by adding a new page called ViewDetails.aspx in the Reviews folder of your web application. Make sure it's based on your custom template. There's no need to set an explicit title, because it will be set programmatically. Instead, remove the Title="" attribute from the Page directive. There's a funny and old bug in ASP.NET that causes programmatic modifications to the page's Title not to stick when this attribute is set to an empty string in Markup View.
+   2. In Markup View, add three Label controls to the cpMainContent content placeholder and name the controls as follows:
+      > TitleLabel