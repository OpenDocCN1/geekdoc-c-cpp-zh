
注意我将虚方法定义为公共方法，但在某些情况下，你可能倾向于将其设为保护（`protected`）。将此方法设为保护而非公共是可以的，但这将需要其他微小的改动。这段讨论让你清楚了应该谨慎使用 EMI（显式接口实现）。许多开发者初学 EMI 时，认为它们很好并尽可能地使用它们。不要这样做！EMI 在某些情况下是有用的，但每当它们让类型变得困难许多时，你应该尽可能避免使用。

## 设计：基类还是接口？

我经常听到这个问题：“我应该设计一个基类型还是接口？”答案并不总是一目了然。这里是一些可能对你有帮助的指南：

- **IS-A 与 CAN-DO 关系** - 类型只能与基类型建立“IS-A”（是一个）的继承关系，如果派生类型使用接口，则不要使用基类型。接口实现的是一种“CAN-DO”（可以做）的关系。CAN 功能似乎作为接口与各种对象类型关联。例如，一个类型可以作为接口转换实例……（注：此处原文存在重复，已忽略重复部分）。
- **易用性** - 对于你开发者来说，在不确切知道正在处理哪种类型的集合的情况下，……通常更容易。
- **一致的实现** - 这些集合类提供的操作仍然非常一致。
- **版本控制** - 如果向基类型添加了方法，派生类型不需要重新编译。

（注：原文结尾存在大量重复文本，已忽略重复部分）。

## 第 14 章

## 字符、字符串与文本处理

在本章中：
字符 ................................................................................................................................................................. . . . 327
`System.String` 类型 ................................................................................................................................................................. . . . . . 330
高效地构建字符串 ................................................................................................................................................. . . . . . 346
获取对象的字符串表示：`ToString` ................................................................................................................................. . . . . . . 350
解析字符串以获取对象：`Parse` ................................................................................................................................................. . . . . . . 359
编码：在字符和字节之间转换 ................................................................................................................................................. . . . . . . . 361
安全字符串 (`Secure Strings`) ............................................................................................................................................................................................................................................ 369

在本章中，我将解释在 Microsoft .NET Framework 中处理单个字符和字符串的机制。我将首先介绍 `System.Char` 结构以及操作字符的各种方法。然后，我将介绍更有用的 `System.String` 类，它允许你处理不可变字符串（一旦创建，字符串无法以任何方式进行修改）。在检查字符串之后，我将向你展示如何使用 `System.Text.StringBuilder` 类高效操作并动态构建字符串。在完成字符串基础之后，我将描述如何将对象格式化为字符串，以及如何使用各种编码来高效地持久化或传输字符串。最后，我将讨论 `System.Security.SecureString` 类，它可以用于保护密码和信用卡信息等敏感字符串数据。

### 字符

在 .NET Framework 中，字符始终以 16 位 Unicode 代码值表示，这使得全球化应用程序的开发变得容易。字符由 `System.Char` 结构的实例表示（值类型）。`System.Char` 类型非常简单。它提供了两个公共的只读常量字段：定义为 `'\0'` 的 `MinValue` 和定义为 `'\ffff'` 的 `MaxValue`。

给定一个 `Char` 实例，你可以调用静态方法 `GetUnicodeCategory`，该方法返回 `System.Globalization.UnicodeCategory` 枚举类型的值。此值指示该字符是控制字符、货币符号、小写字母、大写字母、标点符号、数学符号还是另一个字符（根据 Unicode 标准定义）。

328 第三部分 核心类型

为了方便开发，`Char` 类型还提供了几个静态方法，例如 `IsDigit`、`IsLetter`、`IsWhiteSpace`、`IsUpper`、`IsLower`、`IsPunctuation`、`IsLetterDigit`、`IsControl`、`IsNumber`、`IsSeparator`、`IsSurrogate`、`IsHighSurrogate` 和 `IsSymbol`。这些方法大部分内部都使用 `GetUnicodeCategory` 并返回 `true` 或 `false`。注意，所有这些方法都接收单个字符作为参数，或者接收字符串和一个字符索引作为参数。

此外，你可以通过调用 `ToLowerInvariant` 和 `ToUpperInvariant` 方法以与文化无关的方式单个字符转换为小写或大写形式。或者，`ToLower` 和 `ToUpper` 方法通过查询 `System.CurrentCulture` 属性的使用线程信息来转换字符。你也可以通过向这些方法传递 `CultureInfo` 类的实例来指定特定的字符。`ToLower` 和 `ToUpper` 需要文化信息，因为字母的大小写是一个取决于文化的操作。例如，土耳其语认为 U+0069（拉丁小写字母 I）的大写形式是 U+0130（带点的拉丁大写字母 I），而其他文化认为认为结果为 U+0049（大大写字母 I）。

除了这些静态方法外，`Char` 类型还提供了一些自己的实例方法。`Equals` 方法在两个实例表示相同的 16 位 Unicode 代码点时返回 `true`。由 `IComparable/IComparableChar` 接口定义的 `CompareTo` 方法返回两个字符的比较结果；这种比较不受文化影响。`ConvertFromUtf32` 方法从单个 UTF-32 字符生成一个由 UTF-16 字符组成的字符串。`ConvertToUtf32` 方法从低/高代理对或字符串生成一个 UTF-16 字符。`ToString` 方法返回一个由单个字符组成的 `String` 并返回其 UTF-16 代码点。

最后一个方法 `GetNumericValue` 返回字符的数值等效值。我将在下面的代码中演示这一点：

```csharp
using System;

public static class Program {
    public static void Main() {
        Double d; // "\u0033" 是 "数字 3"
        d = Char.GetNumericValue("\u0033"); // '3' 也可以工作
        Console.WriteLine(d.ToString()); // 显示 "3"
        // "\u00bc" 是俗分数四分之一 ('¼')
        d = Char.GetNumericValue("\u00bc");
        Console.WriteLine(d.ToString()); // 显示 "0.25"
        // 'A' 是 "拉丁大写字母 A"
        d = Char.GetNumericValue('A');
        Console.WriteLine(d.ToString()); // 显示 "-1"
    }
}
```

第 14 章 字符、字符串与文本处理 329

最后，有三种技术允许你在各种类型与 `Char` 实例之间转换，反之亦然。这些技术按优先级列出：

- 强制转换（Casting）：将 `Char` 转换为数值（如 `Int32`）简单的方法就是强制转换。在三种技术中，这种效率最高，因为编译器会发出中间语言 (`IL`) 指令来执行转换，不需要调用任何方法。此外，某些语言（如 C#）允许你指定是否使用检查型（`checked`）代码进行转换。
- 使用 `Convert` 类型：`System` 提供了多个静态方法，可以将 `Char` 转换为数值类型反之亦然。所有这些方法都作为检查操作执行转换，如果转换导致数据丢失，将抛出 `OverflowException`。
- 使用 `IConvertible` 接口：`Char` 类型和 .NET Framework 类库 (`FCL`) 中的所有数值类型都实现了 `IConvertible` 接口。该接口定义了 `Int16` 和 `ToChar` 等方法。这种技术的效率最低，因为在值类型上调用接口方法需要对实例进行装箱（`boxing`）——`Char` 和所有数值类型通过显式成员实现该接口（见第 13 章，“接口”）。这意味着在调用接口的任何方法之前，必须显式地将实例转换为 `IConvertible`。`IConvertible` 除 `GetCode` 之外的所有方法都接受一个实现 `FormatProvider` 接口的对象的引用。如果某些转换需要考虑文化，此参数就会很有用。对于大多数转换，你可以对此参数传递 `null`，因为通常会被忽略。

下面的代码演示了如何使用这三种技术：

```csharp
using System;

public static class Program {
    public static void Main() {
        Char c;
        Int32 n;
        // 使用 C# 强制转换数字 <-> 字符
        c = (Char) 65;
        Console.WriteLine(c); // 显示 "A"
        n = (Int32) c;
        Console.WriteLine(n); // 显示 "65"
    }
}
```

```csharp
c = unchecked((char) (65536 + 65));
Console.WriteLine(c);
```

> // Displays "A"

```csharp
// Convert number <-> character using Convert
c = Convert.ToChar(65);
Console.WriteLine(c);
```

> // Displays "A"

```csharp
n = Convert.ToInt32(c);
Console.WriteLine(n);
```

> // Displays "65"

```csharp
// This demonstrates Convert's range checking
try {
    c = Convert.ToChar(70000);
    Console.WriteLine(c);
} catch (OverflowException) {
    Console.WriteLine("Can't convert 70000 to a Char.");
}
```

> // 对于 16 位来说太大
> // 不执行

```csharp
// Convert number <-> character using IConvertible
c = ((IConvertible)65).ToChar(null);
Console.WriteLine(c);
```

> // Displays "A"

```csharp
n = ((IConvertible)c).ToInt32(null);
Console.WriteLine(n);
```

> // Displays "65"

### System.String 类型

任何应用程序中最常用的类型之一是 `System.String`。`String` 表示一个不可变的有序字符集。`String` 类型直接派生自 `Object`，使其成为一个引用类型，因此，`String` 对象（其字符数组）存储在堆（`heap`）上，而不是线程的栈（`stack`）上。`String` 类型还实现了几个接口（`IComparable/IComparable<String>`, `ICloneable`, `IConvertible`, `IEnumerable/IEnumerable<Char>`, 和 `IEquatable<String>`）。

#### 构造字符串

许多编程语言（包括 C#）将 `String` 视为一种原始类型——也就是说，编译器允许你直接在源代码中表示字面量字符串。编译器将这些字面量字符串放在模块的元数据中，然后在运行时进行加载和引用。

## 第 14 章 字符、字符串与文本处理

在 C# 中，你不能使用 `new` 算符从字面量字符串构造 `String` 对象：

```csharp
using System;

public static class Program {
    public static void Main() {
        String s = new String("Hi there."); // <-- 错误
        Console.WriteLine(s);
    }
}
```

相反，你必须使用简化的语法：

```csharp
using System;

public static class Program {
    public static void Main() {
        String s = "Hi there.";
        Console.WriteLine(s);
    }
}
```

如果你编译这段代码并检查其 IL（使用 `ILasm.exe`），你将看到以下内容：

```il
.method hidebysid static void Main() cil managed
{
  .entrypoint
  // Code size 13 (0xd)
.maxstack 1
  .locals int (string V_0)
IL_0000: ldstr "Hi there."
IL_0005: stloc.V0
IL_0006: ldloc.V0
IL_0007: call void [mscorlib]System.Console::WriteLine(string)
IL_000C: ret
} // end of method Program:Main
```

`newobj` IL 指令用于构造对象的新实例。然而，在 IL 代码示例中并没有 `newobj` 指令。相反，你看到了特殊的 `ldstr`（加载字符串）指令，它使用来自元数据的字面量字符串来构造 `String` 对象。这表明通用语言运行时（CLR）实际上有一种特殊的方法来构造字面量 `String` 对象。

如果你在使用不安全代码（`unsafe code`），你可以从 `Char*` 或 `SByte*` 构造 `String` 对象。要实现这一点，你将使用 C# 的 `new` 算符以及 `Type` 提供的带有 `Char*` 或 `SByte*` 参数的构造函数。这些构造函数会创建一个 `String` 对象，通过 `Char` 实例数组或符号字节数组初始化字符串。其他构造函数没有任何指针参数，并且可以在用托管编程语言编写的安全的（可验证的）代码中调用。

332 第三部分 核心类型

C# 提供了一些特殊语法来帮助你在源代码中输入字面量字符串。对于换行、回车、退格等特殊字符，C# 使用了 C/C++ 开发者熟悉的转义机制：

```csharp
// 包含回车符和换行符的字符串
String s = "Hi\rnthere.";
```

> 重要：虽然前面的示例将回车符和换行符硬编码到字符串中，我不建议这种做法。`System.Environment` 类型定义了一个只读的 `NewLine` 属性，当你的应用程序在 Microsoft Windows 上运行时，它会返回由这些字符组成的字符串。然而，`NewLine` 属性是敏感的，它返回由底层平台所需的换所需的字符串。例如，如果通用语言基础设施（CLI）移植到 UNIX 系统，`NewLine` 属性将返回仅包含单个字符 `\n` 的字符串。以下是定义第一个字符串的正确方法，使其在任何平台上都能正常工作：

```csharp
```
