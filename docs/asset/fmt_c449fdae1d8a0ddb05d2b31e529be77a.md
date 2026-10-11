
尽管列表 4.20 中的 `announcement` 是一个插值字符串，但字符串代码部分中的值也是常量，这允许编译器在编译时对它们求值，而不是等到执行时间。然而，请注意 `windspeed` 是一个字符串而不是整数。常量字符串插值在仅由其他常量字符串形成时有效，而不是由其他数据类型（即使这些类型是常量）。这种限制是为了允许字符串在运行时考虑文化差异。例如，将黄金比例转换为字符串可能是 1.6180339887 或 1,6180339887，取决于文化设置。

## 介绍流程控制

本章稍后的部分有一个代码列表（列表 4.46），展示了以二进制形式查看数字的简单方法。然而，即使是这样简单的程序，如果不使用控制流语句也编写。此类语句控制程序的执行路径。本节讨论了如何根据条件检查更改语句的执行顺序。稍后你将学习如何通过循环结构重复执行语句组。

流程控制语句的摘要出现在表 4.1 中。请注意，“通用语法结构”列表示的是常用用法，而不是完整的词法结构。表 4.1 中的“嵌入语句”可以是除标记语句或声明以外的任何语句，正如本节后面所示，它通常是多个语句组合成一个代码块。

### 表 4.1：流程控制语句

| 语句 | 通用语法结构 | 示例 |
| :--- | :--- | :--- |
| if 语句 | `if(boolean-expression) embedded-statement` | `if (input == "quit") { Console.WriteLine("Game end"); return; }` |
| | `if(boolean-expression) embedded-statement else embedded-statement` | `if (input == "quit") { Console.WriteLine("Game end"); return; } else GetNextMove(); }` |
| while 语句 | `while(boolean-expression) embedded-statement` | `while (count < total) { Console.WriteLine($"{count - {count}"); count++; }` |
| do while 语句 | `do embedded-statement while(boolean-expression);` | `do { Console.WriteLine("Enter name:"); input = Console.ReadLine(); } while(input != "exit");` |

### 表 4.1：流程控制语句（续表）

| 语句 | 通用语法结构 | 示例 |
| :--- | :--- | :--- |
| for 语句 | `for(for-iterator; boolean-expression; for-iterator embedded-statement)` | `for (int count = 1; count <= 10; count++) { Console.WriteLine($"{count = {count}"); }` |
| foreach 语句 | `foreach(type identifier in expression) {` | `foreach (letter in expression) { if (insideDomain) { continue; } }` |
| continue 语句 | `continue` | |
| switch 语句 | `switch(expression) { }` | `switch (input) { case "exit": Console.WriteLine("Exiting..."); break; case "start": GetMove(); break; default: Console.WriteLine(input); break; }` |
| break 语句 | `break` | |
| goto 语句 | `goto label;` | |

```cs
// 输入小于或等于 0
Console.WriteLine("Exiting...");
else
// 条件 2.
if (input < 9) // line 20
// 输入小于 9
Console.WriteLine(
  "$Tic-tac-toe has more than {input}" + 
  " maximum turns.");
else
// 条件 3.
if (input > 9) // line 26
// 输入大于 9
Console.WriteLine(
  "$Tic-tac-toe has fewer {input}" + 
  " maximum turns.");
// 条件 4.
else
// 输入等于 9
Console.WriteLine(
  "Correct, tic-tac-toe has a maximum of 9 turns.");
```

### 4.13

井棋游戏的最大步数是多少？（输入 0 退出）：
9
答得正确，井棋游戏最多有 9 步。

假设用户在第 14 行提示时输入了 9。以下是执行路径：

- 条件 1：检查输入是否小于 0。由于不是如此，跳转到条件 2。
- 条件 2：检查输入是否小于 9。由于不是如此，跳转到条件 3。
- 条件 3：检查输入是否大于 9。由于不是如此，跳转到条件 4。
- 条件 4：显示答案正确。

列表 4.22 包含了嵌套的 if 语句。为了清楚嵌套关系，这些行进行了缩进处理。然而，正如你在第 1 章中所学的，空白不会影响执行路径。如果编写这段代码时不进行缩进且不换行，其执行结果将是相同的。列表 4.23 中嵌套 if 语句中的代码与列表 4.22 等效。

### 列表 4.23: 顺序格式化的 if/else 形式

```cs
if (input < 0)
    Console.WriteLine("Exiting...");
else if (input < 9)
    Console.WriteLine(
        "$Tic-tac-toe has more than {input}" +
        " maximum turns.");
else if (input > 9)
    Console.WriteLine(
        "$Tic-tac-toe has less than {input}" +
        " maximum turns.");
else
    Console.WriteLine(
        "Correct, tic-tac-toe has a maximum" +
        " of 9 turns.");
```

虽然后一种格式更为常见，但在任何情况下你都应该使用使代码最清晰的格式。

这两个 if 语句列表都省略了大括号。然而，正如接下来讨论的，这并不符合指南。指南提倡使用代码块，除非是在最简单的单行场景下。

### 代码块 ({})

在上一个 if 示例中，只有一个语句跟在 if 和 else 后面：即一个单一的 `System.Console.WriteLine()`，类似于列表 4.24。

### 列表 4.24: 无代码块的 if 语句

```cs
if (input < 9)
    Console.WriteLine("Exiting")
```

# 第 4 章：运算符与控制流

然而，通过大括号，我们可以将语句组合成一个单一语句，称为块语句或代码块，允许将多个语句分组为一个语句，从而产生相应的结果。例如列表 4.25 半径计算中高亮的代码块，对应输出 4.14。

### 列表 4.25: 后面跟着代码块的 if 语句

```cs
double radius; // 定义一个用于存储半径的变量
double area; // 定义一个用于存储面积的变量
Console.Write("Enter the radius of the circle: ");
// double.Parse 将 ReadLine()
// 返回值转换为 double
string temp = Console.ReadLine();
radius = double.Parse(temp);
if(radius >= 0)
{
    // 计算面积
    area = Math.PI * radius * radius;
    Console.WriteLine($"The area is: {area}");
}
else
{
    Console.WriteLine("Invalid radius.");
}
```

## 语言对比：C++—局部变量的作用域

在 C++ 中，在块中声明的局部变量的作用域从声明点一直持续到块的结束。尝试在声明之前引用该局部变量将无法找到该变量，因为它不在作用域内。如果“作用域内”有另一个同名的对象，C++ 语言会将该名称解析为该对象，这可能不是你想要的结果。在 C# 中，规则在细微上略有不同：局部变量在它被声明的整个块中都具有作用域，但在其声明之前之前引用该局部变量是非合法的。也就是说，尝试查找该局部变量的操作将成功，但该用法将被视为一个错误。这只是 C# 众多规则之一，旨在防止 C++ 程序中常见的错误。

## 布尔表达式

`if` 语句中圆括号内的条件是一个布尔表达式。在列表 4.29 中，该条件被高亮显示了。

### 列表 4.29：布尔表达式

```csharp
if (input < 9)
{
    // 输入小于 9
    Console.WriteLine("$Tic-tac-toe has more than {input}" + "maximum turns.");
}
// ...
```

布尔表达式出现在许多控制流语句中。它们的关键特征是始终求值为真（true）或假（false）。为了让 `input < 9` 允许作为布尔表达式，它必须产生一个 `bool` 类型的结果。编译器不允许 `x = 42`，因为这个表达式赋值了 `x` 并返回了被赋值的值，而不是检查变量的值是否为 42。

## 语言对比：C++—误用 = 代替 ==

C# 消除了 C 和 C++ 中常见的一种编码错误。在 C++ 中，列表 4.30 是允许的。

### 列表 4.30：C++ 允许，但 C# 不允许将赋值作为条件

```csharp
if (input = 9) // 在 C++ 中允许，在 C# 中不允许
System.Console.WriteLine("Correct, tic-tac-toe has a maximum of 9 turns.");
```
