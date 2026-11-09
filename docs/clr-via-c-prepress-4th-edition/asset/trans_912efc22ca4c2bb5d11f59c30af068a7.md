
另一方面，如果 M 的声明方式如下：

```csharp
private static Int32 M(IComparable t) {
    ...
}
```

那么为了将 x 传递给 M，就必须对 x 进行装箱。

对于接口约束，C# 编译器会发出某些中间语言 (IL) 指令，这些指令会直接在值类型上调用接口方法，而无需对其进行装箱。除了使用接口约束之外，没有其他方法能让 C# 编译器发出这些 IL 指令，因此，在值类型上调用接口方法总是会导致装箱。

### 实现多个具有相同方法名和签名的接口

有时，你可能会发现自己定义了一个类型，它实现多个接口，而这些接口定义了具有相同名称和签名的方法。例如，假设有两个接口定义如下：

```csharp
public interface IWindow {
    Object GetMenu();
}
```

```csharp
public interface IRestaurant {
    Object GetMenu();
}
```

假设你想定义一个实现这两个接口的类型。你就必须通过显式接口方法实现来为该类型的成员提供实现，如下所示：

```csharp
// This type is derived from System.Object and
// implements the IWindow and IRestaurant interfaces.
public sealed class MarioPizzeria : IWindow, IRestaurant {

    // This is the implementation for IWindow's GetMenu method.
    Object IWindow.GetMenu() { ... }

    // This is the implementation for IRestaurant's GetMenu method.
    Object IRestaurant.GetMenu() { ... }

    // This (optional method) is a GetMenu method that has nothing
    // to do with either interface.
    public Object GetMenu() { ... }
}
```

由于该类型必须实现多个独立的 GetMenu 方法，你需要告诉 C# 编译器哪个 GetMenu 方法包含针对特定接口的实现。

实现，各种控件类只需继承它即可正常工作。

相比之下，Microsoft 将 FCL 集合设计为基于接口的。System.Collections.Generic 命名空间定义了若干与集合相关的接口：IEnumerable<out T>、ICollection<T>、IList<T> 和 IDictionary<TKey, TValue>。然后，Microsoft 提供了许多类，例如 List<T>、Dictionary<TKey, TValue>、Queue<T>、Stack<T> 等，这些类实现了上述接口的各种组合。这里，设计者在类与接口之间选择了“CAN-DO”（能做）关系，因为这些不同集合类的实现彼此截然不同。换句话说，List<T>、Dictionary<TKey, TValue> 和 Queue<T> 之间没有太多可共享的代码。

尽管如此，这些集合类提供的操作却相当一致。例如，它们都维护一组可枚举的元素，并且都允许添加和删除元素。如果你有一个引用，其对象类型实现了 IList<T> 接口，你就可以编写代码来插入元素、删除元素和搜索元素，而不必确切知道正在处理的是哪种集合类型。这是一个非常强大的机制。

最后，应该指出的是，你实际上可以两者兼做：定义一个接口，并提供一个实现该接口的基类。例如，FCL 定义了 IComparer<in T> 接口，任何类型都可以选择实现该接口。此外，FCL 还提供了一个抽象基类 Comparer<T>，它实现该接口，并为非泛型 IComparer 的 Compare 方法提供默认实现。同时提供接口定义和基类带来了极大的灵活性，因为开发者现在可以选择自己更偏好的方式。

## 第14章：字符、字符串与文本处理

本章内容：

- 字符 — 327
- System.String 类型 — 330
- 高效构造字符串 — 346
- 获取对象的字符串表示形式：`ToString` — 350
- 解析字符串以获取对象：`Parse` — 359
- 编码：在字符与字节之间转换 — 361
- 安全字符串 — 369

在本章中，我将解释在 Microsoft .NET Framework 中处理单个字符和字符串的机制。我将首先讨论 System.Char 结构以及操作字符的各种方式。然后，我将介绍更有用的 System.String 类，它允许你处理不可变字符串。（字符串一旦创建，就不能以任何方式修改。）在考察字符串之后，我将展示如何高效地执行各种操作，通过 System.Text.StringBuilder 类动态构建字符串。在介绍完字符串基础知识之后，我将描述如何将对象格式化为字符串，以及如何通过使用各种编码高效地持久化或传输字符串。最后，我将讨论 System.Security.SecureString 类，它可用于保护敏感字符串数据，例如密码和信用卡信息。

### 字符

在 .NET Framework 中，字符始终以 16 位 Unicode 代码值表示，这便于开发全球应用程序。字符由 System.Char 结构（一种值类型）的实例表示。System.Char 类型非常简单。它提供两个公共只读常量字段：MinValue（定义为 '\0'）和 MaxValue（定义为 '\uffff'）。

给定一个 Char 实例，你可以调用静态 GetUnicodeCategory 方法，该方法返回 System.Globalization.UnicodeCategory 枚举类型的值。此值指示字符是控制字符、货币符号、小写字母、大写字母、标点字符、数学符号还是其他字符（如 Unicode 标准所定义）。

为便于开发，Char 类型还提供若干静态方法，例如 IsDigit、IsLetter、IsWhiteSpace、IsUpper、IsLower、IsPunctuation、IsLetterOrDigit、IsControl、IsNumber、IsSeparator、IsSurrogate、IsLowSurrogate、IsHighSurrogate 和 IsSymbol。这些方法大多在内部调用 GetUnicodeCategory，并相应地直接返回 true 或 false。请注意，所有这些方法的参数要么是单个字符，要么是 String 以及该 String 中某个字符的索引。

此外，你可以通过调用静态 ToLowerInvariant 或 ToUpperInvariant 方法，以与文化无关的方式将单个字符转换为其小写或大写等效形式。或者，ToLower 和 ToUpper 方法使用与调用线程关联的区域性信息来转换字符（这些方法内部通过查询 System.Globalization.CultureInfo 类的静态 CurrentCulture 属性来获取该信息）。你也可以通过向这些方法传递 CultureInfo 类的实例来指定特定的区域性。ToLower 和 ToUpper 需要区域性信息，因为字母大小写转换是一种依赖于区域性的操作。例如，土耳其语将 U+0069（LATIN LOWERCASE LETTER I）的大写视为 U+0130（LATIN UPPERCASE LETTER I WITH DOT ABOVE），而其他区域性则将结果视为 U+0049（LATIN CAPITAL LETTER I）。

除了这些静态方法之外，Char 类型还提供了一些自己的实例方法。如果两个 Char 实例表示相同的 16 位 Unicode 代码点，则 Equals 方法返回 true。CompareTo 方法（由 IComparable/IComparable<Char> 接口定义）返回两个 Char 实例的比较结果；此比较不区分区域性。ConvertFromUtf32 方法从单个 UTF-32 字符生成一个由一个或两个 UTF-16 字符组成的字符串。ConvertToUtf32 从低/高代理项对或从字符串生成 UTF-32 字符。ToString 方法返回一个由单个字符组成的 String。与 ToString 相反的是 Parse/TryParse，它接受一个单字符 String 并返回其 UTF-16 代码点。

最后一个方法 GetNumericValue 返回字符的数值等效项。我在以下代码中演示此方法：

```csharp
using System;
```
