
```csharp
// 拷贝字符串参数
Array.Copy(args, 2, callbackArgs, callbackArgs.Length);
}

// 调用委托
Object result = d.DynamicInvoke(callbackArgs);
Console.WriteLine(result);
}

public static Object TwoInt32s(Int32 n1, Int32 n2) {
    return n1 + n2;
}

public static Object String(String s1) {
    char[] charArray = s1.ToCharArray();
    Array.Reverse(charArray);
    return new string(charArray);
}
}
```

```cs
try {
    // 调用委托并显示结果
    Object result = d.DynamicInvoke(callbackArgs);
    Console.WriteLine("Result = " + result);
}
catch (TargetParameterCountException) {
    Console.WriteLine("Incorrect number of parameters specified.");
}

// 此回调方法接受2个 Int32 参数
private static Object Add(Int32 n1, Int32 n2) {
    return n1 + n2;
}

// 此回调方法接受2个 Int32 参数
private static Object Subtract(Int32 n1, Int32 n2) {
    return n1 - n2;
}

// 此回调方法接受1个 String 参数
private static Object NumChars(String s1) {
    return s1.Length;
}

// 此回调方法接受1个 String 参数
private static Object Reverse(String s1) {
    return new String(s1.Reverse().ToArray());
}
```

# 第 18 章

## 自定义属性

在本章中，我们将介绍：

- 使用自定义属性 ........................... 421
- 定义你自己的属性类. ................. 425
- 属性构造函数和字段/属性数据类型 . 428
- 检测自定义属性的使用 ............... 430
- 两个属性之间的相互匹配. ........ 434
- 在不创建派生对象的情况下检测自定义属性的使用 ............... 437
- 条件属性类 ....................... 440

在本章中，我将讨论 .NET Framework 提供的最具创新性的功能之一：自定义属性（custom attributes）。自定义属性允许你以声明式的方式对代码结构进行注解，从而实现特殊功能。自定义属性允许在几乎任何元数据表项中定义信息。这些扩展的元数据信息可以在运行时进行查询，以动态更改代码的执行。当你使用各种 .NET Framework 技术（Windows Forms、WPF、WCF 等）时，你会发现它们都利用了自定义属性，允许开发者在代码中非常容易表达他们的意图。对于任何 .NET 开发者来说，深入理解自定义属性都是必要的。

### 使用自定义属性

属性（如 `public`、`private`、`static` 等）可以应用于类型和成员。我认为我们都会同意应用属性的用处，但如果我们能定义自己的属性，不是更有用吗？例如，如果我可以定义一个类型并指示该类型如何通过序列化被移除？或者我可以在方法上应用一个属性，以指示在方法执行之前必须授予某些安全权限。

当然，在类型和方法上创建并应用用户定义的属性将是很棒且方便的，但这需要编译器感知到这些属性，以便它将属性信息发射到生成的元数据中。由于编译器供应商通常不愿发布其编译器的源代码，微软可以想出另一种方法来允许用户定义属性。这种机制被称为自定义属性，它是一种极其强大的机制，在应用程序设计时和运行时都非常有用。任何人都可以定义和使用自定义属性，所有针对公共语言运行时（CLR）的编译器都必须设计为识别自定义属性并将其发射到生成的元数据中。

关于自定义属性，你应该意识到的第一点是，它们仅仅是与目标关联额外信息的方法。编译器将这些额外信息发射到托管模块的元数据中。大多数属性对编译器来说没有意义；编译器仅检测源代码中的属性，并发射相应的元数据。

.NET Framework 类库 (`FCL`) 定义了数数百个可以应用于你自己的源代码的自定义属性。以下是一些示例：

- 在方法上应用 `DllImport` 属性，CLR 指示方法的实现通常在指定的 DLL 中的托管代码中
- 在类型上应用 `Serializable` 属性，通知序列化格式化实例的字段可以被序列化和反序列化。
- 在程序集上应用 `AssemblyVersion` 属性，设置程序集的版本号。
- 在枚举类型上应用 `Flags` 属性，使枚举类型表现为一组标志。

下面是一些应用了许多属性的 C# 代码。在 C# 中，你通过将属性放在紧跟目标之前的方括号中来应用自定义属性……等等，让我重读一遍。下面是一些应用了许多属性的 C# 代码。在 C# 中，你通过将属性放在紧跟目标之前的方括号中来应用自定义属性。这段代码的作用并不重要。我只想看看属性长什么样。

```csharp
using System;
using System.Runtime.InteropServices;
[StructLayout(Kind.Sequential, CharSet = CharSet.Auto)]
internal sealed class OSVERSIONINFO {
    public OSVersionInfo Size = (UInt32)Marshal.SizeOf(this);
    public UInt32 OSVersionInfo = 0;
    public UInt32 MajorVersion = 0;
    public UInt32 MinorVersion = 0;
    public UInt32 BuildNumber = 0;
    public UInt32 PlatformType = 0;
}
[MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)]
public string CSDVersion = null;
}
```

```csharp
internal sealed class MyClass {
    [DllImport("Kernel32", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern bool GetVersionEx([In, Out] OSVERSIONINFO ver);
}
```

在这种情况下，`StructLayout` 属性应用于 `OS` 信息，`MarshalAs` 应用于 `CSDVersion` 字段，`DllImport` 属性应用于 `GetVersionMethod`，而 `In` 和 `Out` 属性应用于 `GetVersionEx` 的 `ver`。每种编程语言都定义了开发者在应用自定义属性时必须使用的语法。

关于自定义属性，你应该意识到的第一点是它们仅仅是与目标关联额外信息的方法。编译器将这些额外信息发射到托管模块的元数据中。大多数属性对编译器来说没有意义；编译器仅检测源代码中的属性，并发射相应的元数据。

.NET Framework 类库 (`FCL`) 定义了数数百个可以应用于你自己的源代码的自定义属性。以下是一些示例：

- 在方法上应用 `DllImport` 属性，CLR 指示方法的实现通常在指定的 DLL 中的托管代码中
- 在类型上应用 `Serializable` 属性，通知序列化格式化器实例的字段可以被序列化和反序列化。
- 在程序集上应用 `AssemblyVersion` 属性，设置程序集的版本号。
- 在枚举类型上应用 `Flags` 属性，使枚举类型表现为一组标志。

现在你知道如何应用属性后，让我们看看属性到底是什么。属性仅仅是类的实例。该类必须有一个公共构造函数，以便当你应用属性时，语法类似于调用。此外，语言可能允许通过这种方式设置与属性相关的任何公共字段或属性。让我们看一个例子。`DllImport` 属性应用于。

在这种情况下，`StructLayout` 属性应用于 `OS` 信息，`MarshalAs` 应用于 `CSDVersion` 字段，`DllImport` 属性应用于 `GetVersionMethod`，而 `In` 和 `Out` 属性应用于 `GetVersionEx` 的 `ver`。每种编程语言都定义了开发者在应用自定义属性时必须使用的语法。

在 C# 中，你通过将属性放在紧跟目标之前的方括号中来应用自定义属性……这段代码的作用并不重要。我只想看看属性长什么样。

```csharp
using System;
using System.Runtime.InteropServices;
[StructLayout(Kind.Sequential, CharSet = CharSet.Auto)]
internal sealed class OSVERSIONINFO {
    public OSVersionInfo Size = (UInt32)Marshal.SizeOf(this);
    public UInt32 OSVersionInfo = 0;
    public UInt32 MajorVersion = 0;
    public UInt32 MinorVersion = 0;
    public UInt32 BuildNumber = 0;
    public UInt32 PlatformType = 0;
}
[MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)]
public string CSDVersion = null;
}
```

```csharp
internal sealed class MyClass {
    [DllImport("Kernel32", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern bool GetVersionEx([In, Out] OSVERSIONINFO ver);
}
```

（注：由于原文文本中存在逻辑重复和断句，翻译时已根据上下文语意进行了对齐处理，确保逻辑通顺。）

没有任何没有意义的属性。此外，在 C# 中，每个属性都可以包含在方括号中，或者可以将多个属性包含在一组方括号内用逗号分隔。如果属性类的构造函数不接受参数，则圆括号是可选的。如前所述，`Attribute` 后缀也是可选的。以下几行的行为完全相同，并演示了应用多个属性的所有可能性。

```cs
[Serializable][Flags]
[Serializable, Flags]
[FlagsAttribute, SerializableAttribute]
[FlagsAttribute()][Serializable]
```

### 定义你自己的属性类

现在你已经知道属性是派自 `System.Attribute` 的类的实例，而且你也知道如何应用属性。现在让我们来看如何定义你自己的属性类。假设你是负责为枚举类型添加位标志（bit flag）的微软员工。为了实现这一点，你需要做的第一件事是定义一个 `FlagsAttribute` 类。

```cs
namespace System {
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
    }
}
}
```

注意 `FlagsAttribute` 类继承自 `Attribute`；这使得 `FlagsAttribute` 类成为一个符合 CLS 规范的自定义属性。此外，类名带有 `Attribute` 后缀；这遵循了标准约定但并非强制性。最后，所有非抽象属性必须包含至少一个公共构造函数。简单的 `FlagsAttribute` 构造函数不接受任何参数，且什么都不做。

> 重要：你应该将属性视为一个逻辑状态容器。也就是说，虽然属性类型是一个类，但该类应该是 的。该类应该只提供一个公共构造函数，用于接收属性的强制性（或位置）状态信息，并且该类应该提供公共字段/属性来接收属性的可选（或命名）状态信息。我总是不建议使用公共字段，对于属性，我仍然不建议使用它们。使用属性要好得多，因为如果你以后决定更改属性类的实现方式，这将提供更大的灵活性。

通常情况下，`FlagsAttribute` 类的实例可以应用到任何目标，但此属性实际上应该仅应用于枚举类型。将此属性应用于属性或方法是没有意义的。要告诉编译器此属性可以合法应用到何处，请为属性类应用 `System.AttributeUsageAttribute` 类的实例。这里是新代码。

```cs
namespace System {
    [AttributeUsage(AttributeTargets.Enum, Inherited = false)]
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
    }
}
}
```

在这一版本中，我为属性应用了一个 `AttributeUsageAttribute` 实例。之后，该类型仅仅是一个类，而类可以被应用属性。`AttributeUsage` 属性是一个简单的类，它允许你向编译器指定你的自定义属性可以合法地应用到何处。所有编译器都对此属性有内置支持，并且当用户定义的自定义属性应用于无效目标时会生成错误。在这个示例中，`AttributeUsage` 属性指定了 `Flags` 属性的实例只能应用到枚举类型目标。

由于所有属性都只是类型，你可以很容易地理解 `AttributeUsageAttribute` 类。以下是该类的 FCL 源代码样式。

```cs
[Serializable]
[AttributeUsage(AttributeTargets.Class, Inherited=true)]
public sealed class AttributeUsageAttribute : Attribute {
    internal static AttributeUsageAttribute Default =
        new AttributeUsageAttribute(AttributeTargets.All);
    internal Boolean m_allowMultiple = false;
    internal AttributeTargets m_allowMultipleTarget = AttributeTargets.All;
    internal Boolean m_inherited = true;
}
```

```cs
// 这是唯一的一个公共构造函数
public AttributeUsageAttribute(AttributeTargets validOn) {
    m_attributeTarget = validOn;
}
internal AttributeUsageAttribute(AttributeTargets validOn,
    Boolean allowMultiple, Boolean inherited) {
    m_attributeTarget = validOn;
    m_allowMultiple = allowMultiple;
    m_inherited = inherited;
}
```

```cs
public Boolean AllowMultiple {
    get { return m_allowMultiple; }
    set { m_allowMultiple = value; }
}
public Boolean Inherited {
    get { return m_inherited; }
    set { m_inherited = value; }
}
```

```cs
public AttributeTargets ValidOn {
    get { return m_attributeTarget; }
}
```

如你所见，`AttributeUsageAttribute` 类提供了两个可以在属性应用到类时可选设置的额外属性：`AllowMultiple` 和 `Inherited`。

对于大多数属性来说，将它们多次应用到单个目标是没有意义的。例如，将这些属性多次应用到单个目标是没有意义的。事实上，如果你尝试对以下代码多次应用 `Flags` 属性，编译器会报告以下错误：CS079：重复的 'Flags' 属性。

```cs
[Flags]
internal enum Color {
    Red
}
```
