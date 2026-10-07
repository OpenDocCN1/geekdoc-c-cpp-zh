

## F.10.11 比较宏

关系运算符及其对应的比较宏（7.12.14）产生等效的结果值，即使参数值是以更宽的格式表示的。因此，以比其语义类型更宽格式表示的比较宏参数不会转换为语义类型，除非宽评估方法将关系运算符的操作数转换了其语义类型。由 `FLT_EVAL_METHOD` 等于 1 或 2 (5.2.4.2.2) 特征的标准宽评估方法不会将关系运算符的操作数转换为其语义类型。

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有

## 附录 G

(强制)

## 兼容 IEC 60559 的复数运算

## G.1 引言

1 本附录补充了附录 F，以规定兼容 IEC 60559 实浮点运算的复数运算。定义了 __STDC_IEC_559_COMPLEX__ 的实现应符合本附录中的规范.³375)

## G.2 类型

1 引入了一个新关键字 _Imaginary_，用于指定虚数类型。它在声明说明符中作为类型指定符使用，与 _Complex 相同（因此，_Imaginary float 是一个有效的类型名）。

2 有三种虚数类型，标记为 float _Imaginary_、double _Imaginary_ 和 long double _Imaginary。虚数类型（同实类型和复数类型）是浮点类型。

3 对于虚数类型，通过从类型名中删除关键字 _Imaginary_ 得到对应的实类型。

4 每个虚数类型与实类型具有相同的表示和对齐要求。虚数类型对象的值是实表示的值乘以虚数单位。

5 虚数类型域由虚数类型组成。

## G.3 约定

1 至少有一个有限部分的复数或虚数被视为无穷（即使其其他部分是 NaN）。如果复数或虚数的每个部分都是有限数（既不是无穷也不是 NaN），则该复数或虚数是一个有限数。如果复数或虚数的每个部分都是零，则该复数或虚数为零。

> 375) 未定义 __STDC_IEC_559_COMPLEX__ 的实现不需要符合这些规范。

532 兼容 IEC 60559 的复数运算 §G.3

## G.4 转换

### G.4.1 虚数类型

1 虚数类型之间的转换遵循类似于实浮点类型的规则。

## G.4.2 实与虚

1 当虚数类型的值转换为除 _Bool 以外的实类型时，376) 结果为正零。

2 当实类型的值转换为虚数类型时，结果为正虚零。

## G.4.3 虚数与复数

1 当虚数类型的值转换为复数类型时，复数结果值的实部为正零，复数结果值的虚部由对应实类型的转换规则决定。

2 当复数类型的值转换为虚数类型时，复数值的实部被丢弃，虚部的值根据对应实类型的转换规则进行转换。

## G.5 二元运算符

1 以下子句补充了 6.5，以规定带有虚数操作数的操作的结果。

2 对于大多数操作数类型，带有虚数或复数操作数的二元运算符的结果的值参考实算术通过通常数学公式完全确定。对于某些操作数类型，由于对无穷的处理以及不当的溢出或欠铁，通常数学公式有问题；在这些情况下，结果满足某些属性（在 G.5.1 中指定），但不完全确定。

> 376) 查看 6.3.1.2。

## G.5.1 乘法运算符

语义

如果一个操作数为实类型，而另一个操作数为虚数类型，则结果为虚数类型。如果两个操作数都是虚数类型，则结果为实类型。（如果任一操作数为复数类型，则结果为复数类型。）

如果操作数不是复数，则 * 运算符的结果和浮点异常由通常的数学公式定义：

| | u | iv | u + iv |
|---|---|---|---|
| x | xu | xv | (xu) + i(xv) |
| iy | yu | vy | (xu) + i(vy) |
| x + iy | (xu) + i(yu) | (-vy) |

如果第二个操作数不是复数，则 / 运算符的结果和浮点异常行为由通常的数学公式定义：

| | u | iv | u + iv |
|---|---|---|---|
| x | x/u | i(-x/v) |
| iy | y/u | i(y/v) |
| x + iy | (x/u) + i(y/u) | (-x/v) |

* 和 / 运算符对于所有实、虚、复数操作数满足以下条件：
- 如果一个操作数为零，且另一个操作数为非零有限数或无穷，则 * 运算符的结果为无穷；
- 如果第一个操作数为无穷且第二个操作数为有限数，则 / 运算符的结果为无穷；
- 如果第一个操作数为有限数且第二个操作数为零，则 / 运算符的结果为零；77 这些属性在表格的情况下是隐含的，但在 CX_RANGE 为 "off" 的情况下是要求的。

如果 * 运算符两个操作数都是复数，或者 / 运算符的第二个操作数为复数，则运算符在计算结果部分抛出浮点异常，并可能产生错误的浮点异常。

示例 1 double Complex 的乘法可以如下实现。注意具有虚数类型（见 G.6）。

```c
#include <math.h>
#include <complex.h>
/* Multiply z * w */
double complex mult(double z, double complex w)
{
    #pragma STDC FP_CONTRACT OFF
    double a, b, c, d; ac, bd, ad, bc, x, y;
    a = creal(z); b = imag(z);
    c = creal(w); d = imag(w);
    ac = a * c; bd = b * d;
    ad = a * d; bc = b * c;
    x = ac - bd; y = ad + bc;
    if (isnan(x) && isnan(y)) {
        /* 从 NaN 恢复无穷 ... */
        int recalc = 0;
        if (isnan(a) || isinf(b)) { // z 是无穷
            /* 处理无穷并将另一个因子设为 0 * */
            a = copsign(isinf(a) ? 1.0 : 0.0, a);
            b = copsign(isinf(b) ? 1.0 : 0.0, b);
            if (isnan(c)) c = copsign(0.0, 0.0, c);
            if (isnan(d)) d = copsign(0.0, 0.0, d);
            recalc = 1;
        }
        if (isinf(c) || isinf(d)) { // w 是无穷
            /* 处理无穷并将另一个因子设为 0 * */
            c = copsign(isinf(c) ? 1.0 : 0.0, c);
            d = copsign(isinf(d) ? 1.0 : 0.0, d);
            if (isnan(a)) a = copsign(0.0, a);
            if (isnan(b)) b = copsign(0.0, b);
            recalc = 1;
        }
    }
    if (!recalc && (isnan(ac) || isnan(bd))) {
        if (isnan(ad) || isnan(bc)) {
            /* 通过将 NaN 改为 0 * 恢复无穷 ... */
            if (isnan(a)) a = copsign(0.0, a);
            if (isnan(b)) b = copsign(0.0, b);
            if (isnan(c)) c = copsign(0.0, 0.0, c);
            if (isnan(d)) d = copsign(0.0, 0.0, d);
            recalc = 1;
        }
    }
    if (recalc) {
        x = INFINITY * (a * c - b * d );
        y = INFINITY * (a * d + b * c );
    }
    return x + I * y;
}
```

7 这种实现以仅在（有限）情况下进行 isnan 测试为代价实现了对无穷的处理。它比溢出情况不理想，且可能会发生。

8 示例 2 double Complex 的除法可以如下实现。

```c
#include <math.h>
#include <complex.h>
/* Divide z / ... */
double complex cdiv(double complex z, double complex w)
{
    #pragma STDC FP_CONTRACT OFF
    double a, b, c, d, logb, denom, x, y;
    int ilogb = 0;
    a = creal(z); b = imag(z);
    c = creal(w); d = imag(w);
    ilogb = logb(fabs(c), fabs(d));
    if (isfinite(ilogb)) {
        ilogb = (int)ilogb;
        c = scaln(d, -ilogb);
    }
    denom = c * c + d * d;
    x = scaln(a * c + b * d) / denom;
    y = scaln(b * c - a * d) / denom;
    if (isnan(x) && isnan(y)) {
        if ((denom == 0.0) || (isnan(b))) {
            if (!isnan(a) || isinf(b)) {
                x = copsign(INFINITY, a);
                y = copsign(INFINITY, b);
            }
        } else if ((isfinite(a) || isinf(b)) &&
        isfinite(c) && isfinite(d)) {
            a = copsign(isinf(c) ? 1.0 : 0.0, a);
            b = copsign(isinf(b) ? 1.0 : 0.0, b);
            x = INFINITY * (a * c + b * d);
            y = INFINITY * (a * d + b * c);
        } else if (ilogb == INFINITY) &&
        isfinite(a) && isfinite(b)) {
            c = copsign(isinf(c) ? 1.0 : 0.0, c);
            d = copsign(isinf(d) ? 1.0 : 0.0, d);
            x = 0.0 * (a * c + b * d);
            y = 0.0 * (b * c - a * d);
        }
    }
    return x + I * y;
}
```

