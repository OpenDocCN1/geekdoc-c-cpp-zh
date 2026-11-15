

命名参数允许为特性分配数据，而无需为每种可能指定哪些特性属性、哪些未指定的组合提供构造函数。由于特性的许多属性可能是可选的，这在许多情况下是一个有用的构造。

## BEGINNER TOPIC

### FlagsAttribute

第 8 章介绍了枚举，并包含了关于 FlagsAttribute 的高级主题。这是一个框架定义的特性，用于表示标志类型值的枚举。以下是作为初学者主题的类似文本，从清单 17.21 中显示的示例代码开始。

### LISTING 17.21: Using FlagsAttribute

```
// FileAttributes defined in System.IO.

[Flags] // Decorating an enum with FlagsAttribute.
public enum FileAttributes
{
    ReadOnly = 1<<0, // 0000000000000001
    Hidden = 1<<1, // 0000000000000010
    // ...
}
```

```
using System;
using System.Diagnostics;
using System.IO;

class Program
{
    public static void Main()
    {
        // ...

        string fileName = @"enumtest.txt";
        FileInfo file = new FileInfo(fileName);

        file.Attributes = FileAttributes.Hidden |
            FileAttributes.ReadOnly;

        Console.WriteLine("\"(0)\" outputs as \"{1}\"",
            file.Attributes.ToString().Replace(", ", " | "),
            file.Attributes);
    FileAttributes attributes =
        (FileAttributes)Enum.Parse(typeof(FileAttributes),
        file.Attributes.ToString());
    Console.WriteLine(attributes);
    // ...
    }
}
```

### Output 17.6:

```
"ReadOnly | Hidden" outputs as "ReadOnly, Hidden"
```

该标志记录枚举值可以组合。此外，它更改了 ToString() 和 Parse() 方法的行为。例如，对装饰有 FlagsAttribute 的枚举调用 ToString() 会输出每个已设置的枚举标志的字符串。在清单 17.21 中，FileAttributes.ToString() 返回 "ReadOnly, Hidden"，而不是如果没有 FlagsAttribute 标志时会返回的 3。如果两个枚举值相同，ToString() 调用将返回第一个。但是，如前所述，应谨慎使用此功能，因为它不可本地化。

将字符串值解析为枚举也可行，前提是每个枚举值标识符都用逗号分隔。

需要注意的是，FlagsAttribute 不会自动分配唯一的标志值或检查它们是否具有唯一值。每个枚举项的值仍必须显式分配。

## Predefined Attributes

AttributeUsageAttribute 特性具有一种您在迄今在本书中创建的自定义特性中未见过的特殊特征。此特性会影响编译器的行为，导致编译器有时会报告错误。与您之前为检索 CommandLineRequiredAttribute 和 CommandLineSwitchAliasAttribute 编写的反射代码不同，AttributeUsageAttribute 没有运行时代码；相反，它具有内置的编译器支持。

AttributeUsageAttribute 是一个预定义特性。此类特性不仅为其装饰的构造提供额外的元数据，而且运行时和编译器的行为也会有所不同，以便支持这些特性的功能。AttributeUsageAttribute、FlagsAttribute、ObsoleteAttribute 和 ConditionalAttribute 等特性是预定义特性的示例。它们包含只有 CLI 提供商或自定义实现才能提供的特殊行为，因为不存在用于其他非自定义特性的扩展点。相比之下，自定义特性完全是被动的。清单 17.21 包含几个预定义特性；第 18 章包含更多。

## System.ConditionalAttribute

在单个程序集中，System.Diagnostics.ConditionalAttribute 特性的行为有点像 #if/#endif 预处理器标识符。但是，System.Diagnostics.ConditionalAttribute 不是从程序集中消除 CIL 代码，而是会可选地导致调用表现得像 no-op（不执行任何操作的指令）。清单 17.22 演示了该概念，输出 17.7 显示了结果。

### LISTING 17.22: Using Reflection with Generic Types

```
#define CONDITION_A

using System;
using System.Diagnostics;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Begin...");
        MethodA();
        MethodB();
        Console.WriteLine("End...");
    }

    [Conditional("CONDITION_A")]
    static void MethodA()
    {
        Console.WriteLine("MethodA() executing...");
    }

    [Conditional("CONDITION_B")]
    static void MethodB()
    {
        Console.WriteLine("MethodB() executing...");
    }
}
```

### OUTPUT 17.7:

```
Begin...
MethodA() executing...
End...
```

此示例定义了 CONDITION_A，因此 MethodA() 正常执行。但是，CONDITION_B 未通过 #define 或使用 csc.exe /Define 选项定义。结果，从此程序集内对 Program.MethodB() 的所有调用都不会执行任何操作，甚至不会出现在代码中。

从功能上讲，ConditionalAttribute 类似于在方法调用周围放置 #if/#endif。但是，语法更简洁，因为开发人员通过将 ConditionalAttribute 特性添加到目标方法来创建该效果，而无需对调用者本身进行任何更改。

请注意，C# 编译器在编译期间会注意到被调用方法上的特性，并且假设预处理器标识符存在，它会消除对该方法的任何调用。还请注意，ConditionalAttribute 不会影响目标方法本身的已编译 CIL 代码（除了添加特性元数据之外）。相反，它在编译期间通过删除调用来影响调用站点。这进一步区分了跨程序集调用时的 ConditionalAttribute 与 #if/#endif。由于装饰的方法仍然被编译并包含在目标程序集中，因此是否调用方法的决定不是基于被调用程序集中的预处理器标识符，而是基于调用者程序集。换句话说，如果您创建一个定义 CONDITION_B 的第二个程序集，则从第二个程序集对 Program.MethodB() 的任何调用都将执行。这在许多跟踪和测试场景中是一个有用的特性。事实上，对 System.Diagnostics.Trace 和 System.Diagnostics.Debug 的调用利用 ConditionalAttribute 在 TRACE 和 DEBUG 预处理器标识符上使用此特性。

由于在未定义预处理器标识符时方法不会执行，因此 ConditionalAttribute 不可用于包含 out 参数或指定非 void 返回值的方法。这样做会导致编译时错误。这很合理，因为装饰方法中的代码可能根本不会执行，因此不知道应该向调用者返回什么。同样，属性不能装饰 ConditionalAttribute。ConditionalAttribute 的 AttributeUsage（参见本章前面的 System.AttributeUsageAttribute 节）为 AttributeTargets.Class（从 .NET 2.0 开始）和 AttributeTargets.Method。这允许该特性用于方法或类。但是，此类用法是特殊的，因为 ConditionalAttribute 仅允许用于 System.Attribute 派生类。

当 ConditionalAttribute 装饰自定义特性时（这是 .NET 2.0 引入的功能），只有在调用程序集中定义了条件字符串，后者才能通过反射检索。如果没有这样的条件字符串，查找自定义特性的反射将无法找到它。

## System.ObsoleteAttribute

如前所述，预定义特性会影响编译器和/或运行时的行为。ObsoleteAttribute 提供了特性影响编译器行为的另一个示例。ObsoleteAttribute 的目的是帮助代码版本控制，为向调用者指示特定成员或类型不再是最新提供了一种手段。清单 17.23 是 ObsoleteAttribute 用法的示例。如输出 17.8 所示，任何编译调用标记有 ObsoleteAttribute 的成员的代码的调用者都会导致编译时警告，可选地导致错误。

### LISTING 17.23: Using ObsoleteAttribute

```
class Program
{
    public static void Main()
    {
        ObsoleteMethod();
```

