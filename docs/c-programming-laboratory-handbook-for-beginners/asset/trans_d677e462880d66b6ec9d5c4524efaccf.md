

![](img/dad8bddd927fabdab2417ecbf1eb24eb_48_0.png)

# 示例程序

用 C 编写的程序，用于反转给定的四位整数，并检查它是否为回文数*使用 for 循环*。输出给定数字并附带合适的消息。

```c
#include<stdio.h>
#include<process.h>
void main()
{
    int n, num, rev=0, rem, i;
    printf("Enter a number: \n");
    scanf("%d", &n);
    num=n;

    /* check if the input is a 4 digit number */
    if(n<=999||n>=10000)
    {
        printf("\nEnter four digit number\n");
        exit(0);
    }

    for(i=n; i!=0;)
    {
        rem=i%10;
        rev=rev*10+rem;
        i=i/10;
    }

    printf("\nReverse of the input is: \n\t%d", rev);

    /* check if the input and the reversed numbers are same */
    if(num==rev)
        printf("\nThe Number is Palindrome\n");
    else
        printf("\nThe Number is not Palindrome\n");
}
```

## 示例输出

```text
Enter a number:
121
Enter four digit number

Enter a number:
12221
Enter four digit number

Enter a number:
4578
Reverse of the input is: 8754
The Number is not Palindrome

Enter a number:
1221
Reverse of the input is: 1221
The Number is Palindrome

Enter a number:
1000
Reverse of the input is: 1
The Number is not Palindrome
```

# 数组

数组是相同类型元素的集合，这些元素位于同一标识符下，并通过索引号引用。数组对于执行排序、搜索等操作既高效又有用。

![](img/dad8bddd927fabdab2417ecbf1eb24eb_49_0.png)

## 数组声明

数组在程序中使用之前必须先声明。

*语法：* `type identifier[size];`

这里的 type 指定要存储在数组中的元素类型。例如，

```c
double height[10];
float width[20];
int min[9];
char name[20];
```

在 C 语言中，数组从位置 0 开始。数组元素在内存中占据相邻位置。数组中的任何项都可以通过其索引访问。例如，

$m = \text{height}[0];$

变量 $m$ 将被赋值为 height 数组第一项的值。

下面的程序段声明一个包含五个整数的数组，并打印该数组的所有元素。

```c
int myArray[5] = {1, 2, 3, 4, 5};
```

```c
/* To print all the elements of the array */
for (int i=0; i<5; i++)
{
    printf("%d", myArray[i]);
}
```

# 相关理论：所用逻辑

多项式的一般形式为

$p(x) = a_nx^n + a_{n-1}x^{n-1} + a_{n-2}x^{n-2} + \cdots + a_1x + a_0$

考虑一个例子

$3x^3 + 4x^2 + 7x + 8$

通常多项式的求值方式为

$3 * x * x * x + 4 * x * x + 7 * x + 8$

因此

乘法次数 = 6

加法次数 = 3

## 霍纳方法

- 多项式表达式

  P(x) = aₙxⁿ + aₙ₋₁xⁿ⁻¹ + aₙ₋₂xⁿ⁻² + … + a₁x + a₀

  可写成另一种形式：

  P(x) = (a₀ + x(a₁ + x(a₂ + … + x(aₙ₋₁ + x·aₙ))))

- 在带括号的表达式中，总是先计算内层括号，因此先计算 (aₙ₋₁ + x·aₙ)。
- 因此，我们可以将常量 aₙ 作为 “result” 变量的初始值。

  result = aₙ

  然后，P(x) = (a₀ + x(a₁ + x(a₂ + … + x(aₙ₋₁ + x·result))))

  内部项作为 result = (aₙ₋₁ + x·result)

  下一项作为 result = (aₙ₋₂ + x·result)

  下一项作为 result = (aₙ₋₃ + x·result)

  .

  .

  .

  外部项作为 result = (a₀ + x·result)

  通常 result = aᵢ + x·result，其中 i 从 n−1 到 0。

### 示例

以如下式子为例

3x³ + 4x² + 7x + 8

它可写成另一种形式：

(8 + x * (7 + x * (4 + x * 3)))

因此

乘法次数 = 3
加法次数 = 3。

传统方法中的乘法次数多于霍纳方法中的乘法次数。因此，霍纳方法更高效。

多项式求值的重要步骤如下：

- 将所有系数读入数组，例如 a。将类似 result 的变量初始化为 a_n。
- 然后重复执行语句

  result = result * x + a[i],

  对于从 n − 1 到 0 的所有 i 值，以步长 −1 执行。

## 示例程序

### 程序 1

在一列中打印 8 的乘法表的程序。此程序将展示如何使用 for 循环，以及如何使用转义序列实现正确的缩进。

```c
#include<stdio.h>
void main()
{
    int i, j=8;
    printf("Times 8 Table\n");
    for(i=0; i<=12; i=i+1)
    {
        printf("%d x %d=%d\n", j, i, j*i);
    }
    printf("\n");
}
```

#### 示例输出

```text
Times 8 Table
8 x 0=0
8 x 1=8
8 x 2=16
8 x 3=24
8 x 4=32
8 x 5=40
8 x 6=48
8 x 7=56
8 x 8=64
8 x 9=72
8 x 10=80
8 x 11=88
8 x 12=96
```

```c
iMarks[1] = 64;
iMarks[2] = 66;
iMarks[3] = 74;
for (i = 0; i < 4; i++)
  newMarks[i] = iMarks[i];
for (j = 0; j < 4; j++)
  printf("%d\n", newMarks[j]);
}
```

## 示例输出

78
64
66
74

## 算法

开始
**步骤 1：** 输入一个数 n
**步骤 2：** 以步长 1 对 i ← 0 到 n 执行 FOR 循环
  输入数组 a[i] 的元素
  结束 FOR
**步骤 3：** 输入 x 的值
**步骤 4：** res ← a[n]
**步骤 5：** 以步长 -1 对 i ← n-1 到 0 执行 FOR 循环
  res ← res * x + a[i]
  结束 FOR
**步骤 6：** 输出 res 的值
停止

## 流程图

![](img/dad8bddd927fabdab2417ecbf1eb24eb_55_0.png)

## 程序

```c
#include<stdio.h>
void main()
{
    int a[40];
    int x, n, i, res;
    printf("\nEnter maximum power of x:\n\t");
    scanf("%d", &n); /* Read the maximum size of array */
    printf("\nEnter the coefficients of the polynomial:\n");
    /*----------------read elements of the array----------------*/
    for(i=0; i<=n; i++)
    {
        printf("\nEnter coefficient of X^%d=\t", i);
        scanf("%d", &a[i]);
    }
    printf("\nEnter the value of X=\t");
    scanf("%d", &x);
    /*----------------Compute the value of the polynomial----------------*/
    res=a[n];
    for(i=n-1; i>=0; i--)
        res=res*x+a[i];
    printf("Value of polynomial=\t%d\n", res); /* print the result of the polynomial */
}
```

## 输出

```text
Enter maximum power of x: 2
Enter the coefficients of the polynomial:
Enter coefficient of X^0=1
Enter coefficient of X^1=2
Enter coefficient of X^2=3
Enter the value of X=2
Value of polynomial=17

Enter maximum power of x: 5
Enter the coefficients of the polynomial:
Enter coefficient of X^0=4
Enter coefficient of X^1=2
Enter coefficient of X^2=6
Enter coefficient of X^3=1
Enter coefficient of X^4=7
Enter coefficient of X^5=8
Enter the value of X=4
Value of polynomial=10156

Enter maximum power of x: 1
Enter the coefficients of the polynomial:
Enter coefficient of X^0=2
Enter coefficient of X^1=3
Enter the value of X=1
Value of polynomial=5
```

# 学习成果

- 验证给定多项式求值的效率。
- 能够使用合适的循环结构。
- 能够使用有效和无效输入执行程序。

# 练习程序

- 1. 编写一个 C 程序，打印从 5 到 −5 的所有整数。
- 2. 编写一个 C 程序，打印前 10 个整数的平方。向用户询问两个整数，先询问较小的一个，再询问较大的一个。通过重复加法将这两个整数相乘。例如，如果从用户处获得 3 和 5，那么我们可以通过将较大的数 (5) 相加三次来求它们的乘积。
- 3. 编写一个简单的 C 程序，使用数组打印出工资超过 3000 的员工人数。
- 4. 编写一个 C 程序，演示如何读取、写入和遍历整数数组。
- 5. 编写一个 C 程序，向用户询问一个整数，并打印该整数的乘法表。

# 学期作业 5

## 问题定义

设计、开发并执行一个 C 程序，将其输入复制到输出，并将每个由一个或多个空白组成的字符串替换为单个空白。

## 目标

- 使用内置函数 getchar() 和 putchar() 处理输入、输出操作。
- 格式化文本。

## 相关理论

*什么是字符串？*

在 C 中，字符串由字符数组表示。字符串的结尾用一个特殊字符标记，即空字符，它只是值为 0 的字符。在 ASCII 字符集中，空字符命名为 NULL。空字符或字符串终止字符由另一个字符转义序列 '\0' 表示。

![](img/dad8bddd927fabdab2417ecbf1eb24eb_58_0.png)

![](img/dad8bddd927fabdab2417ecbf1eb24eb_58_1.png)

