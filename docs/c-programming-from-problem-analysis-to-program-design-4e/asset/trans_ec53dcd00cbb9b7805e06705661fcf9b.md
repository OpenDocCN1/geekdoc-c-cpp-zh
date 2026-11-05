
```
if (conditional_expression) // No semicolon is placed on this line
    statement;               // Could be another if statement
else
    statement;               // Could be another if statement
```

在嵌套的 if...else 中，内部的 if 语句被称为嵌套在外部的 if 内部。然而，内部的 if 也可能包含另一个 if 语句。嵌套的深度没有限制。限制在于你和其他人是否能够阅读并理解你的代码。优秀程序的标志在于其可读性。

当你设计一个需要嵌套 if...else 的解决方案时，有时如果将不同的选项图形化地映射出来，开发算法会更容易。可以采用流程图。另一个选择是决策树，这是一种设计工具，可让你直观地表示复杂流程。节点用于表示决策点，而线条从节点分支出来，表示进一步的条件，或最终基于左侧表达的条件应采取的行动。图 5-7 显示了用于计算小时工和薪资员工奖金的决策树。每周工作超过 40 小时的小时工可获得 $500。其他小时工获得 $100。受雇超过 10 年的薪资员工可获得 $300，而其他员工则获得 $200。图 5-7 以决策树的形式说明了这种情况。

![](img/36e48639a06772bcb0fa1ea2525b33a3_313_0.png)

## 图 5-7 奖金决策树

示例 5-14 显示了如何使用嵌套 if...else 来确定图 5-7 中说明的奖金金额。

## 示例 5.14

```text
// For hourlyEmployees working more than 40 hours, a bonus of $500
// is issued. If hourlyEmployees has not worked more than 40 hours,
// issue a bonus of $100. For those non-hourlyEmployees, issue a
// $300 bonus if they have been employed longer than 10 years;
// otherwise, issue a $200 bonus.
bool hourlyEmployee;
double hours,
       bonus;
int yearsEmployed;

if (hourlyEmployee)
    if (hours > 40)
        bonus = 500;
    else
        bonus = 100;
else
    if (yearsEmployed > 10)
        bonus = 300;
    else
        bonus = 200;
```

在第一个条件表达式中不需要相等运算符。那是因为使用了布尔变量 hourlyEmployee。

示例 5-14 的逻辑也可以用四个单向 if 语句编写，如示例 5-15 所示。这里，每个语句都使用 && 运算符。

## 示例 5.15

```text
if (hourlyEmployee && hours > 40)
    bonus = 500;
if (hourlyEmployee && hours <= 40)
    bonus = 100;
if ((!hourlyEmployee) && yearsEmployed > 10)
    bonus = 300;
if ((!hourlyEmployee) && yearsEmployed <= 10)
    bonus = 200;
```

示例 5-14 中的单个嵌套 if...else 解决方案比示例 5-15 中的四个语句更高效。在示例 5-15 中，即使第一个语句求值为 true，也会评估所有语句。在示例 5-14 中，当前两个行求值为 true 时，500 会被赋给 bonus，并且不会执行额外的求值。

注意，使用逻辑 && 编写的语句如何可以重写为嵌套 if...else。

```text
if (hourlyEmployee && hours > 40)
```

与以下结果相同

```text
if (hourlyEmployee)
    if (hours > 40)
```

当编程嵌套 `if...else` 语句时，了解哪个 `else` 与哪个 `if` 语句匹配非常重要。匹配或配对 else 的规则是，`else` 与最近的、尚未拥有自己的 `else` 的前一个 `if` 配对。通过正确地将 `else` 子句与其对应的 `if` 子句对齐，你会遇到更少的需要调试的逻辑错误。示例 5–16 说明了正确对齐 `if` 和 `else` 子句的重要性。你能将每个 `else` 与正确的 `if` 匹配吗？

## 示例 5.16

```text
if (aValue > 10)                 Line 1
if (bValue == 0)                 Line 2
amount = 5;                      Line 3
else                             Line 4
if (cValue > 100)                Line 5
if (dValue > 100)                Line 6
amount = 10;                     Line 7
else                             Line 8
amount = 15;                     Line 9
else                             Line 10
amount = 20;                     Line 11
else                             Line 12
if (eValue == 0)                 Line 13
amount = 25;                     Line 14
```

如示例 5–17 所示，第 12 行的 `else` 与第 1 行的 `if` 匹配；第 10 行与第 5 行匹配。如果 aValue、bValue、cValue、dValue 和 eValue 全部等于 0，将存储在 amount 中的值是多少？你追踪逻辑时得到 25 吗？请看示例 5–17。通过正确地将 `else` 子句与其对应的 `if` 子句对齐，答案可以更快地确定。

## 示例 5.17

```text
if (aValue > 10)                 Line 1
    if (bValue == 0)             Line 2
        amount = 5;              Line 3
    else                         Line 4
        if (cValue > 100)        Line 5
            if (dValue > 100)    Line 6
                amount = 10;     Line 7
            else                 Line 8
                amount = 15;     Line 9
        else                     Line 10
            amount = 20;         Line 11
else                             Line 12
    if (eValue == 0)             Line 13
        amount = 25;              Line 14
```

规则指出，`else` 与最近的前一个尚未附加 `else` 的 `if` 匹配。然而，你可以使用大括号将 `else` 附加到外部 `if`，如示例 5–18 所示。

## 示例 5.18

```c
if (average > 59)
{
    if (average < 71)
        grade = 'D';
}
else
    grade = 'F';
```

大括号括起了与表达式 of (average > 59) 关联的 `true` 语句。当遇到闭合大括号时，内部 `if` 语句作为语句结束。

请考虑示例 5–19 中基于测试 average 值确定等级的语句。

## 示例 5.19

```c
if (average > 89)
    grade = 'A';
else
    if (average > 79)
        grade = 'B';
    else
        if (average > 69)
            grade = 'C';
        else
            if (average > 59)
                grade = 'D';
            else
                grade = 'F';
```

请特别注意示例 5–19 中的条件表达式。第二个表达式不需要使用 && 的复合表达式。你不必写 `if (average > 79 && average <= 89)`。请确保你理解，除非第一个表达式为 `false`，否则执行永远不会到达表达式 `(average > 79)`。如果平均值不大于 89，它必须等于 89 或小于 89。

当你回顾示例 5–17 和 5–19 时，你可能会想知道当你不断缩进时会发生什么。你的语句很快就会向右偏移，超出视野。

许多程序员用来解决此问题的方法是，当他们有一个长嵌套的多路语句时，编写一系列 `else...if` 语句。

示例 5–19 中的行可以用一系列 `else...if` 语句编写，如示例 5–20 所示。这可以防止缩进问题。

## 示例 5.20

```csharp
if (average > 89)
    grade = 'A';
else if (average > 79)
    grade = 'B';
else if (average > 69)
    grade = 'C';
else if (average > 59)
    grade = 'D';
else
    grade = 'F';
```

示例 5–19 和 5–20 是多路 `if` 语句。单个变量使用关系运算符进行测试。

嵌套 `if...else` 语句也可以使用条件表达式中的相等运算符编写。请考虑示例 5–21，该示例基于测试保存表示日期的数字的整数变量来显示星期几名称。

## 示例 5.21

```csharp
if (weekDay == 1)
    Console.WriteLine("Monday");
else if (weekDay == 2)
    Console.WriteLine("Tuesday");
else if (weekDay == 3)
    Console.WriteLine("Wednesday");
else if (weekDay == 4)
    Console.WriteLine("Thursday");
else if (weekDay == 5)
    Console.WriteLine("Friday");
else
    Console.WriteLine("Not Monday through Friday");
```

当你有一个单个变量，例如 weekDay，被测试为等于四个或更多值时，可以使用 `switch` 语句。示例 5–20 中介绍的嵌套 `if...else` 解决方案不是 `switch` 语句的选项。`switch` 语句仅
