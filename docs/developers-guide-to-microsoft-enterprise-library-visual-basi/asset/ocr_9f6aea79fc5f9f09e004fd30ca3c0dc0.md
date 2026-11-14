```
Loaded the cache with the list of products.

The cache contains the following 3 item(s):
Item key 'ItemOne' (CachingExample.Product) = CachingExample.Product
Item key 'ItemTwo' (CachingExample.Product) = CachingExample.Product
Item key 'ItemThree' (CachingExample.Product) = CachingExample.Product

Getting an item from the cache...
Cached item values are: ID = 79, Name = 'Useful Thing', Description = Something that is useful for everything.
```

In general, the pattern for a function that performs reactive cache loading is:

+   1. Check if the item is in the cache and the value returned is not **Nothing**.
+   2. If it is found in the cache, return it to the calling code.
+   3. If it is not found in the cache, create or obtain the object or value and cache it.
+   4. Return this new value or object to the calling code.

# Extending Your Cache Advance

The Caching block, like all the other blocks in Enterprise Library, contains extension points that allow you to create custom providers and integrate them with the block. You can also replace the default cache manager if you want to use a different caching mechanism, or modify the source code to otherwise change the behavior of the block.

The cache manager is responsible for loading items from a persistent backing store into memory when you instantiate the application block. It also exposes the methods that manipulate the cache. If you want to change the way that the Caching block loads or manages cached items, for example to implement a distributed or specialist caching mechanism, or perform asynchronous or delayed cache loading, you can use the **ICacheManager** interface and implement the methods and properties it defines.

Alternatively, if you just want to use a different backing store or add a new expiration policy, you can create custom backing store providers and expiration policies and use these instead of the built-in providers and policies. To create custom backing store provider, you can implement the **IBackingStore** interface or inherit from the **Base BackingStore** abstract class. To create a custom expiration policy, you can implement the **ICacheItemExpiration** interface and, optionally, the **ICacheItemRefreshAction** interface for a class that refreshes an expired cache item.

For more information about extending the Caching block, see the online documentation and the help files installed with Enterprise Library.