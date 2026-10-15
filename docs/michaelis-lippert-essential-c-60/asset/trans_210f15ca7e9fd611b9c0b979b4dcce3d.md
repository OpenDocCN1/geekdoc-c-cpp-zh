

## 定义预处理器符号（`#define`、`#undef`）

你可以通过两种方式定义预处理器符号。第一种是使用 `#define` 指令，如第 3.57 条清单所示。

**清单 3.57：一个 #define 示例**

```csharp
#define CSHARP2PLUS
```

第二种方法是在为 .NET 编译时使用 define 选项，如输出 3.27 所示。

**输出 3.27**

```text
>csc.exe /define:CSHARPPLUS TicTacToe.cs
```

输出 3.28 显示了使用 Mono 编译器的相同功能。

**输出 3.28**

```text
>mcs.exe -define:CSHARPPLUS TicTacToe.cs
```

要添加多个定义，请用分号将它们分隔开。define 编译器选项的优点是无需更改源代码，因此你可以使用相同的源文件生成两个不同的二进制文件。

要取消定义符号，你使用 `#undef` 指令，其使用方式与 `#define` 相同。

## 发出错误和警告（`#error`、`#warning`）

有时你可能想标记代码中的潜在问题。你通过插入 `#error` 和 `#warning` 指令分别发出错误或警告来实现这一点。清单 3.58 使用井字游戏示例来警告代码尚未防止玩家多次输入相同的移动。清单 3.58 的结果出现在输出 3.29 中。

**清单 3.58：使用 #warning 定义警告**

```csharp
#warning    "Same move allowed multiple times."
```

**输出 3.29**

```text
Performing main compilation...
...\tictactoe.cs(47,16): warning CS1030: #warning: "Same move allowed multiple times."

Build complete -- 0 errors, 1 warnings
```

通过包含 #warning 指令，你确保编译器会报告警告，如输出 3.29 所示。此特定警告是标记代码中存在潜在增强或错误的方式。它可以作为提醒开发人员待办任务的简单方法。

## 关闭警告消息（#pragma）

警告是有帮助的，因为它们指出了可能存在问题的代码。然而，有时出于正当理由需要显式关闭特定警告。C# 2.0 及更高版本的编译器提供了预处理器 #pragma 指令来实现此目的（参见清单 3.59）。

**清单 3.59：使用预处理器 #pragma 指令禁用 #warning 指令**

```csharp
#pragma warning disable 1030
```

请注意，警告编号在编译器输出中以字母 CS 为前缀。然而，此前缀在 #pragma warning 指令中不使用。编号对应于编译器在没有预处理器命令时发出的警告错误编号。

要重新启用警告，#pragma 支持在警告后使用 restore 选项，如清单 3.60 所示。

**清单 3.60：使用预处理器 #pragma 指令恢复警告**

```csharp
#pragma warning restore 1030
```

结合使用，这两个指令可以包围一段代码块，在该块中警告被明确判定为无关紧要。

也许最常见的要禁用的警告之一是 CS1591。当你选择使用 /doc 编译器选项生成 XML 文档，但未能记录程序中所有公共项时，会出现此警告。

## nowarn:<warn list> 选项

除了 #pragma 指令外，C# 编译器通常还支持 nowarn:<warn list> 选项。这实现了与 #pragma 相同的效果，只是你不是将其添加到源代码中，而是将其作为编译器选项插入。nowarn 选项影响整个编译，而 #pragma 选项仅影响其出现的源文件。例如，关闭 CS1591 警告在命令行上将如下所示输出 3.30。

**输出 3.30**

```text
> csc /doc:generate.xml /nowarn:1591 /out:generate.exe Program.cs
```

## 指定行号（#line）

#line 指令控制 C# 编译器报告错误或警告的行号。它主要由发出 C# 代码的实用程序和设计器使用。在清单 3.61 中，文件内的实际行号显示在左侧。

**清单 3.61：#line 预处理器指令**

```text
124     #line 113 "TicTacToe.cs"
125     #warning "Same move allowed multiple times."
126     #line default
```

包含 #line 指令会导致编译器将第 125 行找到的警告报告为第 113 行，如输出 3.31 中的编译器错误消息所示。

**输出 3.31**

```text
Performing main compilation...
...\tictactoe.cs(113,1): warning CS1030: #warning: "Same move allowed multiple times."

Build complete -- 0 errors, 1 warnings
```

在 #line 指令后跟随 default 会逆转所有先前 #line 指令的效果，并指示编译器报告真实行号而不是由先前使用 #line 指令指定的行号。

## 为可视编辑器提供提示（#region、#endregion）

C# 包含两个预处理器指令 #region 和 #endregion，它们仅在可视代码编辑器的上下文中有用。代码编辑器，例如 Microsoft Visual Studio，可以搜索源代码并找到这些指令，以在编写代码时提供编辑器功能。C# 允许你使用 #region 指令声明代码区域。你必须将 #region 指令与匹配的 #endregion 指令配对，两者均可选择在指令后包含描述性字符串。此外，你可以相互嵌套区域。

清单 3.62 以井字游戏程序为例。

**清单 3.62：#region 和 #endregion 预处理器指令**

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

这些预处理器指令例如与 Microsoft Visual Studio 一起使用。Visual Studio 检查代码并提供树形控件来打开和折叠代码（在代码编辑器窗口左侧），该代码与 #region 指令划定的区域匹配（见图 3.5）。

![](img/25683ccec0773ba5b8794b11f2b12877_197_0.png)

**图 3.5：** Microsoft Visual Studio .NET 中的折叠区域

## 摘要

本章首先介绍了与赋值和算术相关的 C# 运算符。接下来，我们使用运算符以及 const 关键字声明常量。对所有 C# 运算符的介绍并非按顺序进行。在讨论关系和逻辑比较运算符之前，本章介绍了 if 语句以及代码块和作用域的重要概念。为了完成对运算符的介绍，我们讨论了位运算符，特别是在掩码方面的应用。我们还讨论了其他控制流语句，如循环、switch 和 goto，并以对 C# 预处理器指令的讨论结束本章。

运算符优先级在章节前面讨论过；表 3.5 总结了所有运算符的优先级顺序，包括一些尚未介绍的运算符。

**表 3.5：运算符优先级顺序***

| 类别 | 运算符 |
|---|---|
| Primary | `x.y`  `f(x)`  `a[x]`  `x++`  `x--`  `new`  `typeof`  `checked(x)`  `unchecked(x)`  `default(T)`  `nameof(x)`  `delegate{}`  `()` |
| Unary | `+`  `-`  `!`  `~`  `++x`  `--x`  `(T)x`  `await x` |
| Multiplicative | `*`  `/`  `%` |
| Additive | `+`  `-` |
| Shift | `<<`  `>>` |
| Relational and type testing | `<`  `>`  `<=`  `>=`  `is`  `as` |
| Equality | `==`  `!=` |
| Logical AND | `&` |
| Logical XOR | `^` |
| Logical OR | `\|` |
| Conditional AND | `&&` |
| Conditional OR | `\|\|` |
| Null coalescing | `??` |
| Conditional | `?:` |
| Assignment and lambda | `=`  `*=`  `/=`  `%=`  `+=`  `-=`  `<<=`  `>>=`  `&=`  `^=`  `\|=`  `=>` |

* 行按从高到低的优先级顺序排列。

也许回顾第 1 章至第 3 章所涵盖所有内容的最佳方法之一是查看附录 B 中的井字游戏程序。通过查看此程序，你可以看到将所学内容组合成完整程序的一种方式。

