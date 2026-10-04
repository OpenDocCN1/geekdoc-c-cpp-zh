

```csharp
enum FileAttributes {
    Device = 0x00040,
    Normal = 0x00080,
    Temporary = 0x00100,
    SparseFile = 0x00200,
    ReparsePoint = 0x00040,
    Compressed = 0x00080,
    Offline = 0x00100,
    NotContentIndexed = 0x02000,
    Encrypted = 0x00400,
    IntegrityStream = 0x00800,
    NoScrubData = 0x02000
}
```

要确定一个文件是否被隐藏，你可以执行如下代码。

```csharp
String file = Assembly.GetEntryAssembly().Location;
FileAttributes attributes = File.GetAttributes(file);
Console.WriteLine("Is {0} hidden? {1}", attributes & FileAttributes.Hidden != 0);
```

![](img/0ce3b788d061e3d3095fa554b1a34adf_393_0.png)

> 注意 枚举类定义了如下所示的 HasFlag() 方法。
`public Boolean HasFlag(Enum flag);`

使用此方法，你可以重写对 Console.WriteLine("Is {0} hidden? {1}", file, attributes.HasFlag(FileAttributes.Hidden)) 调用。

然而，我建议你避免使用 HasFlag 方法，原因是因为它接收一个 Enum 类型的参数，传递给它的任何值都必须经过装箱（boxed），这需要内存分配。

```csharp
File.SetAttributes(file, FileAttributes.ReadOnly | FileAttributes.Hidden);
```

正如 FileAttributes 所示，使用枚举类型来表示可以组合的标志位集是常见的。虽然枚举类型和标志（flags）相似，但它们的语义并不完全相同。例如，枚举类型表示单个数值，而标志表示一组位，其中一些位是开启的，另一些位是关闭的。

在定义用于标识文件标志的枚举类型时，你当然应该显式地为每个符号分配一个数值。通常，每个符号将有一个位被开启。使用一个名为 None 且值为 0 的符号也是常见的，你还可以定义代表常用组合的符号（参见下方的 ReadWrite 符号）。强烈建议对枚举类型应用 System.FlagsAttribute 自定义类型，如下所示：

```csharp
[Flags] // C# 编译器允许使用 "Flags" 或 "FlagsAttribute"
internal enum Actions {
    None = 0,
    Read = 0x0001,
```

## 第三部分 基础类型 **

```csharp
    Write = 0x0002;
    ReadWrite = Actions.Read | Actions.Write;
    Delete = 0x0004;
    Query = 0x0008;
    Sync = 0x0010;
}
```

由于 Actions 是一个枚举类型，在处理位标志标志枚举类型时，你可以使用上一节中描述的所有方法。但是，如果其中某些函数的行为稍微不同一点就更好了。例如，假设你有如下代码：

```csharp
Actions actions = Actions.Read | Actions.Delete; // 0x0005
Console.WriteLine(actions.ToString());   // "Read, Delete"
```

当调用 ToString 时，它会尝试将数值转换为其符号等效值。数值为 0x0005，没有符号等效值。然而，ToString 方法检测到 Actions 类型上存在 [Flags] 属性，ToString 现在将该数值视为一个单一值，而是视为一组位标志。因为 0x0001 和 0x0004 位被设置了，ToString 生成了字符串："Read, Delete"。如果你从 Actions 类型中移除 [Flags] 属性，ToString 将返回 "5"。

我在上一节中讨论了 ToString 方法，并展示了它提供了三种格式化输出的方式："G"（通用）、"D"（十进制）和 "X"（十六进制）。当你使用通用格式对枚举类型进行格式化时，会首先检查该类型是否应用了 [Flags] 属性。如果未应用此属性，将查找并返回与数值匹配的符号。如果应用了 [Flags] 属性，ToString 的工作原理如下：

- 1. 定义枚举类型定义的数值集，并将数字按降序排列。
- 2. 将每个数值与枚举实例中的值进行位与（AND）运算，如果结果等于该数值，则将与数值相关的字符串追加到输出字符串中，并将这些位视为已处理并将其关闭。重复此步骤，直到所有数值都检查完毕，或者枚举实例的所有位都已关闭。
- 3. 如果在检查所有数值后，枚举实例仍不为 0，则枚举实例开启了与任何定义符号都不对应的符号。在这种情况下，ToString 返回枚举实例中原始数字的字符串形式。
- 4. 如果枚举实例的原始值不为 0 且该枚举类型定义了符号，则返回用逗号分隔的符号集。
- 5. 如果枚举实例的原始值为 0 且枚举类型定义了对应值为 0 的符号，则返回该符号。
- 6. 如果我们到达这一步，枚举实例的原始值不为 0 且枚举类型定义了对应值为 0 的符号，则返回该符号。

如果你有偏好，在没有 [Flags] 属性的枚举类型仍然获得该字符串：

```csharp
[Flags] // C# 编译器允许使用 "Flags" 或 "FlagsAttribute"
internal enum Actions {
    None = 0,
    Read = 0x0001,
    Write = 0x0002;
    ReadWrite = Actions.Read | Actions.Write;
    Delete = 0x0004;
    Query = 0x0008;
    Sync = 0x0010;
}
```

