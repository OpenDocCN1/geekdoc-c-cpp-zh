
```csharp
public OSVERSIONINFO() {
    OSVersionInfoSize = (UInt32) Marshal.SizeOf(this);
}

public UInt32 OSVersionInfoSize = 0;
public UInt32 MajorVersion      = 0;
public UInt32 MinorVersion      = 0;
public UInt32 BuildNumber       = 0;
public UInt32 PlatformId        = 0;

[MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)]
public String CSDVersion        = null;
}

internal sealed class MyClass {
    [DllImport("kernel32", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern Boolean GetVersionEx([In, Out] OSVERSIONINFO ver);
}
```

在本例中，StructLayout 特性应用于 OSVERSIONINFO 类，MarshalAs 特性应用于 CSDVersion 字段，DllImport 特性应用于 GetVersionEx 方法，In 和 Out 特性应用于 GetVersionEx 的 ver 参数。每种编程语言都定义了开发人员必须使用的语法，以便将自定义特性应用于某个目标。例如，Microsoft Visual Basic .NET 要求使用尖括号（<、>）而不是方括号。

CLR 允许将特性应用于几乎任何可以在文件的元数据中表示的内容。最常见的是，特性应用于以下定义表中的项：TypeDef（类、结构、枚举、接口和委托）、MethodDef（包括构造函数）、ParamDef、FieldDef、PropertyDef、EventDef、AssemblyDef 和 ModuleDef。具体而言，C# 只允许将特性应用于定义了以下任意目标的源代码：程序集、模块、类型（类、结构、枚举、接口、委托）、字段、方法（包括构造函数）、方法参数、方法返回值、属性、事件和泛型类型参数。

应用特性时，C# 允许你指定一个前缀，专门指示该特性所应用的目标。以下代码展示了所有可能的前缀。在许多情况下，如果省略前缀，编译器仍能确定特性所应用的目标，如前面的示例所示。在某些情况下，必须指定前缀，以便让编译器明确你的意图。下面以斜体显示的前缀是必需的。

```csharp
using System;

[assembly: SomeAttr]             // Applied to assembly
[module:   SomeAttr]             // Applied to module

[type:     SomeAttr]             // Applied to type
internal sealed class SomeType<[typeparam: SomeAttr] T> {  // Applied to generic type variable

    [field: SomeAttr]            // Applied to field
    public Int32 SomeField = 0;
}
```

```csharp
[return: SomeAttr]       // Applied to return value
[method: SomeAttr]       // Applied to method
public Int32 SomeMethod(
    [param: SomeAttr]    // Applied to parameter
    Int32 SomeParam) { return SomeParam; }

[property: SomeAttr]     // Applied to property
public String SomeProp {
    [method: SomeAttr]   // Applied to get accessor method
    get { return null; }
}

[event: SomeAttr]        // Applied to event
[field: SomeAttr]       // Applied to compiler-generated field
[method: SomeAttr]       // Applied to compiler-generated add & remove methods
public event EventHandler SomeEvent;
}
```

现在你知道了如何应用自定义特性，接下来让我们弄清楚特性到底是什么。自定义特性其实就是一个类型的实例。为了符合公共语言规范（CLS），自定义特性类必须直接或间接派生自公共抽象 System.Attribute 类。C# 只允许符合 CLS 的特性。通过查看 .NET Framework SDK 文档，你会看到（前面示例中的）以下类已定义：StructLayoutAttribute、MarshalAsAttribute、DllImportAttribute、InAttribute 和 OutAttribute。所有这些类恰好都定义在 System.Runtime.InteropServices 命名空间中，但特性类可以定义在任何命名空间中。进一步查看后，你会注意到所有这些类都派生自 System.Attribute，因为所有符合 CLS 的特性类都必须如此。

> **注意** 在源代码中将特性应用于目标时，C# 编译器允许省略 `Attribute` 后缀，以减少编程输入并提高源代码的可读性。本章中的代码示例利用了 C# 的这一便利。例如，我的源代码包含 `[DllImport(...)]`，而不是 `[DllImportAttribute(...)]`。

如前所述，特性是一个类的实例。该类必须有一个公共构造函数，以便能够创建它的实例。因此，当你将特性应用于目标时，语法类似于调用该类的某个实例构造函数。此外，语言可能允许某些特殊语法，以便你设置与特性类关联的任何公共字段或属性。让我们看一个示例。回想前面将 DllImport 特性应用于 GetVersionEx 方法的情况：

```csharp
[DllImport("Kernel32", CharSet = CharSet.Auto, SetLastError = true)]
```

这一行的语法对你来说应该显得很奇怪，因为你在调用构造函数时绝不可能使用这样的语法。如果你在文档中查看 DllImportAttribute 类，你会看到它的构造函数需要一个 String 参数。在此示例中，为该参数传递的是 "Kernel32"。构造函数的参数称为位置参数，并且是必需的；应用特性时必须指定该参数。

另外两个“参数”是什么？这种特殊语法允许你在 DllImportAttribute 对象构造之后设置该对象的任何公共字段或属性。在此示例中，当构造 DllImportAttribute 对象并将 "Kernel32" 传递给构造函数时，该对象的公共实例字段 CharSet 和 SetLastError 分别设置为 CharSet.Auto 和 true。用于设置字段或属性的“参数”称为命名参数，并且是可选的，因为在应用特性的实例时不必指定这些参数。稍后，我将解释是什么导致 DllImportAttribute 类的实例实际被构造出来。

另请注意，可以将多个特性应用于单个目标。例如，在本章的第一个程序清单中，GetVersionEx 方法的 ver 参数同时应用了 In 和 Out 特性。将多个特性应用于单个目标时，请注意特性的顺序无关紧要。另外，在 C# 中，每个特性可以括在方括号中，也可以将多个特性用逗号分隔在同一组方括号内。如果特性类的构造函数不接收参数，则圆括号是可选的。最后，如前所述，Attribute 后缀也是可选的。下面几行代码的行为相同，并演示了应用多个特性的所有可能方式：

```
[Serializable][Flags]
[Serializable, Flags]
[FlagsAttribute, SerializableAttribute]
[FlagsAttribute()][Serializable()]
```

## 定义自己的特性类

你知道特性是派生自 System.Attribute 的类的实例，也知道如何应用特性。现在让我们看看如何定义自己的自定义特性类。假设你是负责为枚举类型添加位标志支持的 Microsoft 员工。为此，你要做的第一件事是定义一个 FlagsAttribute 类：

```
namespace System {
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
        }
    }
}
```

注意，FlagsAttribute 类继承自 Attribute；这正是使 FlagsAttribute 类成为符合 CLS 的自定义特性的原因。此外，该类的名称带有 Attribute 后缀；这遵循标准约定，但不是必需的。最后，所有非抽象特性都必须包含至少一个公共构造函数。简单的 FlagsAttribute 构造函数不接收参数，并且不执行任何操作。
