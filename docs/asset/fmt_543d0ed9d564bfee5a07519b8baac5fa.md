
```csharp
SetColor((Color) 547);
```

由于没有符号对应的数值为 547，`SetColor` 方法将抛出 `ArgumentOutOfRangeException` 异常，指示哪个参数无效以及原因是什么。

# 第 15 章 枚举类型与位标志

> `IsDefined` 方法非常方便，但你必须谨慎使用。`IsDefined` 总是执行区分大小写的搜索，没有办法让它执行不区分大小写的搜索。其次，`IsDefined` 相当慢，因为它在内部使用了反射；如果你使用代码来检查每个可能的值，你的应用程序性能无疑会更好。第三，你真的应该在枚举类型本身定义在调用 `IsDefined` 的同一个程序集中时才使用它。假设 `Color` 枚举定义在一个程序集中，而 `SetColor` 方法定义在另一个程序集中。`SetColor` 方法已定义，如果颜色是白色、红色、绿色、蓝色或橙，`SetColor` 执行其工作。然而，如果未来 `Color` 枚举更改以包含紫色，`SetColor` 现在将允许紫色，这是从没有预期的，而且该方法可能会带有不可预测的结果执行。

最后，`System.Enum` 类型允许一个静态的 `TypeObject` 方法，它可以转换 `Byte`、`SByte` 的实例。

`IsDefined` 方法经常用于参数验证。枚举类型通常与标志配合。强烈建议对枚举类型应用 `Flags` 属性，如下：

## 位标志

程序员经常处理位标志集。如 `FileAttributes` 所示，使用枚举类型来表示可以组合的位是常见的。要判断文件是否隐藏，你会执行如下代码：

```csharp
String file = Assembly.GetEntry().Location;
FileAttributes attributes = File.GetAttributes(file);
Console.WriteLine("Is {0} hidden? {1}", file, (attributes & FileAttributes.Hidden) != 0);
```

> 注意 `Enum` 类定义了如下的 `HasFlag` 方法：

public Boolean HasFlag(Enum flag);

使用该方法，你可以这样调用 `Console.WriteLine` 行：

`Console.WriteLine("Is {0} hidden? {1}", attributes.HasFlag(FileAttributes.Hidden));`

然而，由于此原因，我建议避免 `HasFlag` 方法：因为它接受 `Enum` 参数，传递给它的任何值必须装箱，从而需要内存分配。

这里是演示更改文件属性为只读和隐藏的代码：

```csharp
File.SetAttributes(file, FileAttributes.ReadOnly | FileAttributes.Hidden);
```

枚举类型表示单个数值，而位标志表示一组位，其中某些开启的，另一些关闭的。在定义用于标识位标志的枚举类型时，你应该显式地为每个符号分配一个数值。通常，每个符号将开启一个单独的位。通常使用一个定义值为 0 的符号，你可以定义代表常用组合的符号（见下方的 `ReadWrite` 符号）。

```csharp
[Flags] // C# 编译器允许 "Flags" 或 "FlagsAttribute"
internal enum Actions {
    None = 0
    Read = 0x0001,
    Write = 0x0002,
    ReadWrite = Actions.Read | Actions.Write,
    Delete = 0x0004,
    Query = 0x0008,
    Sync = 0x0010
}
```

# 第 15 章 枚举类型与位标记 381

由于 `Actions` 是一个枚举类型，因此在处理位标记枚举类型时，你可以使用上一节中描述的所有方法。然而，如果其中一些函数的行为能略有不同就更好了。例如，假设你有以下代码：

```
Actions actions = Actions.Read | Actions.Delete; // 0x0005
Console.WriteLine(actions.ToString()); // "Read, Delete"
```

当调用 `ToString` 时，它会尝试将数值转换为其符号等效值。数值为 0x005，没有符号等效值。但是，`ToString` 方法检测到 `Actions` 类型上存在 `[Flags]` 特性，现在 `ToString` 不将该数值视为单个值，而是视为位标记集合。由于 0x0001 和 0x0004 位被设置，`ToString` 生成了以下字符串："Read, Delete"。如果你从 `Actions` 类型中移除 `[Flags]` 特性，`ToString` 将返回 "5"。

我在上一节中讨论了 `ToString`，并展示了它提供了三种格式化输出的方法："G"（通用）、"D"（十进制）和 "X"（十六进制）。当你使用通用格式格式化枚举类型的实例时，首先检查其是否应用了 `[Flags]` 特性。如果未应用此特性，将查找并返回与数值值匹配的符号。如果应用了 `[Flags]` 特性，`ToString` 的工作原理如下：

- 1. 获取枚举类型定义的数值集，并对数字按降序排序。
- 2. 将每个数值与枚举实例中的值进行位与（AND）操作，如果结果等于该数值，则将该数值关联的字符串追加到输出字符串中，并将位标记为已处理并关闭。重复此步骤，直到检查完所有数值，或者枚举实例的所有位位都已关闭。
- 3. 如果在检查完所有数值后，枚举实例仍不为 0，则枚举实例中的某些开启位不对应于任何定义的符号。在这种情况下，`ToString` 将枚举实例中的原始数字作为字符串返回。
- 4. 如果枚举实例的原始值不是 0，则返回带有逗号分隔符号集合的字符串。
- 5. 如果枚举实例的原始值是 0，且该枚举类型是一个具有对应值 0 的定义符号，则返回该符号。
- 6. 如果我们到达这一步，则返回 "0"。

如果你愿意，可以在不带 `[Flags]` 特性的情况下定义 `Actions`，并通过 "F" 格式仍然获得正确的字符串：

```
// [Flags] // 现在注释掉了
internal enum Actions {
    None = 0,
    Read = 0x0001,
    Write = 0x0002,
    Readwrite = Actions.Read | Actions.Write,
    Delete = 0x0004,
    Query = 0x0008,
    Sync = 0x0010
}
```

`Actions actions = Actions.Read | Actions.Delete; // 0x0005`

`Console.WriteLine(actions.ToString("F")); // "Read, Delete"`

如果数值具有无法映射到符号的位，返回的字符串将仅包含指示原始数值的十进制数字；字符串中不会出现任何符号。

注意，你在枚举类型中定义的符号可以定义一个值为 0x001F 的符号 `All`。例如，如果一个 `Actions` 类型的实例值为 0x001F，格式化该实例将产生一个包含 "All" 的字符串。其他符号字符串将不会出现。

到为止，我讨论了如何将数值转换为标志标记字符串。也可以通过调用 `Enum` 的静态 `Parse` 和 `TryParse` 方法将字符串转换为枚举。这里是某些演示如何使用这些方法的代码：

// 因为 Query 被定义为 8，'a' 初始化为 8。

`Actions a = (Actions)Enum.Parse(typeof(Actions), "Query", true);`

`Console.WriteLine(a.ToString()); // "Query"`

// 因为定义了 Query 和 Read，'a' 初始化为 9。

`Enum.TryParse<Actions>("Query, Read", false, out a);`

`Console.WriteLine(a.ToString()); // "Read, Query"`

// 创建一个值为 28 的 Actions 实例

`a = (Actions)Enum.Parse(typeof(Actions), "28", false);`

`Console.WriteLine(a.ToString()); // "Delete, Query, Sync"`

当调用 `Parse` 和 `TryParse` 时，内部会执行以下操作：

- 1. 移除字符串开头和结尾的所有空白字符。
- 2. 如果字符串的第一个字符是数字、加号 (+) 或减号 (-)，则假设字符串为数字，并返回一个数值值等于字符串转换后的数值等效值的枚举实例。
- 3. 将传递的字符串拆分为一组标记（用逗号分隔），并移除每个标记中的所有空白。
- 4. 将传递的字符串拆分为一组标记（用逗号分隔），并移除每个标记中的所有空白。
- 5. 如果在检查完所有数值后，枚举实例仍不为 0，则枚举实例中的某些开启位不对应于任何定义的符号。

# 第 15 章 枚举类型与位标记 383

在本章较早，我提到过你不能将方法定义为枚举类型。多年来，这一直让我感到遗憾，因为在很多时候，我希望能够为我的枚举类型提供方法。幸运的是，我现在可以使用 C# 较新的扩展方法功能（在第 8 章“方法”中讨论过）来模拟向枚举类型添加方法。

如果我想为 `FileAttributes` 添加一些方法，可以如下定义一个静态类：

```csharp
internal static class FileAttributesMethods {
    public static bool IsSet(FileAttributes flags, FileAttributes flagToTest) {
        if (flagToTest == 0)
            throw new ArgumentOutOf("flagToTest", "Value must not be 0");
        return (flags & flagToTest) != 0;
    }
    public static bool IsClear(FileAttributes flags, FileAttributes flagToTest) {
        if (flagToTest == 0)
            throw new ArgumentOutOf("flagToTest", "Value must not be 0");
        return !IsSet(flags, flagToTest);
    }
    public static bool AnyFlagsSet(FileAttributes flags, FileAttributes testFlags) {
        return ((flags & testFlags) != 0;
    }
}
```

```csharp
public static FileAttributes Set(this FileAttributes flags, FileAttributes setFlags) {
    return flags | setFlags;
}
```

```csharp
public static FileAttributes Clear(this FileAttributes flags, FileAttributes clearFlags) {
    return flags & ~clearFlags;
}
```

```csharp
public static void ForEach(this FileAttributes flags,
    Action<FileAttributes> processFlag) {
    if (processFlag == null) throw new ArgumentNullException("processFlag");
    for (UInt32 bit = 1; bit != 0; bit <<= 1) {
        UInt32 temp = (UInt32)flags & bit;
        if (temp != 0) processFlag((FileAttributes)temp);
    }
}
```

这里是演示调用这些方法的代码。正如你所见，代码看起来就像我在枚举类型上调用方法：

```csharp
FileAttributes fa = FileAttributes.System;
fa = fa.Set(FileAttributes.ReadOnly);
fa = fa.Clear(FileAttributes.System);
fa.ForEach(f => Console.WriteLine(f));
```

## 第 16 章
## 数组

在本章中：
- 初始化数组元素 ................................................................................................................. . . . . . . . . . . . . . . 388
- 数组类型转换 ................................................................................................................................. . . . . . . . . . . . . . . . . . . . . . . 390
- 所有数组都隐式派自 `System.Array` ................................................................. . 392
- 所有数组都隐式实现 `IEnumerable`、`ICollection` 和 `IList` ...................................................... 393
- 传递和返回数组 ................................................................................................................................... . . . . . . . . . . . . . . . . . 394
- 创建非零下界数组 ..................................................................................................... 395
- 数组访问性能 ........................................................................................................................................ . . . . . . . . . . . . . . . . . . . . . . 396
- 不安全的数组访问与固定大小数组 ................................................................................................................... 401

数组是允许你将多个项视为单个集合的机制。Microsoft .NET 通用语言运行时 (`CLR`) 支持单维数组、多维数组和锯齿数组（即数组的数组）。所有数组类型都隐式派自 `System.Array` 抽象类，而该类又派自 `System.Object`。这意味着数组是引用类型，分配在托管堆上，你的应用程序的变量或字段包含的是指向数组的引用，而不是数组本身。以下代码实现了这一点：

```csharp
Int32[] myIntegers; // 声明指向数组的引用
myIntegers = new Int32[100]; // 创建一个包含 100 个 Int32 的数组
```

在第一行中，`myIntegers` 是一个能够指向 `Int32` 单维数组的变量。初始情况下，`myIntegers` 将被设置为 `null`，因为我还没有分配数组。第二行代码分配了一个包含 100 个 `Int32` 值的数组；所有的 `Int32` 都被初始化为 0。由于数组是引用类型，持有这 100 个未装箱 `Int32` 所需的内存块分配在托管堆上。实际上，除了数组的元素外，数组对象占据的内存块还包含一个类型指针、同步块索引以及一些额外的开销成员。该数组内存块的地址被返回并保存在变量 `myIntegers` 中。

你也可以创建引用类型的数组：

```csharp
Control[] myControls; // 声明指向数组的引用
myControls = new Control[50]; // 创建一个包含 50 个 Control 引用的数组
```
