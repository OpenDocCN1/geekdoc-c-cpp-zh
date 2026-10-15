
```csharp
class EmailDomain
{
    static void Main()
    {
        string email;
        bool insideDomain = false;
        System.Console.WriteLine("Enter an email address: ");

        email = System.Console.ReadLine();

        System.Console.Write("The email domain is: ");

        // Iterate through each letter in the email address.
        foreach (char letter in email)
        {
            if (!insideDomain)
            {
                if (letter == '@')
                {
                    insideDomain = true;
                }
                continue;
            }

            System.Console.Write(letter);
        }
    }
}
```

## 输出 3.25

```text
Enter an email address:
mark@dotnetprogramming.com
The email domain is: dotnetprogramming.com
```

在清单 3.52 中，如果尚未进入电子邮件地址的域部分，可以使用 `continue` 语句将控制转移到循环末尾，并处理电子邮件地址中的下一个字符。

几乎总是可以用 `if` 语句代替 `continue` 语句，而且这样通常可读性更好。`continue` 语句的问题在于，它在一次迭代中提供了多种控制流，这损害了可读性。在清单 3.53 中，示例被重写，用 `if/else` 结构替换了 `continue` 语句，以演示一个不使用 `continue` 语句且可读性更好的版本。

## 清单 3.53：用 if 语句替换 continue 语句

```csharp
foreach (char letter in email)
{
    if (insideDomain)
    {
        System.Console.Write(letter);
    }
    else
    {
        if (letter == '@')
        {
            insideDomain = true;
        }
    }
}
```

## goto 语句

早期的编程语言缺乏现代语言（如 C#）理所当然具有的相对复杂的“结构化”控制流，而是依靠简单条件分支（`if`）和无条件分支（`goto`）语句来满足大部分控制流需求。由此产生的程序往往难以理解。在许多经验丰富的程序员看来，C# 中仍然存在 `goto` 语句似乎是一种时代错误。然而，C# 确实支持 `goto`，并且它是支持 `switch` 语句中贯穿（fall-through）的唯一方法。在清单 3.54 中，如果设置了 `/out` 选项，代码执行会使用 `goto` 语句跳到 `default` 分支，`/f` 选项同理。

## 清单 3.54：演示带 goto 语句的 switch

```csharp
// ...
static void Main(string[] args)
{
    bool isOutputSet = false;
```

然后分支到带标签的语句。幸运的是，C# 阻止你使用 `goto` 跳入代码块；相反，`goto` 只能用于在代码块内部跳转，或跳转到外层代码块。通过这些限制，C# 避免了其他语言中可能出现的多数严重 `goto` 滥用。

尽管有了这些改进，使用 `goto` 通常仍被认为不够优雅、难以理解，并且是代码结构不佳的表现。如果你需要多次或在不同的情况下执行某段代码，要么使用循环，要么将代码提取到单独的方法中。

## 指南

避免使用 `goto`。

## C# 预处理器指令

控制流语句在运行时计算表达式。相比之下，C# 预处理器在编译期间被调用。预处理器命令是对 C# 编译器的指令，指定要编译的代码段，或指明如何处理代码中的特定错误和警告。C# 预处理器命令还可以向 C# 编辑器提供关于代码组织的指令。

## 语言对比：C++——预处理

C 和 C++ 等语言使用预处理器基于特殊标记对代码执行操作。预处理器指令通常告诉编译器如何编译文件中的代码，但本身不参与编译过程。相比之下，C# 编译器将“预处理器”指令作为源代码常规词法分析的一部分来处理。因此，除了定义常量之外，C# 不支持预处理器宏。事实上，对于 C# 来说，“预处理器”这个术语通常用词不当。

每个预处理器指令都以井号（`#`）开头，并且所有预处理器指令都必须出现在同一行中。指令的结束由换行符表示，而不是分号。

每个预处理器指令的列表见表格 3.4。

## 表格 3.4：预处理器指令

| 语句或表达式 | 通用语法结构 | 示例 |
|---|---|---|
| `#if` 指令 | `#if preprocessor-expression`<br>`code`<br>`#endif` | `#if CSHARP2PLUS`<br>`Console.Clear();`<br>`#endif` |
| `#elif` 指令 | `#if preprocessor-expression1`<br>`code`<br>`#elif preprocessor-expression2`<br>`code`<br>`#endif` | `#if LINUX`<br>`...`<br>`#elif WINDOWS`<br>`...`<br>`#endif` |
| `#else` 指令 | `#if` `code`<br>`#else`<br>`code`<br>`#endif` | `#if CSHARP1`<br>`...`<br>`#else`<br>`...`<br>`#endif` |
| `#define` 指令 | `#define conditional-symbol` | `#define CSHARP2PLUS` |
| `#undef` 指令 | `#undef conditional-symbol` | `#undef CSHARP2PLUS` |
| `#error` 指令 | `#error preproc-message` | `#error Buggy implementation` |
| `#warning` 指令 | `#warning preproc-message` | `#warning Needs code review` |
| `#pragma` 指令 | `#pragma warning` | `#pragma warning disable 1030` |
| `#line` 指令 | `#line org-line new-line`<br><br>`#line default` | `#line 467 "TicTacToe.cs"`<br>`...`<br>`#line default` |
| `#region` 指令 | `#region pre-proc-message`<br>`code`<br>`#endregion` | `#region Methods`<br>`...`<br>`#endregion` |

## 排除和包含代码（`#if`、`#elif`、`#else`、`#endif`）

也许预处理器指令最常见的用途是控制代码何时以及如何被包含。例如，要编写既能由 C# 2.0 及更高版本编译器编译，也能由先前的 1.0 版本编译器编译的代码，你可以使用预处理器指令，在使用 1.0 版本编译器编译时排除 C# 2.0 特有的代码。你可以在井字棋示例和清单 3.55 中看到这一点。

**清单 3.55：从 C# 1.x 编译器中排除 C# 2.0 代码**

```csharp
#if CSHARP2PLUS
System.Console.Clear();
#endif
```

在这种情况下，你调用 `System.Console.Clear()` 方法，该方法仅在 CLI 2.0 及更高版本中可用。使用 `#if` 和 `#endif` 预处理器指令，只有在定义了预处理器符号 `CSHARP2PLUS` 时，这行代码才会被编译。

预处理器指令的另一个用途是处理平台之间的差异，例如用 `WINDOWS` 和 `LINUX` `#if` 指令包围 Windows 和 Linux 特有的 API。开发人员经常使用这些指令代替多行注释（`/*...*/`），因为通过定义适当的符号或通过查找并替换即可轻松移除它们。

指令的最后一个常见用途是调试。如果用 `#if DEBUG` 包围代码，在大多数 IDE 中，该代码将从发布构建中移除。IDE 在调试编译时默认定义 `DEBUG` 符号，在发布构建时默认定义 `RELEASE`。

为了处理 else-if 条件，你可以在 `#if` 指令中使用 `#elif` 指令，而不是创建两个完全独立的 `#if` 块，如清单 3.56 所示。

**清单 3.56：使用 `#if`、`#elif` 和 `#endif` 指令**

```csharp
#if LINUX
...
#elif WINDOWS
...
#endif
```

## 定义预处理器符号（`#define`、`#undef`）

你可以通过两种方式定义预处理器符号。第一种是使用 `#define` 指令，如第 3.57 条清单所示。

**清单 3.57：一个 `#define` 示例**

```csharp
#define CSHARP2PLUS
```

第二种方法是在为 .NET 编译时使用 `define` 选项，如输出 3.27 所示。

**输出 3.27**

```text
>csc.exe /define:CSHARPPLUS TicTacToe.cs
```

输出 3.28 显示了使用 Mono 编译器的相同功能。

**输出 3.28**

```text
>mcs.exe -define:CSHARPPLUS TicTacToe.cs
```

要添加多个定义，请用分号将它们分隔开。`define` 编译器选项的优点是无需更改源代码，因此你可以使用相同的源文件生成两个不同的二进制文件。

要取消定义符号，你使用 `#undef` 指令，其使用方式与 `#define` 相同。

## 发出错误和警告（`#error`、`#warning`）

有时你可能想标记代码中的潜在问题。你通过插入 `#error` 和 `#warning` 指令分别发出错误或警告来实现这一点。清单 3.58 使用井字游戏示例来警告代码尚未防止玩家多次输入相同的移动。清单 3.58 的结果出现在输出 3.29 中。

**清单 3.58：使用 `#warning` 定义警告**

```csharp
#warning    "Same move allowed multiple times."
```

**输出 3.29**

```text
Performing main compilation...
...\tictactoe.cs(47,16): warning CS1030: #warning: "Same move allowed multiple times."

Build complete -- 0 errors, 1 warnings
```

通过包含 `#warning` 指令，你确保编译器会报告警告，如输出 3.29 所示。此特定警告是标记代码中存在潜在增强或错误的方式。它可以作为提醒开发人员待办任务的简单方法。

## 关闭警告消息（`#pragma`）

警告是有帮助的，因为它们指出了可能存在问题的代码。然而，有时出于正当理由需要显式关闭特定警告。C# 2.0 及更高版本的编译器提供了预处理器 `#pragma` 指令来实现此目的（参见清单 3.59）。

**清单 3.59：使用预处理器 `#pragma` 指令禁用 `#warning` 指令**

```csharp
#pragma warning disable 1030
```

请注意，警告编号在编译器输出中以字母 `CS` 为前缀。然而，此前缀在 `#pragma warning` 指令中不使用。编号对应于编译器在没有预处理器命令时发出的警告错误编号。

要重新启用警告，`#pragma` 支持在警告后使用 `restore` 选项，如清单 3.60 所示。

**清单 3.60：使用预处理器 `#pragma` 指令恢复警告**

```csharp
#pragma warning restore 1030
```

结合使用，这两个指令可以包围一段代码块，在该块中警告被明确判定为无关紧要。

也许最常见的要禁用的警告之一是 `CS1591`。当你选择使用 `/doc` 编译器选项生成 XML 文档，但未能记录程序中所有公共项时，会出现此警告。

## `nowarn:<warn list>` 选项

除了 `#pragma` 指令外，C# 编译器通常还支持 `nowarn:<warn list>` 选项。这实现了与 `#pragma` 相同的效果，只是你不是将其添加到源代码中，而是将其作为编译器选项插入。`nowarn` 选项影响整个编译，而 `#pragma` 选项仅影响其出现的源文件。例如，关闭 `CS1591` 警告在命令行上将如下所示输出 3.30。

**输出 3.30**

```text
> csc /doc:generate.xml /nowarn:1591 /out:generate.exe Program.cs
```

## 指定行号（`#line`）

`#line` 指令控制 C# 编译器报告错误或警告的行号。它主要由发出 C# 代码的实用程序和设计器使用。在清单 3.61 中，文件内的实际行号显示在左侧。

**清单 3.61：`#line` 预处理器指令**

```text
124     #line 113 "TicTacToe.cs"
125     #warning "Same move allowed multiple times."
126     #line default
```

包含 `#line` 指令会导致编译器将第 125 行找到的警告报告为第 113 行，如输出 3.31 中的编译器错误消息所示。

**输出 3.31**

```text
Performing main compilation...
...\tictactoe.cs(113,1): warning CS1030: #warning: "Same move allowed multiple times."

Build complete -- 0 errors, 1 warnings
```

在 `#line` 指令后跟随 `default` 会逆转所有先前 `#line` 指令的效果，并指示编译器报告真实行号而不是由先前使用 `#line` 指令指定的行号。

## 为可视编辑器提供提示（`#region`、`#endregion`）

C# 包含两个预处理器指令 `#region` 和 `#endregion`，它们仅在可视代码编辑器的上下文中有用。代码编辑器，例如 Microsoft Visual Studio，可以搜索源代码并找到这些指令，以在编写代码时提供编辑器功能。C# 允许你使用 `#region` 指令声明代码区域。你必须将 `#region` 指令与匹配的 `#endregion` 指令配对，两者均可选择在指令后包含描述性字符串。此外，你可以相互嵌套区域。

清单 3.62 以井字游戏程序为例。

**清单 3.62：`#region` 和 `#endregion` 预处理器指令**

```csharp
...
#region Display Tic-tac-toe Board

#if CSHARP2PLUS
    System.Console.Clear();
#endif

// Display the current board;
border = 0;  // set the first border (border[0] = "|")

// Display the top line of dashes.
// ("\n---+---+---\n")
System.Console.Write(borders[2]);
foreach (char cell in cells)
{
    // Write out a cell value and the border that comes after it.
    System.Console.Write($"{ cell } { borders[border] }");

    // Increment to the next border.
    border++;

    // Reset border to 0 if it is 3.
    if (border == 3)
    {
        border = 0;
    }
}
#endregion Display Tic-tac-toe Board
...
```

这些预处理器指令例如与 Microsoft Visual Studio 一起使用。Visual Studio 检查代码并提供树形控件来打开和折叠代码（在代码编辑器窗口左侧），该代码与 `#region` 指令划定的区域匹配（见图 3.5）。

![](img/25683ccec0773ba5b8794b11f2b12877_197_0.png)

**图 3.5：** Microsoft Visual Studio .NET 中的折叠区域

## 摘要

本章首先介绍了与赋值和算术相关的 C# 运算符。接下来，我们使用运算符以及 `const` 关键字声明常量。对所有 C# 运算符的介绍并非按顺序进行。在讨论关系和逻辑比较运算符之前，本章介绍了 `if` 语句以及代码块和作用域的重要概念。为了完成对运算符的介绍，我们讨论了位运算符，特别是在掩码方面的应用。我们还讨论了其他控制流语句，如循环、`switch` 和 `goto`，并以对 C# 预处理器指令的讨论结束本章。

运算符优先级在章节前面讨论过；表 3.5 总结了所有运算符的优先级顺序，包括一些尚未介绍的运算符。

**表 3.5：运算符优先级顺序***

| 类别 | 运算符 |
|---|---|
