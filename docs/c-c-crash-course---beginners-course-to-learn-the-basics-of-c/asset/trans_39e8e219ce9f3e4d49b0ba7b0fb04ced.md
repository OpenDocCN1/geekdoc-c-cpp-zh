

## 语句

既然你已经知道如何使用比较运算符和逻辑运算符，现在我们来讨论条件语句的创建。这些语句是强大的工具，可以帮助你实现编程逻辑。

### If 语句

if 语句的语法如下：

```csharp
if (the conditional expression)
{
    The if statement’s body;
}
```

如你所见，该语法包含三个不同的部分：

1. “if”子句——这部分表示“if”语句的开始。
2. 布尔表达式——这部分可以包含一个逻辑表达式或一个保存布尔数据的变量。与 C 语言不同，C# 不接受整数表达式作为其条件语句。
3. 语句体——你需要用一对花括号将这部分括起来。C# 允许你在这一部分中放置多条语句。

如果布尔表达式的计算结果为 true，程序将运行语句体。如果计算结果为 false，程序将忽略语句体并将控制权传递给后续代码块。下面给出的示例将向你展示“if”语句是如何工作的：

```csharp
Console.WriteLine("Please enter a number.");
int number1 = int.Parse(Console.ReadLine());

int number2 = 0;
if (number1 > number2)
{
    Console.WriteLine("C# is an excellent programming language.");
}
```

这段代码要求用户提供一个数字。如果用户输入的值大于零，程序将在命令提示符中打印“C# is an excellent programming language.”。

重要提示：如果你的条件语句体只有一行，则可以省略花括号。请查看下面的示例：

```csharp
int x = 10;
if (x > 0)
    System.Console.WriteLine("This variable holds a positive number.");
```

### If-Else 语句

与其他编程语言一样，C# 支持“if-else”条件语句。在编写 if-else 语句时，应使用以下语法：

```csharp
if (the Boolean variable or expression)
{
    The conditional statement’s body;
}
else
{
    The else statement’s body;
}
```

上述语法由以下几个部分组成：

- “if”子句——这部分开始条件语句。
- 布尔表达式或变量——该表达式的值决定了程序将使用的代码。
- 条件语句体——可以是单条语句或一组语句。如果使用多条语句，请将它们括在一对花括号内。
- “else”关键字——这是一个 C# 关键字，用于触发“else”子句。
- else 子句体——这与条件语句体相同（见上文）。

在处理 if-else 语句时，计算机程序会分析括号内的值。该值必须是布尔值（即 true 或 false）。如果值为“true”，程序将执行条件语句体并忽略“else”子句。然而，如果值为 false，程序将运行 else 语句体。分析下面的示例：

```csharp
int a = 100;
if (a != 50)
{
    Console.WriteLine("The variable is not equal to 50");
}
else
{
    Console.WriteLine("The variable is equal to 50");
}
```

你可以将这段代码解释为：如果 a != 50，控制台将打印：“The variable is not equal to 50”。另一方面，如果 a == 50，控制台将显示：“The variable is equal to 50”。由于名为 a 的变量保存的是 100，你的命令提示符将显示：

```csharp
Console.WriteLine("a is equal to b");
}
}
```

### Switch-Case 语句

程序员在可能答案很多的情况下使用 switch-case 语句。以下是 switch-case 语句的语法：

```csharp
switch (selector)
{
    case first_integer:
        statements;
        break;
    case second_integer:
        statements;
        break;
    default:
        statements;
        break;
}
```

基本上，选择器是返回可用值（即你可以比较或处理的值）的表达式。“switch”关键字将选择器的值与各个“case”进行比较。如果选择器的值与某个 case 匹配，则分配给该 case 的语句将运行。然而，如果没有匹配项，程序将执行 default 语句（如果有）。这意味着程序在运行任何语句之前会先分析选择器。

重要提示：确保各个 case 的值是唯一的。如果两个或更多 case 共享相同的值，你的程序将产生不理想的结果。

如你所见，每个 case 都有一个“break”子句。“break”子句会终止其所属 case 的语句体。C# 要求你在所有 switch 语句中添加该子句。

你不必把“default”部分放在 switch-case 语句的末尾。然而，如果你希望保持代码的可读性，建议采用这种位置。

## 第7章：循环语句

本章将教你如何使用循环语句。作为程序员，你会使用循环语句来重复运行某些代码块。循环在 C# 编程中扮演着重要的角色。因此，如果你想在 7 天内掌握这门语言，也应认真研读这一部分的内容。

### 循环——基础知识

在创建程序时，你经常需要多次执行代码序列。多次输入相同的代码块会非常枯燥。因此，你需要找到一种快速简便的方法来重复代码。幸运的是，C# 语言支持循环语句。

循环是一种重复运行代码片段的工具。你可以使用它来让代码运行特定的次数，或者只要给定条件得到满足就持续运行。C# 提供了不同类型的循环语句。让我们详细分析每种类型：

### While 循环

这是 C# 中最简单的循环语句。其语法如下：

```csharp
while (the_assigned_condition)
{
    the_loop_body;
}
```

在此语法中，“the_assigned_condition”是一个产生布尔值的表达式。该条件决定了“语句体”将运行多少次。另一方面，“语句体”是你要执行的语句（或语句组）。

下面给出的图示将说明 while 循环的工作原理：

![](img/e2e831cc76860601d1e5511399855ee6_41_0.png)

在处理“while”循环时，C# 程序会检查布尔表达式的值。如果值为“true”，程序将运行循环体内的所有语句。然后，程序会再次检查布尔表达式以查看其值。如果值仍然为 true，程序将重新运行循环体并回到第一步（即检查表达式的值）。此过程将持续进行，直到布尔表达式的计算结果为 false。一旦发生这种情况，程序将处理紧接在循环之后的代码块。

重要提示：如果布尔表达式为 false，你的 C# 程序将不会运行 while 循环体。因此，如果在程序启动时布尔值为 false，那么循环内的语句将永远不会执行。

下面的示例将说明 while 循环是如何工作的：

```csharp
int timer = 10;
while (timer >= 0)
{
    System.Console.WriteLine("Time remaining: " + timer);
    timer--;
}
```

如果你编译并执行这段代码，命令提示符将打印以下数据：

```
Time remaining: 10
Time remaining: 9
Time remaining: 8
Time remaining: 7
Time remaining: 6
Time remaining: 5
Time remaining: 4
Time remaining: 3
Time remaining: 2
Time remaining: 1
Time remaining: 0
```

### Break 运算符

你可以使用“break”（一个 C# 运算符）来提前退出循环。如果程序员不想等待循环自然终止，就会使用这个运算符。基本上，循环一旦遇到 break 运算符就会结束。这种情况会迫使程序跳转到循环之后的代码片段。

在 C# 中，你只能在该运算符位于循环体内时使用它。这意味着“break”只在循环运行期间起作用。

### Do-While 循环

do-while 循环与 while 循环几乎相同。这两者之间唯一的区别是

