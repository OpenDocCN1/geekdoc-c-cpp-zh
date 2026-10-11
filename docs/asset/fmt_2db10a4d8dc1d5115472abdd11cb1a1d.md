
此示例定义了 `CONDITION_A`，因此 `MethodA()` 正常执行。
然而，`CONDITION_B` 没有通过 `#define` 定义，也没有通过 `csc.exe /Define` 选项定义。因此，程序集内部对 `Program.MethodB()` 的所有调用将都不执行。

功能上，`ConditionalAttribute` 类似于在方法调用周围放置 `#if/#endif`。然而，语法更简洁，因为开发者通过向目标方法添加 `ConditionalAttribute` 来实现效果，而无需对调用者本身进行任何更改。

C# 编译器在编译期间会注意到调用方法上的属性；假设前置标识符存在，它将消除任何对该方法的调用。然而，`ConditionalAttribute` 不会影响目标方法本身的编译 CIL 代码（除了添加属性元数据之外）。相反，它在编译期间通过移除调用来影响调用点。这进一步区分了跨程序集调用时 `ConditionalAttribute` 与 `#if/#endif`。因为被装饰的方法仍然被编译并包含在目标程序集中，调用方法的判断基于调用程序集中的预处理器标识符，而不是调用者程序集。也就是说，如果你创建一个定义了 `CONDITION_B` 的第二个程序集，则从第二个程序集对 `Program MethodB()` 的任何调用都将执行。这是许多跟踪和测试场景中非常有用的特性。事实上，对 `System.Diagnostics.Trace` 和 `System.Diagnostics.Debug` 的调用在开启 `ConditionalAttributes` 时使用了这一特性。

由于预处理器标识符未定义时方法不会执行，因此 `ConditionalAttribute` 可能用于包含 `out` 参数或指定 `void` 外返回类型的方法。这样做会导致编译时错误。这是合理的，因为装饰方法内的任何代码都将执行，因此无法确定向调用者返回什么。同样，属性不能装饰有 `ConditionalAttribute`。`ConditionalAttribute` 的 `AttributeUsage`（参见本章前面的“SystemAttributeUsageAttribute”节）被装饰为 `AttributeTargets.Class` 和 `AttributeTargets.Method`，这允许属性分别用在方法或类上。然而，类的用法是特殊的，因为 `ConditionalAttribute` 仅允许用于派生自 `System.Attribute` 的类。

当 `ConditionalAttribute` 装饰自定义属性时，只有当条件字符串在调用程序集中定义时，才能通过反射获取该属性。如果没有此类条件字符串，查找自定义属性的反射将无法找到它。

## System.ObsoleteAttribute

如前所述，预定义属性会影响编译器和/或运行时的行为。`ObsoleteAttribute` 提供了另一个影响编译器行为的属性示例。它的目的是通过提供指示成员或类型已过时的手段来帮助代码版本。列表 18.25 提供了 `ObsoleteAttribute` 使用的示例。如输出 18.9 所示，任何调用标记为 `ObsoleteAttribute` 成员的代码的调用者都将导致编译警告，并可选地导致错误。

### 列表 18.25：使用 ObsoleteAttribute

```csharp
public class Program
{
    public static void Main()
    {
        ObsoleteMethod();
    }
    [Obsolete]
    public static void ObsoleteMethod()
    {
    }
}
```

### 输出 18.9

```
c:\SampleCode\ObsoleteAttributeTest.cs(24,17): warning CS0612:
Program.ObsoleteMethod() is obsolete
```

在这种情况下，`ObsoleteAttribute` 仅显示警告。然而，该属性还有两个额外的构造函数。第一个构造函数 `ObsoleteAttribute(string message)` 将额外的消息参数附加到编译器的过时消息之后。此消息的最佳实践是提供关于什么替代过时代码的指导。第二个构造函数是一个 `bool` 错误参数，强制将警告记录为错误。

`ObsoleteAttribute` 允许第三方通知开发者已弃用的 API。警告（而非错误）允许原始 API 继续工作，直到开发者能够更新调用代码。

## 泛型属性

从 C# 11.0 开始，C# 支持泛型属性。例如，考虑列表 18.26 所示的自定义属性 `ExpectedException<T>`。

### 列表 18.26：泛型属性

```csharp
public class SampleTests{
    [ExpectedException(DivideByZeroException)]
    public static void ThrowDivideByZeroTest(){
        var result = 1/"".Length;
    }
}

[AttributeUsage(AttributeTargets.Method)]
public class ExpectedException<TException> : Attribute where TException : Exception{
    public static TException AssertExceptionThrown(Action testMethod){
        try{
            testMethod();
            throw new InvalidOperationException("$The expected exception, {typeof(TException).FullName}, was not thrown.");
        }
        catch (TException exception){
            return exception;
        }
    }
}
```

我们有一个泛型属性，用于装饰测试方法。为了让此测试方法通过，它必须抛出一个类型为 `TException` 的异常。在列表 18.26 中，`ThrowsDivideByZeroException()` 预期会抛出 `DivideByZeroException`，并通过装饰它的 `ExpectedException<DivideByZeroException>` 识别出来。

## Caller* 属性

在 C# 10.0 中，引入了 **Caller* 属性**（通常称为 `CallerArgumentExpression`）。通过这些属性，编译器会为被调用方法注入调用者的参数值。例如，考虑调用 `AssertExceptionThrown()` 方法：

```cs
ExpectedException<DivideByZeroException>.AssertExceptionThrown(
    () => throw new Exception(),
    "() => throw new Exception()",
    "./FileName.cs");
```

注意，除了预期的异常类型的类型参数外，还有一个表达式以及该表达式的字符串重复，外加上调用者的方法名和文件名。在没有任何额外语言支持的情况下，如果让 `AssertExceptionThrown()` 方法在未抛出预期异常时包含完整的诊断信息，则所有这些参数都是必需。尽管初始表达式以外的所有值显然很容易自动确定（在这种情况下，将表达式重复为字符串尤为令人烦恼）。尽管如此，它们仍然需要被指定，以便被调用方法拥有所有必要的信息来提供详细错误消息（参见列表 18.27）。

注意，除了 `testAction` 之外，所有参数都有 1) 一个属性和 2) 一个默认值。这些属性为编译器提供了元数据，告知这些参数值不应由编译器提供。

### 列表 18.27：CallerArgumentExpression 属性示例

```cs
public class SampleTests
{
    [ExpectedException<DivideByZeroException>]
    public static void ThrowArgumentNullException()
    {
        var result = 1"".Length;
    }
}

[AttributeUsage(AttributeTargets.Method)]
public class ExpectedException<TException> : Attribute where TException : Exception
{
    public static TException AssertExceptionThrown(
        Action testAction,
        [CallerArgumentExpression(nameof(testAction))] string testExpression = null,
        [CallerMemberName] string testActionMemberName = null,
        [CallerFilePath] string testActionFileName = null!
    )
    {
        try {
            testAction();
            throw new InvalidOperationException(
                $"{typeof(TException).FullName}, was not thrown " +
                $"by the expression '{testExpression}' in the method '{testActionMemberName}' and file '{testActionFileName}'");
        }
        catch (TException exception) {
            return exception;
        }
    }
    // Attribute detection
    // ...
}
```

结果是方法的调用被显著简化，如列表 18.28 所示。

### 列表 18.28：调用 Caller* 属性方法

```cs
ExpectedException<DivideByZeroException>.AssertExceptionThrown(() => throw DivideByZeroException());
```

现在，尽管在源代码中没有为 `testActionMemberName` 参数指定任何参数（例如），字符串值 "Method" 会被注入并在 `AssertExceptionThrown()` 方法中可用。显然，此类 Caller* 属性集合是有限的，如表 18.1 所示。

### 表 18.1：Caller* 属性

| 属性 | 说明 | 类型 |
|---|---|---|
| CallerFilePath | 包含调用者的源文件的完整路径。完整路径是编译时的路径。 | string |
| CallerLineNumberAttribute | 调用该方法的源文件中的行号。 | System.Int32 |
| CallerMemberNameAttribute | 调用者的方法名或属性名。 | string |
| CallerArgumentExpressionAttribute | 参数表达式的字符串表示。 | string |

所有的 Caller* 属性都限制使用参数构造结构，且从列表 18.27 中大多自俗易懂。唯一的异常是 `CallerArgumentExpressionAttribute`，因为它需要自己的参数。`CallerArgumentExpressionAttribute` 识别（文本）用于方法内另一个参数的表达式。例如，在列表 18.27 中，表达式 `() => throw new Exception()` 是 `testAction` 的值。

> 7 https://learn.microsoft.com/dotnet/csharp/language-reference/attributes/caller-information

## 属性

总结来说，`CallerArgumentExpression` 以文本识别方法内另一个参数使用的表达式。例如，在列表 18.27 中，表达式 `() => throw new Exception()` 是 `testAction` 的值。（在 C# 11 中允许 `nameof(testAction)` 引用参数。）

注意，为了让编译器允许被动态属性装饰的参数不需要提供参数，必须提供一个默认值。尽管参数上的数据类型应该是非可空的，但唯一合理的值是 `null`。这样做是因为预计编译器会相应地为所有参数提供值。

## 指南

- **不要**显式地为 Caller* 属性参数传递参数。
- **要使用**非可空字符串作为 Caller* 属性参数的数据类型。
- **要为** Caller* 属性字符串参数的默认值分配 `null!`。

结束 10.0
11.0

## 对象的编程

动态对象的引入简化了许多编程场景，并实现了以前无法实现的几个新场景。核心在于，动态对象编程允许开发者使用动态分发机制来编写操作，运行时将在执行时解析该机制，而不是让编译器在编译时进行验证并绑定。

为什么呢？许多对象本质上不是静态类型的。示例包括从 XML/CSV 文件、数据库表、Internet Explorer DOM 或 COM 的 `IDispatch` 接口加载数据，或者调用动态语言（如 IronPython 对象）中的代码。动态对象支持为与不一定具有编译定义结构的运行时环境提供了一个通用解决方案。在动态对象的初始实现中提供了四种绑定方法：

- 使用针对底层 CLR 类型的反射
- 调用自定义的 `IDMetaObjectProvider` 以提供一个 `DynamicMetaObject`
- 通过 COM 的 `IUnknown` 和 `IDispatch` 接口调用
- 调用由 IronPython 等动态语言定义的类型

在这四种方法中，我们将深入研究前两种。它们的原理可以无缝转换到其余情况中——COM 互操作性和动态语言互操作性。

### 使用 dynamic 调用反射

反射的关键特性之一是能够根据执行时识别的成员名称或其他属性（例如属性），动态地查找并调用类型上的成员（参见列表 18.3）。然而，动态对象

- 1. 引入于 C# 4.0。

提供了一种更简单的通过反射调用成员的方法，假设在编译时已经知道成员的签名。重申一下，这一限制规定了在编译时，我们需要知道成员名称以及其签名（参数的数量以及指定的参数是否与签名类型兼容）。列表 18.29（带有输出 18.10）提供了一个示例。

## 使用动态对象编程 921

### 列表 18.29：使用反射的动态编程

```csharp
// ...
dynamic data =
    "Hello! My name is Inigo Montoya";
Console.WriteLine(data);
data = (double)data.Length;
data = data * 3.5 + 28.6;
if(data == 2.4 + 112 + 26.2)
    // 距离（单位：英里）分别是铁人三项锦标赛
    // 游泳、自行车和跑步部分的距离
{
    Console.WriteLine(
        "{data} makes for a long triathlon.");
}
else
{
    data.NonExistentMethodCallStillCompiles();
// ...
```

# 第 18 章：反射、属性与动态编程

```cs
}

// Attribute detection
// ...
```
