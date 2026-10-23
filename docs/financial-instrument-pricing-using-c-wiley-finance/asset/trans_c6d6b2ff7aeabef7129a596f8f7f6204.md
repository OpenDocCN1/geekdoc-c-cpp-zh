

随着位数增长，算术运算变得非常昂贵。其一些特性和属性如下：

- 类似于 IEEE 单精度、双精度和四精度浮点数据类型以及 Intel 扩展双精度类型的类比。
- 这些类型的 `std::numeric_limits` 的特化。
- 能够定义基数 2 和基数 10 的数字类型。
- 这些类型支持无穷大（当结果会溢出时生成无穷大）和 NaN（对于任何数学上未定义的操作都会生成）。

该库同时支持基数 2 和基数 10 类型或数制。数制使用有限数量的不同的符号。每个符号称为一个数字，它表示一个量。这些不同符号的数量称为数制的基数或基数。二进制数制（基数 2）具有数字符号 {0, 1}，十进制数制（基数 10）具有数字符号 {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}，而十六进制数制（基数 16）具有数字符号 {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E}。数字是通过并置数字形成的。

模板类定义为：

```
enum digit_base_type
{
    digit_base_2 = 2,
    digit_base_10 = 10
};
```

```
template <unsigned Digits, digit_base_type base = digit_base_10,
    class Allocator = void, class Exponent = int,
    ExponentMin = 0, ExponentMax = 0>
class cpp_bin_float;
```

```
typedef number<cpp_bin_float<50> > cpp_bin_float_50;
typedef number<cpp_bin_float<100> > cpp_bin_float_100;
```

```
typedef number<backends::cpp_bin_float<24,
    backends::digit_base_2,void,boost::int16_t,-126,127>, et_off>
cpp_bin_float_single;
```

```
typedef number<backends::cpp_bin_float<53,
    backends::digit_base_2,
    void, boost::int16_t, -1022, 1023>, et_off>
cpp_bin_float_double;
```

该库中还有类可提供分别达到 50 和 100 位十进制数字精度的算术类型：

```
template <unsigned Digits10, class ExponentType=boost::int32_t, class Allocator=void>
class cpp_dec_float;
```

```
typedef number<cpp_dec_float<50> > cpp_dec_float_50;
typedef number<cpp_dec_float<100> > cpp_dec_float_100;
```

一般而言，Boost multiprecision 将在我们希望避免溢出或需要计算非常大的数字时使用，无论是永久使用还是用于其他应用程序。

一些典型问题是：

- S1: 我们希望具有任意精度还是定点精度？
- S2: 我们希望使用二进制还是十进制数制？
- S3: 在整数和浮点数之间进行选择。
- S4: 确定应用程序的性能和精度要求。

我们现在通过一些简单的示例介绍该库，以帮助我们熟悉语法。

## A1.3 初始示例和应用

在本节中，我们介绍多精度数据类型以及如何在数值应用中使用它们。

### A1.3.1 计算圆的面积

如果一本书中至少没有提到如何以给定精度计算 π，那么这本书就不完整了。这个数字对应于半径为 1 的圆的面积：

```
template<typename T>
T CircleArea(const T& r)
{
    using boost::math::constants::pi;
    return pi<T>() * r * r;
}
```

```
// radius == 1, so area = pi
const int r = 1;
float r_f = r;
float a_f = CircleArea(r_f);

double r_d = static_cast<double>(r);
double a_d = CircleArea(r_d);
```

```
cpp_dec_float_50 r_mp = static_cast<cpp_dec_float_50>(r);
cpp_dec_float_50 a_mp = CircleArea(r_mp);

cpp_dec_float_100 r_mp100 = static_cast<cpp_dec_float_100>(r);
cpp_dec_float_100 a_mp100 = CircleArea(r_mp100);

std::cout << std::setprecision(std::numeric_limits<float>::digits10)
          << a_f << std::endl;

std::cout << std::setprecision(std::numeric_limits<double>::digits10)
          << a_d << std::endl;

std::cout
    << std::setprecision(std::numeric_limits<cpp_dec_float_50>::digits10)
    << a_mp << std::endl;

std::cout
    << std::setprecision(std::numeric_limits<cpp_dec_float_100>::digits10)
    << a_mp100 << std::endl;
```

该程序的输出为：

```
3.14159
3.14159265358979
3.1415926535897932384626433832795028841971693993751
3.14159265358979323846264338327950288419716939937510582097494459230781640
628620899628034825342117068
```

精确值为：

```
3.14159265358979323846264338327950288419716939937510582097494459230781
64062862089962803482534211706798
```

上面的代码出于教学目的编写，以展示如何定义和显示多精度数据。我们现在讨论叙拉古的阿基米德实际上是如何计算 π 的（详见 Dörrie, 1965）。阿基米德通过外切多边形的周长 a 和内切多边形的周长 b 来近似半径为 r 的圆的周长（我们取 r = 1/2）。该算法基于这样一个事实：两个数 x 和 y 的 *调和平均* 小于它们的 *几何平均*：

$$\frac{2xy}{x+y} < \sqrt{xy}.$$

周长 a 和 b 的阿基米德递推公式为：

$$a_{n+1}=\frac{2a_nb_n}{a_n+b_n},\qquad b_{n+1}=\sqrt{b_na_{n+1}},\ n\ne 0$$

初始值为：

$a_0 = 2\sqrt{3},\ b_0 = 3\ \text{(radius = 1/2)}.$

该算法的代码为：

```
```cpp
template <typename T>
    void ArchimedesPi(int N)
    { // N == number of iterations

      T an, anp1, bn, bnp1;
      an = T(2.0)*boost::multiprecision::sqrt(T(3.0)); bn = T(3.0);

      for (int n = 1; n <= N; ++n)
      {
          anp1 = T(2.0)*an*bn / (an + bn);
          bnp1 = boost::multiprecision::sqrt(bn*anp1);

          an = anp1; bn = bnp1;
      }

      std::cout << "N, value: "
                << std::setprecision(std::numeric_limits<T>::digits10)
                << N << "/" << bn << "\\n\\n";

      std::cout << "Error: " << std::setprecision(8)
                << boost::multiprecision::abs(bn - an) << "\\n";
    }
```
```

我们多次调用此函数并显示输出的子集：

```
```cpp
int N = 200;

for (int n = 0; n <= N; n += 10)
{
    ArchimedesPi< cpp_dec_float_100 >(n);
}
```
```

输出为：

```
```
N, value:
20/3.141592653589662682701706171090774719985979379159334657412021084377287
605362950884738001859546262235

Error: 3.9166728e-13

N, value:
40/3.14159265358979323846264338327930025868175440272163320532165222527356
511645931880184364385214446692
```

```
Error: 3.5621932e-25

N, value:
60/3.141592653589793238462643383279502884089176205070734653848659243661099
9692877181976336684872480311458

Error: 3.2397958e-37

N, value:
80/3.141592653589793238462643383279502884197169399375007601736897232360797
37032492766828422638159104739

Error: 2.9465771e-49

N, value:
100/3.14159265358979323846264338327950288419716939937510582097494450297793
9790038327551870396055373551631

Error: 2.6798963e-61

N, value:
120/3.14159265358979323846264338327950288419716939937510582097494459230781
6406204963949135527982537650455

Error: 2.4373515e-73

N, value:
140/3.14159265358979323846264338327950288419716939937510582097494459230781
6406286208998627960933400058354

Error: 2.2167583e-85

N, value:
160/3.14159265358979323846264338327950288419716939937510582097494459230781
6406286208998628034825342117001

Error: 2.0161299e-97

N, value:
180/3.14159265358979323846264338327950288419716939937510582097494459230781
6406286208998628034825342117068

Error: 1.833314e-109
```

我们因此看到，随着我们增加多边形的边数，近似值会改善。

### A1.3.2 数值微分

在第 22 章（第 22.3 节）中，我们讨论了使用差商和三次样条近似单变量函数的<|message|> 和二阶导数的几种技术。我们还讨论了当我们减去两个几乎相等的数时发生的 *灾难性抵消*。在这种情况下，该操作会使相对精度增加得远大于绝对误差的增加。这种现象也称为 *有效数字丢失*。在近似导数的情况下，我们在第 22.3.5 节中看到，存在一个步长的临界值，低于该值近似值会产生灾难性结果。我们使用浮点运算计算了指数函数的该临界值（大约为 0.003）。

我们使用以下通用差商公式来近似函数的导数：

```
template <typename T>
    T firstDividedDifference(const FunctionType<T>& f, T xval, T h)
{ // 2nd order approximation h^2/6

    return (f(xval+h) - f(xval-h)) / (T(2) * h);
}
```

```
template <typename T>
    T RichardsonfirstDividedDifference(const FunctionType<T>& f,
                                    T xval, T h)
{ // 4th order approximation to df/dx using Richardson extrapolation

    T h2 = h * T(0.5);
    T f1 = 4*firstDividedDifference(f, xval, h2);
    T f2 = firstDividedDifference(f, xval, h);

    return (f1 - f2) / 3;
}
```

```
template <typename T>
    T firstDividedDifferenceOrder4(const FunctionType<T>& f, T xval, T h)
{ // 4th order approximation h^4/30

    return (f(xval -2*h) - 8*f(xval -h) + 8*f(xval + h)
        - f(xval + 2*h)) / (12 * h);
}
```

```
template <typename T>
    T secondDividedDifference(const FunctionType<T>& f, T xval, T h)
{ // 2nd order h^2/12

    return (f(xval+h) - (2 * f(xval)) + f(xval-h)) / (h * h);
}
```

```
template <typename T>
    T secondDividedDifferenceOrder4(const FunctionType<T>& f, T xval, T h)
{ // 4th order h^4/90

    return (-f(xval - 2*h) + 16*f(xval - h) - 30*f(xval)
        + 16*f(xval + h) - f(xval + 2*h)) / (12 * h * h);
}
```

