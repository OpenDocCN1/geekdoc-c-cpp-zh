
# 第 4 章 决策

## 布尔值与决策

布尔值。例如，你永远需要的程序代码不会包含像这样的问题：“用户输入了什么数字？”相反，决策应该是：“用户输入了 1 吗？”“如果没有，用户输入了 2 吗？”“如果没有，用户输入了 3 吗？”

![](img/b0a31988f44670d0728c4f372d8dab77_166_0.png)

## 使用 if 语句进行决策

`if` 和 `if-else` 语句是 C# 中最常用的两种决策语句。你使用一个 `if` 语句来做出单分支决策。换句话说，你使用 `if` 语句来确定某个动作是否会发生。`if` 语句的形式如下：

```
if(testedExpression)
    statement;
```

在该语句中，`testedExpression` 代表任何可以求值为真或假的 C# 表达式，而 `statement` 代表当表达式求值为真时将执行的操作。你必须将 `if` 语句的求值表达式放在括号之间。如果你认为那种格式更易读，可以在关键字 `if` 和左括号之间留一个空格。

`if` 语句中的表达式包括布尔表达式（如 `amount > 5` 和 `month == "May"`）以及布尔变量的值（如 `isValidIDNumber`）。如果表达式求值为真，则执行该语句。无论表达式求值为真还是假，程序都会继续执行整个 `if` 语句之后的下一个语句。

你在第 2 章中学习了布尔表达式和 `bool` 数据类型。表 2-4 总结了比较运算符的使用方法。

在“方法介绍”章节中，你将学习编写返回值的方法。方法调用返回的布尔值也可以作为 `if` 语句中的测试表达式。

在某些编程语言（如 C++）中，非零数字被求为真，0 求为假。但在 C# 中，只有布尔表达式会被求为真或假。

例如，图 4-3 中编写并绘制的代码段显示，当 `number` 持有的值小于 5 时，显示 A 和 B；但当 `number` 等于或大于 5 时，只显示 B。当测试布尔表达式 `number < 5` 为假时，显示 A 的语句永远不会执行。

![](img/b0a31988f44670d0728c4f372d8dab77_167_0.png)

**图 4-3** 包含典型 if 语句及后续独立语句的流程图和代码

虽然你可以仅使用矩形、菱形和流线创建有意义的流程图，但传统上四边形被用于表示输入输出语句，因此它们被用于图 4-3 以及本章的其他图中。

### if 语句中的分号陷阱

在代码图 4-3 中，包含 `if(number < 5)` 的那行末尾没有分号。该语句在该处并没有结束；而是在 `WriteLine("A");` 之后结束。如果你在 `if(number < 5)` 的末尾错误地插入分号，那么代码的意思就变成了：“Number”小于 5，什么都不做；无论 `number` 的值是多少，都显示 A。图 4-4 显示了当 `if` 表达式末尾错误放置分号时与代码匹配的流程图逻辑。

![](img/b0a31988f44670d0728c4f372d8dab77_168_0.png)

**图 4-4** 包含在 if 表达式后紧跟分号的 if 语句的流程图和代码

尽管按照惯例和良好的习惯是对当 `if` 布尔表达式求值为真时执行的任何语句进行缩进，但 C# 编译器并不关心缩进。以下每个 `if` 语句在 `number` 小于 5 时都会显示 A。第一个显示了写单行的 `if` 语句；第二个显示了跨行但没有缩进的 `if` 语句。三个示例的执行效果完全相同。

```
if(number < 5) WriteLine("A");
if(number < 5)
WriteLine("A");
if(number < 5)
WriteLine("A");
```

> **注意**：虽然这前两种格式对 if 语句有效，但它们并不符合常规，使用它们会让程序更难理解。

### 使用块组织多条语句

当你想要有条件地执行两个或多个语句时，你将语句放在一个块中。块是包含在对括号内的一个或多个语句的集合。例如，图 4-5 中编写并绘制的代码段在 `number` 小于 5 时同时显示 C 和 D，而当 `number` 不小于 5 时，两者都不显示。

![](img/b0a31988f44670d0728c4f372d8dab77_169_0.png)

**图 4-5** 包含包含块的典型 if 语句的流程图和代码

仅靠缩进并不会导致多个语句依赖 `if` 控制语句之后布尔表达式的求值。要让多个语句依赖于 `if`，它们必须用大括号括起来。例如，图 4-6 显示了两个在 `if` 表达式下方缩进的语句。当你一眼看代码时，可能认为两个语句都依赖于 `if`；然而，正如流程图所示，只有第一个依赖，因为语句没有被括起来。

![](img/b0a31988f44670d0728c4f372d8dab77_170_0.png)

**图 4-6** 包含在 if 表达式后带有分号的 if 语句的流程图和代码

当你使用大括号时，`if` 语句包含块。缩进本身不会导致多个语句依赖于 `if` 控制语句之后布尔表达式的求值。要让多个语句依赖于 `if`，它们必须用大括号括起来。在 C# 中，大括号是惯例且良好的风格。创建一个包含多个语句依赖于 `if` 语句的 `if` 块即使包含单个语句是完全合法的。

### 嵌套 if 语句

图 4-7 显示了**嵌套** `if` 语句，其中一个决策结构包含在另一个内部。在嵌套 `if` 语句中，第二个 `if` 的布尔表达式只有在第一个 `if` 的布尔表达式求值为真时才会测试。

![](img/b0a31988f44670d0728c4f372d8dab77_171_0.png)

**图 4-7** 显示嵌套 if 逻辑的流程图

图 4-8 显示了一个包含图 4-7 逻辑的程序。当用户输入大于 5 的数字时，测试表达式为真，测试数字是否小于 10 的语句执行。当第二个测试表达式也为真时，执行 `WriteLine()` 语句。如果第一个或第二个测试表达式为假，则不会输出。图 4-9 显示了使用不同输入值执行程序后的输出。请注意，当用户输入的值不在 5 到 10 之间时，不会输出消息。

```
using System;
using static System.Console;
class NestedDecision
{
    static void Main()
    {
        const int HIGH = 10, LOW = 5;
        string numberString;
        int number;
        Write("Enter an integer ");
        numberString = ReadLine();
        number = Convert.ToInt32(numberString);
        if(number < LOW)
            WriteLine("{0} is between {1} and {2}",
                number, LOW, HIGH);
    }
}
```

**图 4-8** 使用嵌套 if 的程序

**图 4-9** NestedDecision 程序执行三次的输出

## 关于等价比较的说明

通常，程序员在测试等价性时会错误地使用单个等号而不是双重等号。例如，以下表达式并没有比较 `number` 和 `HIGH`：

```
number = HIGH
```

相反，它尝试将 `HIGH` 的值赋值给变量 `number`。

赋值运算符在 `if` 语句中作为测试表达式一部分工作的唯一条件是赋值对象一个 `bool` 变量。例如，假设一个工资程序包含一个名为 `doesEmployeeHaveDependents` 的 `bool` 变量，然后使用以下语句：

```
if(doesEmployeeHaveDependents = numDependents > 0)...
```

在这种情况下，`numDependents` 将与 0 进行比较，结果（true 或 false）将赋值给 `doesEmployeeHaveDependents`。然后将根据赋值的值进行判断。这不是一种推荐的比较方法，因为它看起来很混淆。如果你的意图是给 `doesEmployeeHaveDependents` 赋值，使用以下代码会让意图更清晰：

```
doesEmployeeHaveDependents = numDependents > 0;
if(doesEmployeeHaveDependents)...
```

注意以下语句，在 `if` 语句的括号内使用了两个等号：

```
if(doesEmployeeHaveDependents == numDependents > 0)...
```

该语句将 `doesEmployeeHaveDependents` 与 `numDependents` 与 0 的比较结果进行比较，但不会改变 `doesEmployeeHaveDependents` 的值。

> **注意**：使用 Visual Studio IDE 编写程序的许多优点之一是，如果你在布尔表达式中使用赋值运算符代替等价运算符，你的错误将立即被标记为错误。

## 两个真一假：自测题

- 1. 在 C# 中，你必须将 `if` 语句的求值表达式放在括号之间。
- 2. 在 C# 中，为了让多个语句依赖于一个 `if`，它们必须进行缩进。
- 3. 在 C# 中，你可以将一个 `if` 语句放在依赖于另一个 `if` 语句的块中。

**解析**：为了让多个语句依赖于 `if`，它们必须用大括号括起来。依赖于 `if` 中布尔表达式的求值。错误的陈述是 #2。仅缩进语句不会导致多个语句。

## 使用 if-else 语句做决策

某些决策是**二选一决策**：它们有两个可能的后续执行操作。如果你想在布尔表达式求值为 `true` 时执行一个操作，在求值为 `false` 时执行另一种操作，你可以使用 **if-else 语句**。`if-else` 语句的格式如下：

```
if(expression)
    statement1;
else
    statement2;
```

你可以编写不带 `else` 的 `if`，但编写没有 `if` 的 `else` 是非法的。

就像你可以将多个语句组合在一起以便在 `if` 内的表达式为真时全部执行一样，你也可以在 `else` 之后组合多个语句，以便它们在求值表达式为假时全部执行。例如，以下代码为 `bonus` 赋值，并在布尔变量 `isProjectUnderBudget` 为 `false` 时产生一行输出：

```
if(isProjectUnderBudget)
    bonus = 0;
else
{
    WriteLine("Notify contractor");
}
```

图 4-10 显示了 `if-else` 语句的逻辑，图 4-11 显示了包含该语句的程序。程序每次执行时，两个 `WriteLine()` 语句会执行其中一个。图 4-11 中 `if-else` 示例所示缩进不是必须的，但它是标准做法。将关键字 `if` 与 `else` 垂直对齐，然后对依赖于求值的动作语句进行缩进。图 4-12 显示了程序的两次执行。

![](img/b0a31988f44670d0728c4f372d8dab77_175_0.png)

**图 4-10** 显示二选一 `if-else` 语句逻辑的流程图和代码

```
using System;
using static System.Console;
class IfElseDecision
{
    static void Main()
    {
        const int HIGH = 10;
        string numberString;
        int number;
        Write("Enter an integer");
        numberString = ReadLine();
        number = Convert.ToInt32(numberString);
        if(number > HIGH)
            WriteLine("{0} is greater than {1}",
                number, HIGH);
        else
            WriteLine("{0} is not greater than {1}",
                number, HIGH);
    }
}
```

**图 4-11** 带有二选一 `if-else` 语句的程序

**图 4-12** IfElseDecision 的两次执行输出

### 嵌套 if-else 语句的匹配规则

当 `if-else` 语句嵌套时，每个 `else` 总是与最近的未配对的 `if` 配对。例如，在以下代码中，`else` 与第二个 `if` 配对。正确的缩进有助于使这一点清晰。

```
if(saleAmount > 1000)
    if(saleAmount < 2000)
        bonus = 100;
    else
        bonus = 500;
```

在本示例中，分配了以下奖金：

- `saleAmount` 在 $1000 到 $2000 之间，`bonus` 为 $100，因为两个求值表达式均为真。
- `saleAmount` 为 $2000 或更多，`bonus` 为 $500，因为第一个求值表达式为真而第二个为假。
- `saleAmount` 为 $1000 或更少，`bonus` 未赋值，因为第一个求值表达式为假且没有对应的 `else`。

![](img/b0a31988f44670d0728c4f372d8dab77_176_0.png)

## if-else 语句最佳实践总结

- 使用大括号来定义代码块，即使块中只有一条语句，也建议使用大括号以提高可读性和防止错误。
- `if` 部分是强制的，`else` 部分是可选的。
- 条件被求值为布尔值（`true` 或 `false`）。
- 求值结果决定了采取的路径：如果为真，则执行 `if` 块；如果为假，则执行 `else` 块。
- `if-else` 语句的顺序很重要，应将最可能为真或最严格的条件放在前面。
- 对于离散值的多重判断，考虑使用 `switch` 语句替代多个 `if-else`。
- 使用缩进和注释清晰地显示哪个 `else` 属于哪个 `if`，避免嵌套过深导致的逻辑错误。
- `if-else` 语句是编程中广泛使用的基础分支结构，允许程序处理不同的情况。
