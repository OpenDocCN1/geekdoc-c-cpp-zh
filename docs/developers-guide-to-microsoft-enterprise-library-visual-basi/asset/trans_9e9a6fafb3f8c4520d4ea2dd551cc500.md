

带有一个方法的类，该方法从某些数据源（例如数据库或 XML 文件）读取所需数据，并通过为每个项目调用 Add 方法将其加载到缓存中。如果在后台或工作线程上执行此操作，则可以加载缓存而不影响应用程序的交互性或阻塞用户界面。

或者，您可能更愿意使用响应式缓存加载。这种方法适用于可能会也可能不会使用的数据，或者相对易变的数据。在这种情况下（如果您使用持久化后备存储），您可以选择仅在需要加载数据时才实例化缓存管理器。或者，您可以刷新缓存（可能在应用程序结束时），然后按需加载特定项目。例如，您可能发现需要从企业数据存储中检索特定产品的详细信息以在应用程序中显示。此时，如果该项目在合理的时间内可能会再次使用，并且在此期间不太可能更改，则可以选择将其缓存。

## 主动缓存加载

示例“在应用程序启动时主动加载缓存”提供了主动缓存加载的简单演示。在应用程序的启动代码中，您添加代码以使用应用程序所需的项目加载缓存。该示例创建一个 Product 项目列表，然后遍历列表，为每个项目调用缓存管理器的 Add 方法。当然，您将从适合您自己应用程序的位置（例如数据库）获取要缓存的项目。这些项目可能以列表形式提供，或者——例如——通过遍历 DataSet 或 DataReader 中的行来获取。

```
' Create a list of products - may come from a database or other repository
Dim products As New List(Of Product)()
products.Add(New Product(42, "Exciting Thing", _
    "Something that will change your view of life."))
products.Add(New Product(79, "Useful Thing", _
    "Something that is useful for everything."))
products.Add(New Product(412, "Fun Thing", _
    "Something that will keep the grandchildren quiet."))
' Iterate the list loading each one into the cache
Dim i As Integer = 0
While i < products.Count
    theCache.Add(DemoCacheKeys(i), products(i))
    System.Math.Max(System.Threading.Interlocked.Increment(i), i - 1)
End While
```

## 响应式缓存加载

响应式缓存加载的意思是，当您实际需要某个项目时，检查它是否在缓存中，如果不在，则获取它并将其缓存以供将来使用。如果您想要的项目不在缓存中，您可以此时决定获取多个项目。例如，您可能决定在价格查询首次确定产品不在缓存中时加载完整的产品列表。

示例“按需响应式加载缓存”演示了响应式缓存加载的一般模式。在显示缓存内容（以显示它实际上是空的）之后，代码尝试检索 Product 类的缓存实例。请注意，这是一个两步过程，您必须检查返回的值不是 Nothing。如前面本章“缓存中有什么？”部分中所解释的，如果项目最近已过期或已被删除，Contains 方法可能会返回 true。

如果项目在缓存中，代码会显示其属性的值。如果不在缓存中，代码会执行一个例程，使用所有产品加载缓存。此例程与您在前面主动加载缓存的示例中看到的相同。

```
Console.WriteLine("Getting an item from the cache...")
Dim theItem As Product = DirectCast(ffDataCache.GetData(DemoCacheKeys(1)), _
Product)
' You could test for the item in the cache using CacheManager.Contains(key)
' method, but you still must check if the retrieved item is null even
' if the Contains method indicates that the item is in the cache:
If Not theItem Is Nothing Then
    Console.WriteLine("Cached item values are: ID = {0}, Name = '{1}', " _
    & "Description = {2}", theItem.ID, theItem.Name, _
    theItem.Description)
Else
    Console.WriteLine("The item could not be obtained from the cache.")
' Item not found, so reactively load the cache
LoadCacheWithProductList(defaultCache)
Console.WriteLine("Loaded the cache with the list of products.")
ShowCacheContents(defaultCache)
End If
```

在加载产品列表后显示缓存内容后，示例代码随后会再次尝试检索值并显示其属性。您可以在此处查看此示例的完整输出。

```
The cache is empty.

Getting an item from the cache...

The item could not be obtained from the cache.

Loaded the cache with the list of products.

The cache contains the following 3 item(s):
Item key 'ItemOne' (CachingExample.Product) = CachingExample.Product
Item key 'ItemTwo' (CachingExample.Product) = CachingExample.Product
Item key 'ItemThree' (CachingExample.Product) = CachingExample.Product

Getting an item from the cache...
Cached item values are: ID = 79, Name = 'Useful Thing', Description = Something that is useful for everything.
```

通常，执行响应式缓存加载的函数的模式如下：

- 1. 检查项目是否在缓存中，并且返回的值不是 **Nothing**。
- 2. 如果在缓存中找到它，则将其返回给调用代码。
- 3. 如果在缓存中未找到它，则创建或获取对象或值并将其缓存。
- 4. 将此新值或对象返回给调用代码。

## 扩展缓存功能

缓存块（与企业库中的所有其他块一样）包含扩展点，允许您创建自定义提供程序并将其与块集成。如果您想使用不同的缓存机制，也可以替换默认缓存管理器，或者修改源代码以更改块的其他行为。

缓存管理器负责在实例化应用程序块时将项目从持久化后备存储加载到内存中。它还公开操作缓存的方法。如果您想更改缓存块加载或管理缓存项目的方式，例如实现分布式或专用缓存机制，或执行异步或延迟缓存加载，则可以使用 **ICacheManager** 接口并实现其定义的方法和属性。

或者，如果您只想使用不同的后备存储或添加新的过期策略，可以创建自定义后备存储提供程序和过期策略，并使用它们代替内置提供程序和策略。要创建自定义后备存储提供程序，可以实现 **IBackingStore** 接口或继承 **Base BackingStore** 抽象类。要创建自定义过期策略，可以实现 **ICacheItemExpiration** 接口，并可选地实现 **ICacheItemRefreshAction** 接口（用于刷新过期缓存项目的类）。

有关扩展缓存块的更多信息，请参阅随企业库安装的在线文档和帮助文件。

## 摘要

本章介绍了如何使用缓存应用程序块以一致且可配置的方式在应用程序和企业中实现缓存。该块提供非分布式缓存，可以将项目缓存在内存中，并可选择在持久化后备存储（例如独立存储或数据库）中缓存。如果需要，您还可以轻松添加新的后备存储，甚至可以替换缓存管理器，以创建支持其他功能（例如分布式缓存）的机制。

缓存块具有灵活性，以满足大多数类型应用程序的大多数要求。您可以定义多个缓存并对每个缓存进行分区，如果您想为多个缓存使用单个数据库，这很有用。并且，您可以轻松为存储在持久化后备存储中的项目向缓存机制添加加密。

该块还提供广泛的过期机制，包括多种基于时间的过期以及基于文件的过期。与某些缓存机制不同，您可以为每个缓存项目指定多个过期，甚至可以创建自己的自定义过期策略。

除此之外，该块还使管理员和操作员能够使用企业库提供的配置工具通过配置轻松更改行为。他们可以更改缓存的设置（例如轮询频率）、更改块使用的后备存储，以及更改用于加密缓存数据的算法。

本章讨论了所有这些功能，并包含了有关如何在自己的应用程序中使用该块的详细示例。有关缓存块的更多信息，请参阅随企业库安装的在线文档和帮助文件。

