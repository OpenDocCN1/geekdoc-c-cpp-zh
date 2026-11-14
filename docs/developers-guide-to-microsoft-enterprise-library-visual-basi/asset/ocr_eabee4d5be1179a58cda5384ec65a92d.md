database backing store, uses a cache manager named DatabaseCacheManager that is configured with a data cache store backing store. As with the earlier example, the code retrieves a reference to this cache manager by specifying the name when calling the GetInstance method of the current Enterprise Library container.

```
' Retrieve a CacheManager instance that uses a Database Backing Store.
Dim databaseCache As ICacheManager _
= EnterpriseLibraryContainer.Current.GetInstance(Of _
ICacheManager)("DatabaseCacheManager")
...
CacheItemsAndShowCacheContents(databaseCache)
```

The code then executes the same CacheItemsAndShowCacheContents routine you saw in the first example, and passes to it the reference to the databaseCache cache manager. As you will be expecting by now, the result you see when you run this example is the same as you saw in the first example in this chapter.

The connection string for the database we provide with this example is:
Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\Caching.mdf;
Integrated Security=True; User Instance=True

If you have configured a different database using the scripts provided with the example, you may find that you get an error when you run this example. It is likely to be that you have an invalid connection string in your App.config file for your database. In addition, use the Services applet in your Administrative Tools folder to check that the SQL Server (SQLEXPRESS) database service (the service is named MSSQL$SQLEXPRESS) is running.

# REMOVING ITEMS FROM AND FLUSHING THE CACHE

Having seen how you can add items to your cache, and use a variety of backing store options and encryption, it’s time now to see how you can manipulate the cache to remove items, or clear it completely by flushing it. Items are removed from the cache automatically based on their expiration or dependencies, but you can also remove individual items or remove all items.

The example, Remove and flush cached items, actually demonstrates more than just removing and flushing items—it shows how you can use a dependency to remove related items from your cache, how to create extended time expirations, and how to use an array of expirations. There is quite a lot of code in this example, so we’ll step through it and explain each part in turn.

# Using a File Dependency and Extended Time Expiration

The example starts by creating a NeverExpired expiration instance, followed by writing a text file to the current execution folder. It then creates a FileDependency on that file. This is a typical scenario where you read data from a file, such as a text file or an XML document, which you will access frequently in your code. However, if the original file is changed or deleted, you want the equivalent cached item to be removed from the cache.