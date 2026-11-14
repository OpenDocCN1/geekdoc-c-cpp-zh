
## Adding the Items to the Cache

Now (at last) the code can add some items to the cache. It adds four items: the first uses the NeverExpired expiration, the second uses the array that contains the file dependency and extended format time expiration, and the other two just use the simple approach to caching items that you saw in the first example of this chapter. The code then displays the contents of the cache and waits for you to press a key.

```
" Add items to the cache using the key string names in the DemoCacheKeys array.
defaultCache.Add(DemoCacheKeys(0), "A cached item that never expires", _
    CacheItemPriority.NotRemovable, Nothing, never)
defaultCache.Add(DemoCacheKeys(1), "A cached item that depends on both " _
    & "a disk file and an hourly extended time expiration.", _
    CacheItemPriority.Normal, Nothing, expirations)
defaultCache.Add(DemoCacheKeys(2), "Another cached item")
defaultCache.Add(DemoCacheKeys(3), "And yet another cached item.")

ShowCacheContents(defaultCache)
Console.Write("Press any key to delete the text file...")
Console.ReadKey(True)
```

The following is the output you see at this point in the execution.

```
Created a 'never expired' dependency.
Created a text file named ATextFile.txt to use as a dependency.
Created an expiration for 30 minutes past every hour.

The cache contains the following 4 item(s):
Item key 'ItemOne' (System.String) = A cached item that never expires
Item key 'ItemTwo' (System.String) = A cached item that depends on both a disk
file and an hourly extended time expiration.
Item key 'ItemThree' (System.String) = Another cached item
Item key 'ItemFour' (System.String) = And yet another cached item.
```

When you press a key, the code continues by deleting the text file, and then re-displaying the contents of the cache. Then, as in earlier examples, it waits for the items to be scavenged from the cache. The output you see is shown here.

```
Cache contains the following 4 item(s):
Item key 'ItemOne' (System.String) = A cached item that never expires
Item with key 'ItemTwo' has been invalidated.
Item key 'ItemThree' (System.String) = Another cached item
Item key 'ItemFour' (System.String) = And yet another cached item.

Waiting for the dependent item to be scavenged from the cache...
Waiting... Waiting... Waiting... Waiting...
```

```
Cache contains the following 3 item(s):
Item key 'ItemOne' (System.String) = A cached item that never expires
Item key 'ItemThree' (System.String) = Another cached item
Item key 'ItemFour' (System.String) = And yet another cached item.
```

You can see that deleting the text file caused the item with key ItemTwo that depended on it to be invalidated and removed during the next scavenging cycle.

At this point, the code is again waiting for you to press a key. When you do, it continues by calling the Remove method of the cache manager to remove the item having the key ItemOne, and displays the cache contents again. Then, after you press a key for the third time, it calls the Flush method of the cache manager to remove all the items from the cache, and again calls the method that displays the contents of the cache. This is the code for this part of the example.

```
Console.Write("Press any key to remove {0} from the cache...", DemoCacheKeys(0))
Console.ReadKey(True)
defaultCache.Remove(DemoCacheKeys(0))
ShowCacheContents(defaultCache)
Console.Write("Press any key to flush the cache...")
Console.ReadKey(True)
defaultCache.Flush()
ShowCacheContents(defaultCache)
```

The result you see as this code executes is shown here.

```
Press any key to remove ItemOne from the cache...
Cache contains the following 2 item(s):
Item key 'ItemThree' (System.String) = Another cached item
Item key 'ItemFour' (System.String) = And yet another cached item.
Press any key to flush the cache...
The cache is empty.
```

## REFRESHING THE CACHE

So far, when we used the Add method to add items to the cache, we passed a null value for the refreshAction parameter. You can use this parameter to detect when an item is removed from the cache, and discover the value of that item and the reason it was removed.

You must create a class that implements the ICacheItemRefreshAction interface, and contains a method named Refresh that accepts as parameters the key of the item being removed, the value as an Object type, and a value from the CacheItemRemovedReason enumeration. The values from this enumeration are Expired, Removed (typically by your code or a dependency), Scavenged (typically in response to shortage of available memory), and Unknown (a reserved value you should avoid using).

Therefore, inside your **Refresh** method, you can query the parameter values passed to it to obtain the key and the final cached value of the item, and see why it was removed from the cache. At this point, you can make a decision on what to do about it. In some cases, it may make sense to insert the item into the cache again (such as when a file on which the item depends has changed, or if the data is vital to your application). Of course, you should generally only do this if it expired or was removed. If items are being scavenged because your machine is short of memory, you should think carefully about what you want to put back into the cache!

The example, Detect and refresh expired or removed cache items, illustrates how you can capture items being removed from the cache, and re-cache them when appropriate. The example uses the following implementation of the **ICacheItemRefreshAction** interface to handle the case when the cache contains instances of the **Product** type. For a general situation where you cache different types, you would probably want to check the type before attempting to cast it to the required target type. Also notice that the class carries the **Serializable** attribute. All classes that implement the **ICacheItemRefreshAction** interface must be marked as serializable.

```
<Serializable>()> _
Public Class MyCacheItemRefreshAction
    Implements ICacheItemRefreshAction

    Public Sub Refresh(ByVal key As String, ByVal expiredValue As Object, _
        ByVal removalReason As CacheItemRemovedReason) _
        Implements ICacheItemRefreshAction.Refresh

        ' Item has been removed from cache. Perform desired actions here, based on
        ' the removal reason (for example, refresh the cache with the item).
        Dim expiredItem As Product = DirectCast(expiredValue, Product)
        Console.WriteLine("Cached item {0} was expired in the cache with " _
            & " the reason '{1}'", key, removalReason)
        Console.WriteLine("Item values were: ID = {0}, Name = '{1}', " _
            & "Description = {2}", expiredItem.ID, _
            expiredItem.Name, expiredItem.Description)

        ' Refresh the cache if it expired, but not if it was explicitly removed
        If removalReason = CacheItemRemovedReason.Expired Then
            Dim defaultCache As CacheManager _
                = EnterpriseLibraryContainer.Current.GetInstance(Of _
                CacheManager)("InMemoryCacheManager")
            defaultCache.Add(key, New Product(10, "Exciting Thing", _
                "Useful for everything"), CacheItemPriority.Low, _
                New MyCacheRefreshAction(), _
                New SlidingTime(New TimeSpan(0, 0, 10)))
            Console.WriteLine("Refreshed the item by adding it to the cache again.")
        End If
End Sub
End Class
```

To use the implementation of the **ICacheItemRefreshAction** interface, you simply specify it as the **refreshAction** parameter of the **Add** method when you add an item to the cache. The example uses the following code to cache an instance of the **Product** class that will expire after three seconds.

```
defaultCache.Add(DemoCacheKeys(0), New Product(10, "Exciting Thing", _
 "Useful for everything.", _
 CacheItemPriority.Low, New MyCacheRefreshAction(), _
 New SlidingTime(New TimeSpan(0, 0, 3)))
```

The code then does the same as the earlier examples: it displays the contents of the cache, waits five seconds for the item to expire, displays the contents again, waits five more seconds until the item is scavenged, and then displays the contents for the third time. However, this time the Caching block executes the **Refresh** method of our **ICacheItemRefreshAction** callback as soon as the item is removed from the cache. This callback displays a message indicating that the cached item was removed because it had expired, and that it has been added back into the cache. You can see it in the final listing of the cache contents shown here.

```
The cache contains the following 1 item(s):
Item key 'ItemOne' (CachingExample.Product) = CachingExample.Product

Waiting... Waiting... Waiting... Waiting...

The cache contains the following 1 item(s):
Item with key 'ItemOne' has expired.

Cached item ItemOne was expired in the cache with the reason 'Expired'
Item values were: ID = 10, Name = 'Exciting Thing', Description = Useful for everything

Refreshed the item by adding it to the cache again.

Waiting... Waiting...

The cache contains the following 1 item(s):
Item key 'ItemOne' (CachingExample.Product) = CachingExample.Product
```

## LOADING THE CACHE

If you have configured a persistent backing store for a cache manager, the Caching block will automatically load the in-memory cache from the backing store when you instantiate that cache manager. Usually, this will occur when the application starts up. This is an example of **proactive cache loading**. Proactive cache loading is useful if you know that the data will be required, and it is unlikely to change much. Another approach is to create a
