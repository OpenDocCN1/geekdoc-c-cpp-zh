
```csharp
Console.WriteLine("所有版本都包含此内容。");
}
}
```

# C# 3.0: 初学者指南

此程序显示以下内容：

针对性版本编译。
所有版本均包含此。

程序定义了符号 `EXPERIMENTAL`。因此，当遇到 `if` 时，符号表达式求值为真，并且第一个 `WriteLine()` 语句会被编译。如果你删除了 `EXPERIMENTAL` 的定义并重新编译程序，第一个 `WriteLine()` 语句将不会被编译，因为 `if` 语句将无法求值。在任何情况下，第二个 `WriteLine()` 语句都会被编译，因为它不是 `if` 块的一部分。

正如所解释的，你可以在 `if` 中使用符号表达式。例如：

```csharp
// 使用符号表达式。

#define EXPERIMENTAL

#define TRIAL
```

```csharp
using System;

class Test {
    static void Main() {
#if EXPERIMENTAL
        Console.WriteLine("Compiled for experimental version.");
    #endif
    #if EXPERIMENTAL && TRIAL
        // 一个符号表达式。
        Console.Error.WriteLine("Testing experimental trial version.");
    #endif
    Console.WriteLine("This is in all versions.");
}}
```

该程序的输出所示：

Compiled for experimental version.
Testing experimental trial version.
This is in all versions.

在此示例中，定义了两个符号 `EXPERIMENTAL` 和 `TRIAL`。只有当两者都被定义时，第二个 `WriteLine()` 语句才会被编译。
你可以使用 `!` 在符号未定义时编译代码。例如：

```csharp
#if QC_PASSED
    Console.WriteLine("Code has not passed quality control.");
#endif
```

只有当 `QC_PASSED` 未定义时，对 `WriteLine()` 的调用会被编译。

由于 `TRIAL` 未定义，因此使用了第二个条件代码序列的 `#else` 部分。
注意，`#else` 标记了 `#if` 的结束和 `#else` 块的开始。这是必要的，因为任何 `#if` 只能关联一个 `#endif`。此外，任何 `#if` 只能关联一个 `#else`。

`#elif` 指令意味着“else if”，并为多个备选方案建立一个 if-else 链。`#elif` 后面跟着一个符号表达式。如果该表达式为真，则编译该块代码，且不再测试其他的 `#elif` 表达式。否则，将检查系列中的下一个块。如果没有 `#elif` 成功，则存在 `#else`，编译与 `#else` else 关联的代码序列。否则，整个 `#if` 中没有任何代码会被被编译。

```csharp
#else symbol-expression
statement sequence
#endif
```

# 第 15 章：预处理器、RTTI、可空类型和其他高级主题 559

### #undef

`#undef` 指令用于移除之前定义的符号。也就是说，它会“取消定义”一个符号。
`#undef` 的通用形式为：

```csharp
#undef symbol
```

例如：

```csharp
#define MOBILE_DEVICE
```

```csharp
#if MOBILE_DEVICE
//...
#undef MOBILE_DEVICE
// 在此点，MOBILE_DEVICE 变得未定义。
```

在执行 `#undef` 指令后，`MOBILE_DEVICE` 不再被定义。
`#undef` 主要用于允许符号限制在仅需要它的代码段中。

## # 提问专家

> **Q：我注意到 C# 预处理器指令与 C 和 C++ 支持的预处理器指令有许多相似之处。此外，在 C/C++ 中，我知道可以使用 `#define` 来执行文本替换（通过为值定义名称），并创建类似函数的宏。C# 支持这些 `#define` 的用法吗？**

**A：不支持。在 C# 中，`#define` 仅用于定义符号。**

### #error

`#error` 指令强制编译器停止编译。它用于调试。
`#error` 指令的通用形式为：

```csharp
#error error-message
```

当遇到 `#error` 指令时，会显示错误消息。例如，当编译器遇到以下内容时：

```csharp
#error Debug code still being compiled
```

编译停止并显示错误消息“Debug code still being compiled!”。

### #warning

`#warning` 指令与 `#error` 类似，区别在于产生的是警告而不是错误。因此，编译不会停止。`#warning` 指令的通用形式为：

```csharp
#warning warning-message
```

# C# 3.0: 初学者指南 577 560

### #line

`#line` 指令设置行号和文件名，用于调试。`#line` 的通用形式为：

```csharp
#line line-number "filename"
```

在这里，`line-number` 是行号，`filename` 是文件名。这用于告诉编译器代码在源文件中的位置。

### #region

`#region` 指令允许你将一组代码组合在一起，这对于组织大型文件非常有用。通用形式为：

```csharp
#region name
// code
#endregion
```

`#endregion` 指令标记 `#region` 块的结束。

### #pragma

`#pragma` 指令用于提供特定编译器的指令。通用形式为：

```csharp
#pragma directive argument
```

在这里，`directive` 是指令，`argument` 是参数。这用于启用不是 C# 标准部分的功能。

# 第 15 章：预处理器、RTTI、可空类型以及其他高级主题 563

关于类型的信息。例如，此程序显示了 `StreamReader` 类的完整名称：

```csharp
// 演示 typeof。
using System;
using System.IO;
class Useof {
  static void Main() {
    Type t = typeof(StreamReader);
    Console.WriteLine(t.FullName);
  }
}
```

此程序输出以下内容：

System.IO.StreamReader

`System.Type` 包含许多描述类型的方法、字段和属性。你可能想要自己探索它。

### 可空类型 (Nullable Types)

从 2.0 版本开始，C# 引入了一项功能，为既常见又恼人的问题提供了优雅的解决方案。该功能就是可空类型。问题在于如何识别和处理不包含值的字段（换句话说，未赋值的字段）。为了理解这个问题，请考虑一个简单的数据库，它记录了客户名称、账户 ID、发票号和当前余额。在这种情况下，可能会创建一个客户条目，其中一个或多个字段未赋值赋值。例如，客户可能只是请求一份目录。在这种情况下，不需要发票号，该字段将不被使用。

在可空类型出现之前，处理未使用字段的可能性需要使用占位符值，或者使用一个额外的字段来指示是否使用了值。当然，只有当存在一个在其他无效的值时，占位符值才有效，而这在所有情况下都不成立。在所有情况下都添加一个额外字段来指示字段是否被使用，但手动创建和管理此类字段是件令人恼的事。

可空类型是值类型的特殊版本，由结构体表示。除了底层类型定义的值外，可空类型还可以存储值 `null`。因此，可空类型的范围和特征与其底层类型相同。它增加了表示该类型未赋值值的能力。可空类型是 `System.Nullable<T>` 的对象，其中 `T` 必须是非可空的值类型。

您可以通过两种方式指定可空类型。首先，你可以显式地使用类型 `Nullable<T>`。例如，这声明了 `int` 和 `bool` 类型的可空变量：

```csharp
Nullable<int> count;
Nullable<bool> done;
```

## C# 3.0：入门指南

指定可空类型的第二种方式短得多，且更常用。只需在底层类型名称后跟一个 `?`。即可，下面的代码显示了声明可空 `int` 和 `bool` 类型变量的常用方法：

```csharp
int? count;
bool? done;
```

在使用可空类型时，你经常会看到这样创建一个可空对象：

```csharp
int? count = null;
```

这显式地将 `count` 初始化为 `null`。这满足了变量在使用之前必须有值的约束。在这种情况下，该值仅意味着“未定义”。
你可以以普通方式为可空变量赋值，因为底层类型到可空类型的转换是预定义的。例如，这为 `count` 赋值了值 100：

```csharp
count = 100;
```

有两种方法可以判断可空类型是为 null 还是包含值。首先，你可以将值与 null 进行比较。例如，使用前一个语句声明的 `count`，以下代码判断它是否有值：

```csharp
if (count != null) // 有值
```

如果 `count` 不是 null，那么它就包含一个值。
判断可空类型是否包含值的第二种方法是使用 `Nullable<T>` 定义的只读属性 `HasValue`。显示如下：

```csharp
bool HasValue
```

只有当实例包含值时，`HasValue` 才会返回 `true`。否则返回 `false`。使用 `HasValue` 属性，是判断可空对象是否有值的第二种方法：

```csharp
if (count.HasValue) // 有值
```

假设可空对象包含值，你可以通过 `Nullable<T>` 定义的只读属性 `Value` 来获取其值，显示如下：

```csharp
T Value
```

它返回所调用的可空实例的值。如果你尝试从一个 null 变量获取值，将抛出 `System.InvalidOperationException`。也可以通过将可空实例强制转换为其底层类型来获取值。
以下程序整合了这些部分，并演示了处理可空类型的基本机制：

## 第 15 章：预处理器、RTTI、可空类型以及其他高级主题 565

```csharp
// 演示可空类型。
using System;
class NullableDemo {
    static void Main() {
        int? count = null; // 为 int 声明可空类型
        if (count.HasValue) {
            Console.WriteLine("count has this value: " + count.Value);
        } else {
            Console.WriteLine("count has no value");
        }
        count = 100;
        if (count.HasValue) {
            Console.WriteLine("count has this value: " + count.Value);
        } else {
            Console.WriteLine("count has no value");
        }
    }
}
```

输出显示在此：

count has no value
count has this value: 100

### ?? 运算符

如果你尝试使用强制转换将可空对象转换为其底层类型，如果可空对象为 null，则将抛出 `System.InvalidOperationException`。你可以使用合并运算符来避免这种异常的可能性。它允许你指定一个在可空对象包含 null 时使用的默认值。`??` 运算符具有这种通用形式：

```csharp
nullable-object ?? default-value
```

如果 `nullable-object` 包含值，则 `??` 就是该值。否则，使用默认值。例如，在下面的代码中，`balance` 为 null。这导致 `currentBalance` 被赋值为 0。

```csharp
double? balance = null;
double currentBalance;
currentBalance = balance ?? 0.0;
```

## C# 3.0：入门指南

在接下来的序列中，`balance` 被赋予了值 123.75。

```csharp
double? balance = 123.75;
double currentBalance;
currentBalance = balance ?? 0.0;
```

现在，`currentBalance` 将包含 `balance` 的值，即 123.75。
另一点：只有当左侧表达式不包含值时，`??` 的右侧表达式才会被求值。

## 可空对象与关系及逻辑运算符

可空对象在关系表达式中的用法与其对应的非可空类型相同。然而，还有一个额外的规则适用。当使用 `<>`、 `<=` 或 `>=` 运算符比较两个可空对象时，如果其中一个对象为 `null`，结果为 `false`。例如，考虑以下序列：

```csharp
byte? lower = 16;
byte? upper = null;
```

```csharp
// 这里 lower 定义了，但 upper 未定义。
if(lower < upper) // false
```

在这里，小于测试的结果为 `false`。然而，有些违背直觉的是，反向比较：

```csharp
if(lower > upper) // 也是 false!
```

因此，当用于比较的可空对象有一个（或两个）为 `null` 时，比较结果始终为 `false`。因此，`null` 不参与排序关系。
你可以通过 `==` 或 `!=` 运算符测试可空对象是否包含 `null`。例如，这是一个返回 `true` 结果的测试：

```csharp
if(upper == null) // true
```

当逻辑表达式涉及两个对象时，该表达式的结果有三种可能：`true`、`false` 或 `null`（未定义）。以下是适用于 `bool?` 的 `&` 和 `|` 运算符真值表中增加的条目：

| P | Q | P|Q | P&Q |
|---|---|---|---|
| true | null | true | null |
| false | null | null | false |
| null | true | true | null |
| null | false | null | false |

另一点：当 `!` 运算符作用于为 `null` 的 `bool?` 值时，结果为 `null`。

第 15 章：预处理器、RTTI、可空类型以及其他高级主题

### 不安全代码 (Unsafe Code)

C# 允许你编写所谓的“不安全”代码！这听起来可能像是包含错误的代码名称，但事实并非如此。不安全代码并不是糟糕的代码；它是不是在通用语言运行时（CLR）完全管理下执行的代码。正如第 1 节所过的，C# 通常用于创建托管代码。然而，编写在不在 CLR 完全控制下执行的代码也是可能的。由于这种非托管代码不受与托管代码相同的控制和限制，因此被称为“不安全”的，因为无法验证你是否执行了某种类型的有害操作。因此，“不安全”一词并不意味着代码本身有缺陷。它意味着代码可能会执行不受托管上下文监督的操作。

托管代码虽然在大多数情况下是有益的，但它阻止了指针的使用。如果你熟悉 C++，那么你就知道指针是存储其他对象地址的变量。从概念上说，指针就相当于 C# 中的引用（reference）。主要的区别在于，指针可以指向内存中的任何位置，而引用始终指向其类型的对象。由于指针可以指向内存中的任何位置，因此可能会误用指针。使用指针也很容易引入编码错误。这就是为什么 C# 在创建托管代码时不支持指针。然而，指针对于某些类型的编程（例如编写与设备交互的代码）是有用且必需的，C# 允许你创建和使用指针。所有的指针操作都必须标记为不安全的（unsafe），因为它们在托管环境之外执行。

有趣的是，C# 中指针的声明和使用与 C++ 相似；如果你知道如何在 C++ 中使用指针，那么你就可以 C# 中使用它们。但请记住，C# 的重点是创建托管代码。它支持非托管代码的能力使其能够应用于一类特殊问题，而不适用于普通的 C# 编程。实际上，要编译非托管代码，你必须使用 `unsafe` 编译器选项。如果你需要创建大量在 CLR 之外执行的代码，那么可能应该使用 C++。

处理非托管代码是一个高级主题，详细讨论远超本书的范围。尽管如此，我们将简要检查指针以及支持非托管代码的关键字：`unsafe` 和 `fixed`。

### 指针简述

指针是一个存储其他对象地址的变量。例如，如果 `p` 包含 `y` 的地址，则称 `p` “指向” `y`。指针变量必须声明。指针声明的通用形式为：

```c
type* var_name;
```
