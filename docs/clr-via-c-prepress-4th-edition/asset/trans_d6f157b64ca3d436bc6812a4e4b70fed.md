
第 3 章“共享程序集和强命名程序集”。不过，我可以通过向 Assembly 的 Load 方法传递以下字符串，强制 CLR 加载与 IL 无关的版本：

```text
"SomeAssembly, Version=2.0.0.0, Culture=neutral,
PublicKeyToken=01234567890abcde, ProcessorArchitecture=MSIL"
```

如今，CLR 支持 ProcessorArchitecture 的五个可能值：MSIL（Microsoft IL）、x86、IA64、AMD64 和 ARM。

**重要** 一些开发者注意到 System.AppDomain 提供了一个 Load 方法。与 Assembly 的静态 Load 方法不同，AppDomain 的 Load 方法是一个实例方法，允许你将程序集加载到指定的 AppDomain 中。此方法设计为由非托管代码调用，它允许宿主将程序集注入特定 AppDomain。托管代码开发者通常不应调用此方法，因为调用 AppDomain 的 Load 方法时，你向它传递一个标识程序集的字符串。然后该方法应用策略，并在常规位置搜索该程序集。回想一下，AppDomain 具有与之关联的设置，这些设置告诉 CLR 如何查找程序集。为加载此程序集，CLR 将使用与指定 AppDomain 关联的设置，而不是调用方 AppDomain 的设置。

然而，AppDomain 的 Load 方法返回对程序集的引用。由于 System.Reflection.Assembly 类不是从 System.MarshalByRefObject 派生的，因此该程序集对象必须按值封送回调用方 AppDomain。但 CLR 现在将使用调用方 AppDomain 的设置来定位并加载该程序集。如果使用调用方 AppDomain 的策略和搜索位置找不到该程序集，则会抛出 FileNotFoundException。此行为通常不可取，这也是应避免使用 AppDomain 的 Load 方法的原因。

在大多数动态可扩展应用程序中，Assembly 的 Load 方法是将程序集加载到 AppDomain 的首选方式。但是，它确实要求你拥有构成程序集标识的所有组成部分。开发者经常编写工具或实用程序（如 ILDasm.exe、PEVerify.exe、CorFlags.exe、GACUtil.exe、SGen.exe、SN.exe、XSD.exe）来对程序集执行某种处理。所有这些工具都接受一个命令行参数，该参数引用程序集文件的路径名（包括文件扩展名）。要加载指定路径名的程序集，请调用 Assembly 的 LoadFrom 方法：

```csharp
public class Assembly {
    public static Assembly LoadFrom(String path);
    // Less commonly used overloads of LoadFrom are not shown
}
```

在内部，LoadFrom 首先调用 System.Reflection.AssemblyName 的静态 GetAssemblyName 方法，该方法打开指定文件，找到 AssemblyDef 元数据表中的条目，提取程序集标识信息，并将其返回到 System.Reflection.AssemblyName 对象中（同时该文件也会被关闭）。然后，LoadFrom 在内部调用 Assembly 的 Load 方法，并将 AssemblyName 对象传递给它。此时，CLR 应用版本绑定重定向策略，并搜索各个位置以查找匹配的程序集。如果 Load 找到该程序集，就会加载它，并返回一个表示已加载程序集的 Assembly 对象；LoadFrom 返回此值。如果 Load 未能找到程序集，LoadFrom 将加载 LoadFrom 参数中指定路径名处的程序集。当然，如果具有相同标识的程序集已加载，LoadFrom 只会返回表示已加载程序集的 Assembly 对象。

顺便说一下，LoadFrom 方法允许你将 URL 作为参数传递。下面是一个示例：

```csharp
Assembly a = Assembly.LoadFrom(@"http://www.wintellect.com/SomeAssembly.dll");
```

当你传入 Internet 位置时，CLR 会下载该文件，将其安装到用户的下载缓存中，并从那里加载该文件。请注意，你必须处于联机状态，否则将抛出异常。然而，如果该文件之前已下载，并且 Windows Internet Explorer 已设置为脱机工作（参见 Internet Explorer“文件”菜单中的“脱机工作”菜单项），则将使用之前下载的文件，并且不会抛出异常。你也可以调用 UnsafeLoadFrom，它可以加载从 Web 下载的程序集，同时绕过一些安全检查。

**重要** 单台计算机上可能存在多个具有相同标识的不同程序集。由于 LoadFrom 在内部调用 Load，CLR 可能不会加载指定的文件，而是加载另一个文件，从而导致意外行为。强烈建议程序集的每次生成都更改版本号；这可确保每个版本都有其自己的标识，因此 LoadFrom 现在会按预期工作。

Microsoft Visual Studio 的 UI 设计器和其他工具通常使用 Assembly 的 LoadFile 方法。此方法可以从任意路径加载程序集，并且可用于将具有相同标识的程序集多次加载到单个 AppDomain 中。当在设计器/工具中对应用程序的 UI 进行更改并且用户重新生成程序集时，就可能发生这种情况。通过 LoadFile 加载程序集时，CLR 不会自动解析任何依赖项；你的代码必须注册到 AppDomain 的 AssemblyResolve 事件，并让你的事件回调方法显式加载任何依赖程序集。

如果你正在构建一个仅通过反射分析程序集元数据的工具（如本章后面所述），并且希望确保程序集内部包含的任何代码都不执行，那么加载程序集的最佳方式是使用 Assembly 的 ReflectionOnlyLoadFrom 方法，或在少数情况下使用 Assembly 的 ReflectionOnlyLoad 方法。下面是这两个方法的原型：

```csharp
public class Assembly {
   public static Assembly ReflectionOnlyLoadFrom(String assemblyFile);
   public static Assembly ReflectionOnlyLoad(String assemblyString);
   // Less commonly used overload of ReflectionOnlyLoad is not shown
}
```

ReflectionOnlyLoadFrom 方法将加载由路径指定的文件；不会获取该文件的强名称标识，也不会在 GAC 或其他位置搜索该文件。ReflectionOnlyLoad 方法将搜索指定的程序集，搜索位置包括 GAC、应用程序基目录、私有路径和代码基。但是，与 Load 方法不同，ReflectionOnlyLoad 方法不应用版本策略，因此你将获得你指定的确切版本。如果你想自己对程序集标识应用版本策略，可以将字符串传入 AppDomain 的 ApplyPolicy 方法。

当使用 ReflectionOnlyLoadFrom 或 ReflectionOnlyLoad 加载程序集时，CLR 禁止执行该程序集中的任何代码；任何尝试执行使用这两种方法之一加载的程序集中的代码的操作，都会导致 CLR 抛出 InvalidOperationException。这些方法允许工具加载以下程序集：被延迟签名的程序集、通常需要安全权限（否则其加载会被阻止）的程序集，或为不同 CPU 架构创建的程序集。

在使用反射分析通过这两种方法之一加载的程序集时，代码经常必须向 AppDomain 的 ReflectionOnlyAssemblyResolve 事件注册一个回调方法，以手动加载任何被引用的程序集（如果需要，可调用 AppDomain 的 ApplyPolicy 方法）；CLR 不会为你自动执行此操作。调用回调方法时，它必须调用 Assembly 的 ReflectionOnlyLoadFrom 或 ReflectionOnlyLoad 方法，以显式加载被引用的程序集，并返回对此程序集的引用。

**注意** 人们经常询问程序集卸载的问题。遗憾的是，CLR 不支持卸载单个程序集的能力。如果 CLR 允许这样做，那么当线程从某个方法返回到已卸载程序集中的代码时，你的应用程序就会崩溃。CLR 追求的是可靠性、安全性，而允许应用程序以这种方式崩溃将与其目标背道而驰。如果要卸载程序集，必须卸载包含它的整个 AppDomain。第 22 章对此进行了详细讨论。

看起来，使用 ReflectionOnlyLoadFrom 或 ReflectionOnlyLoad 方法加载的程序集似乎可以被卸载。毕竟，这些程序集中的代码不允许执行。但是，CLR 也不允许卸载通过这两种方法之一加载的程序集。原因是，一旦以这种方式加载了程序集，你仍然可以使用反射来创建引用这些程序集内部定义的元数据的对象。卸载该程序集将要求以某种方式使这些对象失效。跟踪这一点在实现和执行速度方面的成本太高。

许多应用程序由一个 EXE 文件和它所依赖的许多 DLL 文件组成。部署此应用程序时，必须部署所有文件。但是，有一种技术可用于仅部署单个 EXE 文件。首先，找出你的 EXE 文件所依赖的、且并非作为 Microsoft .NET Framework 本身的一部分提供的所有 DLL 文件。然后将这些 DLL 添加到你的 Visual Studio 项目中。对于添加的每个 DLL 文件，显示其属性，并将其“生成操作”更改为“嵌入的资源”。这会使 C# 编译器将 DLL 文件嵌入到你的 EXE 文件中，然后你就可以部署这一个 EXE 文件。

在运行时，CLR 将无法找到依赖的 DLL 程序集，这会成为一个问题。为解决此问题，在应用程序初始化时，向 AppDomain 的 AssemblyResolve 事件注册一个回调方法。回调方法的代码应类似如下：

```csharp
private static Assembly ResolveEventHandler(Object sender, ResolveEventArgs args) {
    String dllName = new AssemblyName(args.Name).Name + ".dll";

    var assem = Assembly.GetExecutingAssembly();
    String resourceName = assem.GetManifestResourceNames().FirstOrDefault(rn => rn.EndsWith(dllName));
```
