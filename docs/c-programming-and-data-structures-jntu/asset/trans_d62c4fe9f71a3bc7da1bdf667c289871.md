
程序
```c
/************************************************/
/*              COUNTING WITH if                */
/************************************************/
main()
{
    int count, i;
    float weight, height;
    count = 0;
    printf("Enter weight and height for 10 boys\n");
    for (i = 1; i <= 10; i++)
    {
        scanf("%f%f", &weight, &height);
        if(weight < 50 && height > 170)
            count = count + 1;
    }
    printf("Number of boys with weight < 50 kgs\n");
    printf("and height > 170 cm = %d\n", count);
}
```

输出
```
Enter weight and height for 10 boys
45 176.5
55 174.2
47 168.0
49 170.7
54 169.0
53 170.5
49 167.0
48 175.0
47 167
51 170
Number of boys with weight < 50 kgs
and height > 170 cm = 3
```

图 6.4 使用 if 进行计数

## 6.4 if ... else 语句

if ... else 语句是简单 if 语句的扩展。其一般形式如下：

```c
if (test expression)
{
    True-block statement(s)
}
else
{
    False-block statement(s)
}
statement-x
```

如果测试表达式为真，则执行紧跟在 if 语句之后的真分支语句；否则执行假分支语句。无论哪种情况，只会执行真分支或假分支之一，而不会同时执行两者。图 6.5 说明了这一点。在这两种情况下，控制随后都会转移到 statement-x。

![](img/65953ea584e494f3d396b2252cb5ea53_144_0.png)

图 6.5 if ... else 控制的流程图

让我们考虑一个统计班级中男生和女生人数的例子。我们用代码 1 表示男生，2 表示女生。实现这一功能的程序语句可编写如下：

```c
........
if (code == 1)
    boy = boy + 1;
if (code == 2)
    girl = girl + 1;
........
```

第一个测试判断该学生是否为男生。如果是，则男生人数加 1，程序继续执行第二个测试。第二个测试再次判断该学生是否为女生。这是不必要的。一旦确定学生是男生，就无需再判断是否为女生。一个学生要么是男生，要么是女生，不可能两者都是。上面的程序段可以使用 else 子句修改为如下形式：

```c
........
if (code == 1)
    boy = boy + 1;
else
    girl = girl + 1;
statement-x
........
```

这里，如果 code 等于 1，则执行语句 `boy = boy + 1;`，并在跳过 else 部分后将控制转移到 statement-x。如果 code 不等于 1，则跳过语句 `boy = boy + 1;`，并在控制到达 statement-x 之前执行 else 部分中的语句 `girl = girl + 1;`。

考虑图 6.3 中给出的程序。当 (c – d) 的值为零时，不计算比值，程序没有任何提示就停止了。在这种情况下，我们可能不知道程序是因为值为零还是其他错误而停止。可以通过添加 else 子句来改进该程序，如下所示：

```c
........
if (c - d != 0)
{
    ratio = (float)(a+b)/(float)(c-d);
    printf("Ratio = %f\n", ratio);
}
else
printf("c-d is zero\n");
........
........
```

### 示例 6.3

一个计算幂级数的程序

e^x = 1 + x + x²/2! + x³/3! + ... + x^n/n!, 0 < x < 1

见图 6.6。它使用 if ... else 来测试精度。

该幂级数包含如下类型的递推关系：

T_n = T_{n-1}(x/n)  （当 n > 1 时）  
T_1 = x  （当 n = 1 时）  
T_0 = 1

如果已知 T_{n-1}（通常称为前一项），则可以通过将前一项乘以 x/n 轻松求得 T_n（称为当前项）。于是

e^x = T_0 + T_1 + T_2 + ...... + T_n = sum

程序使用 count 来统计所添加的项数。当项的值小于 0.0001（ACCURACY）时，程序停止。注意，当某项小于 ACCURACY 时，n 的值被设为 999（一个大于 100 的数），因此 while 循环终止。结果在 while 循环外打印。

## 6.5 if ... else 语句的嵌套

当涉及一系列决策时，我们可能必须以嵌套形式使用多个 if ... else 语句，如下所示：

```c
/* ************************************************************* */
/* EXPERIMENT WITH if ... else STATEMENT */
/* ************************************************************* */

#define ACCURACY 0.0001
main()
{
    int n, count;
    float x, term, sum;
    printf("Enter value of x:");
    scanf("%f", &x);
    n = term = sum = count = 1;
    while (n <= 100)
    {
        term = term * x/n;
        sum = sum + term;
        count = count + 1;
        if (term < ACCURACY)
            n = 999;
        else
            n = n + 1;
    }
    printf("Terms = %d Sum = %f\n", count, sum);
}
```

输出
```
Enter value of x:0
Terms = 2 Sum = 1.000000

Enter value of x:0.1
Terms = 5 Sum = 1.105171

Enter value of x:0.5
Terms = 7 Sum = 1.648720

Enter value of x:0.75
Terms = 8 Sum = 2.116997

Enter value of x:0.99
Terms = 9 Sum = 2.691232

Enter value of x:1
Terms = 9 Sum = 2.718279
```

图 6.6 if ... else 语句的示例

![](img/65953ea584e494f3d396b2252cb5ea53_146_0.png)

执行逻辑如图 6.7 所示。如果条件 1 为假，则执行语句 3；否则继续执行第二个测试。如果条件 2 为真，则计算语句 1；否则计算语句 2，然后将控制转移到 statement-x。

![](img/65953ea584e494f3d396b2252cb5ea53_147_0.png)

图 6.7 嵌套 if ... else 语句的流程图

一家商业银行推出了一项向所有储户发放奖金的激励政策。政策如下：无论余额多少，每个人均获得 12 月 31 日余额 2% 的奖金；如果女性账户持有人的余额超过 5000 卢比，则获得 5% 的奖金。该逻辑可编码如下：

```c
if (sex is female)
{
    if (balance > 5000)
        bonus = 0.05 * balance;
    else
        bonus = 0.02 * balance;
}
else
{
    bonus = 0.02 * balance;
}
balance = balance + bonus;
```

在嵌套时，应注意让每个 if 都配对一个 else。考虑上面程序的另一种写法（乍一看似乎是正确的）：

```c
if (sex is female)
    if (balance > 5000)
        bonus = 0.05 * balance;
    else
        bonus = 0.02 * balance;
    balance = balance + bonus;
```

对于 else 属于哪个 if 存在歧义。在 C 语言中，else 与最近的未终止的 if 配对。因此，该 else 与内层 if 关联，而外层 if 没有对应的 else。这意味着计算机将尝试执行语句

`balance = balance + bonus;`

而并没有真正计算男性账户持有人的奖金。

考虑另一种同样看起来正确的写法：

```c
if (sex is female)
{
    if (balance > 5000)
        bonus = 0.05 * balance;
}
else
    bonus = 0.02 * balance;
    balance = balance + bonus;
```

在这种情况下，else 与外层 if 关联，因此会计算男性账户持有人的奖金。但是，对于余额等于或小于 5000 的女性账户持有人，由于内层 if 缺少对应的 else，其奖金不会被计算。

### 示例 6.4

图 6.8 中的程序使用嵌套的 if ... else 语句选择并打印三个数中的最大值。

程序
```c
/**********************************************************************/
/* SELECTING THE LARGEST OF THREE VALUES */
/**********************************************************************/
main()
{
    float A, B, C;

    printf("Enter three values");
    scanf("%f %f %f", &A, &B, &C);

    printf("\nLargest value is:");

    if (A > B)
    {
        if (A > C)
            printf("%f", A);
        else
            printf("%f\n", C);
    }
    else
    {
        if (C > B)
            printf("%f\n", C);
        else
            printf("%f\n", B);
    }
}
```

输出
```
Enter three values
23445 67379  88843
Largest value is 88843.000000
```

图 6.8 选择三个数中的最大值

## 6.6 else if 阶梯

当涉及多路决策时，还有另一种组合 if 的方式。多路决策是一系列 if 的链，其中每个 else 所关联的语句又是一个 if。它采用以下一般形式：

![](img/65953ea584e494f3d396b2252cb5ea53_149_0.png)

这种结构称为 else if 阶梯。条件从（阶梯的）顶部向下依次求值。一旦找到为真的条件，就执行与之关联的语句，并将控制转移到 statement-x（跳过阶梯的其余部分）。当所有 n 个条件均为假时，将执行包含默认语句的最终 else。图 6.9 显示了 else if 阶梯语句的执行逻辑。

让我们考虑一个学术机构中对学生进行评级的例子。评级按照以下规则进行：
