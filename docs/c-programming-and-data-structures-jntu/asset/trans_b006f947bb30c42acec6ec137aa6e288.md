

| 平均分数 | 等级 |
|---|---|
| 80 至 100 | 荣誉 |
| 60 至 79 | 一级 |
| 50 至 59 | 二级 |
| 40 至 49 | 三级 |
| 0 至 39 | 不及格 |

这种分级可以使用 else if 阶梯结构来实现，如下所示（尽管从语法上讲，它是错误的！）

```c
if (marks > 79)
    grade = "Honours";
else if (marks > 59)
    grade = "First Division";
else if (marks > 49)
    grade = "Second Division";
else if (marks > 39)
    grade = "Third Division";
else
    grade = "Fail";
printf("%s\n", grade);
```

再考虑下面给出的另一个例子：

![](img/65953ea584e494f3d396b2252cb5ea53_150_0.png)

图 6.9 else ... if 阶梯结构的流程图

```c
..........
if (code == 1)
    colour = "RED";
else if (code == 2)
    colour = "GREEN";
else if (code == 3)
    colour = "WHITE";
else
    colour = "YELLOW";
..........
```

除 1、2 或 3 以外的代码编号均视为表示 YELLOW 颜色。使用嵌套的 if ... else 语句也可以获得相同的结果。

```c
if (code != 1)
    if (code != 2)
        if (code != 3)
            colour = "YELLOW";
        else
            colour = "WHITE";
    else
        colour = "GREEN";
else
    colour = "RED";
```

在这种情况下，选择哪种方法由程序员自行决定。然而，为了选择一种既有效又高效的 if 结构，程序员必须充分了解 if 语句的各种形式及其嵌套规则。

### 示例 6.5

一家电力分配公司向其家庭用户收费如下：

| 用电量（单位） | 收费标准 |
|---|---|
| 0 - 200 | 每单位 Rs. 0.50 |
| 201 - 400 | Rs. 100 加上超过 200 单位部分每单位 Rs. 0.65 |
| 401 - 600 | Rs. 230 加上超过 400 单位部分每单位 Rs. 0.80 |
| 601 及以上 | Rs. 390 加上超过 600 单位部分每单位 Rs. 1.00 |

图 6.10 中的程序读取客户编号和用电量，并打印客户需支付的金额。

## 6.7 SWITCH 和 BREAK 语句

当分支数量增加时，程序变得难以阅读和理解。有时，甚至连设计者本人也会感到困惑。幸运的是，C 语言有一种内置的多路决策语句，称为 switch。switch 语句将给定变量（或表达式）的值与一系列 case 值进行比较，当找到匹配项时，执行与该 case 关联的语句块。switch 语句的一般形式如下页所示。

决策与分支 6.15

```c
程序
/***************************************************************/
/* 使用 else if 阶梯结构 */
/************************************************************** */
main()
{
    int units, custnum;
    float charges;
    printf("Enter CUSTOMER NO. and UNITS consumed\n");
    scanf("%d %d", &custnum, &units);
    if (units <= 200)
        charges = 0.5 * units;
    else if (units <= 400)
        charges = 100 + 0.65 * (units - 200);
    else if (units <= 600)
        charges = 230 + 0.8 * (units - 400);
    else
        charges = 390 + (units - 600);
    printf("\n\nCustomer No: %d: Charges = %.2f\n",
    custnum, charges);
}
输出
Enter CUSTOMER NO. and UNITS consumed 101 150
Customer No: 101 Charges = 75.00
Enter CUSTOMER NO. and UNITS consumed 202 225
Customer No: 202 Charges = 116.25
Enter CUSTOMER NO. and UNITS consumed 303 375
Customer No: 303 Charges = 213.75
Enter CUSTOMER NO. and UNITS consumed 404 520
Customer No: 404 Charges = 326.00
Enter CUSTOMER NO. and UNITS consumed 505 625
Customer No: 505 Charges = 415.00
```

图 6.10 else ... if 阶梯结构的示例

表达式是一个整数表达式或字符。值-1、值-2……是常量或常量表达式（可求值为整型常量），称为 case 标签。这些值中的每一个在 switch 语句块内都应是唯一的。块-1、块-2……是语句列表，可以包含零个或多个语句。不需要在这些块周围加大括号。注意，case 标签以冒号（:）结尾。

当 switch 执行时，表达式的值会依次与值-1、值-2……进行比较。如果找到某个 case 的值与表达式的值匹配，则执行该 case 后面的语句块。

```c
switch (expression)
{
  case value-1: block-1
  break;
  case value-2: block-2
  break;
  ......
  default:
    default-block
  break;
}
statement-x;
```

每个块末尾的 break 语句表示特定 case 的结束，并使程序从 switch 语句中退出，将控制权转移到 switch 后面的 statement-x。

default 是一个可选 case。如果存在，当表达式的值与任何 case 值都不匹配时，将执行它。如果不存在，当所有匹配都失败时，不执行任何操作，控制权将转到 statement-x。

switch 语句的选择过程如图 6.11 中的流程图所示。

switch 语句可用于对学生的成绩进行分级，如上一节所述。下面进行说明：

```c
index = marks / 10;
switch (index)
{
  case 10:
  case 9:
  case 8:
    grade = "Honours";
    break;
  case 7:
  case 6:
    grade = "First Division";
    break;
  case 5:
    grade = "Second Division";
    break;
  case 4:
    grade = "Third Division";
    break;
  default:
    grade = "Fail";
    break;
}
printf("%s\n", grade);
........
```

![](img/65953ea584e494f3d396b2252cb5ea53_154_0.png)

图 6.11 switch 语句的选择过程

注意，我们使用了一个转换语句

```c
index = marks / 10;
```

其中，index 被定义为整数。变量 index 取以下整数值。

| 分数 | 索引 |
|---|---|
| 100 | 10 |
| 90 – 99 | 9 |
| 80 – 89 | 8 |
| 70 – 79 | 7 |
| 60 – 69 | 6 |
| 50 – 59 | 5 |
| 40 – 49 | 4 |
| : | : |
| 0 | 0 |

程序的这一部分说明了两个重要特性。首先，它使用了空 case。前三个 case 将执行相同的语句

```c
grade = "Honours";
break;
```

case 7 和 case 6 也是如此。其次，对于所有其他分数小于 40 的情况，使用了 default 条件。

switch 语句通常用于菜单选择。例如：

```c
..........
printf(" TRAVEL GUIDE \n\n");
printf(" A Air Timings\n");
printf(" T Train Timings\n");
printf(" B Bus Service\n");
printf(" X to skip\n");
printf("\n Enter your choice\n");
character = getchar();
switch (character)
{
case 'A':
air_display();
break;
case 'B':
bus_display();
break;
case 'T':
train_display();
break;
default:
printf("No choice\n");
}
..........
```

switch 语句可以嵌套。也就是说，一个 switch 可以是另一个 case 块的一部分。ANSI C 允许 15 层嵌套，以及多达 257 个 case 标签。

## 6.8 ? : 运算符

C 语言有一个不寻常的运算符，可用于进行双向决策。该运算符是 ? 和 : 的组合，需要三个操作数。这个运算符通常被称为条件运算符。条件运算符的一般使用形式如下：

```c
conditional expression ? expression1 : expression2
```

首先对条件表达式进行求值。如果结果不为零，则对 expression1 求值，并将其作为条件表达式的值返回。否则，对 expression2 求值并返回其值。例如，以下代码段

```c
if (x < 0)
    flag = 0;
else
    flag = 1;
```

可以写成

```c
flag = (x < 0) ? 0 : 1;
```

考虑以下函数的求值：

```text
y = 1.5x + 3    当 x ≤ 2
y = 2x + 5      当 x > 2
```

可以使用条件运算符进行求值，如下所示：

```c
y = (x > 2) ? (2 * x + 5) : (1.5 * x + 3);
```

条件运算符可以嵌套使用，以计算更复杂的赋值决策。例如，考虑一位销售家用产品的女销售的周薪。如果 x 是一周内售出的产品数量，她的周薪为：

```text
salary = { 4x + 100   当 x < 40
           300        当 x = 40
           4.5x + 150 当 x > 40 }
```

这个复杂的方程可以写成

```c
salary = (x != 40) ? ((x < 40) ? (4 * x + 100) : (4.5 * x + 150)) : 300;
```

同样的计算也可以使用 if ... else 语句进行：

```c
if (x <= 40)
    if (x < 40)
        salary = 4 * x + 100;
    else
        salary = 300;
else
    salary = 4.5 * x + 150;
```

当使用条件运算符时，代码变得更简洁，也许也更高效。然而，可读性较差。当需要超过一层的条件运算符嵌套时，最好使用 if 语句。

### 示例 6.6

一名员工可以在每六个月开始时申请贷款，但公司将根据以下规定批准金额：

- 规则 1：员工在任何时间点不能同时享受超过两笔贷款。
- 规则 2：最大允许贷款总额是有限制的，且取决于员工的类别。

处理贷款申请并批准贷款的程序如图 6.12 所示。

程序使用以下变量：

- loan3 - 当前申请的贷款金额
- loan2 - 之前未偿还的贷款金额
- loan1 - 之前再之前未偿还的贷款金额

