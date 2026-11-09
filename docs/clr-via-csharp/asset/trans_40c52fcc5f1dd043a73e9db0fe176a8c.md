
给定一个枚举类型的实例，可以通过调用从 System.Enum 继承的 ToString 方法，将该值映射为几种字符串表示之一：

```csharp
Color c = Color.Blue;
Console.WriteLine(c);          // "Blue" (General format)
Console.WriteLine(c.ToString()); // "Blue" (General format)
Console.WriteLine(c.ToString("G")); // "Blue" (General format)
Console.WriteLine(c.ToString("D")); // "3" (Decimal format)
Console.WriteLine(c.ToString("X")); // "03" (Hex format)
```

> **注意** 使用十六进制格式时，ToString 始终输出大写字母。此外，输出的位数取决于枚举的基础类型：byte/sbyte 为 2 位，short/ushort 为 4 位，int/uint 为 8 位，long/ulong 为 16 位。如有必要，将输出前导零。

除了 ToString 方法之外，System.Enum 类型还提供了一个静态的 Format 方法，你可以调用它来格式化枚举类型的值：

```csharp
public static string Format(Type enumType, Object value, String format);
```

通常，我更倾向于调用 ToString 方法，因为它需要的代码更少，也更容易调用。但与 ToString 相比，使用 Format 有一个优势：Format 允许你为 value 参数传递数值；你不必拥有枚举类型的实例。例如，下面的代码将显示“Blue”：

```csharp
// The following line displays "Blue".
Console.WriteLine(Enum.Format(typeof(Color), 3, "G"));
```

> **注意** 可以声明一个枚举类型，其中包含多个符号，且所有符号都具有相同的数值。当使用常规格式将数值转换为符号时，Enum 的方法会返回其中一个符号。但是，不保证返回哪个符号名称。此外，如果要查找的数值没有定义符号，则返回包含该数值的字符串。

还可以调用 System.Enum 的静态 GetValues 方法或 System.Type 的实例 GetEnumValues 方法，来获取一个数组，该数组包含枚举类型中每个符号名称对应的一个元素；每个元素包含该符号名称的数值：

```csharp
public static Array GetValues(Type enumType);           // Defined in System.Enum
public           Array GetEnumValues();                 // Defined in System.Type
```

结合使用此方法与 ToString 方法，可以显示枚举类型的所有符号和数值，如下所示：

```csharp
Color[] colors = (Color[]) Enum.GetValues(typeof(Color));
Console.WriteLine("Number of symbols defined: " + colors.Length);
Console.WriteLine("Value\tSymbol\n-----\t------");
foreach (Color c in colors) {
    // Display each symbol in Decimal and General format.
    Console.WriteLine("{0,5:D}\t{0:G}", c);
}
```

上面的代码产生以下输出：

Number of symbols defined: 5

| 值 | 符号 |
|------:|:-------|
| 0 | White |
| 1 | Red |
| 2 | Green |
| 3 | Blue |
| 4 | Orange |

本次讨论展示了可以在枚举类型上执行的一些很酷的操作。我猜想，**ToString** 方法与常规格式结合使用，会相当频繁地用于在程序的用户界面元素（列表框、组合框等）中显示符号名称，只要这些字符串不需要本地化（因为枚举类型不支持本地化）。除了 **GetValues** 方法之外，**System.Enum** 类型和 **System.Type** 类型还提供了以下返回枚举类型符号的方法：

```csharp
// Returns a String representation for the numeric value
public static String GetName(Type enumType, Object value);    // Defined in System.Enum
public        String GetEnumName(Object value);               // Defined in System.Type
```

```csharp
// Returns an array of Strings: one per symbol defined in the enum
public static String[] GetNames(Type enumType);              // Defined in System.Enum
public        String[] GetEnumNames();                       // Defined in System.Type
```

我已经讨论了许多可以用来查找枚举类型符号的方法。但是，你还需要一种方法来查找符号对应的值，例如，该操作可用于转换用户在文本框中输入的符号。使用 **Enum** 的静态 **Parse** 和 **TryParse** 方法之一，可以轻松地将符号转换为枚举类型的实例：

```csharp
public static Object Parse(Type enumType, String value);
public static Object Parse(Type enumType, String value, Boolean ignoreCase);
public static Boolean TryParse<TEnum>(String value, out TEnum result) where TEnum : struct;
public static Boolean TryParse<TEnum>(String value, Boolean ignoreCase, out TEnum result)
    where TEnum : struct;
```

下面是一些演示如何使用此方法的代码：

```csharp
// Because Orange is defined as 4, 'c' is initialized to 4.
Color c = (Color) Enum.Parse(typeof(Color), "orange", true);

// Because Brown isn't defined, an ArgumentException is thrown.
c = (Color) Enum.Parse(typeof(Color), "Brown", false);

// Creates an instance of the Color enum with a value of 1
Enum.TryParse<Color>("1", false, out c);

// Creates an instance of the Color enum with a value of 23
Enum.TryParse<Color>("23", false, out c);
```

最后，使用 **Enum** 的静态 **IsDefined** 方法和 **Type** 的 **IsEnumDefined** 方法，

```csharp
public static Boolean IsDefined(Type enumType, Object value);     // Defined in System.Enum
public          Boolean IsEnumDefined(Object value);              // Defined in System.Type
```

你可以确定一个数值对于枚举类型是否合法：

```csharp
// Displays "True" because Color defines Red as 1
Console.WriteLine(Enum.IsDefined(typeof(Color), 1));

// Displays "True" because Color defines White as 0
Console.WriteLine(Enum.IsDefined(typeof(Color), "White"));

// Displays "False" because a case-sensitive check is performed
Console.WriteLine(Enum.IsDefined(typeof(Color), "white"));

// Displays "False" because Color doesn't have a symbol of value 10
Console.WriteLine(Enum.IsDefined(typeof(Color), 10));
```

**IsDefined** 方法经常用于参数验证。下面是一个示例：

```csharp
public void SetColor(Color c) {
    if (!Enum.IsDefined(typeof(Color), c)) {
        throw(new ArgumentOutOfRangeException("c", c, "Invalid Color value."));
    }
    // Set color to White, Red, Green, Blue, or Orange
}
...
```

参数验证非常有用，因为有人可能会像这样调用 **SetColor**：

```csharp
SetColor((Color) 547);
```

由于没有符号具有对应的值 547，**SetColor** 方法将抛出 **ArgumentOutOfRangeException** 异常，指明哪个参数无效以及原因。

若要确定文件是否隐藏，可以执行如下代码：

```csharp
String file = Assembly.GetEntryAssembly().Location;
FileAttributes attributes = File.GetAttributes(file);
Console.WriteLine("Is {0} hidden? {1}", file, (attributes & FileAttributes.Hidden) != 0);
```

> **注意** `Enum` 类定义了一个 `HasFlag` 方法，定义如下：
>
> ```csharp
> public Boolean HasFlag(Enum flag);
> ```
>
> 使用此方法，你可以将 `Console.WriteLine` 的调用重写为：
>
> ```csharp
> Console.WriteLine("Is {0} hidden? {1}", file,
>     attributes.HasFlag(FileAttributes.Hidden));
> ```
>
> 但是，我建议你避免使用 `HasFlag` 方法，原因如下：由于它接受 `Enum` 类型的参数，你传递给它的任何值都必须装箱，这需要一次内存分配。

下面是一个演示如何将文件属性更改为只读和隐藏的代码：

```csharp
File.SetAttributes(file, FileAttributes.ReadOnly | FileAttributes.Hidden);
```

正如 **FileAttributes** 类型所示，通常使用枚举类型来表示可以组合的位标志集合。然而，尽管枚举类型和位标志相似，但它们的语义并不完全相同。例如，枚举类型表示单个数值，而位标志表示一组位，其中一些位为开，另一些位为关。

当定义用于标识位标志的枚举类型时，你当然应该为每个符号显式分配一个数值。通常，每个符号都会有一个单独的位被置为 1。也很常见的是定义一个名为 **None** 的符号，其值为 0，并且你还可以定义表示常用组合的符号（请参阅下面的 **ReadWrite** 符号）。还强烈建议你为枚举类型应用 **System.FlagsAttribute** 自定义特性类型，如下所示：

```csharp
[Flags]    // The C# compiler allows either "Flags" or "FlagsAttribute".
internal enum Actions {
    None       = 0,
    Read       = 0x0001,
    Write      = 0x0002,
    ReadWrite  = Actions.Read | Actions.Write,
    Delete     = 0x0004,
    Query      = 0x0008,
    Sync       = 0x0010
}
```
