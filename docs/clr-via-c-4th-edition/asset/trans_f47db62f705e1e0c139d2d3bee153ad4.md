
- System.TypeInfo 类型提供以下实例成员：DeclaredNestedTypes 和 GetDeclaredNestedType。
- System.Reflection.Assembly 类型提供以下实例成员：GetType、DefinedTypes 和 ExportedTypes。

> **注意** Microsoft 已为类型名和程序集限定类型名定义了 Backus-Naur Form 文法，该文法用于构造将传递给反射方法的字符串。在使用反射时，了解该文法会非常有用，尤其是在处理嵌套类型、泛型类型、泛型方法、引用参数或数组时。完整文法请参阅 FCL 文档，或在网上搜索“Backus-Naur Form Grammar for Type Names”。你还可以查看 Type 和 TypeInfo 的 MakeArrayType、MakeByRefType、MakeGenericType 和 MakePointerType 方法。

许多编程语言还提供了一个运算符，使你能够从编译时已知的类型名获取 Type 对象。在可能的情况下，你应使用该运算符来获取对 Type 的引用，而不是使用前面列表中的任何方法，因为该运算符通常生成更快的代码。在 C# 中，该运算符称为 typeof，你通常使用该运算符将后期绑定的类型信息与早期绑定（编译时已知）的类型信息进行比较。以下代码演示了它的用法示例。

```
    private static void SomeMethod(Object o) {
        // GetType returns the type of the object at runtime (late-bound)
        // typeof returns the type of the specified class (early-bound)
        if (o.GetType() == typeof(FileInfo)) { ... }
        if (o.GetType() == typeof(DirectoryInfo)) { ... }
    }
```

> **注意** 代码中的第一个 if 语句检查变量 o 是否引用 FileInfo 类型的对象；它并不检查 o 是否引用派生自 FileInfo 类型的对象。换言之，前面的代码测试的是精确匹配，而不是兼容匹配；如果使用强制转换或 C# 的 is 或 as 运算符，则会得到兼容匹配。

如前所述，Type 对象表示一个类型引用，它是一个轻量级对象。如果你想进一步了解该类型本身，则必须获取 TypeInfo 对象，它表示类型定义。你可以通过调用 System.Reflection.IntrospectionExtensions 的 GetTypeInfo 扩展方法，将 Type 对象转换为 TypeInfo 对象。

```
    Type typeReference = ...;  // For example: o.GetType() or typeof(Object)
    TypeInfo typeDefinition = typeReference.GetTypeInfo();
```

类型。其次，如果已正确配置远程处理选项，这些方法允许你构造远程对象。第三，这些版本不会返回对新对象的引用。相反，它们返回 `System.Runtime.Remoting.ObjectHandle`（派生自 `System.MarshalByRefObject`）。

`ObjectHandle` 是一种类型，它允许在一个 AppDomain 中创建的对象传递到其他 AppDomain，而不必强制该对象具体化。当你准备好具体化该对象时，调用 `ObjectHandle` 的 `Unwrap` 方法。此方法会在调用 `Unwrap` 的 AppDomain 中加载定义正在具体化的类型的程序集。如果对象按引用封送，则会创建代理类型和代理对象。如果对象按值封送，则会反序列化副本。

- **`System.Activator` 的 `CreateInstanceFrom` 方法** `Activator` 类还提供了一组静态 `CreateInstanceFrom` 方法。这些方法的行为与 `CreateInstance` 方法完全相同，不同之处在于你必须始终通过字符串参数指定类型及其程序集。程序集通过使用 `Assembly` 的 `LoadFrom` 方法（而不是 `Load`）加载到调用 AppDomain 中。由于这些方法都不接受 `Type` 参数，因此所有 `CreateInstanceFrom` 方法都返回对 `ObjectHandle` 的引用，而该引用必须被解包。

- **`System.AppDomain` 的方法** `AppDomain` 类型提供四个实例方法（每个方法都有若干重载），用于构造某个类型的实例：`CreateInstance`、`CreateInstanceAndUnwrap`、`CreateInstanceFrom` 和 `CreateInstanceFromAndUnwrap`。这些方法的工作方式与 `Activator` 的方法相同，不同之处在于这些方法是实例方法，允许你指定应在哪个 `AppDomain` 中构造对象。以 `Unwrap` 结尾的方法是为了方便而存在，这样你就不必再进行额外的方法调用。

- **`System.Reflection.ConstructorInfo` 的 `Invoke` 实例方法** 使用对 `TypeInfo` 对象的引用，可以绑定到特定构造函数，并获取对该构造函数的 `ConstructorInfo` 对象的引用。然后，你可以使用该 `ConstructorInfo` 对象的引用来调用其 `Invoke` 方法。类型始终在调用 AppDomain 中创建，并返回对新对象的引用。我还会在本章后面更详细地讨论此方法。

> **注意** CLR 不要求值类型定义任何构造函数。然而，这会带来一个问题，因为前面列表中的所有机制都通过调用对象的构造函数来构造对象。不过，`Activator` 的 `CreateInstance` 方法允许你在不调用构造函数的情况下创建值类型的实例。如果要在不调用构造函数的情况下创建值类型的实例，你必须调用接受单个 `Type` 参数的 `CreateInstance` 方法版本，或调用接受 `Type` 和 `Boolean` 参数的版本。

前面列出的机制允许你为除数组（派生自 System.Array 的类型）和委托（派生自 System.MulticastDelegate 的类型）之外的所有类型创建对象。要创建数组，应调用 Array 的静态 CreateInstance 方法（存在多个重载版本）。所有版本的 CreateInstance 的第一个参数都是对你希望在数组中包含的元素类型的引用。CreateInstance 的其他参数允许你指定维度和边界的各种组合。要创建委托，应调用 MethodInfo 的 CreateDelegate 方法。所有版本的 CreateDelegate 的第一个参数都是对你希望创建的委托类型的引用。CreateDelegate 的其他参数允许你指定在调用实例方法时应将哪个对象作为 this 参数传递。

要构造泛型类型的实例，首先获取对开放类型的引用，然后调用 Type 的 MakeGenericType 方法，并传入一个你希望用作类型实参的类型数组。接着，取得返回的 Type 对象，并将其传入前面列出的某个方法。下面是一个示例。

```csharp
using System;
using System.Reflection;

internal sealed class Dictionary<TKey, TValue> { }

public static class Program {
    public static void Main() {
        // Get a reference to the generic type's type object
        Type openType = typeof(Dictionary<,>);

        // Close the generic type by using TKey=String, TValue=Int32
        Type closedType = openType.MakeGenericType(typeof(String), typeof(Int32));

        // Construct an instance of the closed type
        Object o = Activator.CreateInstance(closedType);

        // Prove it worked
        Console.WriteLine(o.GetType());
    }
}
```

如果编译并运行前面的代码，将得到以下输出。

```
Dictionary`2[System.String,System.Int32]
```

## 设计支持加载项的应用程序

在构建可扩展应用程序时，接口应当成为核心。你可以使用基类而不是接口，但通常更倾向于使用接口，因为它允许加载项开发者选择自己的基类。例如，假设你正在编写一个应用程序，并希望其他人能够创建你的应用程序可以无缝加载和使用的类型。

