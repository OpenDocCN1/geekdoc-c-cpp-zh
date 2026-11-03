
## 算法

开始

- **步骤 1：** 输入二次方程的系数 (a, b, c)。
- **步骤 2：** 如果第一个系数为零
    输出“无效输入”
    否则
    d ← b² – 4ac
    r ← √|d|
    如果 d 的值等于零
        输出“根相等”
        r1 ← r2 ← – b/(2a)
        输出 r1, r2
    否则如果 d 的值大于零
        输出“根为实数且互异”
        r1 ← (–b + r)/(2a)
        r2 ← (–b – r)/(2a)
        输出 r1, r2
    否则
        输出“根为复数”
        r1 ← – b/(2a)
        r2 ← r/(2a)
        打印根
    结束如果
    结束如果

结束

## 流程图

![](img/dad8bddd927fabdab2417ecbf1eb24eb_28_0.png)

## 程序

```c
#include<stdio.h>
#include<math.h>
void main()
{
    int a, b, c;
    float d, r, r1, r2;
    printf("\n Enter the three co-efficients:\n");
    scanf("%d%d%d", &a, &b, &c);
    if(a==0) /*-------------check for valid input-----------*/
        printf("\nInvalid Input\n");
    else
    {
        d=(b*b) - (4*a*c);
        r=sqrt(fabs(d));
        if(d==0) /*-------------check if roots are
        equal-------------*/
        {
            printf("\nThe roots are real and equal\n");
            r1=r2=-b/(2.0*a);
            printf("\nThe roots are \n\tr1=\t%f\n\tr2=\t%f\n",
            r1, r2);
        }
        else if(d>0) /*----------------check if roots are real-------
        -------*/
        {
            printf("\nThe roots are real and distinct\n");
            r1=(-b+r)/(2.0*a);
            r2=(-b-r)/(2.0*a);
            printf("\nThe roots are \n\tr1=\t%f\n\tr2=\t%f\n",
            r1, r2);
        }
        else /*-----------------roots are complex----------------*/
        {
            printf("\nThe roots are complex\n");
            r1=-b/(2.0*a);
            r2=r/(2.0*a);
            printf("\nThe roots are:\n\tr1=%f + i %f\n\tr2=%f-i%f\n", r1, r2, r1, r2);
        }
    }
}
```

## 输出

示例 1：

```text
Enter the three co-efficients:
0 1 2
Invalid Input
```

*结论：* 第一个系数不能为零。

示例 2：

```text
Enter the three co-efficients:
2 3 0
The roots are real and distinct
The roots are
   r1=0.000000
   r2=-1.500000
```

示例 3：

```text
Enter the three co-efficients:
1 5 6
The roots are real and distinct
The roots are
   r1=-2.000000
   r2=-3.000000
```

示例 4：

```text
Enter the three co-efficients:
1 2 2
The roots are complex
The roots are:
   r1=-1.000000+i1.000000
   r2=-1.000000-i1.000000
```

## 学习成果

- 能够编写一个“C”程序来求二次方程的根。
- 能够成功执行该程序，并针对所有可能的输入组合进行测试。

## 相关程序

### 程序 1

用 C 语言编写程序，求并输出给定二次方程（系数非零）的所有根，**使用 Switch 语句。**

```c
#include<stdio.h>
#include<math.h>
#include<process.h>
void main()
{
    int option;
    double a, b, c, d;
    double r,r1,r2;
    printf(" Quadratic Equation ax^2+bx+c=0 \n");
    printf("*******************************\n");

    /* Get a, b, and c from user */
    printf("\n a=");
    scanf("%lf", &a);
    printf("b=");
    scanf("%lf", &b);
    printf("c=");
    scanf("%lf", &c);

    if(a==0) /* check for valid input */
    {
        printf("\n Invalid Input \n");
        exit(0);
    }

    /* Calculate determinant */
    d=(b*b)-(4*a*c);
    r=sqrt(abs(d));
    if(d==0)
       option=1;
    else if(d>0)
       option=2;
    else
       option=3;
    /* Use switch statement */
    switch(option)
    {
        case 1: printf("\nThe roots are real and equal\n");
            r1=r2=-b/(2.0*a);
            printf("\nThe roots are \nr1 =\t%f\n\tr2 =\t%f\n", r1, r2);
            break;
        case 2: printf("\nThe roots are real and distinct\n");
            r1=(-b+r)/(2.0*a);
            r2=(-b-r)/(2.0*a);
            printf("\nThe roots are \n\tr1 =\t%f\n\tr2 =\t%f\n",
            r1, r2);
            break;
        case 3: printf("\nThe roots are complex\n");
            r1=-b/(2.0*a);
            r2=r/(2.0*a);
            printf("\nThe roots are:\n\tr1=%f +i %f\n\tr2=%f -i%f\n", r1, r2, r1, r2);
            break;
    }/* End Switch */
}/* End program */
```

### 输出

1.

```text
Quadratic Equation ax^2+bx+c=0
**************************************
a=0
b=1
c=2
Invalid Input
```

2.

```text
Quadratic Equation ax^2+bx+c=0
**************************************
a=1
b=2
c=1
The roots are real and equal
The roots are
    r1=-1.000000
    r2=-1.000000
```

3.

```text
Quadratic Equation ax^2+bx+c=0
************************************
a=1
b=3
c=2
The roots are real and distinct
The roots are
    r1=-1.000000
    r2=-2.000000
```

4.

```text
Quadratic Equation ax^2+bx+c=0
************************************
a=1
b=2
c=1
The roots are complex
The roots are:
    r1=-1.000000+i1.000000
    r2=-1.000000-i1.000000
```

## 学期作业 2

设计、开发并执行一个 C 程序，以实现欧几里得算法，求两个整数的 GCD 和 LCM，并输出结果以及给定的整数。

- 学习欧几里得算法。
- 编写一个 C 程序，对任意给定的一组两个整数执行欧几里得算法。
- 学习将纸笔方法与所开发的算法联系起来，并针对所有可能的输入类型进行测试。

有些情况下，你可能想多次做同一件事。例如，你想把同一个单词打印 10 次。你可以输入 10 个 printf 函数，但使用循环更容易。你唯一需要做的就是设置一个循环，让同一个 printf 函数执行 10 次。循环有三种基本类型，如下所示：

- 1. “for 循环”
- 2. “while 循环”
- 3. “do while 循环”

```c
while (condition)
{
    Action1 /* until condition is true action1 is executed*/
}
Action2 /* if condition fails action2 is executed*/
```

在编程语言中，while 循环是一种*控制流语句*，它允许代码基于给定的*布尔*条件重复执行。while 循环可以看作是一个重复的 *if 语句*。一个 *while* 结构由一块代码和一个条件组成。条件会被求值，如果条件为 *true*，则执行该块内的代码。这一过程会重复，直到条件变为 *false*。因为 *while* 循环在执行代码块之前检查条件，所以这种控制结构称为前置测试循环（入口控制循环）。

### 示例程序：While 循环

### 程序 1

打印消息“Hello”10 次的程序。该程序将让你了解 while 循环如何工作。

```c
#include <stdio.h>
void main()
{
    int i=10;
    while (i > 0)
    {
        printf("Hello\n");
            i=i - 1;
    }
}
```

### 示例输出

```text
Hello
Hello
Hello
Hello
Hello
Hello
Hello
Hello
Hello
Hello
```

### 相关理论

**欧几里得算法**（也称为 **Euclid's algorithm**）是一种计算最大公约数（GCD）的高效方法，最大公约数也称为最大公因数（GCF）或最高公因数（HCF）。它以希腊数学家欧几里得命名。

两个数的 GCD 是能同时整除这两个数且不留余数的最大数。

### 示例

计算 18 和 48 的 GCD：
18 的除数/因数是 1、2、3、6、9 和 18。
48 的除数/因数是 1、2、3、4、6、8、12、16、24 和 48。
因此，18 和 48 的公除数/公因数是 1、2、3 和 6。
于是 GCD(18, 48) = 6。

然而，由于这种方法耗时，通常不用于大数；因此我们使用欧几里得算法。

### 示例

计算 142 和 38 的 GCD

```text
142 = 38 × 3 + 28
38 = 28 × 1 + 10
28 = 10 × 2 + 8
10 = 8 × 1 + 2
8 = 2 × 4 + 0
GCD(142, 38) = 2
```

该算法基于以下两个观察：

- 如果 b 整除 a，则 GCD(a, b) = b。
- 确实如此，因为任何数（尤其是 b）的除数都不会大于该数本身。
- 如果对于整数 t 和 r 有 a = bt + r，则 GCD(a, b) = GCD(b, r)。

### 欧几里得算法

- 1. 用第二个数除第一个数。
- 2. 如果余数为零，则第二个数就是 GCD。
- 3. 否则，重复步骤 1 和 2，其中第二个数变为第一个数，余数变为第二个数。

让我们看一个求 40 和 64 的 GCD 的示例。

- 第一个数 = 40，第二个数 = 64，余数 = 40
- 第一个数 = 64，第二个数 = 40，余数 = 24

