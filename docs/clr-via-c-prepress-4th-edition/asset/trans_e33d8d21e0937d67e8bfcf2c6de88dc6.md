
回想一下，System.Object 定义了一个名为 GetType 的公共非虚实例方法。当调用此方法时，CLR 会确定指定对象的类型，并返回对其 Type 对象的引用。由于在 AppDomain 中每种类型只有一个 Type 对象，因此可以使用相等和不相等运算符来判断两个对象是否为同一类型。

```csharp
private static Boolean AreObjectsTheSameType(object o1, object o2) {
    return o1.GetType() == o2.GetType();
}
```

除了调用 Object 的 GetType 方法外，FCL 还提供了几种获取 Type 对象的方法：

- System.Type 类型提供了静态 GetType 方法的几个重载版本。此方法的所有版本都接受一个 String。该字符串必须指定类型的完整名称（包括其命名空间）。请注意，编译器支持的基元类型名称（例如 C# 的 int、string、bool 等）是不允许的，因为这些名称对 CLR 没有任何意义。如果字符串仅仅是类型的名称，则该方法会检查调用程序集，以查看它是否定义了指定名称的类型。如果定义了，则返回对相应 Type 对象的引用。

    如果调用程序集未定义指定的类型，则会检查 MSCorLib.dll 定义的类型。如果仍然找不到名称匹配的类型，则返回 null 或引发 System.TypeLoadException，具体取决于你调用了 GetType 方法的哪个重载以及传递了什么参数。FCL 文档对此方法有完整说明。

    你可以将程序集限定类型字符串（例如 "System.Int32, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"）传递给 GetType。在这种情况下，GetType 将在指定的程序集中查找该类型（如有必要，会加载该程序集）。

- System.Type 类型提供了静态的 ReflectionOnlyGetType 方法。此方法的行为与上一项中提到的 GetType 方法类似，不同之处在于加载的类型可以反射，但不能执行。

- System.TypeInfo 类型提供以下实例成员：DeclaredNestedTypes 和 GetDeclaredNestedType。

- System.Reflection.Assembly 类型提供以下实例成员：GetType、DefinedTypes 和 ExportedTypes。

**注意** Microsoft 为类型名称和程序集限定类型名称定义了一种巴科斯-诺尔范式语法，用于构造将传递给反射方法的字符串。当你使用反射时，了解该语法会非常方便，特别是在处理嵌套类型、泛型类型、泛型方法、引用参数或数组时。有关完整语法，请参阅 FCL 文档，或进行网络搜索“Backus-Naur Form Grammar for Type”

TypeInfo 公开的属性。

## 构建异常派生类型的层次结构

下面显示的代码使用了本章已经讨论过的许多概念，将一堆程序集加载到 AppDomain 中，并显示所有最终派生自 System.Exception 的类。顺便说一句，这是我编写的程序，用于构建第 20 章“异常和状态管理”中“FCL 定义的异常类”一节所显示的异常层次结构。

```csharp
public static void Go() {
    // Examine and load the assemblies that we want to reflect over
    LoadAssemblies();

    // Filter & sort all the types
    var allTypes =
        (from a in AppDomain.CurrentDomain.GetAssemblies()
         from t in a.ExportedTypes
         where typeof(Exception).GetTypeInfo().IsAssignableFrom(t.GetTypeInfo())
         orderby t.Name
         select t).ToArray();

    // Build the inheritance hierarchy tree and show it
    Console.WriteLine(WalkInheritanceHierarchy(new StringBuilder(), 0, typeof(Exception), allTypes));
}
```

```csharp
private static StringBuilder WalkInheritanceHierarchy(
    StringBuilder sb, Int32 indent, Type baseType, IEnumerable<Type> allTypes) {
    String spaces = new String(' ', indent * 3);
    sb.AppendLine(spaces + baseType.FullName);
    foreach (var t in allTypes) {
        if (t.GetTypeInfo().BaseType != baseType) continue;
        WalkInheritanceHierarchy(sb, indent + 1, t, allTypes);
    }
    return sb;
}
```

```csharp
private static void LoadAssemblies() {
    String[] assemblies = {
        "System,                 PublicKeyToken={0}",
        "System.Core,             PublicKeyToken={0}",
        "System.Data,             PublicKeyToken={0}",
        "System.Design,           PublicKeyToken={1}",
        "System.DirectoryServices, PublicKeyToken={1}",
        "System.Drawing,          PublicKeyToken={1}",
        "System.Drawing.Design,   PublicKeyToken={1}",
        "System.Management,       PublicKeyToken={1}",
        "System.Messaging,        PublicKeyToken={1}",
        "System.Runtime.Remoting, PublicKeyToken={0}",
        "System.Security,         PublicKeyToken={1}",
        "System.ServiceProcess,   PublicKeyToken={1}",
        "System.Web,              PublicKeyToken={1}",
        "System.Web.RegularExpressions, PublicKeyToken={1}",
        "System.Web.Services,        PublicKeyToken={1}",
        "System.Xml,                PublicKeyToken={0}",
    };

    String EcmaPublicKeyToken = "b77a5c561934e089";
    String MSPublicKeyToken = "b03f5f7f11d50a3a";

    // Get the version of the assembly containing System.Object
    // We'll assume the same version for all the other assemblies
    Version version = typeof(System.Object).Assembly.GetName().Version;

    // Explicitly load the assemblies that we want to reflect over
    foreach (String a in assemblies)
    {
        String AssemblyIdentity =
            String.Format(a, EcmaPublicKeyToken, MSPublicKeyToken) +
                ", Culture=neutral, Version=" + version;
        Assembly.Load(AssemblyIdentity);
    }
}
```

## 构造类型的实例

一旦你拥有了对 Type 派生对象的引用，你可能想要构造该类型的实例。FCL 提供了几种机制来实现这一点：

- **System.Activator 的 CreateInstance 方法** Activator 类提供了其静态 CreateInstance 方法的几个重载。调用此方法时，你可以传递对 Type 对象的引用，或传递标识要创建对象类型的 String。接受类型参数的版本更简单。你可以为该类型的构造函数传递一组参数，该方法返回对新对象的引用。

    此方法中使用字符串指定所需类型的版本要稍微复杂一些。首先，你还必须指定一个标识定义该类型的程序集的字符串。其次，如果你正确配置了远程处理选项，这些方法允许你构造远程对象。第三，这些版本不返回对新对象的引用。相反，它们返回一个 System.Runtime.Remoting.ObjectHandle（派生自 System.MarshalByRefObject）。

    ObjectHandle 是一种类型，它允许在一个 AppDomain 中创建的对象传递到其他 AppDomain，而不强制该对象具体化。当你准备好具体化该对象时，可以调用 ObjectHandle 的 Unwrap 方法。此方法会在调用 Unwrap 的 AppDomain 中加载定义正在具体化的类型的程序集。如果对象按引用封送，则会创建代理类型和对象。如果对象按值封送，则会反序列化副本。

- **System.Activator 的 CreateInstanceFrom 方法** Activator 类还提供了一组静态 CreateInstanceFrom 方法。这些方法的行为与 CreateInstance 方法相同，只是你必须始终通过字符串参数指定类型及其程序集。

    使用 Assembly 的 LoadFrom 方法（而不是 Load）将程序集加载到调用 AppDomain 中。由于这些方法都不接受 Type 参数，因此所有 CreateInstanceFrom 方法都返回对 ObjectHandle 的引用，必须对其进行解包。

- **System.AppDomain 的方法** AppDomain 类型提供了四个实例方法（每个都有几个重载）来构造类型的实例：CreateInstance、CreateInstanceAndUnwrap、CreateInstanceFrom 和 CreateInstanceFromAndUnwrap。这些方法的工作方式与 Activator 的方法相同，只是这些方法是实例方法，允许你指定应在哪个 AppDomain 中构造对象。以 Unwrap 结尾的方法是为了方便而存在，这样你就不必进行额外的方法调用。

- **System.Reflection.ConstructorInfo 的 Invoke 实例方法** 使用对 TypeInfo 对象的引用，你可以绑定到特定构造函数，并获取对该构造函数的 ConstructorInfo 对象的引用。然后，你可以使用对 ConstructorInfo 对象的引用来调用其 Invoke 方法。类型始终在调用 AppDomain 中创建，并返回对新对象的引用。我将在本章后面更详细地讨论此方法。

**注意** CLR 不要求值类型定义任何构造函数。然而，这会带来一个问题，因为前面列表中的所有机制都通过调用其构造函数来构造对象。不过，Activator 的 CreateInstance 方法允许你在不调用构造函数的情况下创建值类型的实例。如果你希望在不调用构造函数的情况下创建值类型的实例，则必须调用接受单个 Type 参数的 CreateInstance 方法版本，或接受 Type 和 Boolean 参数的版本。

刚才列出的机制允许你为除数组（派生自 System.Array）和委托（派生自 System.MulticastDelegate 的类型）之外的所有类型创建对象。要创建数组，应调用 Array 的静态 CreateInstance 方法（存在几个重载版本）。所有版本的 CreateInstance 的第一个参数都是对数组中所需元素类型的引用。CreateInstance 的其他参数允许你指定维度和界限的各种组合。要创建委托，应调用 MethodInfo 的 CreateDelegate 方法。所有版本的 CreateDelegate 的第一个参数都是对要创建的委托类型的引用。CreateDelegate 的其他参数允许你指定在调用实例方法时应将哪个对象作为 this 参数传递。

要构造泛型类型的实例，首先获取对开放类型的引用，然后调用 Type 的 MakeGenericType 方法，传入你想用作类型实参的类型数组。然后，获取返回的 Type 对象，并将其传入上面列出的各种方法之一。下面是一个示例：

```csharp
using System;
using System.Reflection;
```

