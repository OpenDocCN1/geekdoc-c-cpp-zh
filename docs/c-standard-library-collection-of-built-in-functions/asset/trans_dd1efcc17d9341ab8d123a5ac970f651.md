
## double ldexp(double x, int exponent)

### 描述

C 库函数 **double ldexp(double x, int exponent)** 返回 **x** 乘以 2 的 **exponent** 次方。

### 声明

以下是 ldexp() 函数的声明。

```c
double ldexp(double x, int exponent)
```

### 参数

- **x** -- 这是表示尾数的浮点值。
- **exponent** -- 这是指数的数值。

### 返回值

此函数返回 x * 2<sup>exp</sup>

### 示例

以下示例展示了 ldexp() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
   double x, ret;
   int n;

   x = 0.65;
   n = 3;
   ret = ldexp(x ,n);
   printf("%f * 2^%d = %f\n", x, n, ret);

   return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
0.650000 * 2^3 = 5.200000
```

## double log(double x)

### 描述

C 库函数 double log(double x) 返回 x 的自然对数（以 e 为底的对数）。

### 声明

以下是 log() 函数的声明。

```c
double log(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回 x 的自然对数。

### 示例

以下示例展示了 log() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 2.7;

    /* finding log(2.7) */
    ret = log(x);
    printf("log(%lf) = %lf", x, ret);

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
log(2.700000) = 0.993252
```

## double log10(double x)

### 描述

C 库函数 double log10(double x) 返回 x 的常用对数（以 10 为底的对数）。

### 声明

以下是 log10() 函数的声明。

```c
double log10(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回 x 的常用对数，x 的值大于零时。

### 示例

以下示例展示了 log10() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 10000;

    /* finding value of log10(10000) */
    ret = log10(x);
    printf("log10(%lf) = %lf\n", x, ret);

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
log10(10000.000000) = 4.000000
```

## double modf(double x, double *integer)

### 描述

C 库函数 **double modf(double x, double *integer)** 返回小数部分（小数点后的部分），并将 integer 设置为整数部分。

### 声明

以下是 modf() 函数的声明。

```c
double modf(double x, double *integer)
```

### 参数

- **x** -- 这是浮点值。
- **integer** -- 这是指向存储整数部分的对象的指针。

### 返回值

此函数返回 x 的小数部分，保持相同的符号。

### 示例

以下示例展示了 modf() 函数的用法。

```c
#include<stdio.h>
#include<math.h>

int main ()
{
    double x, fractpart, intpart;

    x = 8.123456;
    fractpart = modf(x, &intpart);

    printf("Integral part = %lf\n", intpart);
    printf("Fraction Part = %lf \n", fractpart);

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Integral part = 8.000000
Fraction Part = 0.123456
```

## double pow(double x, double y)

### 描述

C 库函数 double pow(double x, double y) 返回 x 的 y 次幂，即 x^y。

### 声明

以下是 pow() 函数的声明。

```c
double pow(double x, double y)
```

### 参数

- x -- 这是浮点底数。
- y -- 这是指数浮点值。

### 返回值

此函数返回 x 的 y 次幂的结果。

### 示例

以下示例展示了 pow() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    printf("Value 8.0 ^ 3 = %lf\n", pow(8.0, 3));
    printf("Value 3.05 ^ 1.98 = %lf", pow(3.05, 1.98));
    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Value 8.0 ^ 3 = 512.000000
Value 3.05 ^ 1.98 = 9.097324
```

## double sqrt(double x)

### 描述

C 库函数 double sqrt(double x) 返回 x 的平方根。

### 声明

以下是 sqrt() 函数的声明。

```c
double sqrt(double x)
```

### 参数

- **x** -- 这是浮点值。

### 返回值

此函数返回 x 的平方根。

### 示例

以下示例展示了 sqrt() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{

    printf("Square root of %lf is %lf\n", 4.0, sqrt(4.0) );
    printf("Square root of %lf is %lf\n", 5.0, sqrt(5.0) );

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Square root of 4.000000 is 2.000000
Square root of 5.000000 is 2.236068
```

## double ceil(double x)

### 描述

C 库函数 **double ceil(double x)** 返回大于或等于 **x** 的最小整数值。

### 声明

以下是 ceil() 函数的声明。

```c
double ceil(double x)
```

### 参数

- **x** -- 这是浮点值。

### 返回值

此函数返回不小于 **x** 的最小整数值。

### 示例

以下示例展示了 ceil() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
   float val1, val2, val3, val4;

   val1 = 1.6;
   val2 = 1.2;
   val3 = 2.8;
   val4 = 2.3;

   printf ("value1 = %.1lf\n", ceil(val1));
   printf ("value2 = %.1lf\n", ceil(val2));
   printf ("value3 = %.1lf\n", ceil(val3));
   printf ("value4 = %.1lf\n", ceil(val4));

   return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
value1 = 2.0
value2 = 2.0
value3 = 3.0
value4 = 3.0
```

## double fabs(double x)

### 描述

C 库函数 double fabs(double x) 返回 x 的绝对值。

### 声明

以下是 fabs() 函数的声明。

```c
double fabs(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回 x 的绝对值。

### 示例

以下示例展示了 fabs() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    int a, b;
    a = 1234;
    b = -344;

    printf("The absolute value of %d is %lf\n", a, fabs(a));
    printf("The absolute value of %d is %lf\n", b, fabs(b));

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
The absolute value of 1234 is 1234.000000
The absolute value of -344 is 344.000000
```

## double floor(double x)

### 描述

C 库函数 double floor(double x) 返回小于或等于 x 的最大整数值。

### 声明

以下是 floor() 函数的声明。

```c
double floor(double x)
```

### 参数

- x -- 这是浮点值。

### 返回值

此函数返回不大于 x 的最大整数值。

### 示例

以下示例展示了 floor() 函数的用法。

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    float val1, val2, val3, val4;

    val1 = 1.6;
    val2 = 1.2;
    val3 = 2.8;
    val4 = 2.3;

    printf("Value1 = %.1f\n", floor(val1));
    printf("Value2 = %.1f\n", floor(val2));
    printf("Value3 = %.1f\n", floor(val3));
    printf("Value4 = %.1f\n", floor(val4));

    return(0);
}
```

让我们编译并运行上面的程序，将会产生以下结果：

```text
Value1 = 1.0
Value2 = 1.0
Value3 = 2.0
```
