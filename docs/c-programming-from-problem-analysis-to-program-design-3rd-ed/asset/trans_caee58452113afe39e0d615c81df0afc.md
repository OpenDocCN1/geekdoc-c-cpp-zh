

```
public static void PrintResults(int largestOne)
{
    Console.WriteLine( );
    Console.WriteLine("The largest value entered was "
                      + largestOne);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(largestOne));
    Console.ReadLine( );
}
}
}
```

在编写选择语句时，尽量避免重复代码。与其为**真**和**假**两种分支重复编写语句，不如将公共语句提取出来，放在选择语句之前或之后。你可能试图用下面的双向 **if** 语句来解决示例 5-11 中提出的问题：

```
if (value1 > value2)
{
    Console.WriteLine("The largest value entered was "
                      + value1);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value1));
}
else
{
    Console.WriteLine("The largest value entered was "
                      + value2);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value2));
}
```

在示例 5-11 中，用于显示最大值及其平方根的 Console.WriteLine( ) 方法调用只包含了一次。而在最后一段代码中，它们出现了两次。

另一种未模块化但消除了重复代码的解决方案如下：

```
int largest;
if (value1 > value2)
{
    largest = value1;
}
else
{
    largest = value2;
}
Console.WriteLine("The largest value entered was "
                  + largest);
Console.WriteLine("Its square root is {0:f2}",
                  Math.Sqrt(largest));
```

编写选择语句的这三种方式会产生相同的输出。在这三种方式中，示例 5-11 中的模块化版本是首选。在这种情况下，你可能看不出一种方法相对于另一种有明显的优势。随着计算机程序复杂度的增加，模块化变得更加重要。图 5-6 展示了当第一个值输入 25、第二个值输入 15 时程序运行所产生的输出。

![](img/e33ae760e23d89eac66541252ad65de8_290_0.png)

**图 5-6** LargestValue 问题的输出

当输入的值相同时，示例 5-11 中的程序会打印什么？

因为 `value1` 不大于 `value2`，所以会执行 `else` 语句，并将 `value2` 存储到 `largestOne` 中。如果你希望显示一条消息表明两个值相同，就需要再增加一个条件表达式作为 `if` 语句的一部分。这个额外的测试将用于判断 `value2` 是否大于 `value1`。可以将该表达式添加为 `else` 语句。添加第二个测试后，你还可以包含另一个 `else` 语句。除非两个条件表达式都评估为 `false`，否则不会进入最后一个 `else`——在这种情况下，两个值是相同的。如果你进行此修改，则需要修改显示最大值的逻辑。一种方法是在 `value1` 和 `value2` 相等时返回其中一个的负值。返回哪个并不重要，因为它们的值相同。`PrintResults()` 方法可以测试 `largestOne` 变量。当其值为负时，可以打印一条消息表明两个值相同。额外的测试如下：

```text
if (value1 > value2)
{
    largestOne = value1;
}
else
    if (value1 < value2)
    {
        largestOne = value2;
    }
    else
        largestOne = -(value1);
```

有时，单个变量可能需要针对多个值进行测试。此前描述的嵌套 if...else 语句可用于此目的。你可能还希望在条件为真（或假）的分支中测试另一个变量。嵌套 if...else 语句也可用于这种情况。在下一节中，你将进一步了解嵌套 if...else 语句。

## 嵌套 if...else 语句

当表达式评估为真时，任何语句都可以包含在要执行的语句中。对于条件为假时要执行的语句也是如此。因此，在 if 内部编写另一个 if 是可以的。可以在单个 if 语句中评估多个不同的表达式。当你在 if 内部放置另一个 if 时，就创建了嵌套 if...else 语句，也称为嵌套 if 语句。

使用嵌套 if 语句，可以测试多个表达式。只要表达式评估为真，就会继续评估条件为真时要执行的语句。当另一个 if 语句是要执行块中的某个语句时，就会执行另一次评估。只要真分支中还包含其他 if 语句，这一过程就会继续。

与双向选择语句一样，只执行一段代码。永远不会同时执行真分支及其相关联的假分支。当该代码块执行完毕后，所有剩余的条件表达式及其语句都会被跳过或绕过。完成该代码块后，控制权总会转移到紧接在 if 块之后的语句。这里再次给出嵌套 if...else 语句的语法，其与双向选择语句的语法一致。不同之处在于，嵌套 if...else 中的语句可能是另一个 if 语句：

```
if (conditional_expression)    //No semicolon is placed on this line.
    statement;                // Could be another if statement
else
    statement;                // Could be another if statement
```

在嵌套 if...else 中，内部 if 语句被称为嵌套在外部 if 语句中。然而，内部 if 也可能包含另一个 if 语句。对嵌套的深度没有限制。限制在于你和他人能否阅读并理解你的代码。好程序的标志就是其可读性。

在设计需要嵌套 if...else 的解决方案时，如果以图形方式画出不同的选项，有时会更容易开发算法。可以使用流程图。另一种选择是决策树，这是一种设计工具，允许你以可视化方式表示复杂过程。节点用于表示决策点，从节点分支出的线条表示进一步的条件，或最终表示根据左侧列出的条件要采取的操作。图 5-7 展示了用于计算小时工和受薪员工奖金的决策树。每周工作超过 40 小时的小时工获得 500 美元。其他小时工获得 100 美元。受雇超过 10 年的受薪员工获得 300 美元，而其他受薪员工获得 200 美元。图 5-7 使用决策树说明了这种情况。

![](img/e33ae760e23d89eac66541252ad65de8_292_0.png)

**图 5-7** 奖金决策树

示例 5-12 展示了如何使用嵌套 if...else 来确定图 5-7 中所说明的奖金金额。

### 示例 5-12

```cpp
// For hourlyEmployees working more than 40 hours, a bonus of $500
// is issued. If hourlyEmployee has not worked more than 40 hours,
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

第一个条件表达式中不需要相等运算符。这是因为使用了布尔变量 hourlyEmployee。

示例 5-12 的逻辑也可以使用四个单向 `if` 语句来编写，如示例 5-13 所示。这里，每个语句都使用了 `&&` 运算符。

### 示例 5-13

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

示例 5-12 中的单个嵌套 `if...else` 解决方案比示例 5-13 中的四个语句高效得多。在示例 5-13 中，即使第一个语句评估为 `true`，每个语句也都会被评估。而在示例 5-12 中，当前两行评估为 `true` 时，就会向 `bonus` 赋值 500，并且不再执行额外的评估。

注意，使用逻辑 `&&` 编写的语句如何改写为嵌套的 `if...else`。

```text
if (hourlyEmployee && hours > 40)
```

与以下写法产生相同的结果：

```text
if (hourlyEmployee)
    if (hours > 40)
```

在编写嵌套 `if...else` 语句时，重要的是要知道哪个 `else` 与哪个 `if` 语句匹配。对齐（或匹配）else 的规则是：`else` 与最近的、且没有自己的 `else` 的前一个 `if` 匹配。通过正确地将 `else` 子句与对应的 `if` 子句对齐，可以减少需要调试的逻辑错误。示例 5-14 说明了正确对齐 `if` 和 `else` 子句的重要性。你能将每个 `else` 与正确的 `if` 匹配起来吗？

### 示例 5-14

```text
if (aValue > 10)                         Line 1
if (bValue == 10)                        Line 2
amount = 5;                              Line 3
else                                     Line 4
    if (cValue > 100)                    Line 5
        if (dValue > 100)                Line 6
        amount = 10;                     Line 7
        else                             Line 8
        amount = 15;                     Line 9
    else                                 Line 10
        amount = 20;                     Line 11
else                                     Line 12
    if (eValue == 0)                     Line 13
    amount = 25;                         Line 14
```

