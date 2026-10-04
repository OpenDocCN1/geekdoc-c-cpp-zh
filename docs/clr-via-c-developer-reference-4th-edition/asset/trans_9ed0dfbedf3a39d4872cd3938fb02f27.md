
要加载指定路径名的程序集，你需要调用 `Assembly.LoadFrom` 方法。

```csharp
public class Assembly {
    public static Assembly LoadFrom(String path);
    // 未显示较常用的 LoadFrom 重载
}
```

在内部，`LoadFrom` 会调用 `System.Reflection.AssemblyName` 的静态方法 `GetAssemblyName`，该方法打开指定的文件，找到 `AssemblyDef` 元数据表条目，提取程序集身份信息并以 `System.Reflection.AssemblyName` 对象返回（文件随后会被关闭）。然后，`LoadFrom` 在内部调用 `Assembly` 的 `Load` 方法，并传递 `AssemblyName` 对象。此时，CLR 会执行版本绑定重定向策略，并在各个位置查找匹配的程序集。如果 `Load` 找到了程序集，它将加载它，并返回一个表示已加载程序集的 `Assembly` 对象；`Load` 返回其值。如果 `Load` 未找到程序集，`LoadFrom` 将根据其参数中指定的路径名称加载程序集。或者，如果已经加载了相同身份的程序集，`LoadFrom` 仅返回一个表示已加载程序集的 `Assembly` 对象。

顺便一下，`LoadFrom` 允许你将 URL 作为参数。这是一个示例：

```csharp
Assembly a = Assembly.LoadFrom("http://Wintellect.com/SomeAssembly.dll");
```

当你传递 Internet 位置时，CLR 会下载该文件，将其安装到用户的缓存中并加载文件数据。注意，你可能需要在线，否则将抛出异常。如果文件之前已经下载过，并且 Windows Internet Explorer 设置为离线工作（查看 Internet Explorer 文件菜单中的“离线工作”菜单），将使用之前下载的文件，且不会抛出异常。你还可以调用 `UnsafeLoadFrom`，它可以加载 Web 下载的程序集并绕过安全检查。

> **重要**：在单台机器上可能存在具有相同身份的多个程序集。由于 `LoadFrom` 是内部调用的，CLR 可能不会加载指定的文件而是加载另一个文件，导致产生意料之外的行为。强烈建议在构建程序集时指定版本号；这可以确保每个版本都有自己的身份，并且正因如此，`LoadFrom` 将按预期方式工作。

Visual Studio 的 UI 设计器和其他工具通常使用 `Assembly` 的 `LoadFile` 方法。该方法可以从任何路径加载程序集，并用于在单个 `AppDomain` 中多次加载具有相同身份的程序集。这发生在设计器/工具中对应用程序的 UI 进行更改且用户重新加载程序集时。通过 `LoadFile` 加载程序集时，CLR 不会自动解析任何依赖项；你的代码必须注册 `AppDomain` 的 `AssemblyResolve` 事件，并由你的回调函数显式地加载任何依赖程序集。

如果你正在构建一个仅通过反射分析程序集元数据的工具（如本章稍后讨论的），并且你想确保程序集内部的任何代码都不会执行，那么加载程序集的最佳方法是使用 `Assembly` 的 `ReflectionOnlyFrom` 方法，或者在某些较少的情况下，使用 `Assembly` 的 `ReflectionOnlyLoad` 方法。以下是这两个方法的原型。

```csharp
public class Assembly {
    public static Assembly ReflectionOnlyLoad(String assemblyFile);
    public static Assembly ReflectionOnlyLoad(String assemblyString);
    // 未显示常用的 ReflectionOnlyLoad 重载
}
```

`ReflectionOnlyLoad` 方法通过路径加载文件；不会获取身份的强名称，且不会在 GAC 或其他地方搜索文件。`ReflectionOnlyLoad` 方法会在 GAC、应用程序基目录、私有路径和代码中搜索指定的程序集。然而，与 `Load` 方法不同，`ReflectionOnlyLoad` 方法不应用版本策略，因此你将获得指定的精确版本。如果你想自己对程序集身份应用版本策略，可以将字符串传递给 `AppDomain` 的 `ApplyPolicy` 方法。

当使用 `ReflectionOnlyFrom` 或 `ReflectionOnlyLoad` 加载程序集时，CLR 禁止任何代码执行；任何尝试这两种方法执行已加载程序集代码的尝试都会导致 CLR 抛出 `InvalidOperationException`。这些方法允许加载延迟签名的、通常需要安全权限才能防止加载的程序集，或为不同的 CPU 架构创建的程序集。

通常，使用反射分析通过这两种方法之一加载的程序集时，代码必须向 `AppDomain` 的 `ReflectionOnlyAssembly-Resolve` 事件注册回调方法，以手动加载任何引用的程序集（如果需要，调用 `AppDomain` 的 `ApplyPolicy` 方法）；CLR 不会自动为你完成操作。当回调被调用时，它必须调用 `Assembly` 的 `ReflectionOnlyLoadFrom` 或 `ReflectionOnlyLoad` 方法来显式加载引用的程序集并返回其引用。

> **注意**：人们经常询问程序集卸载的问题。遗憾的是，CLR 不支持卸载单个程序集的功能。如果 CLR 允许这样做，当线程从方法代码返回已卸载的程序集时，你的应用程序将会崩溃。CLR 关注健壮性和安全性，允许应用程序以这种方式崩溃将与其目标背道而驰。如果你想卸载程序集，你必须卸载包含它的整个 `AppDomain`。这在第 22 章中详细讨论过。

似乎使用 `ReflectionOnlyLoadFrom` 或 `ReflectionOnlyLoad` 方法加载的程序集可以被卸载。毕竟，在这些程序集中是不允许执行的。然而，CLR 也不允许通过这两种方法加载的程序集被卸载。原因是程序集以此方式加载后，你仍然使用反射创建引用这些程序集内部定义的元数据的对象。在执行速度方面，跟踪这些将会非常昂贵。

![img/0ce3b788d061e3d09554b1a34f612_png]

许多应用程序使用依赖许多 DLL 文件的 EXE 文件。然而，在部署此应用程序时，有一种技术可以使用你来部署单个文件。首先，将这些 DLL 添加到 Visual Studio 项目。对于每个 DLL，选择其属性并将“生成操作”（Build Action）更改为“嵌入资源”（Embedded Resource）。这会导致 C# 编译器将 DLL 嵌入到你的 EXE 中，你可以使用 `AssemblyResolve` 事件初始化回调方法。代码看起来像这样：

```csharp
private static ResolveEventHandler(Object sender, ResolveEventArgs args) {
  String dllName = new Assembly(args.Name) + ".dll";

  var assemble = Assembly.ExecutingAssembly();
  String resourceName = assemble.GetResourceNames().FirstOrDefault(name => name.EndsWith(dllName));
  if (resourceName == null) return null; // 找到找到，可能另一个处理程序会找到它
  using (var stream = assemble.GetResourceStream(resourceName)) {
    Byte[] assemblyData = new Byte[stream.Length];
    stream.Read(assemblyData, 0, stream.Length);
    return Assembly.Load(assemblyData);
  }
}
```
现在，当方法第一次调用引用依赖 DLL 中的类型时，将触发 `AssemblyResolve` 事件，之前的回调代码将找到嵌入资源并加载它。

# 使用反射构建动态扩展应用程序

如你所知，元数据存储在许多表中。当你构建程序集或模块时，你使用的编译器会创建类型定义表、字段定义表、方法表等。`System.Reflection` 命名空间包含几种类型的表，允许你编写反射（或解析）这些表的代码。实际上，该命名空间中的类型为程序集或模块包含的元数据提供了对象模型。

使用这些对象模型，你可以轻松枚举类型元数据表中的所有类型。对于每个类型，你可以获取其基类型、实现的接口以及与该类型相关的标志。`System.Reflection` 命名空间中的其他类型允许你查询类型的字段、方法和事件。你还可以发现应用到任何元数据实体上的自定义属性。
