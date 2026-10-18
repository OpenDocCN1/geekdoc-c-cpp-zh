
# Table 7.5  Common members of `std::numeric_limits` from the STL limits Library (examples in CppBookCode, FloatingPoint.cpp).

| STL algorithm function | Description | Examples |
|---|---|---|
| `numeric_limits<T>::epsilon()` | Returns a machine epsilon value that is the minimum difference between 1.0 and the nearest higher value representable in the FP format. | ```cpp
#include <limits>

cout << boolalpha;
cout << "numeric_limits<double>::epsilon() = " << numeric_limits<double>::epsilon() << endl;
cout << "numeric_limits<double>::radix = " << numeric_limits<double>::radix << endl;
cout << "numeric_limits<double>::digits = " << numeric_limits<double>::digits << endl;
cout << "numeric_limits<double>::digits10 = " << numeric_limits<double>::digits10 << endl;
cout << "numeric_limits<double>::max() = " << numeric_limits<double>::max() << endl;
cout << "numeric_limits<double>::min() = " << numeric_limits<double>::min() << endl;
cout << "numeric_limits<double>::has_denorm = " << numeric_limits<double>::has_denorm << endl;
cout << "numeric_limits<double>::has_infinity = " << numeric_limits<double>::has_infinity << endl;
cout << "numeric_limits<double>::denorm_min() = " << numeric_limits<double>::denorm_min() << endl;
cout << "numeric_limits<double>::lowest() = " << numeric_limits<double>::lowest() << endl;
``` |
| `numeric_limits<T>::min()` | Returns the minimum absolute value for type T. |  |
| `numeric_limits<T>::max()` | Returns the maximum value for type T. |  |

## 7.4.5 The Standard FP Operation Model

It is common practice to define the relation of a mathematical operation with respect to its counterpart in the FP domain. For example, the addition of two real values x and y in the FP domain can be represented as follows:

$D(x+y)=(x+y)(1+\rho),\ \text{where }|\rho|\leq\varepsilon$  (7.39)

The + operator can be replaced by other operators, such as −, *, or /. This is called the *standard FP model*.

## 7.4.6 Computations That Are Conscious of Numerical Errors

So far, we have discussed inevitable errors related to the rounding of real values to their closest representations in the FP domain. However, a second source of errors can be generated during mathematical operations on FP numbers. To understand this, let’s consider FP addition, which involves proper *exponent scaling*, followed by *normalization*. For instance, adding two values, i.e. $2.72\cdot10^{-1}$ and $1.78\cdot10^{-3}$, the latter component’s exponent must be scaled to the higher one, as shown in Figure 7.11.

![Figure 7.11 Adding two FP numbers (a). To perform addition, the values must be scaled to have the same exponent (b). Large differences in the exponents (high dynamics) can lead to the loss of significant digits.](img/31dee73f41f3d43a1f2e2b4eaffa2afd_548_0.png)

In our example, we get the following:

$2.72\cdot10^{-1}+1.78\cdot10^{-3}\Rightarrow 2.72\cdot10^{-1}+0.01\cdot10^{-1}=2.73\cdot10^{-1}$

We can see that when using only $p=3$ precision digits we lose two digits from the second term due to the shift necessary for the exponent scaling. This can lead to significant errors. The conclusion is that if we have a choice, e.g. when adding a series of FP numbers, we should always order the addition in such a way as to add the values of exponents that are as similar as possible.

Precise descriptions of FP addition, multiplication, and other algorithms can be found in the literature (Knuth 1998). On most modern systems, these are implemented in the microprocessor or a software library. The good news is that adding and subtracting FP numbers is exact if there is no overflow (e.g. due to the *guard digits*). This feature does not hold for multiplication and division, but in this case the relative error does not exceed ½ ULP – assuming there is no overflow.

When performing FP computations, we should be aware of the many peculiarities that can lead to imprecise or even totally incorrect results. The most obvious are the previously mentioned overflow and underflow. However, similarly dangerous is subtracting numbers that are nearly equal in magnitude. In such a case, most of the leading digits vanish, and a rounding error may occur that promotes the digit in the last place to a more significant position. For example, when subtracting 2.71828 − 2.71829, we end up with 1e−05, which reflects only the last digit since all the others are canceled out. But if 2.71828 and 2.71829 were already rounded off, then after subtraction the last digits may be less accurate, since they may already be inaccurate due to the previous rounding. That is, the digits remaining after subtraction convey incorrect information. Even worse, they are promoted to more significant positions of the significand (in our example, 1 in the first position). Errors arising from such situations, called *catastrophic cancelations*, can be very severe. They can arise even in simple computations, such as when finding the roots of a quadratic equation \(ax^2+bx+c=0\), as discussed in Section 3.16. Its solution is simple, and the roots are given in the analytical form:

$$x_1=\frac{1}{2a}\left(-b-\sqrt{b^2-4ac}\right),\quad x_2=\frac{1}{2a}\left(-b+\sqrt{b^2-4ac}\right) \tag{7.40}$$

A problem may arise if \(ac\ll b^2\) and \(b<0\). In this case, \(\sqrt{b^2-4ac}\approx |b|\), and \(x_1\) will suffer from subtracting two almost-identical values. A simple way out, in this case, is to first observe that

$$x_1x_2=c \tag{7.41}$$

and to compute \(x_2\) from Eq. (7.40) and then, finally, \(x_1\) from Eq. (7.41). The following code shows this idea:

```
```cpp
double a {}, b {}, c {};
// Read in a, b, c ...

double x1 {}, x2 {};

double d = b * b - 4.0 * a * c;
if( d > 0.0 )
{
    if( b < 0.0 )
    {
        x1 = (-b+sqrt(d)) / (a + a); // -b becomes positive and we have addition
        x2 = c / x1;
    }
    else
    {
        x1 = ( -b - sqrt( d ) ) / ( a + a ); // adding two negative values
        x2 = c / x1;
    }
}
```
```

This code needs polishing to become fully operable. However, the main point of this section is to emphasize that rather than naively implementing the formulas shown in a mathematics book, frequently we need to reformulate the problem to avoid errors specific to the floating-point domain. Many expressions need a closer look in the light of FP computations before implementation. Another example is \(x^2-y^2\), which is almost always better implemented using the familiar equivalent form \((x-y)(x+y)\). Not only do we save one multiplication, but we also avoid catastrophic cancelation errors, which are likely in the first representation (Goldberg 1991).

A terse but practical introduction to the subject of floating-point computations is the paper by Allison (2006). For a more in-depth introduction with mathematical proofs, we recommend the
