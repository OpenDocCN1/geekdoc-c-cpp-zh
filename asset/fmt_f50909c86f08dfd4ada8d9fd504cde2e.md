
```c
01: // 显示数字正负号的程序
02: main()
03: {
04:     int a;
05: 
06:     printf("Enter a number : ");
07:     scanf("%d", &a);
08:     if (a < 0)
09:         printf("Negative");
10:     else
11:         if (a > 0)
12:             printf("Positive");
13:     else
14:         printf("Zero");
15: }
```

在上例中，你有三种选择（正、负和零）。这要求我们一个接一个地检查两个条件。因此，我们必须使用多条语句。首先检查 `a` 是否小于 0，如果该条件失败，你仍然还有两个选择（正和零）。因此，在采取下一步行动之前，你必须检查其中任何一种可能的情况。

如果条件 `a > 0` 为真，意味着 `a` 是正数。由于我们已经检查了 `a` 是否为负，剩下的唯一选项就是零。因此，`else` 部分显示消息“零”。

以下示例根据学生获得的成绩授予学生相应的等级。

```c
01: #include <stdio.h>
02: void main()
03: {
04:     int marks;
05: 
06:     printf("Enter marks : ");
07:     scanf("%d", &marks);
08: }
```

# 初学者 C 语言 (C Language For Beginners)

```c
09: // 根据分数显示等级
10: if (marks > 80)
11:     printf("First grade");
12: else
13:     if (marks > 60)
14:         printf("Second grade");
15:     else
16:         if (marks > 50)
17:             printf("Third grade");
18:     else
19:         printf("Fail");
20: }
```

上述代码段首先检查分数是否大于 80。如果是，它会显示消息“First grade”（一等）。否则，它检查第二个条件，如果为真，则显示“Second grade”（二等）。如果第二个条件也为假，它会检查第三个条件，如果为真，则显示消息“Third grade”（三等），如果仍然为假，则显示“Fail”（不及）。

我们我们将讨论 `switch` 语句，它是多重 `if` 语句的替代方案。

## 嵌套 if 语句 (Nested if statement)

在某些情况下，你需要将一个 `if` 语句放在另一个 `if` 语句内部。当你将一个 `if` 语句放在另一个 `if` 语句内部时，被称为嵌套 `if` 语句。这是一个简单的示例。

```c
// 检查 a 是否等于 b 和 c
if (a == b)
    if (a == c)
        printf("All three numbers are same");
```

只有当两个条件都为真时，才会执行 `printf()`。首先，C 检查第一个条件。如果第一个条件为真，它进入 `if` 语句。只有当第二个 `if` 也满足时，才会执行 `printf`。

## 初学者 C 语言 (2 C Language For Beginners)

```c
if (condition-1)
    if (condition-2)
        statement - 1;
    else
        statement - 2;
else
    statement - 3;
```

下面的表将说明哪条语句将被执行。

| Condition-1 | Condition-2 | 执行了什么？ |
|---|---|---|
| True | True | Statement-1 |
| True | False | Statement-2 |
| False | - | Statement-3 |

以下示例将让你更了解嵌套 `if` 语句。程序根据产品代码和销售额显示佣金。如果销售处理代码 1 且销售额超过 10000，则佣金为 5%，否则为 3%。当代码为 2 且销售额超过 20000 时，佣金率为 7%，否则为 4%。

```c
01: #include <stdio.h>
02: main()
03: {
04:     unsigned int samt;
05:     float comm;
06:     int code;
07:     printf("Enter code and sales amount:");
08:     scanf("%d%u", &code, &samt);
09:     if (code == 1)
10:         if (samt > 10000)
11:             comm = samt * 0.05;
12:         else
13:             comm = samt * 0.03;
14:     else if (code == 2)
15:         if (samt > 20000)
16:             comm = samt * 0.07;
17:         else
18:             comm = samt * 0.04;
19:     printf("Commission : %f", comm);
20: } // main 结束
```

## 条件运算符 (Conditional)

`if` 语句默认允许你执行一条语句，复合语句则用来克服这一局限性。如果你在只允许执行一条语句的情况下必须执行多条语句，那么你必须使用复合语句。

复合语句通过将所有要执行的语句放在的一对大括号 `{}` 中来创建。复合语句可以用任何可以使用简单语句的地方。

以下示例在两个条件任一为真时会执行两个语句。

```c
if(a > b)
{
    c = d;
    d = e;
}
else
{
    a = d;
    d = f;
}
```

## 三元运算符 (?:)

有时，你需要根据不同的条件采取不同的行动。观察以下示例。

```c
01: // 显示数字正负号的程序
02: main()
03: {
04:     int a;
05: 
06:     printf("Enter a number : ");
07:     scanf("%d", &a);
08:     printf((a < 0) ? "Negative" : (a > 0) ? "Positive" : "Zero");
09: }
```

在上例中，你有三种选择（正、负和零）。这要求我们一个接一个地检查两个条件。因此，我们必须使用多条语句。

以下示例根据学生获得的成绩授予学生相应的等级。

```c
01: #include <stdio.h>
02: void main()
03: {
04:     int marks;
05: 
06:     printf("Enter marks : ");
07:     scanf("%d", &marks);
```

## 初学者 C 语言 延续

```c
09: // 根据分数显示等级
10: if (marks > 80)
11:     printf("First grade");
12: else
13:     if (marks > 60)
14:         printf("Second grade");
15:     else
16:         if (marks > 50)
17:             printf("Third grade");
18:     else
19:         printf("Fail");
20: }
```

上述代码段首先检查分数是否大于 80。如果是，它会显示消息“First grade”。否则，它检查第二个条件，如果为真，则显示“Second grade”。如果第二个条件也为假，它会检查第三个条件，如果为真，则显示消息“Third grade”，如果仍然为假，则显示“Fail”。

我们我们将讨论 `switch` 语句，它是多重 `if` 语句的替代方案。

## 嵌套 if 语句

在某些情况下，你需要将一个 `if` 语句放在另一个 `if` 语句内部。当你将一个 `if` 语句放在另一个 `if` 语句内部时，被称为嵌套 `if` 语句。这是一个简单的示例。

```c
// 检查 a 是否等于 b 和 c
if (a == b)
    if (a == c)
        printf("All three numbers are same");
```

`printf()` 只有在两个条件都为真时才会执行。首先，C 检查第一个条件。如果第一个条件为真，它进入 `if` 语句。只有当第二个 `if` 也满足时，才会执行 `printf`。

## 初学者 C 语言 2

```c
if (condition-1)
    if (condition-2)
        statement - 1;
    else
        statement - 2;
else
    statement - 3;
```

下面的表将说明哪条语句将被执行。

| Condition-1 | Condition-2 | 执行了什么？ |
|---|---|---|
| True | True | Statement-1 |
| True | False | Statement-2 |
| False | - | Statement-3 |

以下示例将让你更了解嵌套 `if` 语句。程序根据产品代码和销售额显示佣金。如果销售处理代码 1 且销售额超过 10000，则佣金为 5%，否则为 3%。当代码为 2 且销售额超过 20000 时，佣金率为 7%，否则为 4%。

```c
01: #include <stdio.h>
02: main()
03: {
04:     unsigned int samt;
05:     float comm;
06:     int code;
07:     printf("Enter code and sales amount:");
08:     scanf("%d%u", &code, &samt);
09:     if (code == 1)
10:         if (samt > 10000)
11:             comm = samt * 0.05;
12:         else
13:             comm = samt * 0.03;
14:     else if (code == 2)
15:         if (samt > 20000)
16:             comm = samt * 0.07;
17:         else
18:             comm = samt * 0.04;
19:     printf("Commission : %f", comm);
20: } // main 结束
```

## 条件运算符 (?:)

`if` 语句默认允许你执行一条语句，复合语句则用来克服这一局限性。如果你在只允许执行一条语句的情况下必须执行多条语句，那么你必须使用复合语句。

复合语句通过将所有要执行的语句放在的一对大括号 `{}` 中来创建。复合语句可以用任何可以使用简单语句的地方。

以下示例在两个条件任一为真时会执行两个语句。

```c
if(a > b)
{
    c = d;
    d = e;
}
else
{
    a = d;
    d = f;
}
```

## 三元运算符 (?:)

有时，你需要根据不同的条件采取不同的行动。观察以下示例。

```c
01: // 显示数字正负号的程序
02: main()
03: {
04:     int a;
05: 
06:     printf("Enter a number : ");
07:     scanf("%d", &a);
08:     printf((a < 0) ? "Negative" : (a > 0) ? "Positive" : "Zero");
09: }
```

## 初学者 C 语言 延续

```c
09: // 根据分数显示等级
10: if (marks > 80)
11:     printf("First grade");
12: else
13:     if (marks > 60)
14:         printf("Second grade");
15:     else
16:         if (marks > 50)
17:             printf("Third grade");
18:     else
19:         printf("Fail");
20: }
```

## switch 语句

当需要检查的条件较多时，`if` 语句变得冗长且难以理解。更好的替代方案是 `switch` 语句。它根据结果采取不同的行动。根据产品代码查找折扣率，可以使用以下 `switch` 语句。

```c
switch(pc)
{
  case 1 : dis = 07; break;
  case 2 : dis = 08; break;
  case 3 : dis = 05; break;
  case 4 : dis = 06; break;
```

首先将 `pc` 与 1 比较。如果条件为真，则执行相应的语句。否则检查下一个 case，依此类推。如果没有任何 case 为真，则执行 `default` 后的语句。

默认情况下，`switch` 执行条件为真的语句。这意味着如果 `pc` 是 2，则从 case 2 开始的所有语句都将执行。为了防止其他 case 的代码被执行，你必须使用 `break` 语句退出整个 `switch` 语句。虽然 `break` 不是 `switch` 语句语法的一部分，但它通常在每个 case 中使用。

```c
switch (expression)
{
  case value-1 : statements;
  [case value-2 : statements] ...
  [default : statements]
}
```

至少有一个 case 是必须的，第二个 case 开始以及 default 是可选的。

## 初学者 C 语言

注意：语法中的三个点 `...` 表示前一个项目可以重复任意次数。在 `switch` 语法中，`case` 语句可以重复任意次数。

## 总结

- C 提供了许多高级语言所提供的所有条件语句。简单 `if` 语句用于采取两种可能的行动之一（或根据条件采取一种行动）。由于比较所花费的时间比计算长，因此使用正确的控制语句来减少条件的数量是重要的。熟练地使用控制语句是学习编程语言的第一块里程碑。因此，请阅读本章直到理解所有内容。

## 练习

- 1. 接受一个数字并显示它是偶数还是奇数。编写两个程序——一个使用条件运算符，另一个使用普通的 `if` 语句。
- 2. 接受科目成绩和科目代码（1 到 4），并显示学生通过还是不及格。及格根据科目代码如下：1-40、2-50、3-45、4-55。
- 3. 接受两个数字并显示这两个数字之间的关系。输出应显示以下消息之一：“两个数字相等”、“第一个数字更大”或“第二个数字更大”。
- 4. 从用户处接受三个数字并显示三个数中最大的。

# 6. 循环结构

循环是一种允许你重复执行一组语句的机制。在编程中，你经常需要重复执行某组语句。例如，如果你编写一个程序来获取 20 个学生的成绩并显示每位学生是及格还是不及格，你就必须反复获取每个学生的分数并执行所需的操作。

在本章中，我们将讨论 C 语言中可用的循环结构以及相关的语句，如 `break` 语句。

- 可用的循环结构
- while 循环
- for 循环
- do... while 循环
- break 语句
- continue 语句
- 嵌套循环
- 总结
- 练习题

## 可用的循环结构

以下是 C 语言中可用的循环结构。

- while
- for
- do ... while

所有所有的结构都用于重复执行一组语句。然而，使用哪一个取决于哪种循环结构更符合需求。

## while 循环

只要给定的条件为真，就会执行该语句。当条件为假时，循环终止，并执行循环后的下一个语句。

下面的示例说明了如何使用 while 循环。

```
01: // 打印从 1 到 10 数字的程序
02: #include <stdio.h>
03:
04: void main()
05: {
06: int n = 1;
07:
08: //只要 n 小于 11 就重复循环
09: while (n < 11)
10: {
11:     printf("%d\n", n);
12:     n++; // n 递增 1
13: } // while 循环结束
14: }
```

上面的 while 循环将在屏幕上显示从 1 到 10 的数字。

以下是 while 循环的语法。

```
while (condition)
statement;
```

条件可以是任何有效的 C 条件。只要条件为真，语句就会重复执行。一旦条件为假，循环终止，控制权转移到紧接在循环之后的语句。

语句可以是单条语句，也可以是复合语句。

下面的程序用于显示给定数字中的最大值。它会提示用户输入数字，直到用户输入 0 为止。

```
01: // 显示给定数字中最大值的程序
02: #include <stdio.h>
03:
04: void main()
05: {
06:     int num;
07:     int largen = 0;
08:
09:     printf("Enter a number [0 to stop :");
10:     scanf("%d", &num);
```
