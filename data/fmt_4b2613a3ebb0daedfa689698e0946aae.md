
`current = 'z'`;

```
do
{
    // 获取 current 的 Unicode 值
    unicodeValue = current;
    System.Console.Write($"{current}={unicodeValue}\t");
    // 继续到字母表中的上字母
    current--;
}
while(current >= 'a');
```

输出 4.9 显示了列表 4.15 的结果。

# 输出 4.9

| z=122 | y=121 | x=120 | w=119 | v=118 | u=117 | t=116 | s=115 | r=114 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| q=113 | p=112 | o=111 | n=110 | m=109 | l=108 | k=107 | j=106 | i=105 |
| h=104 | g=103 | f=102 | e=101 | d=100 | c=99 | b=98 | a=97 | |



## 高级主题

## 线程安全的递增和递减

尽管加减运算符非常简洁，但这些运算符并不是原子的。在执行运算符期间可能会发生线程上下文切换，并导致竞态条件。你可以使用 `lock` 语句来防止竞态条件。然而，对于简单的加减，一种开销更小的方案是使用 `System.Threading.Interlocked` 类中线程安全的 `Increment()` 和 `Decrement()` 方法。这些方法依赖处理器功能来实现快速、线程安全的加减。更多细节请参阅第 19 章。

## 常数表达式和常量局部变量

第 3 章讨论了字面量，即直接嵌入到代码中的值。可以使用运算符在常量表达式中组合多个字面量。根据定义，常量表达式是指 C# 编译器可以在编译时进行求值（而不是在程序运行时进行求值）的表达式，因为它完全由常数操作数组成。常量表达式可以用于初始化常量局部变量，这允许你为常量值指定一个名称（类似于局部变量 `variables` 允许你为存储位置指定名称）。例如，一天的秒数可以是一个常量表达式，在其他表达式中通过名称使用。

列表 4.19 中的 `const` 关键字声明了一个常量局部变量。由于常量局部变量在定义上是变量的相反面——常量意味着“无法改变”——因此在代码后续修改该值的任何尝试都会导致编译错误。

### 列表 4.19：声明常量

```cs
// ...
public long Main()
{
    // 常量表达式
    const int secondsDay = 60 * 60 * 24;
    const int secondsPerWeek = secondsDay * 7;
    // 常量
    // ...
}
```

## 第 4 章：运算符与流程控制

## 指南原则

不要对任何可能随时间改变的值使用常量。π 的值和金原子中的质子数是常量；金价、你的公司名称以及程序版本号则可能会改变。

请注意，列表 4.19 中赋值给 `secondWeek` 的表达式是一个常量表达式，因为表达式中的所有操作数也是常数。

## 介绍流程控制

在本章稍后有一个代码列表（列表 4.45），展示了以二进制形式查看数字的简单方法。然而，即使是这样简单的程序，如果不使用流程控制语句也无法编写。此类语句控制程序的执行路径。本节将讨论如何根据条件检查来更改语句的执行顺序。之后，你将学习如何通过循环结构重复执行语句组。

表 4.1 列出了流程控制语句的摘要。请注意，“通用语法结构”（General Syntax Structure）一列表示常见的语句用法，而不是完整的词法结构。表 4.1 中的嵌入语句（embedded-statement）可以是除标记语句或声明外的任何语句，但通常是一个块语句。

表 4.1 中的每个 C# 流程控制语句都出现在井棋程序中，并可以在第 4 章源代码的 `TicTacToe.cs` 文件中找到（访问 https://itlc.com/EssentialCSharp.cs）。该程序显示井棋盘，提示每位玩家，并随着每次走棋进行更新。

本章的其余部分将更详细地查看每条语句。在介绍了 `if` 语句后，它引入了代码块、作用域、布尔表达式和位运算符，以继续介绍剩余的流程控制语句。由于 C# 与其他语言具有相似性而对表 4.1 熟悉的读者，可以直接跳到标题为“C# 预处理器指令”的部分，或跳到章节末尾的总结。

- 3. 在美国外的读者称为 "nought and crosses"。

### 表 4.1：流程控制语句

| 语句 | 通用语法结构 | 示例 |
| --- | --- | --- |
| if 语句 | if(boolean-expression) 嵌入语句 | if (input == "quit") { System.Console.WriteLine("game end"); return; } |
| else 语句 | if(boolean-expression) 嵌入语句 else 嵌入语句 | if (input == "quit") { System.Console.WriteLine("game end"); return; } else { } |
| while 语句 | while(boolean-expression) 嵌入语句 | while (count < total) { System.Console.WriteLine("count: " + count); count++; } |

### 表 4.1：流程控制语句（续）

| 语句 | 通用语法结构 | 示例 |
| --- | --- | --- |
| do while 语句 | while(boolean-expression); 嵌入语句 | do { System.Console.WriteLine("Enter name:"); string input = Console.ReadLine(); while (input != "exit") { // 嵌入语句 } |
| for 语句 | for(initializer; boolean-expression; for-iterator) 嵌入语句 | for (int count = 0; count < 10; count++) { System.Console.WriteLine("count: " + count); } |
| foreach 语句 | foreach(type identifier in expression) 嵌入语句 | foreach (char letter in email) { if (letter == '@') { bool insideDomain = true; continue; } } |
| continue 语句 | | continue; |

### 表 4.1：流程控制语句（续） |

| 语句 | 通用语法结构 | 示例 |
| --- | --- | --- |
| switch 语句 | switch(expression) { case constant: 语句; ... } | switch (expression) { case 1: // 语句 break; default: // 语句 } |

## if 语句

`if` 语句是 C# 中最常见的语句之一。它评估一个布尔表达式（结果为 true 或 false）。如果条件为真，则执行结果语句。它可能包含一个 `else` 子句，在条件为假时执行。其通用形式如下：

```cs
if (condition)
    consequence-statement
else
    alternative-statement
```

**列表 4.20：if/else 示例**

```cs
class TicTacToe
{
    static void Main()
    {
        string input; // 声明变量以存储输入
        System.Console.Write(
            "1 - Play against computer\n" +
            "2 - Play another player.\n" +
            "Choice:"
        );
        input = Console.ReadLine();
        if(input=="1") {
            // 用户选择了与电脑游戏
            System.Console.WriteLine("Play against computer.");
        }
        else {
            // 默认 2 人玩家（即使户没有输入 2）
            System.Console.WriteLine("Play another player.");
        }
    }
}
```

## 嵌套 if

有时代码需要多个 `if` 语句。列表 4.21 中的代码首先确定用户是否通过输入数字选择退出；如果用户没有选择退出，则检查用户是否知道最大回合数。

### 列表 4.21：嵌套 if 语句

```cs
class TicTacToeTrivia
{
    static void Main()
    {
        int input; // 声明变量以存储输入
        System.Console.Write(
            "What is the maximum number "
            "of turns in tic-tac-toe?" +
            "(Enter 0 to exit.)"
        );
        // Parse() 将 ReadLine() 的
        // 返回转换为 int 类型
        input = int.Parse(Console.ReadLine());
        if (input < 0) // 第 16 行
            // 输入小于等于 0
            System.Console.WriteLine("Exiting...");
        else
            if (input < 9) // 第 20 行
                // 输入小于 9
                System.Console.WriteLine(
                    "$Tic-tac-toe has more {input}" +
                    "maximum turns.");
            else
                if(input > 9) // 第 26 行
                    // 输入大于 9
                    System.Console.WriteLine(
                        "$Tic-tac-toe has fewer {input}" +
                        "maximum turns.");
                else
                    // 输入等于 9
                    System.Console.WriteLine( // 第 33 行
                        "Correct, tic-tac-toe " +
                        "has a maximum of 9 turns.");
    }
}
```

输出 4.13 显示了列表 4.21 的结果。

# 输出 4.13

```
What is the maximum number of turns in tic-tac-toe? (Enter 0 to exit): 9
Correct, tic-tac-toe has a maximum of 9 turns.
```

假设用户在第 14 行提示时输入了 9。以下是执行路径：

- 1. 第 16 行：检查输入是否小于 0。由于不是如此，跳转到第 20 行。
- 2. 第 20 行：检查输入是否小于 9。由于不是如此，跳转到第 26 行。
- 3. 第 26 行：检查输入是否大于 9。由于不是如此，跳转到第 33 行。
- 4. 第 33 行：显示答案正确。

列表 4.21 包含了嵌套的 `if` 语句。为了清楚嵌套关系，对代码行进行了缩进。然而，正如你在第 1 章中所学到的那样，空白并不影响执行路径。如果这段代码在编写时没有刻意使用这些换行符，其执行结果将是相同的。列表 4.22 中嵌套 `if` 语句中出现的代码等同于列表 4.21。

代码列表 4.22: 顺序格式化的 if/else 形式

```
if (input < 0)
    System.Console.WriteLine("Exiting...")
else if (input < 9)
    System.Console.WriteLine(
        "Tic-tac-toe has more {input}" +
        " maximum turns.")
else if (input < 9)
    System.Console.WriteLine(
        "Tic-tac-toe has less than {input}" +
        " maximum turns.")
else
    System.Console.WriteLine(
        "Correct, tic-tac-toe has a maximum " +
        " of 9 turns.")
```

虽然后者的格式更为常见，但在任何情况下你都应该使用使代码最清晰的格式。

这两个 `if` 列表都省略了大括号。然而，接下来的讨论将说明，这并不符合指南 true。指南建议使用代码块，也许在最简单的单行场景下除外。

## 代码块 ({})

在之前的 `if` 语句示例中，`if` 和 `else` 后面只跟了一个语句：单个 `System.Console.WriteLine()`，类似于列表 4.23。

### 列表 4.23: 无代码块的 if 语句

```
if(input < 9)
System.Console.WriteLine("Exiting");
```

然而，通过大括号，我们可以将多个语句组合成单一语句，称为**块语句**或**代码块**，允许将多个语句分组为一个作为结果的单一语句。以列表 4.24 中半径计算中高亮的代码块为例。

### 列表 4.24: 紧跟代码块的 if 语句

```
class CircleAreaCalculator
{
    static void Main()
    {
        double radius; // 声明一个存储半径的变量
        double area; // 声明一个存储面积的变量
        System.Console.WriteLine("Enter the radius of the circle:");
        // double.Parse 将 ReadLine() 
        // 返回转换为 double
        radius = double.Parse(System.Console.ReadLine());
        if (radius > 0)
        {
            // 计算圆的面积
            area = Math.PI * radius;
            System.Console.WriteLine(
$"The area of the circle is: { area : 0.00}");
        }
        else
        {
            System.Console.WriteLine(
$"{ radius } is not a valid radius.");
        }
    }
}
```

输出 4.14 显示了列表 4.24 的结果。

### 输出 4.14

```
Enter the radius of the circle: 3
The area of the circle is: 28.27
```

在这个示例中，`if` 语句检查半径是否为正。计算并显示圆的面积；否则，显示无效半径的提示。

注意，在这个示例中，第一个 `if` 后面跟着两个语句。然而，这两个语句都出现在大括号内。

在这个示例中，第一个 `if` 后面跟着两个语句。然而，这两个语句都出现在大括号内。

在这个示例中，第一个 `if` 后面跟着两个语句。然而，这两个语句都出现在大括号内。

### 列表 4.25: 依赖缩进的错误代码

```
if (input < 0)
    . = .
System.Console.WriteLine(
    "
 of of is is  ..0)
```

在这个示例中，第一个 `if` 后面跟着两个语句。然而，这两个语句都出现在大括号内。

### 列表 4.26: 使用大括号的 if 语句

```
if (input < 0)
{
    area = Math.PI * radius;
}
System.Console.WriteLine(
    "The area of the circle is: " + area);
```
