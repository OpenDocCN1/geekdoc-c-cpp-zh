

分数 8/10，或 4/5，可以在基数 10 中精确表示。但大多数计算机系统会以基数 2 存储结果，而在该基数中，4/5 是一个无限重复的小数：

```
0.1100110011001100...
```

因此，0.8 在存储到 x 时会被舍入为近似值，且该值可能取决于舍入方法。

然而，可能存在一种实现并不满足 IEC 60559 的所有要求；例如，底层硬件可能无法胜任。因此，C99 定义了两个宏，可在预处理器指令中用于检查合规性。首先，宏

```
__STDC_IEC_559__
```

如果实现符合 IEC 60559 浮点规范，则有条件地定义为常量 1。其次，宏

```
__STDC_IEC_559_COMPLEX__
```

如果实现遵循 IEC 60559 兼容的复数运算，则有条件地定义为常量 1。

如果实现未定义这些宏，则无法保证 IEC 60559 合规性。

## The fenv.h Header File

fenv.h 头文件提供了一种与浮点环境交互的手段。也就是说，它允许你设置浮点控制模式值，以控制浮点计算的进行方式，并且允许你确定浮点状态标志或异常的值，这些标志或异常报告有关算术计算影响的信息。控制模式设置的示例是指定用于舍入数字的方法。状态标志的示例是当操作产生浮点溢出时被设置的标志。设置状态标志的操作被描述为引发异常。

状态标志和控制模式只有在硬件支持它们时才有意义。例如，如果硬件没有该选项，你就无法更改舍入方法。

你使用预处理器指令来打开支持：

```
#pragma STDC FENV_ACCESS ON
```

支持保持开启，直到程序到达包含该 pragma 的块的末尾，或者，如果该 pragma 是外部的，则到文件或翻译单元的末尾。或者，你可以使用以下指令关闭支持：

```
#pragma STDC FENV_ACCESS OFF
```

你也可以发出以下 pragma：

```
#pragma STDC FENV_ACCESS DEFAULT
```

这会恢复编译器的默认状态，该状态取决于实现。

此功能对于从事关键浮点计算的人员很重要，但对普通用户来说兴趣有限，因此本附录不涉及细节。

## The STDC FP_CONTRACT Pragma

某些浮点处理器可以将多操作符浮点表达式收缩为单个操作。例如，处理器可能能够一步计算以下表达式：

```
x*y - z
```

这会提高计算速度，但会降低计算的可预测性。STDC FP_CONTRACT pragma 允许你打开或关闭此功能。默认状态取决于实现。

要为特定计算关闭收缩功能，然后再次打开，可以这样做：

```
#pragma STDC FP_CONTRACT OFF
val = x * y - z;
#pragma STDC FP_CONTRACT ON
```

## Additions to the math.h Library

C90 数学库在很大程度上声明了类型为 double 参数和类型为 double 返回值的函数，例如以下

```
double sin(double);
double sqrt(double);
```

C99 和 C11 库为所有这些函数提供了类型为 float 和类型为 long double 的版本。这些函数在名称中使用 f 或 l 后缀，如下所示：

```
float sinf(float);            /* float version of sin() */
long double sinl(long double);  /* long double version of sin() */
```

具有不同精度级别的函数族允许你为特定目的选择所需的最有效类型和函数组合。

C99 还添加了几种在科学、工程和数学计算中常用的函数。表 RS.V.14 列出了所有数学函数的类型为 double 的版本，并标识了 C99 的新增内容。在许多情况下，函数返回的值可以使用现有函数计算，但新函数速度更快或更准确。例如，log1p(x) 表示与 log(1 + x) 相同的值，但 log1p(x) 使用不同的算法，对于 x 的小值更准确。因此，你通常会使用 log() 函数进行计算，但如果高精度至关重要，则对于 x 的小值使用 log1p()。

除了这些函数之外，数学库还定义了几个与数字分类和舍入相关的常量和函数。例如，一个值可以被分类为无穷大、非数字(NaN)、正常、次正规和真零。(NaN 是一个特殊值，表示值不是数字；例如，asin(2.0) 返回 NaN，因为 asin() 仅对范围在 −1 到 1 之间的参数有定义。次正规数是指其大小小于可完全精确表示的最小值的数。) 还有专门的比较函数，其行为与标准关系运算符在有一个或多个参数为异常值时不同。

你可以使用 C99 的分类方案来检测计算中的不规则性。例如，来自 math.h 的 isnormal() 宏如果其参数是正常数则返回 true。以下是使用该函数在数字变为次正规时终止循环的代码：

```
#include <math.h>  // for isnormal()
...
float num = 1.7e-19;
float numprev = num;

while (isnormal(num))  // while num has full float precision
{
    numprev = num;
    num /= 13.7f;
}
```

简而言之，对浮点计算如何处理的详细控制支持得到了扩展。

## Support for Complex Numbers

复数是一个具有实部和虚部的数。实部是普通实数，例如浮点类型所表示的。虚部表示一个虚数。虚数本身是 -1 的平方根的倍数。在数学中，复数通常写成 4.2 + 2.0i 的形式；i 象征地表示 -1 的平方根。

C99 支持三种复数类型（在 C11 中此支持为可选）：

- `float _Complex`
- `double _Complex`
- `long double _Complex`

例如，float _Complex 值将使用与 float 的两个元素数组相同的内存布局存储，实值存储在第一个元素中，虚值存储在第二个元素中。

C99 和 C11 实现也可能支持三种虚数类型：

- `float _Imaginary`
- `double _Imaginary`
- `long double _Imaginary`

包含 `complex.h` 头文件可让你使用 `complex` 表示 `_Complex`，使用 `imaginary` 表示 `_Imaginary`。

复数类型的算术运算遵循数学的通常规则。例如，`(a+b*I)*(c+d*I)` 的值是 `(a*c-b*d)+(b*c+a*d)*I`。

`complex.h` 头文件定义了一些宏和几个接受复数并返回复数的函数。特别是，宏 `I` 表示 -1 的平方根。它使你能够执行以下操作：

```
double complex c1 = 4.2 + 2.0 * I;
float imaginary c2 = -3.0 * I;
```

C11 提供了一种第二种方法，即 `CMPLX()` 宏，用于为复数赋值。例如，如果 `re` 和 `im` 是类型为 `double` 的值，你可以这样做：

```
double complex c3 = CMPLX(re, im);
```

其意图是该宏可以更好地处理特殊情况，例如 `im` 为无穷大或非数字，比直接赋值更好。

`complex.h` 头文件原型化了几个复数函数。许多是 `math.h` 函数的复数等价物，使用 `c` 前缀。例如，`csin()` 返回其复数参数的复数正弦。其他函数专门与复数的特性相关。例如，`creal()` 返回复数的实部，`cimag()` 以实数形式返回虚部。也就是说，给定 `z` 为类型 `double complex`，以下为真：

```
z = creal(z) + cimag(z) * I;
```

如果你熟悉复数并需要使用它们，你会想要浏览 `complex.h` 的内容。

以下是说明复数支持某些部分的简短程序。

```
// complex.c -- complex numbers
#include <stdio.h>
#include <complex.h>
void show_cmlx(complex double cv);
int main(void)
{
    complex double v1 = 4.0 + 3.0*I;
    double re, im;
    complex double v2;
    complex double sum, prod, conjug;
    printf("Enter the real part of a complex number: ");
```
