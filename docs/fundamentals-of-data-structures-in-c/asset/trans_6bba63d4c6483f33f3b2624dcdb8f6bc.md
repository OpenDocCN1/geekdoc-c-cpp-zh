
将被执行。如果条件为假，控制将直接转移到花括号外的语句，并执行可执行-Y语句，而不执行可执行-X语句。可执行-X语句（即if语句的主体）应括在花括号内。请注意，如果if语句的主体（即可执行-X语句）只包含一条语句，则括住它们的花括号不是必须的。如果表达式的值为零，则视为假；如果表达式的值为非零值，则视为真。表1.14显示了可用作if语句内条件的各种表达式。

| 条件表达式 | 含义 |
| :--- | :--- |
| a == b | a 等于 b |
| a != b | a 不等于 b |
| a < b | a 小于 b |
| a > b | a 大于 b |
| a <= b | a 小于或等于 b |
| a >= b | a 大于或等于 b |

请注意，= 用于赋值，而 == 用于比较两个量。两个或多个条件可以在 if 语句中使用逻辑与运算符（&&）或逻辑或运算符（||）组合。if 语句可以在单个 if 语句中比较任意数量的变量。程序 1.5 有助于您更好地理解。

程序 1.5:

```c
/* Program to find the biggest of two numbers using an if statement */
/* big_num.c */
#include<stdio.h>
void main()
{
    int value1, value2, big = 0;
    printf("Enter two values : ");
    scanf("%d %d", &value1, &value2);
    big = value1;
    if (value1 < value2)
    {
        big = value2;
    }
    printf("The biggest number is %d", big);
}
```

程序显示以下输出
Enter two values : 8 21
The biggest number is 21

用户输入 8 和 21 后，它们分别被赋值给变量 value1 和 value2。变量 value1 中存储的值被赋给变量 big（即，8 被赋给变量 big）。if 语句检查条件，即 value1 是否小于 value2（即，8 < 21）。由于在这种情况下条件为真，value2 被赋给变量 big（即，21 被赋给变量 big），并且 printf() 函数显示消息。

### 1.9.2 if-else 语句

if-else 语句是 if 语句的扩展，用于在条件为假时也执行一个或多个语句。if 语句默认会在条件为真时执行单个语句或一组语句，但在条件为假时不执行任何操作。else 语句会在条件为假时执行单个语句或一组语句。if-else 语句的一般形式或语法是

```c
if (condition)
{
    executable-X-statements(s);
}
else
{
    executable-y-statements(s);
}
```

图 1.4 显示了 if-else 语句的操作。if 语句中使用的条件应指定在括号内。如果条件为真，则从条件之后直到 else 之前的语句将被执行。如果条件为假，则 else 之后的语句将被执行。程序 1.6 有助于您更好地理解。

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_46_0.png)

程序 1.6:

```c
/* Program to check whether the no is odd or even using an if-else statement */
/* odd_even.c */
#include <stdio.h>
void main()
{
    int number;
    printf("Enter a number : ");
    scanf("%d", &number);
    if(number % 2 == 0)   /* if remainder is zero */
    {
    printf("The number is even");
    }
    else
    {
    printf("The number is odd");
    }
}
```

程序显示以下输出
Enter a number : 258
The number is even

用户输入 258 后，它被赋给变量 number。if 语句检查条件，即变量的余数是否为零。由于在这种情况下条件为真，if 块中的语句被执行。else 块被跳过，程序结束。

### 多个 if-else 语句

多个 if-else 语句提供了一种测试多个条件并为每个条件执行一个或多个语句的方法。多个 if-else 语句比一系列 if-else 语句快得多，因为当满足任一条件时，if 结构就会退出。

程序 1.7:

```c
/* mul_if.c */
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
printf("\nEnter the value of i : ");
scanf("%d",&i);
if(i == 1)
printf("Hello Chocks");
else if (i == 2)
printf("Hello Girish");
else if (i == 3)
printf("Hello Madhu");
else if (i == 4)
printf("Hello Mani");
else
printf("Hello Moorthy");
}
```

程序显示以下输出
RUN1 Enter the value of i : 2
Hello Girish
RUN2 Enter the value of i : 7
Hello Moorthy

在 run1 中，用户输入 2 后，它被赋给变量 i。if 语句检查条件，即 i 是否等于 1（例如，if(i==1)）。由于条件为假，控制转移到下一个 if 语句（例如，else if(i==2)），并检查 i 是否等于 2。由于条件为真，执行其后的语句。printf() 函数显示消息

Hello Girish

所有其他 else if 语句都被忽略，程序结束。

在 run2 中，由于没有任何条件为真，所有 if 语句都被忽略，控制转移到 else 块。printf() 函数显示消息

Hello Moorthy

程序结束。请注意，程序中可以包含任意数量的 if-else 语句，但每个 if 语句内指定的条件应不同。

### 嵌套 if-else 语句

if-else 语句内包含一个或多个 if-else 语句称为嵌套 if 语句。程序 1.8 有助于您更好地理解。

程序 1.8:

```c
/* nest_if.c */
#include<stdio.h>
void main()
{
int choice, yrs_of_exp;
printf("\nEnter 1 for Project Leader");
printf("\nEnter 2 for Software Engineer");
printf("\nEnter your choice : ");
scanf("%d", &choice);
printf("Enter Years Of Experience : ");
scanf("%d", &yrs_of_exp);
if(choice == 1)
{
if(yrs_of_exp > 5)
printf("\nSalary Hike is 7500");
else
printf("\nSalary Hike is 6000");
}
else if(choice == 2)
{
if(yrs_of_exp > 3)
printf("\nSalary Hike is 5000");
else
printf("\nSalary Hike is 4000");
}
else
 printf("\nInvalid Choice ...");
}
```

程序显示以下输出
Enter 1 for Project Leader
Enter 2 for Software Engineer
Enter Your Choice : 1
Enter Years Of Experience : 8
Salary Hike is 7500

当用户输入 1（表示 `Project Leader`）时，控制进入第一个 `if` 语句。第一个 if 语句内的嵌套 if 检查条件。由于经验年限（即 `yrs_of_exp`）大于 5，`printf()` 函数显示消息

Salary Hike is 7500

嵌套 `if` 的控制退出，同时主 if 的控制也退出，程序结束。

### 1.9.3 switch 语句

switch 语句允许我们从多个选项中做出决策。它通常称为 `switch-case` 语句。`switch` 语句的一般形式或语法是

```c
switch(expression)
{
 case constant1 : statement(s);
 case constant2 : statement(s);
 ..... .....
 case constantN : statement(s);
 default : statement(s);
}
```

switch 语句会从多个可用组中选择特定的一组语句。选择基于包含在 `switch` 语句中的表达式的当前值。每个 case 由一个或多个整数值表达式标记。如果某个 case 匹配表达式值，则从该 case 开始执行，并在遇到 `break` 语句时结束。所有 `case` 表达式必须不同。如果没有其他 case 满足，则执行标记为 `default` 的 case。`switch` 语句中的 `default` 是可选的。**程序 1.9** 有助于您更好地理解。
