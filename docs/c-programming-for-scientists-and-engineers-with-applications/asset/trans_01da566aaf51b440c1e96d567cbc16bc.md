

## 208 控制结构

```c
else if (y > z)
printf("The largest number is: %d\n", y);
```

```c
else
printf("The largest number is : %d\n", z);
```

请注意，即使所有数字都相同，默认情况也会打印正确的答案。

|| 条件 考虑对两种不同类型的数据以相同方式处理的情况。下面的示例展示了在复合条件中使用 || 运算符的实现。如图 4.7 的流程图所示。

![](img/8356e6c3bfe3b10354682c60b1e74b1d_227_0.png)

图 4.7 复合条件的流程图

带有简单条件的代码为：

```c
if(cond1)
{
  stmt1;
  stmt2;
}
else if(cond2)
```

```c
{
  stmt1;
  stmt2;
}
```

由于两个嵌入序列包含相同的语句，这也可以写成：

```c
if(cond1 || cond2)
{
  stmt1;
  stmt2;
}
```

例如，考虑二次方程 $ax^2 + bx + c = 0$ 的解。如果 $a = 0$ 或 $b^2 - 4ac < 0$，则无法使用求解方程实根的公式。将使用以下代码来求解方程。

```c
if(a == 0 || (b * b - 4 * a * c ) < 0)
{
  printf("This is not a solvable equation");
}
else
{
  d = sqrt(b * b - 4 * a * c);
  x1 = (-b + d) / (2 * a);
  x2 = (-b - d) / (2 * a);
}
```

可以使用复合逻辑表达式。在下面的示例中，如果大四学生的平均学点（GPA）至少为 3.5，就有资格奖学金。奖学金也可以授予 GPA 至少为 3.75 的大二学生。

```c
if((level == senior) && (GPA > Bplus) || (level == junior) && (GPA > Aminus))
{
  printf("student-id : %d is eligible for a scholarship\n", std_id);
}
```

在此示例中，level 和 GPA 是变量，而 junior、senior、Aminus 和 Bplus 是常量。

## 4.2.3 多路结构

有一种特殊的语句，等同于 if-else...if-else...if...else...else。当所有条件都检查同一个变量的值，且这些值可能可能是 1, 2, 3 等时，可以使用这种语句。这通常用于带有赋值的代码。这种结构被称为 case 结构（分支结构）。在 C 中，可以通过 switch 语句来实现。
下面的示例展示了使用 if-else 来实现 case 结构：

```c
int student_code;

scanf("%d", &student_code);

printf("The student code = %d\n", student_code);
if (student_code == 1)
{
    printf("The student is a freshman.\n");
}
else if (student_code == 2)
{
    printf("The student is a sophomore.\n");
}
else if (student_code == 3)
{
    printf("The student is a junior.\n");
}
else if (student_code == 4)
{
    printf("The student is a senior.\n");
}
else
{
    printf("The student is unclassified.\n");
}
```

如果 student_code 匹配条件分支，则执行相应的分支语句。如果 student_code 不匹配 1, 2, 3 或 4，则默认执行 else 分支。如果每个分支只有一个语句，则不需要使用大括号。

## 4.2.2 选择结构

Switch 语句 switch 语句也可以用于实现 case 结构。switch 语句的标准形式如下：

```c
switch(expression)
{
  case constant:
    stmt1;
  break;
  case constant:
    stmt2;
  break;
}
```

表达式预期为预设值集之一。表达式的值用法如下 ![](img/8356e6c3bfe3b10354682c60b1e74b1d_230_0.png)

```c
switch(expression)
{
  case 1:
    sequence1;
  break;
  case 2:
    sequence2;
    break;
  case 3:
    sequence3;
    break;
  case 4:
    sequence4;
    break;
  default:
    sequence5;
}
```

在这个结构中，表达式的值可能有 1, 2, 3 或 4；对于 case 2 执行 sequence2，以此类推。对于 case 1 执行 sequence1，对于 case 2 执行 sequence2，以此类推。如果表达式的值不是 1, 2 或 4，则执行默认 case。break 语句是一种特殊的语言，将控制转移到结构的末尾。一旦执行了特定的 case，就需要这个语句。如果没有 break 语句，执行将不会从特定的 case 终止，而是继续执行下一个 case。例如，如果执行从 case 3 开始，执行继续到 case 4 和默认 case，如果 case 3 或 case 4 没有 break 语句。下面的示例展示了使用 switch 结构处理记录：

```c
int student_code;

scanf("%d", &student_code);

printf("Student code = %d\n", student_code);

switch(student_code)
{
  case 1:
    printf("The student is a freshman.\n");
    break;
  case 2:
    printf("The student is a sophomore.\n");
    break;
  case 3:
    printf("The student is a junior.\n");
    break;
  case 4:
    printf("The student is a senior.\n");
    break;
  default:
    printf("The student is unclassified.\n");
}
```

表达式 student_code 的有效值为 1, 2, 3 和 4。任何其他值都会导致默认 case。注意，switch 语句仅适用于 int 和 char 类型。为了实现 case，控制表达式必须求值为整数常量或特定的字符值（如 'a'）。case 代码必须是整数常量或字符（char）常量。下面的代码展示了逻辑 case 的评估：

```c
int a, b;

scanf("%d %d", &a, &b);

switch((a-b) > 0)
{
  case 0:
    printf("This is case 1: a is less than or equal to b.");
    break;
  case 1:
    printf("This is case 2: a is greater than b.");
    break;
}
```

注意，在这种情况下，如果没有进一步的条件语句（如 if-else 语句），无法区分小于和等于。这是因为逻辑语句产生二二响应。这种类型的语句只有两个 case 代码：0 或 1。在大多数情况下，使用 if-else 语句来实现逻辑判断。

switch 语句的一种变体是同时检查两个或多个 case，前提它们需要相同的操作。下面的示例展示了这样的 switch 结构：

```c
switch(expression)
{
  case 1:
    printf("This is case 1: %d\n", expression);
    break;
  case 2:
  case 3:
    printf("This is case 2 or case 3: %d\n", expression);
    break;
  default:
    printf("This is the default: %d\n", expression);
}
```

注意 case 2 没有 break 语句，在 case 2 或 case 3 下执行相同的一组语句。如果需要用同一组程序语句处理相似的数据集，这是一个方便的结构。

case 结构可以像下面的示例所示用于多次匹配，其中使用计数来指示找到了多少次匹配。

```c
int count=0;
if(a==b)
    count += 1;
if(b==c)
    count += 1;
if(a==c)
    count += 1;

switch(count)
{
  case 0:
    printf("If abc is a triangle, it is scalene.");
    break;
  case 1:
    printf("If abc is a triangle, it is isosceles.");
    break;
  case 3:
    printf("If abc is a triangle, it is equilateral.");
    break;
  default:
    printf("This is impossible.");
}
```

在这个序列中，if 语句测试所有条件并确定 count 的值。switch case 结构使用 count 的值来区分三边都不相等、两边相等以及三边相等。注意，在这个代码中默认 case 并不是必需的，但在这里包含是为了说明这一点。初始测试将满足其中一个 case 值。

## 4.2.4 课习题

- 1. 判断下列陈述的对错。
  - a. 关系表达式给操作数赋值，使其为真。
  - b. 当关系运算符包含两个字符时（如 >= <= 或 !=），它们之间不应有空格。
  - c. 在包含算术运算的关系表达式中，算术运算先于关系运算。
  - d. 关系表达式可以比较任何数据类型的操作数。
  - e. 关系表达式用于分支结构中进行逻辑选择。
  - f. 关系表达式求值为 0 或 1。
  - g. 关系表达式也称为条件。

