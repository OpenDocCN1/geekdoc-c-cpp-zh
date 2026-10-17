
```
for (Index i = 0; i < n; ++i)
  v(i) = ureal(ran);
return v;
}
```

`default_random_engine`非常简单，运行成本低，对于非正式用途来说已经足够好了。对于更专业的用途，标准库提供了一系列具有更好随机性属性和不同运行成本的引擎。示例包括`linear_congruential_engine`、`mersenne_twister_engine`和`random_device`。如果你想使用这些引擎，或者总的来说，如果你需要比`default_random_engine`更好的随机数生成器，那么你有一些内容需要阅读。要想了解你的系统随机数生成器的质量，请完成练习 10。

`std_lib_facilities.h`中的两个随机数生成器定义如下：

```cpp
int randint(int min, int max)
{
    static default_random_engine ran;
    return uniform_int_distribution<>{min,max}(ran);
}

int randint(int max)
{
    return randint(0,max);
}
```

这些简单的函数通常非常有用，但为了尝试点别的，让我们生成一个正态分布：

```cpp
auto gen = bind(normal_distribution<double>{15,4.0}, default_random_engine{});
```

标准库函数`bind()`来自`<functional>`，它构造一个函数对象，当调用该对象时，会使用其第二个参数作为第一个参数的参数来调用第一个参数。因此在这里，`gen()`返回符合正态分布的值，其均值为 15，标准差为 4.0，并使用`default_random_engine`。我们可以这样使用它：

```cpp
vector<int> hist(2*15);
for (int i = 0; i < 500; ++i)    // generate histogram of 500 values
    ++hist[int(round(gen()))];
```

```cpp
for (int i = 0; i != hist.size(); ++i) {   // write out histogram
    cout << i << '\t';
    for (int j = 0; j != hist[i]; ++j)
        cout << '*';
    cout << '\n';
}
```

我们得到：

0
1
2
3  **
4  *
5  *****
6  ****
7  ****
8  ******
9  *********
10  **************************
11  ****************************
12  *******************************
13  *****************************
14  ******************************
15  *******************************
16  ************************
17  ****************************
18  ****************************
19  ***************************
20  ***********
21  *********
22  *********
23  ******
24  *****
25  *
26  *
27
28
29

正态分布非常常见，也被称为高斯分布或（原因显而易见） simply “钟形曲线”。其他分布包括`bernoulli_distribution`、`exponential_distribution`和`chi_squared_distribution`。你可以在《C++程序设计语言》中找到它们的描述。整数分布返回封闭区间 `[a:b]`内的值，而实数（浮点数）分布返回开区间 `[a:b)`内的值。

默认情况下，引擎（除了可能的`random_device`）在每次运行程序时都会给出相同的序列。这对初始调试最为方便。如果我们想要引擎产生不同的序列，我们需要用不同的值对其进行初始化。这类初始化器通常被称为“种子”。例如：

```cpp
auto gen1 = bind(uniform_int_distribution<>{0,9}, 
default_random_engine{}); 
auto gen2 = bind(uniform_int_distribution<>{0,9}, 
default_random_engine(10)); 
auto gen3 = bind(uniform_int_distribution<>{0,9}, 
default_random_engine(5));
```

为了获得不可预测的序列，人们通常使用当天时间（精确到最后一纳秒；§26.6.1）或类似的东西作为种子。

## 24.8 标准数学函数

标准数学函数（`cos`、`sin`、`log`等）由标准库提供。它们的声明位于`<cmath>`中。

| 标准数学函数 | 描述 |
|:---|:---|
| `abs(x)` | 绝对值 |
| `ceil(x)` | 大于或等于 x 的最小整数 |
| `floor(x)` | 小于或等于 x 的最大整数 |
| `sqrt(x)` | 平方根；x 必须为非负数 |
| `cos(x)` | 余弦 |
| `sin(x)` | 正弦 |
| `tan(x)` | 正切 |
| `acos(x)` | 反余弦；结果非负 |
| `asin(x)` | 反正弦；返回最接近 0 的结果 |
| `atan(x)` | 反正切 |
| `sinh(x)` | 双曲正弦 |
| `cosh(x)` | 双曲余弦 |
| `tanh(x)` | 双曲正切 |
| `exp(x)` | 以 e 为底的指数 |
| `log(x)` | 自然对数，以 e 为底；x 必须为正数 |
| `log10(x)` | 以 10 为底的对数 |

标准数学函数为`float`、`double`、`long double`和`complex`（§24.9）类型的参数提供。如果你进行浮点运算，你会发现这些函数很有用。如果你需要更多细节，文档随处可见；你的在线文档是一个很好的起点。

如果标准数学函数无法产生在数学上有效的结果，它会设置变量`errno`。例如：

```cpp
errno = 0;
double s2 = sqrt(-1);
if (errno) cerr << "something went wrong with something somewhere";
if (errno == EDOM) // domain error
cerr << "sqrt() not defined for negative argument";
pow(very_large, 2) // not a good idea
if (errno == ERANGE) // range error
cerr << "pow(" << very_large << ", 2) too large for a double";
```

如果你进行严肃的数学运算，你必须检查`errno`，以确保在得到结果后它仍为 0。如果不为 0，说明出了问题。查看你的手册或在线文档，看看哪些数学函数可以设置`errno`，以及它们使用哪些值作为`errno`。

如示例所示，非零的`errno`仅表示“出问题了”。非标准库函数在出错时设置`errno`的情况并不少见，因此你必须更仔细地查看`errno`的值，以了解具体出了什么问题。如果在调用标准库函数后立即测试`errno`，并且你确保在调用前`errno==0`，你就可以依赖我们在示例中对`EDOM`和`ERANGE`的使用方式。`EDOM`在域错误（即参数问题）时设置。`ERANGE`在范围错误（即结果问题）时设置。

基于`errno`的错误处理相当原始。它源自最初的（1975 版）C 语言数学函数。

## 24.9 复数

复数在科学和工程计算中广泛使用。我们假设如果你需要复数，你将了解它们的数学性质，因此我们只展示如何在 ISO C++ 标准库中表示复数。你在`<complex>`中找到复数的声明及其相关标准数学函数：

```cpp
template<class Scalar> class complex {
// a complex is a pair of scalar values, basically a coordinate pair
    Scalar re, im;
public:
    constexpr complex(const Scalar & r, const Scalar & i) :re(r), im(i) { }
    constexpr complex(const Scalar & r) :re(r), im(Scalar ()) { }
    complex() :re(Scalar ()), im(Scalar ()) { }
    constexpr Scalar real() { return re; }   // real part
    constexpr Scalar imag() { return im; }   // imaginary part
    // operators: = += -= *= /=
};
```

标准库`complex`保证支持标量类型`float`、`double`和`long double`。除了`complex`的成员和标准数学函数（§24.8）外，`<complex>`还提供了一组有用的操作：

| 复数运算符 | 描述 |
|:---|:---|
| `z1+z2` | 加法 |
| `z1-z2` | 减法 |
| `z1*z2` | 乘法 |
| `z1/z2` | 除法 |
| `z1==z2` | 相等 |
| `z1!=z2` | 不等 |
| `norm(z)` | `abs(z)`的平方 |
| `conj(z)` | 共轭：如果`z`是`{re,im}`，则`conj(z)`是`{re,-im}` |
| `polar(rho,theta)` | 给定极坐标`(rho,theta)`构造复数 |
| `real(z)` | 实部 |
| `imag(z)` | 虚部 |
| `abs(z)` | 也称为 rho |
| `arg(z)` | 也称为 theta |
| `out << z` | 复数输出 |
| `in >> z` | 复数输入 |

注意：`complex`不提供`<`或`%`。完全像使用内置类型（如`double`）一样使用`complex<T>`。例如：

```cpp
using cplx = complex<double>; // sometimes complex<double> gets verbose
void f(cplx z, vector<cplx>& vc)
{
    cplx z2 = pow(z,z);
    cplx z3 = z*9.3+vc[3];
    cplx sum = accumulate(vc.begin(), vc.end(), cplx{});
    // ...
}
```

请记住，并非我们习惯从`int`和`double`中获得的所有运算都定义在`complex`上。例如：

```cpp
if (z2<z3)     // error: there is no < for complex numbers
```
