
> **重要** 你应当把特性视为一个逻辑状态容器。也就是说，虽然特性类型是一个类，但这个类应当保持简单。该类应当只提供一个公共构造函数，用于接受特性的必需（或位置）状态信息；该类还可以提供公共字段/属性，用于接受特性的可选（或命名）状态信息。该类不应提供任何公共方法、事件或其他成员。
> 
> 一般来说，我总是反对使用公共字段，对特性也是如此。使用属性要好得多，因为如果你以后决定更改特性类的实现方式，这会提供更大的灵活性。

到目前为止，**FlagsAttribute** 类的实例可以应用于任何目标，但这个特性实际上应当只应用于枚举类型。把该特性应用于属性或方法毫无意义。为了告诉编译器这个特性可以合法地应用于哪些位置，你要把 **System.AttributeUsageAttribute** 类的实例应用于该特性类。下面是新的代码：

```csharp
namespace System {
    [AttributeUsage(AttributeTargets.Enum, Inherited = false)]
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
        }
    }
}
```

在这个新版本中，我把 **AttributeUsageAttribute** 的实例应用到了该特性上。毕竟，特性类型只是一个类，而类是可以应用特性的。**AttributeUsage** 特性是一个简单的类，它允许你向编译器指定自定义特性可以合法地应用于哪些位置。所有编译器都内置支持该特性，并且当用户定义的自定义特性被应用于无效目标时，编译器会生成错误。在这个示例中，**AttributeUsage** 特性指定 **Flags** 特性的实例只能应用于枚举类型目标。

因为所有特性都只是类型，所以你可以很容易地理解 **AttributeUsageAttribute** 类。该类的 FCL 源代码如下所示：

```csharp
[Serializable]
[AttributeUsage(AttributeTargets.Class, Inherited=true)]
public sealed class AttributeUsageAttribute : Attribute {
    internal static AttributeUsageAttribute Default =
        new AttributeUsageAttribute(AttributeTargets.All);

    internal Boolean m_allowMultiple = false;
    internal AttributeTargets m_attributeTarget = AttributeTargets.All;
    internal Boolean m_inherited = true;

    // This is the one public constructor
    public AttributeUsageAttribute(AttributeTargets validOn) {
        m_attributeTarget = validOn;
    }
}
```

对大多数特性而言，将其多次应用于同一个目标没有意义。例如，把 **Flags** 或 **Serializable** 特性多次应用于同一个目标不会带来任何好处。事实上，如果你尝试编译下面的代码，编译器会报告以下消息：**“error CS0579: Duplicate 'Flags' attribute.”**

```csharp
[Flags][Flags]
internal enum Color {
}
```

不过，对于少数特性来说，将同一特性多次应用于同一个目标确实有意义。在 FCL 中，**ConditionalAttribute** 特性类允许将自身的多个实例应用于同一个目标。如果你没有显式地将 **AllowMultiple** 设置为 **true**，那么你的特性最多只能应用于一个选定目标一次。

**AttributeUsageAttribute** 的另一个属性 **Inherited** 指示：当特性应用于基类时，是否应同时应用于派生类和重写方法。以下代码演示了特性被继承意味着什么：

```csharp
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited=true)]
internal class TastyAttribute : Attribute {
}

[Tasty][Serializable]
internal class BaseType {
    [Tasty] protected virtual void DoSomething() { }
}

internal class DerivedType : BaseType {
    protected override void DoSomething() { }
}
```

在这段代码中，**DerivedType** 及其 **DoSomething** 方法都被视为 **Tasty**，因为 **TastyAttribute** 类被标记为可继承。不过，**DerivedType** 不是可序列化的，因为 FCL 的 **SerializableAttribute** 类被标记为不可继承特性。

请注意，.NET Framework 只把类、方法、属性、事件、字段、方法返回值和参数这些目标视为可继承的。因此，在定义特性类型时，只有当你的目标包含上述任一目标时，才应将 **Inherited** 设置为 **true**。注意，可继承特性不会导致为派生类型向托管模块中发出额外的元数据。稍后我会在“检测自定义特性的使用”一节中进一步说明。

![](img/3c46ff5b170881db4209d365b1f7a808_459_0.png)

> **注意** 如果你定义了自己的特性类，却忘记将 **AttributeUsage** 特性应用于你的类，那么编译器和 CLR 会假定你的特性可以应用于所有目标、只能应用于单个目标一次，并且是可继承的。这些假设模拟了 **AttributeUsageAttribute** 类中的默认字段值。

## 特性构造函数和字段/属性数据类型

在定义自己的自定义特性类时，你可以定义其构造函数来接收参数，这些参数必须由开发人员在你特性类型的实例应用时指定。此外，你还可以在类型中定义非静态公共字段和属性，用于标识开发人员可以为你的特性类实例可选选择的设置。

在定义特性类的实例构造函数、字段和属性时，你必须将数据类型限制在一个很小的子集内。具体来说，合法数据类型仅限于以下这些：**Boolean**、**Char**、**Byte**、**SByte**、**Int16**、**UInt16**、**Int32**、**UInt32**、**Int64**、**UInt64**、**Single**、**Double**、**String**、**Type**、**Object**，或者枚举类型。此外，你还可以使用上述任意类型的一维、从零开始的数组。不过，你应避免使用数组，因为构造函数接收数组的自定义特性类不符合 CLS。

应用特性时，你必须传递一个编译时常量表达式，且其类型与特性类定义的类型匹配。只要特性类定义了 **Type** 参数、**Type** 字段或 **Type** 属性，你就必须使用 C# 的 `typeof` 运算符，如下面的代码所示。只要特性类定义了 **Object** 参数、**Object** 字段或 **Object** 属性，你就可以传递 **Int32**、**String** 或任何其他常量表达式（包括 `null`）。如果该常量表达式表示值类型，那么在构造特性实例时，该值类型将在运行时装箱。

下面是一个特性及其用法的示例：

```csharp
using System;

internal enum Color { Red }

[AttributeUsage(AttributeTargets.All)]
internal sealed class SomeAttribute : Attribute {
    public SomeAttribute(String name, Object o, Type[] types) {
        // 'name' refers to a String
        // 'o' refers to one of the legal types (boxing if necessary)
        // 'types' refers to a 1-dimension, 0-based array of Types
    }
}

[Some("Jeff", Color.Red, new Type[] { typeof(Math), typeof(Console) })]
internal sealed class SomeType {
}
```

从逻辑上说，当编译器检测到应用于某个目标的自定义特性时，编译器会通过调用该特性类的构造函数来构造其实例，并传入任何指定的参数。然后，编译器使用通过增强构造函数语法指定的值来初始化任何公共字段和属性。现在自定义特性对象已初始化，编译器会将该特性对象的状态序列化到目标的元数据表项中。
