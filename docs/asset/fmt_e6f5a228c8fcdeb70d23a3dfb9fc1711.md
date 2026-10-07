
```csharp
for (int a = 2; a < args.Length; a++)
    callbackArgs[a - 2] = Int32.Parse(args[a]);
callbackArgs(callbackArgs);
} catch (FormatException) {
    Console.WriteLine("Parameters must be integers.");
    return;
}
}
if (d.GetType() == typeof(String)) {
    // 复制字符串参数
    Array.Copy(args, 2, callbackArgs, 0, callbackArgs.Length);
}
try {
    // 调用委托并显示结果
    Object result = d.DynamicInvoke(callbackArgs);
    Console.WriteLine("Result = " + result);
} catch (TargetCountException) {
    Console.WriteLine("Incorrect number of parameters specified.");
}
}
// 此回调方法接收两个 Int32 参数
private static Object Add(Int32 n1, Int32 n2) {
    return n1 + n2;
}
// 此回调方法接收两个 Int32 参数
private static Object Subtract(Int32 n1, Int32 n2) {
    return n1 - n2;
}
// 此回调方法接收一个 String 参数
private static Object NumChars(String s1) {
    return s1.Length;
}
// 此回调方法接收一个 String 参数
private static Object Reverse(String s1) {
    Char[] chars = s1.ToCharArray();
    Array.Reverse(chars);
    return new String(chars);
}
```

# 436 第三部分 核心类型

这是一种在应用设计时和运行时都非常有用的机制。任何人都可以定义和使用自定义属性，所有针对通用语言运行时 `CLR` 的编译器都必须设计为识别自定义属性，并将其发射到生成的元数据中。

关于自定义属性，你首先应该意识到的是，它们只是与目标关联附加信息的一种方式。编译器会将这些附加信息发射到托管模块的元数据中。大多数属性对编译器来说没有意义；编译器只需检测源代码中的属性，并发射相应的元数据。

`.NET Framework` 类库 `FCL` 定义了足足几百个自定义属性，这些属性可以应用于你自己的源代码中。以下是一些示例：

- 对方法应用 `DllImport` 属性会通知 `CLR`，该方法的实现实际上位于指定 `DLL` 中的未托管代码中。
- 对类型应用 `Serializable` 属性会通知序列化格式器，实例的字段可以被序列化和反序列化。
- 对程序集应用 `AssemblyInfo` 属性可以设置程序集的版本号。
- 对枚举类型应用 `Flags` 属性会使该枚举类型表现为位标志集。

以下是一些应用了许多属性的 `C#` 代码。在 `C#` 中，你通过将属性放在目标正前的方括号中来对目标应用自定义属性。理解这段代码在什么并不重要。我只想看看属性看起来像什么样。

```csharp
using System;
using System.Runtime.InteropServices;
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
internal sealed class OSVERSIONINFO {
    public OSVERSIONInfo Size = (UInt32)Marshal.SizeOf(this);
}
public UInt32 OSVersionInfoSize = 0;
public UInt32 MajorVersion = 0;
public UInt32 MinorVersion = 0;
public UInt32 BuildNumber = 0;
public UInt32 PlatformId = 0;
[MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)]
public string CSVersion = null;
```

# 第18章 自定义属性 437

```csharp
internal sealed class MyClass {
[DllImport("Kernel32", CharSet = CharSet.Auto, SetLastError = true)]
public extern Boolean GetVersionEx([In, Out] OSVERSION info);
}
```

在这种情况下，应用于 `OSVERSION` 类的 `StructLayout` 属性、应用于 `CSVersion` 字段的 `MarshalAs` 属性、应用于 `GetVersionEx` 方法的 `DllImport` 属性，以及 `In` 和 `Out` 属性分别应用于 `GetVersionEx` 的参数。每种编程语言都定义了开发者向目标应用自定义属性必须使用的语法。Microsoft Visual Basic .NET 需要角括号 `<>` 而不是方括号 `[]`。

`CLR` 允许将属性应用于任何可以在文件元数据中表示的内容。最常见的是，属性应用于以下定义表中的项：`TypeDef`（类、结构体、枚举、接口和委托）、`MethodDef`（包括构造函数）、`ParamDef`、`FieldDef`、`PropertyDef`、`EventDef`、`AssemblyDef` 和 `ModuleDef`。具体来说，`C#` 允许你将属性应用于定义以下任何内容的源代码：程序集、模块、类型（类、结构体、枚举、接口、委托）、字段、方法（包括构造函数）、方法参数、返回值、属性、事件和泛型类型参数。

当你应用属性时，`C#` 允许你指定一个特定的前缀，以指示该属性应用于哪个目标。以下代码显示了所有的前缀。在许多情况下，如果你省略前缀，编译器仍然可以确定目标属性的应用范围，如前面的示例所示。在某些情况下，必须指定前缀以向编译器明确你的意图。以下斜体显示的前缀是强制性的。

```csharp
using System;
[assembly:SomeAttr] // 应用于程序集
[module:SomeAttr] // 应用于模块
```

```csharp
[type:SomeAttr] // 应用于类型
internal sealed class SomeType<T> { // 应用于泛型类型变量
```

```csharp
[field:SomeAttr] // 应用于字段
public Int32 SomeField = 0;
```

```csharp
[return:SomeAttr] // 应用于返回值
[method:SomeAttr] // 应用于方法
public Int32 SomeMethod(
[param:SomeAttr] // 应用于参数
Int32 SomeParam) { return SomeParam; }
```

```csharp
[property:SomeAttr] // 应用于属性
public String SomeProp {
[method:SomeAttr] // 应用于方法
get { return null; }
```

# 438 第三部分 核心类型

现在你已经知道了如何应用自定义属性，让我们来看看属性到底是什么。自定义属性仅仅是某个类型的实例。为了符合通用语言规范 `CLS`，自定义属性类必须直接或间接地派自公共抽象的 `System.Attribute` 类。`C#` 仅允许符合 `CLS` 标准的属性。通过检查 `.NET Framework SDK` 文档，你会发现以下类（来自前面的示例）：`StructLayoutAttribute`、`MarshalAsAttribute`、`DllImportAttribute`、`InAttribute`、`OutAttribute`。这些都定义在 `System.Runtime.InteropServices` 命名空间中，但属性类可以命名为任何。进一步检查，你会发现这些类都派自 `System.Attribute`，所有符合 `CLS` 的属性类都必须。

# 440 第三部分 核心类型

**重要** 你应该将属性视为一个逻辑容器。也就是说，虽然属性类型是一个类，但该类应该是简洁的。该类应该只提供一个公共构造函数，用于接收属性的强制性（或位置性）状态，并且该类可以提供公共字段/属性来接收属性的可选（或命名））状态。该类不应该提供任何公共方法、事件或其他成员。

通常情况下，我总是不建议使用公共字段，对于属性我仍然不建议使用它们。使用属性要好得多，因为如果你以后决定更改属性类的实现方式，这可以提供更大的灵活性。

到目前为止，**FlagsAttribute** 类的实例可以应用到任何目标，但此属性实际上应该只应用于枚举类型上。将该属性应用到属性或方法是没有意义的。为了告诉编译器此属性在何处可以合法应用，你需要在属性类上应用一个 **System.AttributeUsageAttribute** 类的实例。这里是新代码：

```cs
namespace System {
    [AttributeUsage(AttributeTargets.Enum, Inherited = false)]
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() { }
    }
}
```

在这个版本中，我将 **AttributeUsageAttribute** 的实例应用到了该属性上。毕竟，属性类型只是一个类，而类是可以被应用属性的。**AttributeUsage** 是一个简单的类，允许你为编译器指定你的自定义属性在何处可以合法应用。所有编译器都对此属性有内置支持，并且当用户定义的自定义属性应用到无效目标时，它们会生成错误。在这个示例中，**AttributeUsage** 属性指定了 **FlagsAttribute** 的实例只能应用于枚举类型。

由于所有属性都只是类型，你可以轻松地理解 **AttributeUsageAttribute** 类。以下是该类的 `FCL` 源代码所示：

```cs
[Serializable]
[AttributeUsage(AttributeTargets.Class, Inherited=true)]
public sealed class AttributeUsageAttribute : Attribute {
    internal static readonly AttributeUsageAttribute Default = new AttributeUsageAttribute(AttributeTargets.All);
    internal Boolean m_allowMultiple = false;
    internal AttributeTargets m_attributeTarget = AttributeTargets.All;
    internal Boolean m_inherited = true;
    // 这是唯一的公共构造函数
    public AttributeUsageAttribute(AttributeTargets validOn) {
        m_attributeTarget = validOn;
    }
```

![](img/47eccf75186e2a4895549653d7520b0a_457_0.png)

```cs
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
```

```cs
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

你可以看到，`AttributeUsageAttribute` 类有一个公共构造函数，允许你传递位标志，指示你的属性可以被合法应用。`System.AttributeTargets` 枚举类型在 `FCL` 中的定义如下：

```cs
[Serializable]
public enum AttributeTargets {
Assembly = 00001,
Module = 00002,
```
