
在云世界（尤其是 App Engine 中），我们有许多服务，它们提供云应用可能需要的能力。在本章中，我将讨论 App Engine 提供的一组常见服务。这不会是一次详尽无遗的考察——App Engine 开发有很多服务，Google 的 App Engine 团队也在不断扩展他们提供的服务集合。不过，我们会看一些服务示例，以了解服务提供哪些类型的能力，以及服务接口如何工作。

本章有点像大杂烩。App Engine 提供很多服务，而且大多数都非常简单。它们不值得各自单独用一整章来专门讨论，但彼此之间又不太能很好地组合在一起。你可以根据需要从本章中挑选服务。

## 15.1 快速访问重要内容：Memcache 服务

Memcache 可能是你在实际应用中最常用的服务之一——而且它非常简单，只需一两段就能解释清楚。在你构建的每个 App Engine 应用中，你都会把数据存储在数据存储区（datastore）中。问题在于，从数据存储区检索内容需要时间。初次考虑检索所需时间时，它似乎微不足道——通常只是零点几秒的一小部分。但想想在实时服务中，你可能每秒要处理数千个请求，这些时间就会累积起来。

你不会惊讶地发现，memcache 提供的正是其名称所暗示的东西：内存缓存。你始终把数据的主副本保存在数据存储区中。但你也可以把副本放入 Memcache，一旦放进去，检索它基本上就是瞬时的。

Memcache 是简单服务的一个很好的例子。它通过简单的库 API 提供能力。在幕后，它做了很多非常微妙的工作，以提供一个可从整个 App Engine 云中的机器访问的缓存，但作为 Memcache 的客户端，这一切对你都是不可见的。你只需调用几个函数，它们看起来就像简单的内存缓存。这是一个非常优雅的小服务，而且非常有用。

当然，Memcache 也有一些陷阱。首先，它是不可靠的存储。不能保证你存入 Memcache 的东西以后还在。它是快速获取内容的捷径，而不是像数据存储区那样可靠持久存储的替代品。如果你有一段时间不访问某个缓存对象，或者你往缓存里放了太多东西导致空间耗尽，它就会开始丢弃这些对象。每当你使用 Memcache 时，都需要包含回退到数据存储区的逻辑。不要以为只要把某个东西放进 Memcache，就一定能自动取回来！

其次，Memcache 旨在存储小对象。你发送给 Memcache 的任何请求最大为 1 兆字节。因此你不能存储大于 1 兆字节的任何内容；如果你想通过单个请求访问多个对象（无论是 get 还是 put），所有这些对象的总大小也不能超过 1 兆字节。

所以，例如，如果我们想在聊天应用中使用 Memcache，就不能用它来提供对所有聊天消息列表的快速访问：那个列表很容易增长到超过 1 兆字节。但我们可以用它来存储所有可用聊天室的列表：按照我们的设置方式，聊天室列表永远不会超过 1 兆字节。

### 在 Python 中使用 Memcache

在 Python 中，Memcache 基本上就是一个简单的键/值字典。你用字符串值键把对象放进去。在 Python 中，你可以用如下代码把对象存入缓存：

```python
from google.appengine.api import memcache

memcache.set(key="aString", value=aValue)
```

检索也同样简单：

```python
v = memcache.get(key="aString")
```

如果键不在缓存中，get 将返回值或返回 None。

你也可以在一次调用中执行多个更新/检索。要设置多个值，使用 set_multi 并给它一个字典作为参数：

```python
memcache.set_multi({"key1": "value1", "key2": "value2"})
```

要检索多个值，使用 get_multi 并传入一个键列表。它返回键/值对的字典：

```python
dict = memcache.get_multi(["key1", "key2"])
```

最后，正如我之前提到的，如果一段时间没有被访问，或者空间耗尽，Memcache 会丢弃内容。你可以通过提供 time 参数，给 Memcache 一个关于在丢弃某个内容之前应等待多久的提示。time 参数基本上是说：“请把这个内容在内存中最多保留这么久。” 不能保证它会在那么长时间内一直保持存储；如果缓存在此之前耗尽空间，它仍然会丢弃该值。但直到该时间段到期之前，它不会因为该值太久未使用而将其丢弃。time 参数是你希望保留该值的秒数。因此，例如，要至少存储两个小时，你可以使用 memcache.set(key='foo', value='bar', time=7200)。

### 在 Java 中使用 Memcache

按照 App Engine 的通常风格，在为 Java 提供 Memcache 访问时，App Engine 建立在标准 Java API 之上。Java 中有一个提议的标准缓存处理机制，描述在 Java 规范请求文档 JSR 107 中。App Engine 使用 JSR107 API 提供对 Java 中 Memcache 的访问。同样像往常一样，作为标准过程一部分设计的 API 比自定义设计的 API 更繁琐。因此，从 Java 使用 Memcache 需要更多样板代码。但在概念上，它仍然与我们在 Python 中看到的一样。事实上，它必须如此，因为它们共享底层实现。表面 API 不同，但服务完全相同。缓存不过是从键到值的映射。在 Java 中，值需要可序列化——就像你想把它们放入数据存储区时完全一样。之前我们看到，在 Python 中要把某个东西放入 Memcache，只需执行 memcache.set。在 Java 中，加上样板代码，代码可能如下：

```java
import java.util.Map;
import net.sf.jsr107cache.Cache;
import net.sf.jsr107cache.CacheException;
import net.sf.jsr107cache.CacheFactory;
import net.sf.jsr107cache.CacheManager;
import com.google.appengine.api.memcache.stdimpl.GCacheFactory;

class MyApplicationClass {
    Cache cache;
    Map cacheConfig = new HashMap();
    {
        try {
            CacheFactory factory = CacheManager.getInstance().getCacheFactory();
            cache = factory.createCache(cacheConfig);
        } catch (CacheException e) {
            // don't worry about it
        }
    }
    cache.put(aKey, aValue);
    // ...
}
```

是的，与 Python 版本相比，它有点冗长。而且由于你使用了无类型 map，编译器会生成警告。另外，你还有一个令人担忧的空 catch 子句。别担心。Map 参数接受一组特定于实现的键/值对，但它有意不指定类型，以便实现可以使用它想要的任何键和值。而在 App Engine 中，你总会得到一个缓存实例：CacheFactory 永远不会抛出 CacheException，所以你可以让 catch 块保持为空。

一旦你把样板代码处理好，它基本上就和 Python 中一样简单了。要存储对象，使用 cache.put；要检索对象，使用 cache.get：

```java
cache.put("aKey", aSerializableValue);

value = (ValueType)cache.get("aKey");
```

此外，还有 getAll 和 putAll 方法，它们的工作方式与 Python 的 get_multi 和 set_multi 完全一样。getAll 接受键的集合并返回键/值对的映射；putAll 接受键/值对的映射并更新所有这些键/值对。

不幸的是，用于从 Java 访问 Memcache 的 JSR107 标准不允许你为单个对象设置缓存过期时间。在 Java 中，它是缓存的策略属性。获取缓存时，你可以提供配置参数，其中之一就是缓存过期时间。因此，例如，要请求所有缓存对象至少保留两个小时，你可以在创建缓存时向属性映射添加一个参数：

```java
class MyApplicationClass {
    Cache cache;
    Map cacheConfig = new HashMap();
    cacheConfig.put(GCacheFactory.EXPIRATION_DELTA, 7200);
    {
        try {
            CacheFactory factory = CacheManager.getInstance().getCacheFactory();
            cache = factory.createCache(cacheConfig);
        } catch (CacheException e) {
            // don't worry about it
        }
    }
    // ... rest of the class
}
```
