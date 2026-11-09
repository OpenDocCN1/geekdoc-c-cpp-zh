the item. Therefore, while removing items from cache, the Web server removes low priority items before the high priority items from the cache. The possible values for the **CacheItemPriority** enumeration are listed in Table 9.8:

**Table 9.8: Possible Values for the CacheItemPriority Enumeration**

| Values | Description |
|---|---|
| AboveNormal | Specifies that the cache items at this level are not deleted frequently when the server frees the system memory |
| BelowNormal | Specifies that the cache items at this level are deleted frequently when the server frees the system memory |
| Default | Specifies that the default value for a cached item is Normal |
| High | Specifies that the cache items at this level are least likely to be deleted when the server frees the system memory |
| Low | Specifies that the cache items at this level are most likely to be deleted when the server frees the system memory |
| Normal | Specifies that the cache items at this level are deleted after the deletion of the **Low** and **BelowNormal** priority items; this is the default value for all the cached items |
| NotRemovable | Specifies that the cache items at this level are not deleted automatically |

You can define the **CacheItemPriority** enumeration while inserting an item into cache, as shown in the following code snippet:

```
```csharp
Cache.Insert("MyValue", value, Nothing, DateTime.MaxValue,
             TimeSpan.FromSeconds(20), CacheItemPriority.High, null)
```
```

The preceding code inserts the item into cache with high priority.

# ## Retrieving Data from Cache

Retrieving data from the cache and displaying it on the Web page is one of the easiest tasks in ASP.NET. To retrieve data, you need to specify the key and the value that represent the data, as shown in the following code snippet:

```
```csharp
value=Cache["MyValue"];
```
```

It is important to note that while retrieving the data from cache, you should check whether the data exists in the cache or not, as shown in the following code snippet:

```
```csharp
value = Cache["MyValue"];
if (value == null)
    // Do something here
else
    // Do something here
```
```

# ## Deleting Items from Cache

Generally, an expiration policy is used to implement data caching. This expiration policy removes data automatically on the basis of the time limit specified in it. However, there are times when you need to delete data from cache manually. The following code snippet shows how to delete data manually:

```
```csharp
Cache.Remove["MyData1"];
```
```

# # Implementing Data Caching

Data caching is used to store the custom data in cache. Let’s understand the concept of data caching by implementing it in a new Web site. Perform the following steps to create a new Web site named **DataCachingExample** (also available on the CD):

+   1. *Open* Microsoft Visual Studio 2010.
+   2. *Click* **File→New→Web Site.** The New Web Site dialog box appears.
+   3. *Select* the ASP.NET Web Site template and *name* it **DataCachingExample** and *click* the OK button.