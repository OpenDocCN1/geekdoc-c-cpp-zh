
被赋值为 11，这是赋值给 `Connected` 的值。（在这种情况下，不需要加枚举名称前缀，因为它出现在其作用域内。）`Disconnected` 的值为 12。

列表 9.31: 定义一个枚举类型

```sharp
enum ConnectionState : short
{
    Disconnected,
    Connecting = 10,
    Connected,
    Joined = Connected,
    Disconnecting
}
```

枚举始终有一个底层类型，该类型可以是除 `char` 以外的任何整数类型。事实上，枚举类型的性能与底层类型完全相同。默认情况下，底层的值类型是 `int`，但你可以使用继承语法指定不同的类型。例如，列表 9.15 使用了 `short` 而不是 `int`。为了保持一致性，枚举的语法模拟了继承的语法，但它并没有实际上创建继承关系。所有枚举的基类都是 `System.Enum`，它又派生自 `System.Value`。此外，这些枚举是密封的（sealed）；你不能从现有的枚举派生以更多成员。

## 指南

- 考虑使用默认的 32 位整数类型作为枚举的底层类型。只有在为了互操作性必须这样做时才使用较小的类型；只有当你创建一个带有超过 32 个标志的标志枚举（flags enum）¹时才使用较大的类型。

枚举本质上只是在底层类型上薄薄地覆盖了一层名称；没有任何机制可以将枚举变量的值限制为仅声明中命名的值。例如，由于可以将整数 42 强制转换为 `short`，因此也可以将整数 42 强制转换为 `ConnectionState` 类型，即使没有对应的 `ConnectionState` 枚举值。如果该值可以转换为底层类型，那么转换到枚举类型的转换也将是成功的。

10. 参见本章节后后部分“作为标志的枚举”节中的讨论。

这种奇特特征的优势是，可以在后续 API 发布中为枚举添加新值，而不会破坏早期的版本。此外，枚举值为已知值提供了名称，同时允许在运行时分配未知值。负担在于，开发者必须针对可能出现的未命名值进行防御性编码。例如，将 `ConnectionState.Disconnecting` 替换为 `default` 并期望 `default` 情况的唯一可能值是 `ConnectionState.Disconnect` 是不明智的。相反，你应该显式处理 `Disconnecting` 情况，并让 `default` 情况报告错误或表现无害。然而，如前面提到的，枚举与底层类型以及反向转换需要显式强制转换；它不是隐式转换。例如，如果方法的签名是 `void ReportState(ConnectionState state)`，则代码无法调用 `ReportState(10)`。这种异常仅发生在传递 0 时，因为 0 到任何枚举都有隐式转换。

虽然你可以在代码的后续版本中向枚举添加更多值，但你应该谨慎地这样做。在枚举中间插入枚举值将推后之后所有枚举值的值（例如，在 `Connected` 之前添加 `Flooded` 或 `Locked` 将改变 `Connected` 的值）。这将影响所有针对新版本重新编译的代码版本。然而，任何针对旧版本编译的代码将继续使用旧值，导致预期的值完全不同。除了在列表末尾插入枚举值外，避免更改枚举值的另一种种方法是显式地分配值。

## 第 9 章：介绍结构体和记录

## 指南

- 考虑向现有枚举添加新成员，但要记住兼容性风险。
- 避免创建代表“不完整”值集的枚举，例如产品版本号。
- 避免在枚举中创建“留供以后使用”的值。
- 避免创建包含单个值的枚举。
- 为简单枚举提供一个值为 0（none）的值，并知道在没有提供显式初始化时，0 将将是默认值。

## 高级主题

### 枚举之间的类型兼容性

C# 也不支持两个不同枚举数组之间的直接强制转换。然而，CLR（公共语言运行时）支持转换，只要这两个枚举共享相同的底层类型。为了绕过 C# 的这一限制，技巧是首先强制转换为 `System.Array`，如列表 9.32 结尾所示。

列表 9.32: 枚举数组之间的强制转换

```sharp
enum ConnectionState1
{
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
enum ConnectionState2
{
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
public class Program
{
    public static void Main()
    {
        ConnectionState1[] states = (ConnectionState1[])(Array)new ConnectionState2[42];
    }
}
```

此示例利用了 CLR 的赋值兼容性概念比 C# 的概念更宽松的特性。（其他非法转换也适用同样的技巧，例如从 `int[]` 到 `uint[]`）。然而，你应该谨慎地使用这种方法，因为没有 C# 规范要求这种行为在不同的 CLR 实现中生效。

## 枚举与字符串之间的转换

枚举相关的便利性之一是 `ToString()` 方法（由 `System.Console.WriteLine()` 等方法调用）会像列表 9.33 所示输出枚举值的标识符：

列表 9.33: 将枚举标识符写入缓冲区

```sharp
System.Diagnostics.Trace.WriteLine(
  "The connection is currently {ConnectionState.Disconnecting}");
```

之前的代码将输出 9.3 中的文本写入缓冲区。

## 输出 9.3

```
The connection is currently Disconnecting.
```

从字符串转换为枚举并不那么明显，因为它涉及到 `System.Enum` 基类。列表 9.34 提供了如何做的示例。

列表 9.34: 使用 Enum.TryParse 将字符串转换为枚举

```sharp
System.Diagnostics.Trace priority;
if(Enum.TryParse("Idle", out priority))
{
  System.Diagnostics.Trace.WriteLine(priority);
}
```

此示例描述了一种编译时的表示，字面量见第 18 章。`TryParse<T>` 方法使用了泛型，产生了列表 9 所示的等效语法。

## 枚举

无论代码使用 "Parse" 还是 "TryParse" 方法，关于字符串转换为枚举的关键警告在于强制转换是非优的，除非成功是肯定的。因此，开发者应该在消息未暴露给用户的情况下使用此类类型。

## 指南

- 避免枚举/字符串转换，除非字符串必须本地化。

很多时候，开发者不仅希望枚举值是唯一的，还希望能够表示组合。例如，考虑 `System.IO.FileAttributes`。这个枚举在列表 9.35 所示指示了文件的各种属性：只读、隐藏等。与 `ConnectionState` 属性（每个枚举值都是互斥）不同，`FileAttributes` 枚举值可以并且用于组合：一个文件可以是只读又是隐藏的。为了支持这种行为，每个枚举成员的值是一个唯一的位。

列表 9.35: 使用标志（Flags）枚举

```sharp
[Flags]
public enum {
    None = 0,                          // 000000000000
    ReadOnly = 1 << 0,                 // 000000000001
    Hidden = 1 << 1,                   // 000000000010
    System = 1 << 2,                  // 000000000100
    Directory = 1 << 4,               // 000000010000
    Archive = 1 << 5,                 // 000000100000
    Device = 1 << 6,                  // 000010000000
    Normal = 1 << 7,                  // 000100000000
    Temporary = 1 << 8,               // 001000000000
    SparseFile = 1 << 9,               // 010000000000
    ReparsePoint = 1 << 10,          // 100000000000
    Compressed = 1 << 11,            // 110000000000
    Offline = 1 << 12,               // 100000000000
}
```
