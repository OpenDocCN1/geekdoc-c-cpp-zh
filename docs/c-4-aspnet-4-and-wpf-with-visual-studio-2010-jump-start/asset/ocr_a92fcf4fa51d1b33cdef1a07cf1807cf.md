The preceding example from makes use of the new cache at `System.Runtime.Caching`. You need to reference this namespace in your ASP.NET project for this to work.

To start, you create a default instance of the cache object.

```
```csharp
ObjectCache cache = MemoryCache.Default;
```
```

You then can work with this cache as you would with the traditional ASP.NET cache object.

```
```csharp
string usernameFromXml = cache["userFromXml"] as string;
```
```

To get the cache started, you need to create an object that defines what type of cache you are dealing with. You can build a custom implementation, or you can use one of the default implementations provided with .NET 4.

```
```csharp
CacheItemPolicy policy = new CacheItemPolicy();
policy.ChangeMonitors.Add(new HostFileChangeMonitor(userFilePaths));
```
```

The `HostFileChangeMonitor` is a means to look at directories and file paths and monitor for change. So, for instance, when the XML file changes, that triggers an invalidation of the cache. Other implementations of the `ChangeMonitor` object include the `FileChangeMonitor` and the `SqlChangeMonitor`.

Running this example, notice that the text *Bill Evjen* is loaded into the cache on the first run, and this text appears in the `Label1` control. Keep your application running and then you can go back to the XML file and change the value, and you will then notice that this causes the cache to be invalidated on the page's refresh.

# ## HISTORICAL DEBUGGING WITH INTELLITRACE

One of the more exciting features of Visual Studio 2010 is a new feature called IntelliTrace. IntelliTrace provides you a historical debugger that allows you to look back in the history of your application running and allows you to jump at previous points in time to see what was occurring.

This feature only works with Visual Studio 2010 Ultimate Edition and is not available in the other editions of the IDE. As of today, it also does not work on 64-bit machines. Therefore, you need to be working with a 32-bit computer to work with the historical debugging feature.

When stopping at a breakpoint within your application, you will now be able to see this history in the IntelliTrace dialog directly as illustrated in the next figure.

![](bbox=[0.255, 0.895, 0.47, 0.985])