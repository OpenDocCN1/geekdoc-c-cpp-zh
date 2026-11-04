
```csharp
10  Console.WriteLine("Welcome\nto\nC#\nProgramming!");
11 } // end Main
12 } // end class Welcome3
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_89_0.png)

**图 3.11** | 用单条语句显示多行。

此应用的大部分内容与图 3.1 和图 3.10 中的应用相同，因此这里只讨论更改之处。第 2 行

```csharp
// Displaying multiple lines with a single statement.
```

说明了此应用的目的。第 5 行开始 Welcome3 类声明。

```csharp
Console.WriteLine("Welcome\nto\nC#\nProgramming!");
```

在控制台窗口中显示四行独立的文本。通常，字符串中的字符会完全按照它们在双引号中出现的样子显示。但请注意，两个字符 `\` 和 n（在该语句中重复三次）不会显示在屏幕上。反斜杠（`\`）称为转义字符。它向 C# 表明字符串中存在一个“特殊字符”。当字符串中出现反斜杠时，C# 会将下一个字符与反斜杠组合成转义序列。

| 转义序列 | 描述 |
| --- | --- |
| `\n` | 换行。将屏幕光标定位到下一行的开头。 |
| `\t` | 水平制表符。将屏幕光标移动到下一个制表位。 |
| `\"` | 双引号。用于在字符串中放置双引号字符（"）——例如，`Console.Write("\"in quotes\"");` 显示 "in quotes"。 |
| `\r` | 回车。将屏幕光标定位到当前行的开头——不会将光标推进到下一行。回车后输出的任何字符都会覆盖该行之前输出的字符。 |
| `\\` | 反斜杠。用于在字符串中放置反斜杠字符。 |

**图 3.12** | 常见转义序列。

## 3.5 字符串内插

许多程序会将数据格式化为字符串。C# 6 引入了一种称为字符串内插的机制，使你能够在字符串字面量中插入值来创建格式化字符串。图 3.13 演示了这一能力。

```csharp
 1 // Fig. 3.13: Welcome4.cs
 2 // Inserting content into a string with string interpolation.
 3 using System;
 4
 5 class Welcome4
 6 {
 7     // Main method begins execution of C# app
 8     static void Main()
 9     {
10         string person = "Paul"; // variable that stores the string "Paul"
11         Console.WriteLine($"Welcome to C# Programming, {person}!");
12     } // end Main
13 } // end class Welcome4
```

```text
Welcome to C# Programming, Paul!
```

**图 3.13** | 使用字符串内插将内容插入字符串。

### 声明 string 变量 person

第 10 行

```csharp
string person = "Paul"; // variable that stores the string "Paul"
```

是一条变量声明语句（也称为声明），它指定此应用中使用的变量的名称（person）和类型（string）。变量在使用前要用名称和类型声明：

- 变量的名称使应用能够访问内存中对应的值——名称可以是任何有效标识符。（有关标识符命名要求，请参见 3.2 节。）
- 变量的类型指定内存中该位置存储何种信息。string 类型的变量存储基于字符的信息，例如

```text
Enter first integer: 45
Enter second integer: 72
Sum is 117
```

**图 3.14** | 显示从键盘输入的两个数之和。

第 5 行

```csharp
class Addition
```

开始 Addition 类的声明。请记住，每个类声明的主体以左花括号（第 6 行）开始，并以右花括号（第 26 行）结束。应用从 Main（第 8—25 行）开始执行。

### 3.6.1 声明 int 变量 number1

第 10 行

```csharp
int number1; // declare first number to add
```

是一条变量声明语句，指定 number1 的类型为 int——它将保存整数值（整数，例如 7、–11、0 和 31914）。int 的取值范围是 –2,147,483,648（int.MinValue）到 +2,147,483,647（int.MaxValue）。我们很快会讨论 float、double 和 decimal 类型，用于指定带小数点的数字（如 3.4、0.0 和 –11.19），以及 char 类型，用于指定字符。float 和 double 类型的变量在内存中存储实数的近似值。decimal 类型的变量精确存储带小数点的数字（精确到 28—29 位有效数字），因此 decimal 变量常用于货币计算——我们在第 4 章的 Account 类中使用 decimal 类型表示余额。char 类型的变量表示单个字符，例如大写字母（例如 A）、数字（例如 7）、特殊字符（例如 * 或 %）或转义序列（例如换行字符 `\n`）。int、float、double、decimal 和 char 等类型称为简单类型。简单类型名称是关键字，必须全部使用小写字母。附录总结了简单类型（bool、byte、sbyte、char、ushort、int、uint、long、ulong、float、double 和 decimal）的特征，包括存储每种类型的值所需的内存量。

### 3.6.2 声明变量 number2 和 sum

第 11—12 行的变量声明语句

```csharp
int number2; // declare second number to add
int sum; // declare sum of number1 and number2
```

将变量 number2 和 sum 声明为 int 类型。

> **良好编程实践 3.6**
> 将每个变量声明在单独的一行。这种格式便于在每条声明旁边插入注释。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_93_0.png)

> **良好编程实践 3.7**
> 按照惯例，变量名标识符以小写字母开头，名称中第一个单词之后的每个单词都以大写字母开头（例如 firstNumber）。这种命名约定称为驼峰命名法。

### 3.6.3 提示用户输入

第 14 行

```csharp
Console.Write("Enter first integer: "); // prompt user
```

使用 Console.Write 提示用户输入。

### 3.6.4 将值读入变量 number1

第 16 行

```csharp
number1 = int.Parse(Console.ReadLine());
```

分两步工作。首先，它调用 Console 的 ReadLine 方法，该方法等待用户在键盘上输入一串字符并按 Enter 键。如前所述，有些方法会执行任务，然后返回该任务的结果。在本例中，ReadLine 返回用户输入的文本。然后，返回的字符串被用作 int 类型的 Parse 方法的参数，该方法将这串字符转换为 int 类型的数据。

**可能的错误用户输入**

从技术上讲，用户可以将任何内容作为输入值键入。ReadLine 会接受它，并将其传递给 int 的 Parse 方法。该方法假定字符串包含有效的整数值。在这种情况下，如果用户键入非整数值，就会发生称为异常的运行时逻辑错误，应用将终止。你将在第 16 章学习的字符串处理技术可用于在尝试将字符串转换为 int 之前检查输入格式是否正确。C# 还提供了一种称为异常处理的技术，它使应用能够处理异常并继续执行，从而帮助你使应用更健壮。这也称为使应用具有容错能力。我们在 8.5 节介绍异常处理，然后在第 10 章再次使用它。我们将在第 13 章以及全书更深入地研究异常处理。

**将值赋给变量**

在第 16 行中，通过使用赋值运算符 =，将调用 int 的 Parse 方法的结果（一个 int 值）放入变量 number1。该语句读作“number1 获取 int.Parse 返回的值”。运算符 = 是二元运算符，因为它处理两条信息。这些信息称为它的操作数——在本例中，是 number1 和调用 int.Parse 的结果。该语句称为赋值语句，因为它将值赋给变量。赋值运算符 = 右侧的所有内容总是在执行赋值之前求值。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_93_1.png)

> **良好编程实践 3.8**
> 在二元运算符两侧各放一个空格，使代码更具可读性。

