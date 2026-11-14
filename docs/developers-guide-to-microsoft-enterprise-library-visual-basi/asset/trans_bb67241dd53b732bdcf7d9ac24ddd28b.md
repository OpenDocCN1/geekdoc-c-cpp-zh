

## 将项目添加到缓存

现在（终于）代码可以向缓存添加一些项目了。它添加了四个项目：第一个使用 NeverExpired 过期，第二个使用包含文件依赖和扩展格式时间过期的数组，另外两个只是使用本章第一个示例中所示的缓存项目的简单方法。然后代码显示缓存的内容，并等待您按键。

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

此时执行会显示以下输出。

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

当您按键时，代码继续删除文本文件，然后重新显示缓存的内容。然后，与前面的示例一样，它等待项目从缓存中被清除。您看到的输出如下所示。

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

您可以看到，删除文本文件导致依赖于它的键为 ItemTwo 的项目被使无效，并在下一次清除周期中被移除。

此时，代码再次等待您按键。当您按下时，它继续调用缓存管理器的 Remove 方法来移除键为 ItemOne 的项目，并再次显示缓存内容。然后，在您第三次按键后，它调用缓存管理器的 Flush 方法来移除缓存中的所有项目，并再次调用显示缓存内容的方法。这是示例中这部分的代码。

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

此代码执行时您看到的结果如下所示。

```
Press any key to remove ItemOne from the cache...
Cache contains the following 2 item(s):
Item key 'ItemThree' (System.String) = Another cached item
Item key 'ItemFour' (System.String) = And yet another cached item.
Press any key to flush the cache...
The cache is empty.
```

## 刷新缓存

到目前为止，当我们使用 Add 方法向缓存添加项目时，我们为 refreshAction 参数传递了 null 值。您可以使用此参数来检测项目何时从缓存中移除，并发现该项目的值及其被移除的原因。

您必须创建一个实现 ICacheItemRefreshAction 接口的类，并包含一个名为 Refresh 的方法，该方法接受作为参数要移除的项目的键、作为 Object 类型的值，以及来自 CacheItemRemovedReason 枚举的值。此枚举的值为 Expired、Removed（通常由您的代码或依赖项移除）、Scavenged（通常作为响应可用内存不足）和 Unknown（您应避免使用的保留值）。

因此，在您的 **Refresh** 方法中，您可以查询传递给它的参数值以获取项目的键和最终缓存值，并查看它为何从缓存中移除。此时，您可以决定如何处理。在某些情况下，将项目重新插入缓存可能有意义（例如，当项目依赖的文件已更改，或数据对您的应用程序至关重要时）。当然，您通常只应在项目过期或被移除时才这样做。如果项目因机器内存不足而被清除，您应该仔细考虑要将什么重新放入缓存！

示例“检测并刷新过期或已移除的缓存项目”说明了如何捕获从缓存中移除的项目，并在适当时重新缓存它们。该示例使用 **ICacheItemRefreshAction** 接口的以下实现来处理缓存包含 **Product** 类型实例的情况。对于缓存不同类型的一般情况，您可能希望在尝试将其转换为所需目标类型之前先检查类型。还要注意，该类带有 **Serializable** 特性。所有实现 **ICacheItemRefreshAction** 接口的类都必须标记为可序列化。

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

要使用 **ICacheItemRefreshAction** 接口的实现，您只需在向缓存添加项目时将其指定为 **Add** 方法的 **refreshAction** 参数。该示例使用以下代码来缓存 **Product** 类的一个实例，该实例将在三秒后过期。

```
defaultCache.Add(DemoCacheKeys(0), New Product(10, "Exciting Thing", _
 "Useful for everything.", _
 CacheItemPriority.Low, New MyCacheRefreshAction(), _
 New SlidingTime(New TimeSpan(0, 0, 3)))
```

然后代码与前面的示例做同样的操作：它显示缓存的内容，等待五秒钟让项目过期，再次显示内容，再等待五秒钟直到项目被清除，然后第三次显示内容。但是，这次缓存块会在项目从缓存中移除后立即执行我们 **ICacheItemRefreshAction** 回调的 **Refresh** 方法。此回调显示一条消息，指示缓存项目因过期而被移除，并且已重新添加到缓存中。您可以在下面显示的缓存内容最终列表中看到它。

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

## 加载缓存

如果您为缓存管理器配置了持久化后备存储，则在实例化该缓存管理器时，缓存块将自动从后备存储加载内存缓存。通常，这将在应用程序启动时发生。这是 **主动缓存加载** 的示例。如果您知道数据将被需要且不太可能发生太大变化，主动缓存加载很有用。另一种方法是创建一个

