
```csharp
// This callback method takes 2 Int32 arguments
private static Object Add(Int32 n1, Int32 n2) {
    return n1 + n2;
}

// This callback method takes 2 Int32 arguments
private static Object Subtract(Int32 n1, Int32 n2) {
    return n1 - n2;
}

// This callback method takes 1 String argument
private static Object NumChars(String s1) {
    return s1.Length;
}

// This callback method takes 1 String argument
private static Object Reverse(String s1) {
    Char[] chars = s1.ToCharArray();
    Array.Reverse(chars);
    return new String(chars);
}
```

# 第 18 章

## 自定义属性

- 本章内容：

- 使用自定义属性 ..................................................................... 435

- 定义你自己的属性类 ....................................................................... 439

- 属性构造函数和字段/属性数据类型 ........................................ 443

- 检测自定义属性的使用 ................................................................ 444

- 两个属性实例之间的匹配 ........................................................ 448

- 在不创建实例的情况下检测自定义属性的使用 ................................ 451

- 属性派生对象 ..................................................................................... 

- 条件属性类 ................................................................................ 454

在本章中，我将讨论微软 .NET 框架提供的最具创新性的功能之一：自定义属性。自定义属性允许你以声明的方式标记代码结构，从而实现特殊功能。自定义属性允许将信息定义并应用到几乎任何元数据表项中。这些可扩展的元数据信息可以在运行时查询，并动态更改代码的执行方式。当你使用各种 .NET 框架技术（Windows Forms、Web Forms、XML 服务等）时，你会发现它们都利用了自定义属性，允许开发者在代码中非常容易地表达意图。对于任何 .NET 框架开发者来说，深入理解自定义属性都是必要的。

## 使用自定义属性

属性（如 `public`、`private`、`static` 等）可以应用于类型和成员。我们都会同意应用属性是有用的，但如果如果我们能定义自己的属性，不是会更有用吗？例如，如果我可以定义一个类型并指示该类型可以通过序列化进行远程调用呢？或者我可以在方法上应用一个属性，指示该类型可以通过序列化进行远程调用？

当然，创建和应用用户定义的属性是非常棒的，但这需要编译器识别这些属性。微软提出了另一种方法，称为“自定义属性”，它在设计时和运行时都很有用。

## 438 第三部分 核心类型

现在你已经知道如何应用自定义属性，让我们来找出属性究竟是什么。属性简单来说就是一个类型的实例。为了符合公共语言规范（CLS），自定义属性类必须直接或间接地派生自公共抽象类 `System.Attribute`。C# 仅允许使用符合 CLS 规范的属性。通过检查 .NET Framework SDK 文档，你会发现以下类（来自之前的示例）是：`LayoutAttribute`、`MarshallAsAttribute`、`DllImportAttribute`、`InAttribute` 和 `OutAttribute`。这些类恰好定义在 `System.Runtime.Interop` 命名空间中，但属性类可以定义在任何命名空间。进一步检查，你会发现所有这些类都派自 `System.Attribute`，而且所有符合 CLS 规范的属性类都必须如此。

- 在源代码中向目标应用属性时，C# 编译器允许你省略 `Attribute` 后缀以减少编程输入并提高源代码的可读性。我的代码示例利用了这种 C# 的便利性。例如，我的源代码包含 `[DllImport(...)]` 而不是 `[DllImportAttribute(...)]`。

正如我之前提到的，属性是一个类的实例。该类必须有一个公共构造函数，以便创建它的实例。当你向目标应用属性时，语言可能会允许某些特殊语法，允许你设置与属性类相关的任何字段或属性。让我们来看一个例子。回想 `DllImport` 属性应用于 `GetVersionEx` 方法时的应用：

```csharp
[DllImport("Kernel32", CharSet = CharSet.Auto, SetLastError = true)]
```

这一行的语法看起来可能非常奇怪，因为在调用构造函数时你不能使用这样的语法。如果你检查文档中的 `DllImportAttribute` 类，你会发现示例中的 "kernel32" 是作为此参数传递的。构造函数的参数是位置参数且是强制性的；在应用属性时必须指定该参数。

另外两个“参数”是什么？这种特殊语法允许你在构造 `DllImportAttribute` 对象后设置该对象的任何字段或属性。在这个示例中，当 `DllImportAttribute` 对象被构造并将 "Kernel32" 传递给构造函数时，对象的公共实例字段 `CharSet` 和 `SetLastError` 分别被设置为 `CharSet.Auto` 和 `true`。设置字段或属性的“参数”被称为命名参数，它们是可选的，因为在应用属性实例时不必指定这些参数。稍后，我将解释是什么导致了 `DllImportAttribute` 类实例的构造。

另外请注意，可以向单个目标应用多个属性。例如，在本章的第一个程序列中，`GetVersion` 方法的 `var` 参数同时应用了 `In` 和 `Out` 属性。在向单个目标应用多个属性时，请注意属性的顺序没有意义。此外，在 C# 中，每个属性都可以包含在方括号中，或者多个属性可以在同一组方括号内用逗号分隔。如果属性类的构造函数不接受任何参数，则括号是可选的。最后，正如前面提到的，`Attribute` 后缀也是可选的。以下几行的行为完全相同，并演示了应用多个属性的所有可能方式：

- `[Serializable][Flags]`

- `[Serializable, Flags]`

- `[FlagsAttribute, SerializableAttribute]`

- `[FlagsAttribute()]`

## 定义自己的属性类

你知道属性是派生自 `System.Attribute` 的类的实例，也知道如何应用属性。现在让我们来看如何定义你自己的自定义属性类。假设你是负责为枚举类型添加位标志支持的微软员工。为了实现这一点，你要做的第一件事是定义一个 **FlagsAttribute** 类：

```csharp
namespace System {
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
    }
}
```

注意 `FlagsAttribute` 类继承自 `Attribute`；这使得 `FlagsAttribute` 类成为一个符合 CLS 规范的自定义属性。此外，类名带有 `Attribute` 后缀；这遵循标准约定但并非强制性。最后，所有非抽象属性必须至少包含一个公共构造函数。`FlagsAttribute` 构造函数不接受参数，且什么都不做。

**重要** 你应该将属性看作一个逻辑容器。也就是说，虽然属性类型是一个类，但该类应该是简单的。该类应该只提供公共构造函数来接受属性的强制（或位置的）状态，并且该类可以提供公共字段/属性来接受属性的可选（或命名的）状态。该类不应提供任何公共方法、事件或其他成员。

通常情况下，我不建议使用公共字段，对于属性仍然不建议使用它们。使用属性要好得多，因为如果你以后决定更改属性类的实现方式，这将提供更大的灵活性。

到目前，`FlagsAttribute` 类的实例可以应用到任何目标，但此属性实际上应该只应用于枚举类型。将属性应用到属性或方法是没有意义的。为了告诉编译器此属性可以在何处合法应用，你将 `System.AttributeUsageAttribute` 类的实例应用到属性类。这里是新代码：

```csharp
namespace System {
    [AttributeUsage(AttributeTargets.Enum, Inherited = false)]
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
    }
}
```

在这个新版本中，我将 `AttributeUsageAttribute` 实例应用到了属性。毕竟，`Attribute` 类型只是一个类，而类可以被应用属性。`AttributeUsage` 是一个简单的类，允许你指定你的属性可以在何处合法应用。因为所有属性都是类型，当用户定义的自定义属性应用到无效目标时，编译器会生成错误。在这个示例中，`AttributeUsage` 指定了 `Flags` 属性只能应用于枚举类型。这里是该类的 FCL 源代码：

```csharp
[Serializable]
[AttributeUsage(AttributeTargets.Class, Inherited=true)]
public sealed class AttributeUsage : Attribute {
    internal static AttributeUsage Default =
        new AttributeUsage(AttributeTargets.All);
}
```

```csharp
internal Boolean m_allowMultiple = false;
internal AttributeTargets m_attributeTarget = AttributeTargets.All;
internal Boolean m_inherited = true;
```

```csharp
// 这是唯一的公共构造函数
public AttributeUsageAttribute(AttributeTargets validOn) {
    m_attributeTarget = validOn;
}
```

```csharp
internal AttributeUsageAttribute(AttributeTargets validOn,
Boolean allowMultiple, Boolean inherited) {
m_attributeTarget = validOn;
m_allowMultiple = allowMultiple;
m_inherited = inherited;
}
```

```csharp
public Boolean AllowMultiple {
    get { return m_allowMultiple; }
    set { m_allowMultiple = value; }
}
```

```csharp
public Boolean Inherited {
    get { return m_inherited; }
    set { m_inherited = value; }
}
```

```csharp
public AttributeTargets ValidOn {
    get { return m_attributeTarget; }
}
```

正如你所见，`AttributeUsageAttribute` 类有一个公共构造函数，允许你传递位标志，指示你的属性可以在何处合法应用。`System.AttributeTargets` 枚举类型在 FCL 中的定义如下：

```csharp
[Serializable]
public enum AttributeTargets {
Assembly = 00001,
Module = 00002,
Class = 00004,
Struct = 00008,
Enum = 00010,
Constructor = 00020,
Method = 00040,
Property = 00080,
Field = 00100,
Event = 00200,
Interface = 00400,
Parameter = 00800,
Delegate = 01000,
ReturnValue = 02000,
GenericParameter = 04000,
Assembly | Module | Class | Struct | Enum |
Constructor | Method | Property | Field | Event |
Interface | Parameter | Delegate | ReturnValue |
GenericParameter
}
```

`AttributeUsageAttribute` 类还提供了两个额外的公共属性，可以在属性应用到属性类时可选设置：`AllowMultiple` 和 `Inherited`。

442

第三部分 核心类型

对于大多数属性

```csharp
[Flags]
internal enum Color {
    Red
}
```

然而，对于某些属性，将该属性多次应用于单个目标是有是有意义的。在 FCL（框架类库）中，`ConditionalAttribute` 类允许将自身的多个实例应用到单个目标上。如果你没有显式地将 `AllowMultiple` 设置为 `true`，你的属性也可以被多次应用于所选目标上。

`AttributeUsageAttribute` 有另一个属性 `Inherited`，它指示该属性是否应该派生到应用于基类上的类和方法。以下代码演示了属性被继承的含义：

```csharp
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited=true)]
internal class TastyAttribute : Attribute {
}

[Serializable]
internal class BaseType {
    [Tasty]
    protected virtual void DoSomething() {}
}

internal class DerivedType : BaseType {
    protected override void DoSomething() {}
}
```

在此代码中，`DerivedType` 及其它的 `DoSomething` 方法都被视为 Tasty，因为 `TastyAttribute` 类被标记为可继承。然而，`DerivedType` 是不可序列化的，因为 FCL 的 `SerializableAttribute` 被标记为不可继承的属性。

请注意，NET 框架仅认为类、方法、属性、事件、字段、方法返回值和参数是可继承的。当你定义属性时，如果你的目标包含这些中的任何一个，你应该将 `Inherited` 设置为 `true`。请注意，继承的属性不会导致为派生类型向托管模块（emit）额外的元数据。我将在稍后的“检测自定义属性的使用”章节中详细介绍这一点。

> **注意：** 如果你定义了自己的属性类，但忘记在你的类上应用 `AttributeUsage` 属性，编译器和 CLR 将假设你的属性可以应用于所有目标上，且在单个目标上只能应用一次，并且是可以继承的。这些假设模拟了 `AttributeUsageAttribute` 类中的默认字段值。

![](img/0ba8f96d6619cf5f73315fb4561d09b5_459_0.png)

## 属性构造函数和字段/属性数据类型

在定义自己的自定义属性类时，你可以定义其构造函数以接收参数，开发者在应用你的属性类型实例时必须指定这些参数。此外，你可以在你的类型中定义非事实的公共字段和属性，用于标识开发者可以为你的属性类实例可选选择的设置。

在定义属性类的实例构造函数、字段和属性时，你必须将自己限制在一个小部分数据类型内。具体来说，合法数据类型集仅限于以下：Boolean、Char、Byte、SByte、Int16、UInt16、Int32、UInt32、Int64、UInt64、Double、String、Type 或枚举类型。此外，你可以使用这些类型中任何一种的一维的、零基的数组。然而，你应该避免使用数组，因为自定义属性类的构造函数接收数组是不符合 CLS 标准的。

在应用属性时，你必须传递一个与属性类定义的类型匹配的编译时常量表达式。每当属性类定义 `Type` 参数、`Type` 字段或 `Type` 属性时，你必须使用 C# 的 `typeof`，如下代码所示。每当属性类定义 `Object` 参数、`Object` 字段或 `Object` 属性时，你可以传递 Int32、String 或任何其他常量（包括 null）。如果常量表达式表示值类型，则在构造属性实例时，该值类型将在运行时装箱（boxed）。

这里有一个属性及其用法的示例：
