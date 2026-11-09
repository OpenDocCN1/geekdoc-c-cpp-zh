
在你的方法内部，必须让 SecureString 对象先创建一个包含已解密字符的非托管内存缓冲区，然后你的方法才能使用该缓冲区。为了让恶意代码访问敏感数据的时机窗口尽可能小，你的代码应尽可能缩短对已解密字符串的访问时间。使用完该字符串后，你的代码应尽快将缓冲区清零并释放它。此外，切勿将 SecureString 的内容放入 String；如果这样做，String 会以未加密的形式存在于堆中，并且其字符在垃圾回收后内存被重用之前不会被清零。SecureString 类没有重写 ToString 方法，其目的正是为了避免暴露敏感数据（如果将其转换为 String 就会暴露）。

下面是一个示例代码，演示如何初始化和使用 SecureString（编译此代码时，你需要为 C# 编译器指定 /unsafe 开关）：

```csharp
using System;
using System.Security;
using System.Runtime.InteropServices;

public static class Program {
    public static void Main() {
        using (SecureString ss = new SecureString()) {
            Console.Write("Please enter password: ");
            while (true) {
                ConsoleKeyInfo cki = Console.ReadKey(true);
                if (cki.Key == ConsoleKey.Enter) break;

                // Append password characters into the SecureString
                ss.AppendChar(cki.KeyChar);
                Console.Write("*");
            }
            Console.WriteLine();

            // Password entered, display it for demonstration purposes
            DisplaySecureString(ss);
        }
        // After 'using', the SecureString is Disposed; no sensitive data in memory
    }

    // This method is unsafe because it accesses unmanaged memory
    private unsafe static void DisplaySecureString(SecureString ss) {
        Char* pc = null;
        try {
            // Decrypt the SecureString into an unmanaged memory buffer
            pc = (Char*) Marshal.SecureStringToCoTaskMemUnicode(ss);

            // Access the unmanaged memory buffer that
            // contains the decrypted SecureString
            for (Int32 index = 0; pc[index] != 0; index++)
                Console.Write(pc[index]);
        }
        finally {
            // Make sure we zero and free the unmanaged memory buffer that contains
            // the decrypted SecureString characters
            if (pc != null)
                Marshal.ZeroFreeCoTaskMemUnicode((IntPtr) pc);
        }
    }
}
```

System.Runtime.InteropServices.Marshal 类提供了五个方法，你可以调用它们将 SecureString 的字符解密到非托管内存缓冲区中。这些方法全部是静态方法，都接受一个 SecureString 参数，并且都返回一个 IntPtr。每个方法都有一个对应的方法，你必须调用对应方法来清零内部缓冲区并释放它。表 14-4 展示了 System.Runtime.InteropServices.Marshal 类将 SecureString 解密到内存缓冲区的方法，以及用于清零并释放缓冲区的对应方法。

**表 14-4** Marshal 类用于处理安全字符串的方法

| 将 SecureString 解密到缓冲区的方法 | 清零并释放缓冲区的方法 |
|---|---|
| SecureStringToBSTR | ZeroFreeBSTR |
| SecureStringToCoTaskMemAnsi | ZeroFreeCoTaskMemAnsi |
| SecureStringToCoTaskMemUnicode | ZeroFreeCoTaskMemUnicode |
| SecureStringToGlobalAllocAnsi | ZeroFreeGlobalAllocAnsi |
| SecureStringToGlobalAllocUnicode | ZeroFreeGlobalAllocUnicode |

## 第 15 章：枚举类型和位标志

- 本章内容：
  - 枚举类型 373
  - 位标志 379
  - 向枚举类型添加方法 383

在本章中，我将讨论枚举类型和位标志。由于 Microsoft Windows 和许多编程语言使用这些结构已经很多年了，我相信你们中的许多人已经熟悉如何使用枚举类型和位标志。然而，公共语言运行时（CLR）和框架类库（FCL）协同工作，使枚举类型和位标志成为真正的面向对象类型，提供了我怀疑大多数开发人员并不熟悉的酷炫功能。令我惊讶的是，这些功能（也是本章的重点）使得应用程序代码的开发变得如此容易。

### 枚举类型

*枚举类型*是一种定义一组符号名称和值对的类型。例如，这里显示的 Color 类型定义了一组符号，每个符号标识一种颜色：

```csharp
internal enum Color {
    White,      // Assigned a value of 0
    Red,        // Assigned a value of 1
    Green,      // Assigned a value of 2
    Blue,       // Assigned a value of 3
    Orange      // Assigned a value of 4
}
```

当然，程序员总是可以用 0 表示白色、1 表示红色等来编写程序。但是，程序员不应在代码中硬编码数字，而应改用枚举类型，至少有两点原因：

- 枚举类型使程序更易于阅读和维护。使用枚举类型，符号名称贯穿整个代码，程序员无需在脑中映射每个硬编码值的含义（例如，白色是 0，或反之）。此外，如果某个符号的数值发生变化，只需重新编译代码，无需对源代码进行任何更改。另外，文档工具和其他实用程序（如调试器）可以向程序员显示有意义的符号名称。

- 枚举类型是强类型的。例如，如果我将 Color.Orange 作为值传递给需要 Fruit 枚举类型参数的方法，编译器将报告错误。

在 Microsoft .NET Framework 中，枚举类型不仅仅是编译器关心的符号。枚举类型在类型系统中被视为一等公民，这允许执行一些非常强大的操作，而这些操作在其他环境（例如非托管 C++）中根本无法使用枚举类型完成。

每个枚举类型都直接派生自 System.Enum，而 System.Enum 派生自 System.ValueType，System.ValueType 又派生自 System.Object。因此，枚举类型是值类型（在第 5 章“基元、引用和值类型”中描述），可以以未装箱和已装箱的形式表示。但是，与其他值类型不同，枚举类型不能定义任何方法、属性或事件。不过，你可以使用 C# 的扩展方法功能来模拟向枚举类型添加方法。有关示例，请参阅本章末尾的“向枚举类型添加方法”一节。

编译枚举类型时，C# 编译器会将每个符号转换为该类型的常量字段。例如，编译器会像处理你编写了类似以下代码一样处理前面显示的 Color 枚举：

```csharp
internal struct Color : System.Enum {
    // Below are public constants defining Color's symbols and values
    public const Color White  = (Color) 0;
    public const Color Red    = (Color) 1;
    public const Color Green  = (Color) 2;
    public const Color Blue   = (Color) 3;
    public const Color Orange = (Color) 4;

    // Below is a public instance field containing a Color variable's value
    // You cannot write code that references this instance field directly
    public Int32 value__;
}
```

C# 编译器实际上不会编译此代码，因为它禁止你定义从特殊的 System.Enum 类型派生的类型。然而，这个伪类型定义展示了内部发生的情况。基本上，枚举类型只是一个结构，其中定义了一组常量字段和一个实例字段。常量字段会被写入程序集的元数据中，并且可以通过反射访问。这意味着你可以在运行时获取与枚举类型关联的所有符号及其值。这也意味着你可以将字符串符号转换为其等效的数值。System.Enum 基类型为你提供了这些操作，它提供了几个可在枚举类型实例上执行的静态和实例方法，让你不必使用反射。我将讨论其中一些

