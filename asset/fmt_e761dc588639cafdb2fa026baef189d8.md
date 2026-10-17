
```csharp
using System;
using System.Security;
using System.Runtime.InteropServices;

public static class Program {
    public static void Main() {
        using (SecureString ss = new SecureString()) {
            Console.Write("请输入密码: ");
            while (true) {
                ConsoleKeyInfo cki = Console.ReadKey(true);
                if (cki.Key == ConsoleKey.Enter) break;

                // 将字符追加到 SecureString 中
                ss.AppendChar(cki.KeyChar);
            }
            Console.WriteLine();

            // 输入密码，为了演示目的显示它
            DisplaySecureString(ss);
        }
        // 'using' 后，SecureString 被销毁；内存中没有敏感数据
    }
}

// 此方法是不安全的，因为它访问非托管内存
private static void DisplaySecureString(SecureString ss) {
    Char* pc = null;
    try {
        // 将 SecureString 解密到非托管缓冲区
        pc = (Char*)Marshal.SecureStringToUnicode(ss);

        // 访问非托管缓冲区
        //包含解密后的字符串
        for (int index = 0; pc[index] != 0; index++) {
            Console.Write(pc[index]);
        }
    } finally {
        // 确保清零并释放非托管缓冲区
        // 解密后的字符
        if (pc != null)
            Marshal.ZeroFreeCoTaskUnicode((IntPtr)pc);
    }
}
```

`System.Runtime.InteropServices.Marshal` 类提供了五个方法，你可以调用这些方法将 `SecureString` 的字符解密到非托管内存缓冲区。所有这些方法都是静态的，都接受 `SecureString` 参数，并且都返回 `IntPtr`。每个方法都有一个对应的方法，你必须调用该方法以清空内部缓冲区并释放它。表 14-4 显示了 `System.Runtime.InteropServices.Marshal` 类将 `SecureString` 解密到内存缓冲区的方法以及相应的清零并释放缓冲区的方法。

# 表 14-4 Marshal 类处理安全字符串的方法

| 将 SecureString 解密到缓冲区的方法 | 清零并释放缓冲区的方法 |
|---|---|
| `SecureStringToBSTR` | `ZeroFreeBSTR` |
| `SecureStringToCoTaskMemAnsi` | `ZeroFreeCoTaskMemAnsi` |
| `SecureStringToCoTaskMemUnicode` | `ZeroFreeCoTaskMemUnicode` |
| `SecureStringToGlobal1AAllocAnsi` | `ZeroFreeGlobal1AAllocAnsi` |
| `SecureStringToGlobal1AAllocUnicode` | `ZeroFreeGlobal1AAllocUnicode` |

# 枚举类型与位标志

- 本章内容包括：
- 枚举类型............................................................... 373
- 位标志............................................................... 379
- 为枚举类型添加方法....................................................... 383

在本章中，我将讨论枚举类型和位标志。由于 Microsoft Windows 和许多编程语言多年来一直使用这些结构，我确信你们中的许多人已经熟悉了如何使用枚举类型和位标志。然而，公共语言运行时 `CLR` 和框架类库 `FCL` 共同工作，使得枚举类型和位标志变为了真正的面向对象类型类型，这些类型提供了一些我怀疑大多数开发者并不熟悉的新功能。令我惊讶的是，这些作为本章重点的新功能，竟然能让应用程序代码的开发变得如此简单。

# 枚举类型

枚举类型是一种定义了一组符号名称和值对应值对的类型。例如，这里所示的 `Color` 类型定义了一组符号，每个符号识别一种颜色：

```csharp
internal enum Color {
    White,  // 分配值为 0
    Red,    // 分配值为 1
    Green,  // 分配值为 2
    Blue,   // 分配值为 3
    Orange  // 分配值为 4
}
```

当然，程序员总是可以编写程序，使用 0 表示白色，1 表示红色，以此此类推。然而，程序员不应该在代码中硬编码数字，而应该使用枚举类型，其原因至少有两个点：

- 枚举类型使程序更易于阅读和维护。使用枚举类型，整个代码中使用的符号名称，程序不需要在脑中映射每个硬编码值的含义（例如，白色是 0 或反之亦然）。此外，如果符号的数值发生变化，可以重新编译代码而无需对源代码进行任何更改。此外，文档工具和其他程序（如调试器）可以向程序员显示符号名称。
- 枚举类型是强类型的。例如，如果尝试将 `Color.Orange` 作为值传递给需要 `Fruit` 枚举类型作为参数的方法，编译器将报告错误。

在 Microsoft `.NET Framework` 中，枚举类型不仅仅是编译器关心的符号。枚举类型被视为类型系统中的一等公民，这允许进行在非托管 C++ 或其他环境（例如，非托管 C++）中无法实现的强大操作。

每个枚举类型都直接派自 `System.Enum`，`System.Enum` 派自 `System.Object.ValueType`，后者又派自 `System.Object`。因此，枚举类型是值类型（在第 5 章“原始、引用和值类型”中描述），并以拆箱和箱的形式表示。与其他值类型不同，枚举类型不能定义任何方法、属性或事件。但是，你可以使用 C# 扩展方法来模拟为枚举类型添加属性。参见本章末尾的“为枚举类型添加方法”部分的示例。

当枚举类型被编译时，C# 编译器会将每个符号转换为该类型的常量字段。例如，编译器处理之前定义的 `Color` 枚举的方式，就像你写了类似下面的代码：

```csharp
struct Color : System.Enum {
    // 下面是定义 Color 符号和值的公共常量
    public const Color White = (Color 0);
    public const Color Red = (Color 1);
    public const Color Green = (Color 2);
    public const Color Blue = (Color 3);
    public const Color Orange = (Color 4);

    // 下面是一个包含 Color 变量值的公共实例字段
    // 你不能编写引用此实例字段的代码
    public Int32 value__;
}
```

C# 编译器实际上不会编译这段代码，因为它禁止你定义派生自特殊 `System.Enum` 的类型。然而，这个伪类型定义显示了内部发生了什么。基本上，枚举类型只是一个定义了一系列常量字段和一个实例字段的结构。常量字段被发射到程序集的元数据中，可以通过反射访问。这意味着你可以在运行时获取与枚举类型相关的所有符号及其值。这也意味着你可以将字符串符号转换为其等效的数值。这些操作可以通过 `System.Enum` 基类型提供，它提供了几个静态和实例方法，可以在枚举类型的实例上执行这些方法，从而省去了你必须使用反射的麻烦。我将在接下来讨论其中一些操作。

第 15 章 枚举类型与位标志

由枚举类型定义的**重要符号**是常量值。当编译器看到引用枚举类型符号的代码时，编译器会在编译时替换符号的数值，该代码将不再引用定义该符号的枚举类型。这意味着定义枚举类型的程序集在运行时可能是不需要的；它只在编译时需要。如果你有代码引用了枚举类型——而不仅仅是引用由该类型定义的符号——那么包含枚举类型定义的程序集在运行时是需要的。出现版本问题是因为枚举类型是常量而不是只读值。我已经在第 7 章“常量与字段”的“常量”部分解释了这些问题。

例如，`System.Enum` 类型有一个静态方法 `GetUnderlyingType`，而 `System.Type` 类型有一个实例方法 `GetUnderlyingType()`……

```csharp
public static Type GetUnderlyingType(Type enumType); // 定义在 System.Enum 中
public Type GetUnderlyingType();                   // 定义在 System.Type 中
```

这些方法返回持有核心类型。这些方法返回枚举类型的底层类型。每个枚举类型都有底层类型，可以是 `byte`、`sbyte`、`short`、`ushort`、`int`（C# 默认选择的类型）、`uint`、`long` 或 `ulong`。这些 C# 原始类型对应 FCL 类型。然而，为了简化实现，C# 编译器要求在此处指定原始类型名称（例如 `Int32`），生成以下内容：

```csharp
internal enum Color : byte {
    White,
    Red,
    Green,
    Blue,
    Orange
}
```

以这种方式定义枚举类型后，下面的代码显示了 `GetUnderlyingType()` 如何……

```csharp
// 这一行显示 "System.Byte"
Console.WriteLine(Enum.GetUnderlyingType(typeof(Color)));
```

C# 编译器将枚举类型视为原始类型。因此，你可以使用许多熟悉的运算符（`==`, `!=`, `<`, `>=`, `+`, `|`, `~`）来操作枚举类型实例。通常，我倾向于调用 `ToString` 方法，因为代码更少且更容易调用。但使用 `Format` 比 `ToString` 有一个优势：`Format` 允许你传递数值，而你不需要枚举类型的实例。例如，下面的代码将显示 "Blue"：

```csharp
// 这一行显示 "Blue"
Console.WriteLine(Enum.Format(typeof(Color), 3, "G"));
```

除了 `ToString` 方法外，`System.Enum` 类型还提供了一个静态方法 `Format`，用来格式化枚举类型：

> 注意 可以定义具有相同数值的多个符号的枚举类型。当使用通用格式化将数值转换为符号时，Enum 的方法返回符号之一。然而，无法保证返回的是哪一个符号。此外，对于要查找的数值没有定义符号，则返回一个包含该数值的字符串。

你还可以调用 `System.Enum` 的静态 `GetValues` 方法或 `System.Type` 的实例 `GetEnumValues` 方法来获取一个包含枚举类型中每个符号名称元素的数组；每个元素包含该符号的数值：

```csharp
Color[] colors = (Color[])Enum.GetValues(typeof(Color));
Console.WriteLine("定义的符号数量: " + colors.Length);
```

# 控制台 15 枚举类型与位

```csharp
Console.WriteLine("Value\tsymbol\n-----\t----");
```

之前的代码产生以下输出：

定义的符号数量： 5

| Value | Symbol |
|---|---|
| 0 | White |
| 1 | Red |
| 2 | Green |
| 3 | Blue |
| 4 | Orange |

这段讨论展示了在枚举类型上可以执行的一些酷炫操作。我推测，只要字符串不需要本地化（因为枚举类型不支持本地化），在程序的用户界面元素（如列表框、复选框等）中，使用带有通用格式的 `ToString` 方法将频繁使用符号名称。除了 `GetValues` 方法外，`System.Enum` 类型和 `System.Type` 类型还提供了以下返回枚举类型符号的方法：

```csharp
// 返回数值的字符串表示形式
public static String GetName(Enum type, Object value); // 定义在 System.Enum 中
public static Object GetEnumName(Object value); // 定义在 System.Type 中
```

```csharp
// 返回字符串数组：枚举中定义的每个符号返回一个
public static String[] GetNames(Enum type); // 定义在 System.Enum 中
public static String[] GetNames(); // 定义在 System.Type 中
```

我发现了一些可以使用来查找枚举符号的方法。但你还需要一个可以查找符号等效值的方法，该操作可以用于将用户在文本框中输入的符号转换为值，例如。将符号转换为枚举实例可以使用 `Enum` 的 `Parse` 和 `TryParse` 方法之一轻松地实现：

```csharp
public static Object Parse(Enum type, String value);
public static Object Parse(Enum type, String value, Boolean ignoreCase);
public static Boolean TryParse<TEnum>(String value, out TEnum result) where TEnum : struct;
public static Boolean TryParse<TEnum>(String value, Boolean ignoreCase, out TEnum result) where TEnum : struct;
```

这里是演示如何使用该方法的代码：

```csharp
// 因为 Orange 被定义为 4，所以 'c' 初始化为 4。
Color c = (Enum)Parse(typeof(Color), "orange", true);
```

# 第三部分 基础类型

```csharp
// 因为没有定义 Brown，所以抛出 ArgumentException 
c = (Color)Enum.Parse(typeof(Color), "Brown", false);
```

```csharp
// 创建一个值为 1 的 Color 枚举实例
Enum.TryParse(Color, "1", false, out c);
```

```csharp
// 创建一个值为 23 的 Color 枚举实例
Enum.TryParse(Color, "23", false, out c);
```

最后，使用 `Enum` 的静态方法 `IsDefined` 和 `Type` 的 `IsDefined` 方法，

```csharp
public static Boolean IsDefined(Type enumType, Object value); // 定义在 System.Enum 中
public Boolean IsDefined(Object value); // 定义在 System.Type 中
```

你可以判断一个数值对于某个枚举类型是否是法的：

```csharp
// 显示 "True"，因为 Color 将 Red 定义为 1
Console.WriteLine(Enum.IsDefined(typeof(Color), 1));
```

```csharp
// 显示 "True"，因为 Color 将 White 定义为 0
Console.WriteLine(Enum.IsDefined(typeof(Color), "White"));
```

```csharp
// 显示 "False"，因为执行了区分大小写的检查
Console.WriteLine(Enum.IsDefined(typeof(Color), "white"));
```

```csharp
// 显示 "False"，因为 Color 没有值为 10 的符号
Console.WriteLine(Enum.IsDefined(typeof(Color), 10));
```

`IsDefined` 方法经常被用于参数验证。这里有一个示例：

```csharp
public void SetColor(Color c, Color c) {
    if (!Enum.IsDefined(typeof(Color), c)) {
        throw new ArgumentOutOfRangeException("c", c, "Invalid color value.");
    }
    // 设置颜色为 White, Red, Green, Blue 或 Orange
    //...
}
```

参数验证是有用的，因为有人可以这样调用 `SetColor`：
