

> **注意**
枚举也可以用作布尔值的更具可读性的替代方案。例如，像 `SetState(true)` 这样的方法调用，其可读性不如 `SetState(DeviceState.On)`。

使用枚举值时，需要在其前面加上枚举名称。例如，若要使用 `Connected` 值，你应使用语法 `ConnectionState.Connected`。请勿将枚举类型名作为值名的一部分，以避免出现诸如 `ConnectionState.ConnectionStateConnected` 这样的冗余。按照惯例，枚举名称本身应为单数（除非枚举是位标志，这一点将在后面讨论）。也就是说，命名规范应为 `ConnectionState`，而不是 `ConnectionStates`。

枚举值实际上只是整数常量。默认情况下，第一个枚举值被赋予 0，随后的每一项递增 1。但是，你可以为枚举分配显式值，如清单 9.11 所示。

## 清单 9.11：定义枚举类型

```
enum ConnectionState : short
{
    Disconnected,
    Connecting = 10,
    Connected,
    Joined = Connected,
    Disconnecting
}
```

在这段代码中，`Disconnected` 的默认值为 0，而 `Connecting` 被显式分配为 10；因此，`Connected` 将被分配为 11。`Joined` 被分配为 11，即 `Connected` 的值。（在这种情况下，你不需要在 `Connected` 前加上枚举名称，因为它出现在其作用域内。）`Disconnecting` 为 12。

枚举始终具有基础类型，它可以是除 `char` 以外的任何整数类型。事实上，枚举类型的性能与基础类型完全相同。默认情况下，基础值类型为 `int`，但你可以使用继承类型语法指定其他类型。例如，清单 9.11 没有使用 `int`，而是使用了 `short`。为了保持一致性，枚举的语法模仿了继承的语法，但这实际上并不建立继承关系。所有枚举的基类是 System.Enum，而 System.Enum 又派生自 System.ValueType。此外，这些类是密封的；你不能从现有的枚举类型派生以添加更多成员。

![](img/ef6a8a417630b222bfb3f3b949facff0_437_0.png)

枚举本质上只是在基础类型上叠加的一组名称；没有机制将枚举类型变量的值限制在声明中命名的值范围内。例如，由于可以将整数 42 强制转换为 short，因此也可以将整数 42 强制转换为 ConnectionState 类型，尽管没有对应的 ConnectionState 枚举值。如果值可以转换为基础类型，则到枚举类型的转换也会成功。

这一独特特性的优势在于，枚举可以在后续 API 版本中添加新值，而不会破坏早期版本。此外，枚举值为已知值提供了名称，同时仍允许在运行时分配未知值。负担在于开发人员必须针对未命名值的可能性进行防御性编程。例如，将 `case ConnectionState.Disconnecting` 替换为 `default` 并期望 `default` 情况中唯一可能的值是 `ConnectionState.Disconnecting` 是不明智的。相反，你应该显式处理 `Disconnecting` 情况，而 `default` 情况应报告错误或保持无害行为。然而，如前所述，枚举与其基础类型之间（以及反之）的转换需要显式强制转换；它不是隐式转换。例如，如果方法签名为 `void ReportState(ConnectionState state)`，代码不能调用 `ReportState(10)`。唯一的例外是传递 0，因为存在从 0 到任何枚举的隐式转换。

虽然你可以在代码的后续版本中为枚举添加更多值，但应谨慎操作。在枚举中间插入一个枚举值会提升后续所有枚举值的值（例如，在 `Connected` 之前添加 `Flooded` 或 `Locked` 会改变 `Connected` 的值）。这将影响所有针对新版本重新编译的代码版本。但是，针对旧版本编译的任何代码将继续使用旧值，使得预期的值完全不同。除了在列表末尾插入枚举值外，避免更改枚举值的一种方法是显式分配值。

### 准则

- **考虑** 向现有枚举添加新成员，但请记住兼容性的风险。
- **避免** 创建表示“不完整”值集的枚举，例如产品版本号。
- **避免** 在枚举中创建“保留供将来使用”的值。
- **避免** 包含单个值的枚举。
- **应** 为简单枚举提供值为 0（无）的值，知道在未提供显式初始化时，0 将是默认值。

枚举与其他值类型略有不同，因为它们先派生自 `System.Enum`，然后才派生自 `System.ValueType`。

### 枚举之间的类型兼容性

C# 也不支持在两种不同枚举的数组之间进行直接强制转换。但是，CLR 支持，前提是两个枚举共享相同的基础类型。为了绕过 C# 的这一限制，技巧是先强制转换为 `System.Array`，如清单 9.12 末尾所示。

## 清单 9.12：在枚举数组之间进行强制转换

```
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

class Program
{
static void Main()
{
ConnectionState1[] states =
(ConnectionState1[])(Array)new ConnectionState2[42];
}
}
```

此示例利用了这样一个事实：CLR 的赋值兼容性概念比 C# 的概念更宽松。（其他非法转换，如 `int[ ]` 到 `uint[ ]`，也可以采用相同的技巧。）然而，请谨慎使用这种方法，因为没有 C# 规范要求这种行为在不同的 CLR 实现中必须有效。

### 在枚举和字符串之间转换

枚举的便利之一在于，`ToString()` 方法（由 `System.Console.WriteLine()` 等方法调用）会写出枚举值标识符：

```
System.Diagnostics.Trace.WriteLine(
$"The connection is currently { ConnectionState.Disconnecting }");
```

上述代码会将文本（如输出 9.3 所示）写入跟踪缓冲区。

### 输出 9.3

> The connection is currently Disconnecting.

从字符串到枚举的转换实现起来要复杂一些，因为它涉及 System.Enum 基类上的静态方法。清单 9.13 提供了一个不使用泛型（参见第 12 章）的示例，输出 9.4 显示了结果。

## 清单 9.13：使用 Enum.Parse() 将字符串转换为枚举

```csharp
ThreadPriorityLevel priority = (ThreadPriorityLevel)Enum.Parse(
    typeof(ThreadPriorityLevel), "Idle");
Console.WriteLine(priority);
```

### 输出 9.4

Idle

在这段代码中，`Enum.Parse()` 的第一个参数是类型，你使用 `typeof()` 关键字指定它。此示例展示了在编译时识别类型的一种方式，类似于类型值的字面量（参见第 18 章）。

在 Microsoft .NET Framework 4 之前，没有 `TryParse()` 方法，因此针对早期版本编写的代码如果字符串可能不对应于枚举值标识符，则需要包含适当的异常处理。Microsoft .NET Framework 4 的 `TryParse<T>()` 方法使用泛型，但类型参数可以被推断，从而实现清单 9.14 所示的到枚举的转换行为。

## 清单 9.14：使用 Enum.TryParse<T>() 将字符串转换为枚举

```csharp
System.Diagnostics.ThreadPriorityLevel priority;
if(Enum.TryParse("Idle", out priority))
{
    Console.WriteLine(priority);
}
```

如果字符串可能无法成功转换，此技术消除了使用异常处理的需要。相反，代码可以检查从 `TryParse<T>()` 调用返回的布尔结果。

无论代码使用“Parse”还是“TryParse”方法，从字符串转换为枚举的关键注意事项是，这种强制转换不具有本地化特性。因此，开发人员应仅将此类强制转换用于未向用户展示的消息（假设本地化是要求）。

### 准则

- **避免** 在字符串必须本地化为用户语言的情况下进行直接的枚举/字符串转换。

