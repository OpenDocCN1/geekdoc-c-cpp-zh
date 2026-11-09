
要确定某个文件是否隐藏，可以执行如下代码：

```
String file = Assembly.GetEntryAssembly().Location;
FileAttributes attributes = File.GetAttributes(file);
Console.WriteLine("Is {0} hidden? {1}", file, (attributes & FileAttributes.Hidden) != 0);
```

**注意** Enum 类定义了一个 **HasFlag** 方法，定义如下：

```
public Boolean HasFlag(Enum flag);
```

使用此方法，可以将对 Console.WriteLine 的调用改写为如下形式：

```
Console.WriteLine("Is {0} hidden? {1}", file,
                  attributes.HasFlag(FileAttributes.Hidden));
```

但是，出于以下原因，我建议避免使用 **HasFlag** 方法：由于它接受 **Enum** 类型的参数，因此传递给它的任何值都必须装箱，这需要分配内存。

下面的代码演示了如何将文件属性更改为只读和隐藏：

```
File.SetAttributes(file, FileAttributes.ReadOnly | FileAttributes.Hidden);
```

正如 **FileAttributes** 类型所示，使用枚举类型来表示可组合的位标志集合很常见。然而，尽管枚举类型和位标志相似，但它们并不具有完全相同的语义。例如，枚举类型表示单个数值，而位标志表示一组位，其中一些位为开，一些位为关。

在定义用于标识位标志的枚举类型时，当然应显式地为每个符号分配一个数值。通常，每个符号都会有一个单独的位被打开。也常见到名为 None 的符号被定义为值 0，还可以定义表示常用组合的符号（参见下面的 **ReadWrite** 符号）。还强烈建议将 **System.FlagsAttribute** 自定义特性类型应用到枚举类型，如下所示：

```
[Flags]    // The C# compiler allows either "Flags" or "FlagsAttribute".
internal enum Actions {
    None    = 0,
    Read    = 0x0001,
    Write   = 0x0002,
    ReadWrite = Actions.Read | Actions.Write,
    Delete  = 0x0004,
    Query   = 0x0008,
    Sync    = 0x0010
}
```

由于 **Actions** 是枚举类型，因此在处理位标志枚举类型时，可以使用上一节中描述的所有方法。不过，如果其中一些函数的行为稍有不同，那会更好。例如，假设有以下代码：

```
Actions actions = Actions.Read | Actions.Delete;   // 0x0005
Console.WriteLine(actions.ToString());             // "Read, Delete"
Console.WriteLine(actions.ToString("F"));       // "Read, Delete"
```

如果数值中有一位无法映射到符号，则返回的字符串将仅包含一个十进制数，指示原始数值；字符串中不会出现任何符号。

请注意，在枚举类型中定义的符号不必是纯 2 的幂。例如，Actions 类型可以定义一个名为 All 的符号，其值为 0x001F。如果 Actions 类型的实例的值为 0x001F，则格式化该实例将生成一个包含“All”的字符串。其他符号字符串不会出现。

到目前为止，我已经讨论了如何将数值转换为标志字符串。也可以通过调用 Enum 的静态 Parse 和 TryParse 方法，将逗号分隔的符号字符串转换为数值。下面的代码演示了如何使用这些方法：

```csharp
// Because Query is defined as 8, 'a' is initialized to 8.
Actions a = (Actions) Enum.Parse(typeof(Actions), "Query", true);
Console.WriteLine(a.ToString()); // "Query"

// Because Query and Read are defined, 'a' is initialized to 9.
Enum.TryParse<Actions>("Query, Read", false, out a);
Console.WriteLine(a.ToString()); // "Read, Query"

// Creates an instance of the Actions enum with a value of 28
a = (Actions) Enum.Parse(typeof(Actions), "28", false);
Console.WriteLine(a.ToString()); // "Delete, Query, Sync"
```

调用 Parse 和 TryParse 时，内部会执行以下操作：

- 1. 它会移除字符串开头和结尾的所有空白字符。
- 2. 如果字符串的第一个字符是数字、加号（+）或减号（-），则假定该字符串是数字，并返回一个枚举实例，其数值等于该字符串转换后的数值。
- 3. 传入的字符串会被拆分为一组标记（以逗号分隔），并去除每个标记中的所有空白。
- 4. 每个标记字符串都会在枚举类型已定义的符号中查找。如果未找到该符号，Parse 会抛出 System.ArgumentException，TryParse 会返回 false。如果找到该符号，则将其数值按位或到累计结果中，然后查找下一个标记。
- 5. 如果所有标记都已查找并找到，则返回累计结果。

绝不要对位标志枚举类型使用 IsDefined 方法。它不会起作用，原因有两个：

- 如果向 IsDefined 传递字符串，它不会将该字符串拆分为单独的标记来查找；它会尝试将该字符串当作一个包含逗号的大符号来查找。由于不能定义包含逗号的符号的枚举，因此该符号将永远找不到。
- 如果向 IsDefined 传递数值，它会检查枚举类型是否定义了单个符号，其数值与传入的数字匹配。由于这对位标志来说不太可能，因此 IsDefined 通常会返回 false。

### 为枚举类型添加方法

在本章前面，我提到过不能将方法定义为枚举类型的一部分。而且，多年来这让我感到遗憾，因为有很多时候我都希望能为我的枚举类型提供一些方法。幸运的是，我可以使用 C# 的扩展方法特性（在第 8 章“方法”中讨论）来模拟向枚举类型添加方法。

如果我想向 FileAttributes 枚举类型添加一些方法，可以如下定义一个包含扩展方法的静态类：

```csharp
internal static class FileAttributesExtensionMethods {
    public static Boolean IsSet(this FileAttributes flags, FileAttributes flagToTest) {
        if (flagToTest == 0)
            throw new ArgumentOutOfRangeException("flagToTest", "Value must not be 0");
        return (flags & flagToTest) == flagToTest;
    }

    public static Boolean IsClear(this FileAttributes flags, FileAttributes flagToTest) {
        if (flagToTest == 0)
            throw new ArgumentOutOfRangeException("flagToTest", "Value must not be 0");
        return !IsSet(flags, flagToTest);
    }

    public static Boolean AnyFlagsSet(this FileAttributes flags, FileAttributes testFlags) {
        return ((flags & testFlags) != 0);
    }

    public static FileAttributes Set(this FileAttributes flags, FileAttributes setFlags) {
        return flags | setFlags;
    }

    public static FileAttributes Clear(this FileAttributes flags,
        FileAttributes clearFlags) {
        return flags & ~clearFlags;
    }

    public static void ForEach(this FileAttributes flags,
        Action<FileAttributes> processFlag) {
        if (processFlag == null) throw new ArgumentNullException("processFlag");
        for (UInt32 bit = 1; bit != 0; bit <<= 1) {
            UInt32 temp = ((UInt32)flags) & bit;
            if (temp != 0) processFlag((FileAttributes)temp);
        }
    }
}
```

下面是一些演示调用其中一些方法的代码。如你所见，这段代码看起来就像我在枚举类型上调用方法：

```csharp
FileAttributes fa = FileAttributes.System;
fa = fa.Set(FileAttributes.ReadOnly);
fa = fa.Clear(FileAttributes.System);
fa.ForEach(f => Console.WriteLine(f));
```

的 Int32 数组。最初，myIntegers 将被设置为 null，因为我还没有分配数组。第二行代码分配一个包含 100 个 Int32 值的数组；所有 Int32 都初始化为 0。由于数组是引用类型，容纳 100 个未装箱 Int32 所需的内存块会在托管堆上分配。实际上，除了数组元素之外，数组对象占用的内存块还包含类型对象指针、同步块索引以及一些额外的开销成员。该数组内存块的地址会被返回并保存到变量 myIntegers 中。

也可以创建引用类型数组：

```
Control[] myControls;        // Declares a reference to an array
myControls = new Control[50]; // Creates an array of 50 Control references
```

第一行中，myControls 是一个能够指向 Control 引用的一维数组的变量。最初，myControls 将被设置为 null，因为我还没有分配数组。第二行分配一个包含 50 个 Control 引用的数组；所有这些引用都初始化为 null。由于 Control 是引用类型，创建该数组只会创建一组引用；此时并不会创建实际对象。该内存块的地址会被返回并保存到变量 myControls 中。

图 16-1 展示了值类型数组和引用类型数组在托管堆中的样子。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_371_0.png)

**图 16-1** 托管堆中的值类型数组和引用类型数组。

图中，Controls 数组展示了执行以下代码行后的结果：

```
myControls[1] = new Button();
myControls[2] = new TextBox();
myControls[3] = myControls[2];  // Two elements refer to the same object.
myControls[46] = new DataGrid();
myControls[48] = new ComboBox();
myControls[49] = new Button();
```
