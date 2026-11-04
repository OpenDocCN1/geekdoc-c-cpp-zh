
幂运算具有最高优先级，除非被括号覆盖，如下所示：

2**4-3 = 16-3 = 13
2**(4-3) = 2**1 = 2

代码清单 1.4 展示了 Arithmetic.c 的内容，它说明了如何执行算术运算。

### 代码清单 1.4：Arithmetic.c

```c
#include <stdio.h>

int main()
{
    int x = 5 + 3;
    int y = 5 - 3;
    int z = 5 * 3;
    int w = 5 / 3;

    printf("5 + 3 = %d\n",x);
    printf("5 - 3 = %d\n",y);
    printf("5 * 3 = %d\n",z);
    printf("5 / 3 = %d\n",w);

    return (0);
}
```

代码清单 1.4 包含一个 main() 函数，该函数初始化 4 个整数变量 x、y、z 和 w，随后是 4 个 printf() 语句，用于显示这些相同变量的值。运行代码清单 1.4 中的 C 程序后，输出如下：

5 + 3 = 8
5 - 3 = 2
5 * 3 = 15
5 / 3 = 1

## 递增/递减运算符

在 C 中，有两种方法可以将变量递增或递减 1。一种方法如下面的代码块所示：

```c
int a=5, b=9;
a += 1;
b -= 1;
```

上述代码块执行后，a 的值为 6，b 的值为 8。但是，前面的结构不能与 == 运算符组合使用：必须先执行递增或递减操作，然后才能执行 if 逻辑。

第二种方法是使用递增和递减运算符，分别是 ++ 和 --。当这些运算符出现在变量的*左*侧时，递增或递减操作会在任何其他操作*之前*执行。然而，当这些运算符出现在变量的*右*侧时，递增或递减操作会在其他算术操作*之后*执行。以下代码块说明了这些要点：

```c
int x=0, y=1;
if(++x == 1) { //first add 1 to x and then compare (this is true)
               // do something
}

if(y++ == 1) { //first compare and then add 1 to y (this is true)
               //do something
}
```

上述代码块执行后，x 的值为 1，y 的值为 2，并且*两个* if 语句都会执行。

现在考虑下面的代码块，其中 x 和 y 分别初始化为值 6 和 2：

```c
int x=6, y=2;
if(--x == 6) {
//subtract 1 from x and then compare (this is false)
    // do something
}

if(y++ == 3) { // first compare then add 1 to y (this is false)
    // do something
}
```

执行前面的一对 if 语句后，x 等于 5，y 等于 3，但*两个* if 语句都不会执行（请将此结果与前面的一对 if 语句进行比较）。

## 三元运算符

三元运算符是执行 if/else 条件逻辑的一种简写方式。作为一个简单示例，考虑以下代码块：

```c
if (a < b)
{
    x = 1;
}
else
{
    x = 2;
}
```

前面的代码片段可以用更抽象的条件形式表示如下：

```c
if (expr1)
{
    expr2;
}
else
{
    expr3;
}
```

简化前面 if/else 逻辑的另一种方式是使用具有以下形式的三元运算符：

```
expr1 ? expr2 : expr3
```

例如，本节开头的代码块可以表示如下：

```
x = (a<b ? 1 : 2);
```

在前面的代码片段中，如果不等式 a<b 为真，则将 x 赋值为 1；否则，将 x 赋值为 2。

本章接下来的部分包含代码示例，说明如何使用 C 内置函数计算一个数的向上取整值和向下取整值、一个数的绝对值以及一些三角函数。第 4 章提供了更多 C 内置函数（然后向你展示如何在 C 中定义自定义函数）。

## 计算向上取整值和向下取整值

C 提供了各种执行算术和数学计算的内置函数，例如 ceil() 函数和 floor() 函数。代码清单 1.5 展示了 MathValues.c 的内容，它说明了如何计算小数值的向上取整值和向下取整值。

### 代码清单 1.5：MathValues.c

```c
#include <math.h>
#include <stdio.h>

int main()
{
   double y, z;

   y = ceil(1.05);      // y = 2.0
   z = ceil(-1.05);     // z = -1.0
   printf("y = %.2f ; z = %.2f\n", y, z);

   y = floor(2.8);
   z = floor(-2.8);
   printf("y = %.2f ; z = %.2f\n", y, z);

   return 0;
}
```

**代码清单 1.5** 包含一个 `main()` 函数，该函数通过两次调用 C 内置的 `ceil()` 函数来初始化变量 `y` 和 `z`。接下来，一个 `printf()` 语句显示 `z` 和 `y` 的值，然后通过调用 C 内置的 `floor()` 函数为 `y` 和 `z` 赋予不同的值，之后显示它们的值。编译并执行 **代码清单 1.5** 中的代码后，输出如下：

```text
The absolute value of x1 is 4.
fabs( -11.230000 ) = 11.230000
```

## 计算绝对值

C 提供了对浮点数执行算术计算的内置函数，例如 `fabs()` 函数。**代码清单 1.6** 展示了 `AbsValues.c` 的内容，它说明了如何计算整数和小数值的绝对值。

### 代码清单 1.6：AbsValues.c

```c
#include <math.h>
#include <stdlib.h>
#include <stdio.h>

int main()
{
    int x1 = -4, y1;
    double x2=-11.23,y2;

    y1 = abs(x1);
    printf("The absolute value of x1 is %d\n", y1);

    y2 = fabs(x2);
    printf("fabs( %lf ) = %lf\n", x2, y2);

    return 0;
}
```

代码清单 1.6 包含一个 main() 函数，该函数初始化变量 x1、y1 和 y2。变量 y1 和 y2 分别通过调用内置函数 abs() 和 fabs() 进行初始化。两个 printf() 语句显示 x1、y1、x2 和 y2 的值。编译并执行代码清单 1.6 中的代码后，输出如下：

The absolute value of x1 is 4.
fabs( -11.230000 ) = 11.230000

## 在 C 中计算三角函数值

C 还提供了执行三角函数计算的内置函数。代码清单 1.7 展示了 TrigValues.c 的内容，它说明了如何使用 sin()、cos() 和 tan() 函数分别返回 x 的正弦、余弦和正切值。

### 代码清单 1.7：TrigValues.c

```c
#include <math.h>
#include <stdio.h>

#define PI 3.1415926535

int main()
{
    double pi, x, y1, y2, y3;

    x = PI/4;
    y1 = sin(x);
    y2 = cos(x);
    y3 = tan(x);

    printf("sin( %lf ) = %lf\n", x, y1);
    printf("cos( %lf ) = %lf\n", x, y2);
    printf("tan( %lf ) = %lf\n", x, y3);

    return 0;
}
```

代码清单 1.7 包含一个 main() 函数，该函数将变量 x 初始化为 PI/4，然后分别通过调用 C 内置函数 sin()、cos() 和 tan() 来初始化变量 y1、y2 和 y3。三个 printf() 语句显示 y1、y2 和 y3 的值。编译并执行代码清单 1.7 中的代码后，输出如下：

sin( 0.785398 ) = 0.707107
cos( 0.785398 ) = 0.707107
tan( 0.785398 ) = 1.000000

## 在 C 中使用不同的进制

整数和十进制数默认以 10 为基数，但你可以使用其他进制，例如二进制、八进制和十六进制。代码清单 1.8 展示了 OtherBases.c 的内容，其中包含各种代码片段，说明如何在 C 中处理二进制、八进制和十六进制数。

请注意以下注意事项：二进制整数字面量是 C++14 的特性，并不属于任何 C 标准。虽然二进制整数在 C 中是 GCC 的非标准扩展，但当需要执行位级操作（第 7 章讨论）时，这个特性可能很有用。

### 代码清单 1.8：OtherBases.c

```c
#include <stdio.h>

// binary values start with 0b:
int a=0b0101; // decimal value is 5

// octal values start with 0:
int b=016;   // decimal value is 14

// hex values start with 0x or 0X:
int x1=0x18, x2=0X37, x3=0xAB;

int main()
{
    int a1=0b0101, b1=0x16, c1=123;
    int x1=0x18, x2=0X37, x3=0xAB;

    printf("a1=%d b2=%d c3=%d\n",a1, b1, c1);
    printf("x1=%d x2=%d x3=%d\n",x1, x2, x3);
}
```
