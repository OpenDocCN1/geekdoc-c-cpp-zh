

# 616 第 11 章：异常处理

异常。此外，由于异常通常在抛出它们的同一语句中构造，因此任何额外的异常数据都应该允许作为构造函数的一部分。（创建所有构造函数的明显例外是：当需要某些数据且构造函数必须绕过这些要求时。）

- 继承链应保持较浅（大约少于五层）。

当重新抛出一个与捕获到的异常不同的异常时，内部异常起着重要作用。例如，如果数据库调用抛出了 `System.Data.SqlClient.SqlException`，但数据访问层将其重新抛出 `DatabaseException`，那么接收 `SQLException`（或内部异常）的 `DatabaseException` 构造函数会将原始的 `SqlException` 保存在 `InnerException` 属性中。这样，如果需要有关原始异常的额外信息，开发者可以从 `InnerException` 属性检索异常（例如 `exception.InnerException`）。

### 准则
**避免使用深层异常层次结构。**
如果异常的处理方式与现有的 CLR 异常相同，则**不要创建**新的异常类型。请**抛出**现有的框架异常。
**应该创建**新的异常类型，用于通信唯一的程序错误，该错误无法通过现有的 CLR 异常通信，并且可以以不同于其他现有 CLR 异常类型的方式进行程序化处理。
**应该在**所有自定义异常类型上提供一个无参数构造函数。还应提供接收消息和内部异常的构造函数。
**应该以** "Exception" 后缀命名异常类。
**应该使**异常在运行时是可序列化的。
**考虑**为异常提供属性，以便通过程序化访问与异常相关的额外信息。

# 定义自定义异常

## 高级主题

### 可序列化异常
可序列化对象是运行时可以持久化到文件流的对象（例如），然后可以从流中恢复。对于异常，这种行为对于某些分布式通信技术可能是必要的。为了支持序列化，异常声明应该包含 `System.SerializableAttribute` 或实现 `Serializable`。此外，它们必须包含一个接收 `System.Runtime.SerializationInfo` 和 `System.Runtime.StreamingContext` 的构造函数。列表 11.5 显示了使用 `System.SerializableAttribute` 的示例。

列表 11.5：定义可序列化异常

```csharp
// 通过属性支持序列化
[Serializable]
class DatabaseException : Exception
{
    ...

    // 用于异常的反序列化
    public DatabaseException(
        SerializationInfo serializationInfo,
        StreamingContext context)
        : base(serializationInfo, context)
    {
        //...
    }
}
```

上述的 `DatabaseException` 示例演示了使异常可序列化的属性和构造函数要求。
直到 .NET Standard 2.0，.NET Core 中才有可用 `System.SerializableAttribute`。如果你正在编写将在包括 2.0 之前的 .NET Standard 版本在多个框架上编译的代码，请考虑定义自己的 `System.SerializableAttribute` 作为补丁（polyfill）。补丁是填充

# 第 11 章：异常处理

特定技术版本中空白的代码，从而添加该功能或至少为缺失的功能提供垫接层（shim）。

# 重新抛出包装过的异常

有时，在栈的较低级抛出的异常在较高层级捕获时可能不再具有意义。例如，考虑由于服务器系统空间不足而发生的 `System.IO.IOException`。捕获此类异常的客户端并不一定能理解为什么没有 I/O 活动的上下文。同样，一个地理坐标请求 API 出了 `System.UnauthorizedAccessException`（该异常与调用的 API 完全无关）。在第二个示例中，调用者没有上下文来理解 API 调用有什么关系。从调用 API 的代码角度来看，这些异常带来的困扰多于诊断的帮助。与其向客户端暴露异常，不如先捕获异常然后抛出一个不同的异常，例如 `InvalidOperationException`（甚至是自定义异常），用作通信系统处于无效状态的手段。在这些情况下，请务必设置包装异常的 `InnerException` 属性（通常通过构造函数调用，如 `new InvalidOperationException(string, Exception)`），以便让更接近调用框架的人员可以使用用于诊断目的的额外内容。

在考虑是否包装并重新抛出异常时，需要记住的一个细节是：原始堆栈跟踪（它提供了异常抛出位置的上下文）将被包装异常抛出位置的新堆栈跟踪替换（假设没有使用 `ExceptionDispatchInfo`）。幸运的是，当原始异常嵌入在包装异常中时，原始堆栈跟踪仍然可用。

最终，异常的预期接收者是编写错误调用你 API 代码的程序员。因此，你应该尽可能提供尽可能信息，以指示程序员哪里做错了，以及（可能更重要的是）如何修复。异常类型是通信机制的关键部分，因此你必须明智地选择它。

# 准则

- **考虑**将从低层抛出的特定异常包装在更合适的异常中，如果低层异常在较高层操作的上下文中不符合逻辑。
- **应该**在包装异常时指定内部异常。
- **应该**将开发者作为异常的受众，在可能的情况下识别问题以及解决问题的机制。

![](img/ffe0f34eac7523830420733690014d17_653_0.png)

# 初学者主题

# 检查和未检查的转换

正如我们在第 2 章高级主题中首次讨论过的那样，C# 提供了特殊的关键字来标记代码块，并向运行时指示如果目标数据类型太小而无法包含分配的数据时应该发生什么。默认情况下，如果目标数据类型无法包含分配的数据，数据将在赋值期间被截断。例如，请参见列表 11.6 和输出 11.1。

列表 11.6：整数值溢出

```csharp
using System;
public class Program{
    public static void Main()
    {
        // int.MaxValue 等于 2147483647
        int n = int.MaxValue;
        n = n + 1;
        Console.WriteLine(n);
    }
}
```

# 输出 11.1

```
-2147483648
```

列表 11.6 中的代码将值 -2147483648 写入控制台。然而，将代码放在 `checked` 块中或运行编译器时使用 `checked` 选项会导致运行时抛出 `System.OverflowException` 类型的异常。`checked` 块的语法使用 `checked` 关键字，如列表 11.7 输出 11.2 所示。如果计算仅涉及常量，则默认将进行检查。

# 列表 11.7：checked 块示例

```csharp
using System;
public class Program
{
    public static void Main()
    {
        checked
        {
            // int.MaxValue 等于 2147483647
            int n = int.MaxValue;
            n = n + 1;
            Console.WriteLine(n);
        }
    }
}
```

# 输出 11.2

```
未处理异常: OverflowException: 算术运算溢出。at Program.Main() in ...Program.cs:line 12
```

如输出 11.2 所示，如果在 `checked` 块内运行时发生了溢出赋值，则抛出异常。注意，输出 11.2 中的位置信息（Program.cs:line X）仅在调试编译（即使用编译器的 /Debug 选项进行编译）中出现。

> 9. 除了输出 11.2，如果安装了 .NET Framework 调试器，可能会弹对话提示用户向微软发送错误消息、检查解决方案或调试应用程序。

