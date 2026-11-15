

## 定义预处理器符号 (#define, #undef)

可以通过两种方式定义预处理器符号。第一种是使用 #define 指令，如清单 3.55 所示。

### 清单 3.55：#define 示例

```
#define CSHARP2
```

第二种方法是在针对 .NET 编译时使用 define 选项，如输出 3.27 所示。

### 输出 3.27:

```
>csc.exe /define:CSHARP2 TicTacToe.cs
```

输出 3.28 显示了使用 Mono 编译器的相同功能。

### 输出 3.28:

```
>mcs.exe -define:CSHARP2 TicTacToe.cs
```

要添加多个定义，请用分号将它们分隔开。define 编译器选项的优点是无需更改源代码，因此可以使用相同的源文件生成两个不同的二进制文件。

要取消定义符号，请以与使用 #define 相同的方式使用 #undef 指令。

## 发出错误和警告 (#error, #warning)

有时您可能希望标记代码中的潜在问题。为此，请插入 #error 和 #warning 指令，分别发出错误或警告。清单 3.56 使用井字棋示例来警告代码尚未防止玩家多次输入相同的移动。清单 3.56 的结果显示在输出 3.29 中。

### 清单 3.56：使用 #warning 定义警告

```
#warning "Same move allowed multiple times."
```

### 输出 3.29:

```
Performing main compilation...
..\tictactoe.cs(47,14): warning CS1030: #warning: "Same move allowed
multiple times."
Build complete -- 0 errors, 1 warnings
```

通过包含 #warning 指令，您可以确保编译器会报告警告，如输出 3.29 所示。此特定警告是一种标记代码中存在潜在增强或错误的方法。它可以是提醒开发人员待办任务的一种简单方式。

## 关闭警告消息 (#pragma)

警告很有帮助，因为它们指向可能存在问题的代码。但是，有时最好显式关闭特定警告，因为它们可以合理地被忽略。C# 2.0 及更高版本的编译器提供了预处理器 #pragma 指令，专门用于此目的（请参阅清单 3.57）。

### 清单 3.57：使用预处理器 #pragma 指令禁用 #warning 指令

```
#pragma warning disable 1030
```

请注意，编译器输出中的警告编号前缀为字母 CS。但是，此前缀不用于 #pragma warning 指令。该编号对应于编译器在没有预处理器命令时发出的警告错误编号。

要重新启用警告，#pragma 支持在警告后使用 restore 选项，如清单 3.58 所示。

### 清单 3.58：使用预处理器 #pragma 指令恢复警告

```
#pragma warning restore 1030
```

结合使用，这两个指令可以围绕特定代码块，其中警告被明确确定为无关紧要。

也许最常见的要禁用的警告之一是 CS1591，因为当您选择使用 /doc 编译器选项生成 XML 文档，但忽略记录程序中的所有公共项时，就会出现此警告。

## nowarn:<warn list> 选项

除了 #pragma 指令之外，C# 编译器通常还支持 nowarn:<warn list> 选项。这与 #pragma 达到相同的结果，不同之处在于，您不需要将其添加到源代码中，而是可以将命令作为编译器选项插入。此外，nowarn 选项影响整个编译，而 #pragma 选项仅影响其出现的文件。例如，关闭 CS1591 警告将在命令行上显示为输出 3.30 所示。

### 输出 3.30:

```
> csc /doc:generate.xml /nowarn:1591 /out:generate.exe Program.cs
```

## 指定行号 (#line)

#line 指令控制 C# 编译器报告错误或警告的行号。它主要由发出 C# 代码的实用程序和设计器使用。在清单 3.59 中，文件中的实际行号显示在左侧。

### 清单 3.59：#line 预处理器指令

| 124 | #line 113 "TicTacToe.cs" |
| 125 | #warning "Same move allowed multiple times." |
| 126 | #line default |

包含 #line 指令会导致编译器将行 125 上发现的警告报告为位于行 113 上，如输出 3.31 中的编译器错误消息所示。

### 输出 3.31:

```
Performing main compilation...
..\tictactoe.cs(113,16): warning CS1030: #warning: "Same move allowed
multiple times."
Build complete -- 0 errors, 1 warnings
```

在 #line 指令后跟 default 会撤销所有先前 #line 指令的效果，并指示编译器报告真实行号，而不是先前 #line 指令指定的行号。

## 可视化编辑器提示 (#region, #endregion)

C# 包含两个预处理器指令，#region 和 #endregion，它们仅在可视化代码编辑器的上下文中有用。代码编辑器（例如 Microsoft Visual Studio .NET IDE 中的编辑器）可以搜索源代码并找到这些指令，以便在编写代码时提供编辑器功能。C# 允许您使用 #region 指令声明代码区域。您必须将 #region 指令与匹配的 #endregion 指令配对，两者都可以选择在指令后包含描述字符串。此外，您可以相互嵌套区域。再次，清单 3.60 以井字棋程序为例。

### 清单 3.60：#region 和 #endregion 预处理器指令

```
...
#region Display Tic-tac-Toe Board

#if CSHARP2
System.Console.Clear();
#endif

// Display the current board;
border = 0; // set the first border (border[0] = "/")

// Display the top line of dashes.
// ("\n-+---+---+---")
System.Console.Write(borders[2]);
foreach (char cell in cells)
{
    // Write out a cell value and the border that comes after it.
    System.Console.Write(" {0} {1}", cell, borders[border]);

    // Increment to the next border;
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

这些预处理器指令的一个用法示例是 Microsoft Visual Studio .NET。Visual Studio .NET 检查代码并提供一个树控件，用于打开和折叠代码（在代码编辑器窗口的左侧），该代码与 #region 指令划定的区域匹配（请参见图 3.5）。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_193_0.png)

### 图 3.5：Microsoft Visual Studio .NET 中折叠的区域

## 摘要

本章首先介绍了与赋值和算术相关的 C# 运算符。接下来，您将运算符与 const 关键字一起用于声明常量表达式。然而，对所有 C# 运算符的介绍并非按顺序进行。在讨论关系和逻辑比较运算符之前，本章介绍了 if 语句以及代码块和作用域的重要概念。为了结束对运算符的介绍，我讨论了按位运算符，尤其是关于掩码的运算符。

运算符优先级在本章前面已讨论过，但表 3.5 总结了所有运算符的优先级顺序，包括一些尚未介绍的运算符。

### 表 3.5：运算符优先级顺序*

| 类别 | 运算符 |
| :--- | :--- |
| 主要 | x.y f(x) a[x] x++ x-- new typeof(T) checked(x) unchecked(x) default(T) delegate() () |
| 一元 | + - ! ~ ++x --x (T)x |
| 乘法 | * / % |
| 加法 | + - |
| 移位 | << >> |
| 关系和类型测试 | < > <= >= is as |
| 相等 | == != |
| 逻辑 AND | & |
| 逻辑 XOR | ^ |
| 逻辑 OR | \| |
| 条件 AND | && |
| 条件 OR | || |
| 空合并 | ?? |
| 条件 | ?: |
| 赋值 | = => *= /= %= += -= <<= >>= &= ^= |= |

* 行按从高到低的优先级顺序排列。

在介绍了大部分运算符之后，下一个主题是控制流语句。本章的最后几节详细介绍了预处理器指令和位运算符，其中包括代码块、作用域、布尔表达式和按位运算符。

也许回顾第 1–3 章所涵盖所有内容的最佳方法之一是查看附录 B 中的井字棋程序。通过审查该程序，您可以看到将所学所有内容整合到一个完整程序中的一种方法。

