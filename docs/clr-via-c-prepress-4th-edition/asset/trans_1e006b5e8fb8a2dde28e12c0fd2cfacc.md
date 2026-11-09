
```csharp
if (value < 0)        // The 'value' always identifies the new value.
    throw new ArgumentOutOfRangeException("value", value.ToString(),
        "The value must be greater than or equal to 0");
m_Age = value;
}
}
}
```

编译器会通过在开发者指定的属性名前面加上 `get_` 或 `set_` 来自动为这些方法生成名称。

C# 内置支持属性。当 C# 编译器看到试图获取或设置属性的代码时，编译器实际上会生成对其中一个方法的调用。如果你使用的编程语言不直接支持属性，你仍然可以通过调用所需的访问器方法来访问属性。效果完全相同；只是源代码看起来不那么漂亮。

除了生成访问器方法之外，编译器还会为源代码中定义的每个属性，在托管程序集的元数据中生成一个属性定义项。该项包含一些标志和属性的类型，并引用 get 和 set 访问器方法。这些信息的存在只是为了在“属性”这一抽象概念与其访问器方法之间建立关联。编译器和其它工具可以使用此元数据，该元数据可通过使用 System.Reflection.PropertyInfo 类获得。CLR 不使用此元数据信息，在运行时只需要访问器方法。

## 自动实现的属性

如果你创建属性只是为了简单地封装一个支持字段，那么 C# 提供了一种简化的语法，称为自动实现的属性 (AIP)，如下所示为 Name 属性所示：

```csharp
public sealed class Employee {
    // This property is an automatically implemented property
    public String Name { get; set; }

    private Int32 m_Age;

    public Int32 Age {
        get { return(m_Age); }
        set {
            if (value < 0)    // The 'value' keyword always identifies the new value.
                throw new ArgumentOutOfRangeException("value", value.ToString(),
                    "The value must be greater than or equal to 0");
            m_Age = value;
        }
    }
}
```

当你声明一个属性并且不为 get/set 方法提供实现时，C# 编译器会自动为你声明一个私有字段。在此示例中，该字段的类型将为 String，即属性的类型。而且，编译器会自动为你实现 get_Name 和 set_Name 方法，分别用于返回字段中的值和设置字段的值。

你可能会想，这样做与只声明一个名为 Name 的公共 String 字段相比有什么价值。嗯，有很大的区别。使用 AIP 语法意味着你已经创建了一个属性。任何访问此属性的代码实际上都在调用 get 和 set 方法。如果你后来决定自己实现 get 和/或 set 方法，而不是接受编译器的默认实现，那么任何访问该属性的代码都不必重新编译。但是，如果你将 Name 声明为字段，然后后来将其改为属性，那么所有访问该字段的代码都必须重新编译，以便现在访问属性方法。

- 就个人而言，我不喜欢编译器的 AIP 功能，因此通常出于以下原因避免使用它：字段声明的语法可以包含初始化，这样你就可以在一行代码中声明并初始化字段。然而，没有方便的语法将 AIP 设置为初始值。因此，你必须在每个构造函数方法中显式初始化每个 AIP。

- 运行时序列化引擎会将字段的名称持久化到序列化流中。AIP 的支持字段的名称由编译器决定，而且每次重新编译代码时，它实际上可能会更改此支持字段的名称，从而使反序列化包含 AIP 的任何类型的实例的能力失效。不要对你打算序列化或反序列化的任何类型使用 AIP 功能。

- 调试时，你不能在 AIP 的 get 或 set 方法上放置断点，因此无法轻松检测应用程序何时获取或设置此属性。你可以在手动实现的属性上设置断点，这在跟踪 bug 时非常方便。

你还应该知道，当你使用 AIP 时，属性必须可读和可写；也就是说，编译器必须同时生成 get 和 set 方法。这是合理的，因为只写字段如果无法读取其值就没有用；同样，只读字段将始终具有其默认值。此外，由于你不知道编译器生成的支持字段的名称，你的代码必须始终使用属性名来访问该属性。而且，如果你决定显式实现其中一个访问器方法，那么你必须显式实现两个访问器方法，并且你不再使用 AIP 功能。对于单个属性，AIP 功能是全有或全无的。

## 明智地定义属性

就个人而言，我不喜欢属性，我希望 Microsoft .NET Framework 及其编程语言不支持属性。原因是属性看起来像字段，但它们是方法。众所周知，这会导致大量的混淆。当程序员看到看起来像是在访问字段的代码时，程序员会做出许多假设，而这些假设对于属性来说可能并不成立。例如，

- 属性可以是只读或只写的；字段访问始终可读和可写。如果你定义属性，最好同时提供 get 和 set 访问器方法。

- 属性方法可能抛出异常；字段访问从不抛出异常。

- 属性不能作为 out 或 ref 参数传递给方法；字段可以。例如，以下代码将无法编译：

```csharp
using System;

public sealed class SomeType {
   private static String Name {
      get { return null; }
      set {}
   }

   static void MethodWithOutParam(out String n) { n = null; }

   public static void Main() {
      // For the line of code below, the C# compiler emits the following:
      // error CS0206: A property, indexer or dynamic member access may not
      // be passed as an out or ref parameter
      MethodWithOutParam(out Name);
   }
}
```

- 属性方法可能需要很长时间执行；字段访问始终立即完成。使用属性的一个常见原因是执行线程同步，这可能会永久停止线程，因此，如果需要线程同步，则不应使用属性。在这种情况下，首选方法是方法。此外，如果你的类可以远程访问（例如，你的类派生自 System.MarshalByRefObject），调用属性方法会非常慢，因此，方法优先于属性。在我看来，派生自 MarshalByRefObject 的类永远不应使用属性。

- 如果连续多次调用，属性方法可能每次返回不同的值；字段每次返回相同的值。System.DateTime 类有一个只读的 Now 属性，返回当前日期和时间。每次查询此属性时，它都会返回不同的值。这是一个错误，Microsoft 希望他们可以通过将 Now 改为方法而不是属性来修复该类。Environment 的 TickCount 属性是此错误的另一个示例。

- 属性方法可能导致可观察的副作用；字段访问从不这样做。换句话说，类型的用户应该能够以他或她选择的任何顺序设置类型定义的各种属性，而不会注意到该类型有任何不同的行为。

- 属性方法可能需要额外的内存，或返回对实际上不属于对象状态的内容的引用，因此修改返回的对象对原始对象没有影响；查询字段始终返回对保证属于原始对象状态的对象的引用。使用返回副本的属性可能会让开发人员非常困惑，而且这种特性通常没有文档记录。

我注意到人们使用属性的频率远高于应有的程度。如果你
