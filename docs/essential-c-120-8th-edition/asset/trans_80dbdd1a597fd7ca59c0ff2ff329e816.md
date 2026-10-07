

> 在 C、C++ 和 C# 之间迁移使用递增和减运算符的代码时，请务必小心；C 和 C++ 的实现不需要遵循与 C# 相同的规则。

# 高级主题

## 线程安全的递增与递减

尽管递增和减运算符非常简洁，但这些运算符并不是原子的。在执行运算符期间可能会发生线程切换，并导致竞态条件。你可以使用 `lock` 语句来防止竞态条件。然而，对于简单的加减，开销较小的替代方案是使用 `System.Threading.Interlocked` 类中线程安全的 `Increment()` 和 `decrement()` 方法。这些方法依赖处理器功能来执行快速、线程安全的加减。更多细节请参见第 19 章。

## 常量表达式与常量局部变量

第 3 章讨论了字面量，即直接嵌入代码中的值。可以使用运算符在常量表达式中组合多个字面量值。根据定义，常量表达式是指 C# 编译器可以在编译时求值（而不是在程序运行时求值）的表达式，因为它完全由常量操作数组成。常量表达式可以用于初始化常量局部变量，这允许你为常量值命名（类似于局部变量允许你为存储位置命名）。例如，一天中秒数的计算可以是一个常量表达式，并通过名称在其他表达式中使用。

列表 4.19 中的 `const` 关键字声明了两个常量局部变量：`secondsPerDay` 和 `secondsPerWeek`。由于常量局部变量根据定义是变量的对面——常量意味着“无法改变”——因此在代码后面任何修改该值的尝试都将导致编译错误。

列表 4.19：声明常量

```cs
const int secondsDay = 60 * 60 * 24;
const int secondsPerWeek = secondsDay * 7;
```

## 指南

不要对任何可能随时间变化的值使用常量。圆周率 pi 的值和金原子中质子的数量是常量；金价和你的程序版本号则可能会改变。

在列表 4.19 中，`60 * 60 * secondsDay * 7` 都是常量表达式。请注意，赋值给 `secondsPerWeek` 的表达式是一个常量表达式，因为表达式中的所有操作数也是常量。

C# 10 支持常量插值字符串，如果插值字符串仅由其他常量字符串组成，则可以定义常量插值字符串。

列表 4.20：非数值类型使用二元运算符

```cs
const string windSpeed = "42";
const string announcement = $"""
华盛顿原本的塔科马桥
被风速 { windSpeed } 英/小时的风摧毁。
""";
Console.WriteLine(announcement);
```

尽管列表 4.20 中的 `announcement` 是一个插值字符串，但字符串代码部分中的值也是常量，这允许编译器在编译时对它们求值，而不是等到执行时间。然而，请注意 `windspeed` 是一个字符串而不是整数。常量字符串插值在仅由其他常量字符串形成时有效，而不是由其他数据类型（即使这些类型是常量）。这种限制是为了允许字符串在运行时考虑文化差异。例如，将黄金比例转换为字符串可能是 1.6180339887 或 1,6180339887，取决于文化设置。

## 介绍流程控制

本章稍后的部分有一个代码列表（列表 4.46），展示了以二进制形式查看数字的简单方法。然而，即使是这样简单的程序，如果不使用控制流语句也编写。此类语句控制程序的执行路径。本节讨论了如何根据条件检查更改语句的执行顺序。稍后你将学习如何通过循环结构重复执行语句组。

流程控制语句的摘要出现在表 4.1 中。请注意，“通用语法结构”列表示的是常用用法，而不是完整的词法结构。表 4.1 中的“嵌入语句”可以是除标记语句或声明以外的任何语句，正如本节后面所示，它通常是多个语句组合成一个代码块。

## 表 4.1：流程控制语句

| 语句 | 通用语法结构 | 示例 |
| :--- | :--- | :--- |
| if 语句 | `if(boolean-expression) embedded-statement` | `if (input == "quit") { Console.WriteLine("Game end"); return; }` |
| | `if(boolean-expression) embedded-statement else embedded-statement` | `if (input == "quit") { Console.WriteLine("Game end"); return; } else GetNextMove(); }` |
| while 语句 | `while(boolean-expression) embedded-statement` | `while (count < total) { Console.WriteLine($"{count - {count}"); count++; }` |
| do while 语句 | `do embedded-statement while(boolean-expression);` | `do { Console.WriteLine("Enter name:"); input = Console.ReadLine(); } while(input != "exit");` |

## 表 4.1：流程控制语句（续表）

| 语句 | 通用语法结构 | 示例 |
| :--- | :--- | :--- |
| for 语句 | `for(for-iterator; boolean-expression; for-iterator embedded-statement)` | `for (int count = 1; count <= 10; count++) { Console.WriteLine($"{count = {count}"); }` |
| foreach 语句 | `foreach(type identifier in expression) {` | `foreach (letter in expression) { if (insideDomain) { continue; } }` |
| continue 语句 | `continue` | |
| switch 语句 | `switch(expression) { }` | `switch (input) { case "exit": Console.WriteLine("Exiting..."); break; case "start": GetMove(); break; default: Console.WriteLine(input); break; }` |
| break 语句 | `break` | |
| goto 语句 | `goto label;` | |

