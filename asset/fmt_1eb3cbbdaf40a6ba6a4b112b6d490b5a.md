
注意，我在上面将虚方法定义为公共方法，但在某些情况下，你可能倾向于将其定义为保护方法。这将导致微小的更改。这段讨论清楚地表明 EMI 应该谨慎使用。当许多开发者首次学习 EMI 时，他们认为它们很酷并尽可能使用。不要这样做！EMI 在某些情况下很有用，但你应该尽可能避免它们，因为它们会让类型变得复杂。

## 设计：基类还是接口？

我经常听到“我应该设计基类型还是接口？”答案并不总是显而易见的。这里有一些可以帮助你的指南：

- **IS-A 与 CAN-DO 关系**：类型只能继承基类型的 IS-A 关系，不要使用基类型；使用接口。接口意味着 CAN-DO 关系。接口的功能似乎与各种类型关联，作为接口。
- **易用性**：实现接口通常比实现基类容易。
- **一致的实现**：这些集合类提供的操作仍然是一致的。
- **版本控制**：如果你在基类型中添加了方法，派生类型就需要更改。

在与数据流相关的 FCL 中，`System.IO.Stream` 是抽象类。它提供了许多方法，例如 **Read** 和 **Write**。其他类——`System.IO.FileSystem`、`System.IO.MemoryStream` 和 `System.Net.Sockets.NetworkStream`——都派自 `Stream`。微软选择了一个

img/ba8f96d66195f73315fb4561d0b5_342.png

## 第 14 章

字符、字符串与文本处理

在本章中：

- 字符. ................................................................................................................................................. . . . . . . . . . . . . . . . . . . 327
- System.String 类型. ................................................................................. . . . . . . . . . . . . . . . . . . . . . . . . 330
- 高效构建字符串. ................................................................................................. . . . . . . . . . . . . . . . . . . . . . . . . 346
- 获取对象的字符串表示：ToString . . . . . . . . . . . . . . . . . . . . . . . . . . . . 350
- 解析字符串以获取对象：Parse ................................................................. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 359
- 编码：字符与字节之间的转换 ................................................................. . . . . . . . . . . . . . . . . . . . . . 361
- 安全字符串 ................................................................................................................................................. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 369

在本章中，我将解释在 Microsoft .NET Framework 中处理单个字符和字符串的机制。我将首先介绍 `System.Char` 结构体以及操纵字符的各种方法。然后，我将介绍更有用的 `System.String` 类，它允许你处理不可变字符串（一旦创建，字符串无法以任何方式进行修改）。在研究字符串之后，我将向你展示如何使用 `System.Text.StringBuilder` 类高效地执行各种操作以动态构建字符串。在完成字符串基础知识后，我将描述如何将对象格式化为字符串，以及如何使用各种编码高效地持久或传输字符串。最后，我将讨论 `System.Security.SecureString` 类，它可以用于保护密码和信用卡信息等敏感字符串数据。

## 字符

在 .NET Framework 中，字符始终由 16 位 Unicode 值表示，这便于全球化应用的开发。字符由 `System.Char` 结构体（一种值类型）的实例表示。`System.Char` 类型非常简单。它提供了两个公共只读常量字段：定义为 `'\0'` 的 `MinValue` 和定义为 `'\ffff'` 的 `MaxValue`。

给定一个 `Char` 实例，你可以调用静态方法 `GetUnicodeCategory`，它返回一个 `System.Globalization.UnicodeCategory` 枚举类型的值。该值指示该字符是控制字符、货币符号、小写字母、大写字母、标点符号、数学符号或其他字符（由 Unicode 标准定义）。

## 核心类型

为了方便开发，`Char` 类型还提供了几个静态方法，例如 `IsDigit`、`IsLetter`、`IsWhiteSpace`、`IsUpper`、`IsLower`、`IPunctuation`、`IsLetterOrDigit`、`IsControl`、`IsNumber`、`IsSeparator`、`IsSurrogate`、`IsHighSurrogate` 和 `IsSymbol`。这些方法中的大多数在内部调用 `GetUnicodeCategory` 并简单地返回 true 或 false。请注意，所有这些方法都以单个字符作为参数，或者以 `String` 以及 `String` 中的字符索引作为参数来检查字符。

此外，你可以通过调用静态 `ToLowerInvariant` 和 `ToUpperInvariant` 方法以与文化无关的方式将单个字符转换为其小写或大写形式。或者，`ToLower` 和 `ToUpper` 方法使用与调用线程相关的文化信息来转换字符（这些方法通过查询 `System.Thread` 类的静态属性 `CurrentCulture` 获取这些信息）。你也可以通过向这些方法传递 `CultureInfo` 类实例来指定特定的字符。`ToLower` 和 `ToUpper` 需要文化信息，因为字母的大小写是取决于文化的操作。例如，在土耳其语中，U+0069（拉丁小写字母 I）的大写是 U+0130（带点的拉丁大写字母 I），而其他文化认为结果是 U+0049（拉丁大写字母 I）。

除了这些静态方法，`Char` 类型还提供了一些自己的方法。`Equals` 方法在两个实例表示相同的 16 位 Unicode 代码点时返回 true。`CompareTo` 方法（由 `IComparable/IComparableChar` 定义）返回两个 char 实例的比较；这种比较不具有文化感知。`ConvertFromUtf32` 方法从单个 UTF-32 字符生成一个由 UTF-16 字符组成的字符串。`ConvertToUtf32` 从低/高代理对或从字符串生成 UTF-16 字符。`ToString` 方法返回一个由单个字符组成的字符串，而 `Parse/TryParse` 接受单个字符字符串并返回其 UTF-16 代码点。

最后一个方法 `GetNumericValue` 返回字符的数值等效值。我在下面的代码中演示了这一点：

```csharp
using System;

public static class Program
{
    public static void Main()
    {
        double d; // '\u0033' 是 "数字 3"
        d = Char.GetNumericValue("\u0033"); // '3' 也可以
        Console.WriteLine(d.ToString()); // 显示 "3"

        // // '\u00bc' 是 "通俗分数四分之一 ('¼')"
        d = Char.GetNumericValue("\u00bc");
        Console.WriteLine(d.ToString()); // 显示 "0.25"

        // // 'A' 是 "拉丁字母 A"
        d = Char.GetNumericValue('A');
        Console.WriteLine(d.ToString()); // 显示 "-1"
    }
}
```

第 14 章 字符、字符串与文本处理 329

最后，三种技术允许你在类型与 `Char` 之间进行进行转换。这些技术按偏好排序列举如下：

- 将 `Char` 转换为数值（如 `Int32`）最简单的方法是直接强制类型转换。在三种技术中，这种效率最高，因为编译器产生中间语言 (IL) 指令来执行转换，不需要调用方法。此外，某些语言（如 C#）允许你指示是否使用检查或未检查代码来执行转换。
- `Convert` 类型 `System` 提供了几个静态方法，可以将 `Char` 转换为数值类型并反之亦然。所有这些方法都作为检查操作执行转换，如果转换导致数据丢失，将抛出 `OverflowException`。
- `Convertible` 接口 `Char` 和 .NET Framework 类库 (FCL) 中的所有数值类型都实现了 `Convertible` 接口。该接口定义了使用 `Int16` 和 `ToChar` 方法。这种技术是三种技术中效率最低的，因为在值类型上调用接口方法需要对实例进行装箱（boxing），`Char` 和所有数值类型都是值类型。`IConvertible` 的方法在类型无法转换（例如将 `Char` 转换为布尔）或转换导致数据丢失时会抛出 `System.InvalidException`。请注意，许多类型（包括 FCL 的 `Char` 和数值类型）以显式接口成员实现的方式实现 `IConvertible` 的方法（在第 13 章“接口”中描述）。这意味着在调用接口的任何方法之前，你必须显式将实例转换为 `IConvertible`。`IConvertible` 除 `GetTypeCode` 之外的所有方法都接受一个实现 `IFormat` 接口的对象的引用。此参数对于考虑某些文化信息很有用。对于大多数转换，你可以为此参数传递 null，因为无论如何它都会被忽略。

```csharp
c = unchecked((Char) 65536 + 65));
Console.WriteLine(c);
// 输出 "A"
```

```csharp
// 使用 Convert 进行数字与字符转换
c = Convert.ToChar(65);
Console.WriteLine(c);
// 输出 "A"
```

```csharp
n = Convert.ToInt32(c);
Console.WriteLine(n);
// 输出 "65"
```

```csharp
// 此处演示了 Convert 的范围检查
try {
    c = Convert.ToChar(70000);
    // 对于 16 位长度来说太大了
    Console.WriteLine(c);
    // 不执行
} catch (OverflowException) {
    Console.WriteLine("无法将 70000 转换为 Char。");
}
```

```csharp
// 使用 IConvertible 进行数字与字符转换
c = ((IConvertible) 65).ToChar(null);
Console.WriteLine(c);
// 输出 "A"
```

```csharp
n = ((IConvertible) c).ToInt32(null);
Console.WriteLine(n);
// 输出 "65"
```

## System.String 类型

任何应用程序中使用频率最高的类型之一是 `System.String`。`String` 表示一个不可变的有序字符集合。`String` 类型直接派自 `Object`，使其成为一种引用类型，因此，`String` 对象（其字符数组）存储在堆（heap）中，而永远不会存储在线程的栈（stack）上。`String` 类型还实现了几个接口（`IComparable/IComparable<String>`、`ICloneable`、`IConvertible`、`IEnumerable/IEnumerable<Char>` 以及 `IEquatable<String>`）。

## 创建字符串

许多编程语言（包括 C#）将 `String` 视为一种原始类型——也就是说，编译器允许你直接在源代码中表示字面量字符串。编译器将字面量字符串放置在模块的元数据中，然后在运行时对其进行加载和引用。

## 第 14 章 字符、字符串与文本处理 331

在 C# 中，你不能使用 `new` 操作符从字面量字符串构造 `String` 对象：

using System;

```csharp
public static class Program {
    public static void Main() {
        String s = new String("Hi there."); // <-- 错误
        Console.WriteLine(s);
    }
}
```

相反，你必须使用简写语法：

using System;

```csharp
public static class Program {
    public static void Main() {
        String s = "Hi there.";
        Console.WriteLine(s);
    }
}
```

如果你编译这段代码并检查其 IL（使用 `ILasm.exe`），你将看到以下内容：

```il
.method hidebyis static void Main() cil managed {
    .entrypoint size
    // 代码大小 13 (0d)
    .maxstack 1
    .locals int (string V_0)
    IL_0000: ldstr "Hi there."
    IL_0005: stloc.0
    IL_0006: ldloc.0
    IL_0007: call void [mscorlib]System.Console::WriteLine(string)
    IL_000c: ret
} // 方法 Program:Main 结束
```

`new` IL 指令构造一个对象的新实例。然而，IL 代码示例中并没有出现 `new` 指令。相反，你看到了特殊的 `ldstr`（加载字符串）指令，它使用来自元数据的字面量字符串来构造 `String` 对象。这表明通用语言运行时（CLR）确实有一种构造字面量 `String` 对象的特殊方法。

如果你在使用不安全代码（unsafe code），可以从 `Char*` 或 `SByte*` 构造 `String` 对象。要实现这一点，你需要使用 C# 的 `new` 操作符以及 `String` 类型提供的接收 `Char*` 或 `SByte` 的构造函数之一。这些构造函数创建 `String` 对象，通过 `Char` 实例数组或有符号字节初始化字符串。其他构造函数没有任何指针参数，可以使用使用任何托管编程语言编写的安全（可验证的）代码进行调用。

C# 提供了一些特殊语法来帮助你将字符串输入源代码。对于换行符、回车符、退格键等特殊字符，C# 使用了 C/C++ 开发者熟悉的转义机制：

```csharp
// 包含回车符和换行符
String s = "Hi\rnthere.";
```

> **重要**：虽然前面的示例将回车符和换行符硬编码到字符串中，但我我不建议这种做法。相反，`System.Environment` 类型定义了一个只读的 `NewLine` 属性，当你的应用程序在 Microsoft Windows 上运行时，它会返回由这些字符组成的字符串。`NewLine` 属性是平台敏感的，它返回底层平台获取换行符所需的字符串。例如，如果通用语言基础设施（CLI）被移植到 UNIX 系统，`NewLine` 属性将返回仅由单个字符 `\n` 组成的字符串。以下是定义上述字符串的正确方法，使其能够在任何平台上正确工作：

```csharp
String s = "Hi" + Environment.NewLine + "there.";
```

使用 `+` 运算符连接字符串形成单个字符串：

```csharp
// 连接字符串形成单个字符串
String s = "Hi" + " " + "there.";
```

C# 还提供了一种特殊方式来声明字符串，其中引号之间的字符被视为字符串的一部分。这种特殊的声明被称为逐字字符串，通常用于指定路径或目录：

```csharp
// 指定路径或目录
String path = @"C:\Windows\System32";
```

## 14 章 字符、字符串与文本处理 350

## 字符串是不可变的

关于 `String` 对象最重要的一点是它是不可变的。一旦创建，字符串就不会变长、变短，或改变其字符。出于性能考虑，`String` 类型与 CLR 紧密集成。该类是密封的（sealed），这意味着你不能将其作为基类。

## 比较字符串

比较可能是对字符串执行的最常见操作。比较字符串有两个原因：确定等等性或对其进行排序（通常是为了演示）。

在确定等等性或排序时，强烈建议调用这些方法之一（由 `String` 定义）：
