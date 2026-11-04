
```csharp
var endTime2 = startTime + elapsed;
Console.WriteLine(endTime == endTime2);
```

从 TimeSpan 值可以获得不同的度量，包括该值的组成部分（毫秒、秒、分钟、小时和天），以及总计。两者 的示例在下一个示例中显示：

```csharp
Console.WriteLine(elapsed.Hours + ":" + elapsed.Minutes);
Console.WriteLine(elapsed.TotalSeconds);
```

可以通过使用格式字符串获得更美观的格式。ToString 方法产生的默认结果会写下小时、分钟和秒，每个都用两位数字表示并以冒号分隔。如果 TimeSpan 值存储了非平凡的天数或毫秒值，也会打印出来。例如：

```csharp
42.12:34:56.789  // 42 days, 12 hours, 34 minutes, 56 seconds, 789 milliseconds
```

Parse 和 TryParse 方法可用，以及它们的 Exact 变体，完全类似于 DateTime 上的静态方法。

### 性能测量

> 某些人热衷于各种性能测量。其他人则对在应用程序或库的性能尚未出现红旗（尚未）的情况下过度进行此类实践持怀疑态度。无论如何，如果你必须进行此类测量，请以正确的方式进行。减去 DateTime 值由于精度有限而不足。使用 Stopwatch 类才是正确的方法，正如我们在第 27 章“Diagnostics and Instrumentation”中讨论 System.Diagnostics 命名空间时将会看到的那样。

## 使用 DateTime 值的算术运算

在关于 TimeSpan 的讨论中，你了解到两个 DateTime 值之间的差值会产生一个 TimeSpan。另一方面，将 DateTime 和 TimeSpan 相加，则会返回另一个 DateTime 值。为了方便，DateTime 结构体还提供了一系列 Add 方法，避免了首先创建 TimeSpan 值的需要：

```csharp
var hundredDaysFestival = DateTime.Now.AddDays(100);
```

提供了一个 Subtract 方法用于从 DateTime 值中减去 TimeSpan，主要用于不支持运算符重载的语言。这显示了良好的 API 设计如何适应可能缺少 C# 中存在的某些便利性的语言。事实上，运算符重载支持不在通用语言规范（CLS）合规性规则列表中。

## DateTimeOffset

在掌握了 DateTime 和 TimeSpan 之后，我们可以思考将两者结合成单个值意味着什么。这正是 DateTimeOffset 所做的，作为克服 DateTime 对本地时间与 UTC 时间的简单处理方式所存在某些问题的方法，如 Kind 属性所示。

DateTimeOffset 包含一个 DateTime 和一个类型为 TimeSpan 的偏移量。偏移量用于表示 DateTime 值与 UTC 时间之间的差异。这与使用时区的概念并不完全相同，因为后者还具有夏令时和调整规则的概念。

如今，出于各种优势，使用 DateTimeOffset 比使用普通的旧 DateTime 更受推荐。一个很大的优势是该类型表示的日期/时间值明确定义了一个时间点。我们不会进一步详细说明何时适合使用 DateTimeOffset 而非 DateTime。相反，请参考 MSDN 了解该主题的更多文档。从使用角度来看，这两个结构体具有相似的公共契约，因此你应该立即感到自在。

## GUID 值

在 COM 时代，接口的标识和映射由唯一的标识号驱动，称为 GUID。虽然这只是全局唯一标识符的众多用途之一，但 COM 绝对是立刻浮现在脑海中的那个。

为了 COM 互操作以及其他用途，.NET Framework 有一个结构体来表示此类标识符：System.Guid。GUID 基本上只是一个“非常随机”的 128 位整数，具有全局唯一性属性。在此上下文中，全局意味着无论何时何地生成，两个生成的 GUID 相同的可能性非常低。因此，安全地为某些用途生成 GUID（例如标识 COM 接口）并假设它不会与第三方生成的此类标识符冲突。

虽然 GUID 可用于 COM 相关编程以外的其他目的，但应问一下全局唯一属性是否对所解决的问题是必要的。如果不是这样，那么一个更小的，例如 32 位的标识符可能是更好的选择。它不仅在存储方面更便宜，通常还可以以增量的方式生成这些数字，使标识符更容易记忆。例如，收银员会很高兴西红柿的标识符是 42 而不是 [5b8a5333-1bfd-494a-b73a-8812d254d89b]。

可以通过多种方式从已知值创建 GUID，使用构造函数以及 Parse 和 TryParse 方法。由于 GUID 使用了不同的文本表示形式，因此还提供了一组 Exact 解析方法。刚才显示的那些 GUID 字符串形式之一可以很容易地用于创建新的 Guid 值，如下所示：

```csharp
var myId = new Guid("5b8a5333-1bfd-494a-b73a-8812d254d89b");
```

这里是否使用大括号包围 GUID 无关紧要，大写和小写也不影响结果。GUID 看似奇怪的由五个不等段组成的格式是由于标识符的典型内部表示，这从其他构造函数重载中也很明显：

```csharp
public Guid(int a, short b, short c, byte[] d);
public Guid(int a, short b, short c, byte d, byte e, byte f, byte g, byte h, byte i, byte j, byte k);
public Guid(uint a, ushort b, ushort c, byte d, byte e, byte f, byte g, byte h, byte i, byte j, byte k);
```

我们不会详细介绍 GUID 背后的历史及其各种字节级表示。相反，请参考 Win32 和 COM 文档（如果你感兴趣的话）。

在很多情况下，你一开始并没有预定义的 GUID 值，需要即时生成一个。这就是 NewGuid 静态方法可以派上用场的地方，它内部只是简单地使用 CoCreateGuid COM API 生成此类新标识符：

```csharp
Console.WriteLine(Guid.NewGuid());
```

如果需要特定的文本输出，可以使用 ToString 方法传入格式字符串来影响输出的形状。我们在讨论处理文本时，特别是“Formatting Text”部分，会单独讨论格式字符串的概念。

### 让系统完成其工作

有些方法似乎是纯粹的魔法。Guid.NewGuid 似乎绝对是极致的魔法，提供关于提供全局唯一值的保证（失败的概率非常、非常低）。

篡改此类 API 的结果可能不是一个好主意，因为你可能会破坏该函数的保证。有真实的故事，人们使用 GUID 创建 API 来生成他们认为唯一的标识符。结果发现这些人只取了 GUID 的 128 位中的一部分，认为 GUID 的一部分仍具有与整个 GUID 相同的唯一性保证。因为生成的 GUID 值中的某些部分源自机器的身份，你可能会选择一个不具有全局唯一性属性的部分。注意！

在很多场景中，生成新的 GUID 不是运行时的事情，而必须在开发时完成（例如，将 .NET 程序集及其类型暴露给 COM 世界）。虽然 Guid.NewGuid 方法可用于此目的，但随各种 SDK 提供的工具也可以使用。特别是 uuidgen.exe 工具非常方便。在 Visual Studio 内部，一个基于 UI 的版本（称为 guidgen.exe）可通过 Tools 菜单的 Create GUID 条目获得，如图 26.16 所示。
