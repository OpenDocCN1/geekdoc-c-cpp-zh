

上述任何类型的零基索引数组。然而，你应该避免使用数组，因为接收数组的自定义属性构造函数是不符合 CLS 标准的。

在应用属性时，你必须传递一个与属性类定义的类型匹配的编译时常量表达式。如果属性类定义了 `Type` 参数、`Type` 字段或 `Type` 属性，你必须使用 `typeof` 运算符，如下代码所示。只要属性类定义了 `Object` 参数、`Object` 字段或 `Object` 属性，你就可以传递 `Int32`、`String` 或任何其他常量表达式（包括 null）。如果常量表达式表示值类型，则在构造属性实例时，该值类型将被装箱。

这里有一个属性及其使用的示例。

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
internal sealed class SomeAttribute : Attribute {
    public SomeAttribute(String name, Object o, Type[] types) {
        // 'name' 指向 String
        // 'o' 指向合法类型之一（必要时进行装箱）
        // 'types' 指向一维、从 0 开始索引的 Types 数组
    }
}

Some("Jeff", Color.Red, new Type[]{ typeof(Console) });
internal sealed class SomeType {
}
```

从逻辑上讲，当编译器检测到目标上应用自定义属性时，编译器通过调用其构造函数来构建属性类的实例，并传递任何指定的参数。编译器使用增强型构造函数语法所指定的值来初始化任何公共字段和属性。现在自定义属性已经初始化，编译器将属性对象的状态序列化到目标的元数据表条目中。

> 重要：我发现开发者思考自定义属性的最佳方式是：类实例被序列化为存储在元数据中的字节流。稍后，在运行时，可以通过反序列化元数据中包含的字节来构造该类的实例。实际上，实际发生的情况是编译器颁发了创建属性类实例所需的信息。每个构造函数参数都以一个 1 字节的类型 ID 后跟值的形式写入。在“序列化”构造函数的参数后，编译器通过写入字段/属性名称、后跟 1 字节的 ID 然后是值，来发射每个指定的字段和属性值。对于数组，首先保存元素计数，然后是每个单独的元素。

## 检测自定义属性的使用

定义属性类本身是没用的。当然，你可以随心所欲地定义属性类并应用你所需要的所有实例，但这只会向程序集写入额外的元数据——你的应用程序代码的行为不会发生变化。

在第 15 节*枚举类型和位标志*中，你已经看到在枚举类型上应用 `Flags` 属性改变了 `System.Enum.ToString` 和 `Format` 方法的行为。这些方法行为不同的原因在于，它们在运行时检查它们正在操作的枚举类型是否关联了 `Flags` 属性元数据。代码可以使用一种称为*反射（reflection）*的技术来查找属性的存在。我将在这里给出一些简短的反射演示，但将在第 23 节“程序集加载与反射”中进行详细讨论。

如果你是负责实现 `Enum.Format` 方法的微软员工，你将按照如下方式实现它：

```csharp
public override string ToString() {
    // 该枚举类型上是否应用了
    // FlagsAttribute 类型的实例？
    if (this.GetType().IsDefined(typeof(FlagsAttribute), false)) {
        // 是：执行将值视为位标记枚举类型的代码。
    } else {
        // ：执行将值视为普通枚举类型的代码。
    }
}
```

这段代码调用 `Type` 的 `IsDefined` 来查看与其关联的 `FlagsAttribute` 类的实例。如果 `IsDefined` 返回 `true`，则枚举类型关联了 `FlagsAttribute` 实例，`Format` 方法知道将值视为一组位标记。如果 `IsDefined` 返回 `false`，`Format` 将值视为普通枚举类型。

因此，如果你定义了自己的类，你必须实现某些代码检查来判断你的属性类实例（在某些目标上）是否存在，并执行某些替代代码路径。这正是自定义属性实用的之处！

FCL（框架类库）提供了许多方法来检查属性是否存在。如果你通过 `System.Type` 检查属性是否存在，可以使用如前所示的 `IsDefined` 方法。然而，有时你想要检查类型以外的目标上的属性，例如程序集或模块。为了讨论讨论，让我们集中在由 `System.Reflection.CustomAttributeExtensions` 类定义的扩展方法上。该类定义了三个静态方法来获取与目标关联的属性：`IsDefined`、`GetAttributes` 和 `GetCustomAttribute`。这些函数中的每一个都有多个重载版本。例如，每个方法都有一个适用于类型成员（类、结构体、枚举、接口、委托、构造函数、方法、属性、字段、事件和返回值）、参数和程序集的版本。还有版本允许你告诉系统向上遍历派生层次，以便将继承的属性包含在结果中。表 18-1 简要描述了每个方法的作用。

## 表 18-1 System.Reflection.CustomAttributeExtensions 反射元数据以寻找符合 CLS 标准的自定义属性的方法

| 方法 | 描述 |
| --- | --- |
| IsDefined | 如果目标至少存在一个指定的 Attribute 派生类的实例，则返回 `true`。此方法是高效的，因为它不会构造（反序列化）任何属性类的实例 |
| GetAttributes | 返回应用到目标的指定属性对象的集合。在编译时使用参数、字段和属性对每个实例进行构造（反序列化）。如果目标没有属性类的实例，则返回一个空集合。此方法通常用于 AllowMultiple 设置为 `true` 的属性 |
| GetCustomAttribute | 如果目标应用了指定属性类的实例，则返回该实例。在编译时使用参数、字段和属性对其进行构造（反序列化）。如果目标没有应用指定的属性，则返回 `null`。此方法通常用于 AllowMultiple 设置为 `false` 的属性。 |

如果你想查看是否应用了属性，可以调用 `IsDefined`，因为它比另外两个方法更高效。然而，你知道当属性应用到目标时，你可以为构造函数指定参数并可选设置字段和属性。使用 `IsDefined` 不构造属性对象、调用其构造函数或设置其字段和属性。

如果你想构造属性对象，可以调用 `GetCustomAttributes` 或 `GetCustomAttribute`。每当调用这些方法时，都会根据源代码中指定的值构造指定属性类型的实例及其每个字段和属性。这些方法返回应用的属性类的引用。

当你调用这些任何方法时，它们在内部必须扫描托管模块的元数据，通过字符串比较来定位指定的自定义属性类。显然，这些操作需要时间。如果你关注性能，应该考虑缓存调用结果，而不是反复请求相同的信息。

System.Reflection 命名空间定义了允许你检查模块元数据内容的类：Assembly、Module、ParameterInfo、MemberInfo、Type、MethodInfo、ConstructorInfo、FieldInfo、EventInfo、PropertyInfo 以及它们相应的 Builder 类。所有这些类都提供了 `IsDefined` 和 `GetCustomAttributes`。

反射类定义的 `GetCustomAttributes` 版本返回 Object 实例数组（`Object[]`）而不是 Attribute 实例数组（`Attribute[]`）。因为反射类能够返回非符合 CLS 标准的属性类的对象。

