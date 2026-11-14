

## 4.2.1.1 Mandelbrot 集

The Mandelbrot set—named after its creator, Benoît B. Mandelbrot—is the set of complex numbers that don't reach infinity by successive squaring and adding the original value:

曼德勃罗集——以其创建者布瓦·B·曼德勃罗命名——是指那些通过连续平方并加上原始值而不会趋于无穷大的复数集合：

\( M = \{c \in \mathbf{C} : \lim_{n \to \infty} z_n(c) \neq \infty \} \)

where

\( z_0(c) = c \quad z_{n+1}(c) = z_n^2 + c \)

It can be shown that a point is outside the Mandelbrot set when \(|z_n(c)| > 2\). The most expensive part of computing the magnitude is the square root at the end. C++ provides a function norm which is the square of abs, i.e., the calculation of abs without the final sqrt. Thus, we replace the continuation criterion abs(z) < 2 with norm(z) < 4.

可以证明，当 \(|z_n(c)| > 2\) 时，该点位于曼德勃罗集之外。计算模长最耗时的部分是最后的平方根运算。C++ 提供了一个名为 norm 的函数，它是 abs 的平方，即不包含最后一次 sqrt 的 abs 计算。因此，我们将继续判据 abs(z) < 2 替换为 norm(z) < 4。

```
=> c++11/mandelbrot.cpp
```

The visualization of the Mandelbrot set is a color coding of the iterations needed to reach that limit. To draw the fractal, we used the cross-platform library Simple DirectMedia Layer (SDL 1.2). The numeric part is realized by the class mandel_pixel that computes for each pixel on the screen how many iterations are needed until norm(z) > 4 and which color that represents:

曼德勃罗集的可视化是对达到该极限所需迭代次数的颜色编码。为了绘制分形，我们使用了跨平台库 Simple DirectMedia Layer (SDL 1.2)。数值部分由类 mandel_pixel 实现，它计算屏幕上每个像素直到 norm(z) > 4 所需的迭代次数以及该次数代表的颜色：

```
class mandel_pixel
{
public:
  mandel_pixel(SDL_Surface* screen, int x, int y,
               int xdim, int ydim, int max_iter)
  : screen(screen), max_iter(max_iter), iter(0), c(x, y)
  {
    // scale y to [-1.2,1.2] and shift -0.5+0i to the center
    c *= 2.4f / static_cast<float>(ydim);
    c-= complex<float>(1.2 * xdim / ydim + 0.5, 1.2);
    iterate();
  }

  int iterations() const { return iter; }
  uint32_t color() const { ... }

private:
  void iterate()
  {
    complex<float> z= c;
    for (; iter < max_iter && norm(z) <= 4.0f; iter++)
      z= z * z + c;
  }
  // ...
  int iter;
  complex<float> c;
};
```

The complex numbers are scaled such that their imaginary parts lie between -1.2 and 1.2 and are shifted by 0.5 to the left. We have omitted the code lines for the graphics, as they are beyond the scope of this book. The complete program is found on GitHub, and the resulting picture in Figure 4-7.

复数被缩放，使其虚部介于 -1.2 和 1.2 之间，并向左平移 0.5。我们省略了图形相关的代码行，因为它们超出了本书的范围。完整程序可在 GitHub 上找到，生成的图片见图 4-7。

In the end, our core computation is realized in three lines and the other ≈ 50 lines are needed to draw a nice picture, despite our having chosen a very simple graphics library. This is unfortunately not an uncommon situation: many real-world applications contain far more code for file I/O, database access, graphics, web interfaces, etc., than for the scientific core functionality.

最终，我们的核心计算只需三行代码即可实现，而其他约 50 行代码用于绘制一幅漂亮的图片，尽管我们选择了一个非常简单的图形库。不幸的是，这并非罕见情况：许多现实世界的应用程序包含的文件 I/O、数据库访问、图形、Web 界面等代码远多于科学核心功能的代码。

## 4.2.1.2 混合复数计算

As demonstrated before, complex numbers can be built from most numeric types. In this regard, the library is quite generic. For its operations it is not so generic: a value of type complex<T> can only be added (subtracted, etc.) with a value of type complex<T> or T. As a consequence, the simple code

如前所示，复数可以由大多数数值类型构建。在这方面，该库非常通用。但对于其操作则不那么通用：类型 complex<T> 的值只能与类型 complex<T> 或 T 的值相加（相减等）。因此，简单的代码

```
complex<double> z(3, 5), c = 2 * z;
```

![](img/ba4defb7bf504868bf19451f3cd4b9bb_213_0.png)

doesn't compile since no multiplication is defined for int and complex<double>. The problem is easily fixed by replacing 2 with 2.0. However, the issue is more annoying in generic functions, e.g.:

无法编译，因为未定义 int 和 complex<double> 之间的乘法。将 2 替换为 2.0 即可轻松解决此问题。然而，在泛型函数中，这个问题更令人烦恼，例如：

```cpp
template <typename T>
inline T twice(const T& z)
{
    return 2 * z;  // Error!
}

int main ()
{
    complex<double> z(3, 5), c;
    c = twice(z);
}
```

The function twice will not compile for the same reason as before. If we wrote 2.0 * z it would compile for complex<double> but not for complex<float> or complex<long double>. The function

函数 twice 出于与之前相同的原因无法编译。如果我们写 2.0 * z，它可以为 complex<double> 编译，但不能为 complex<float> 或 complex<long double> 编译。函数

```cpp
template <typename T>
complex<T> twice(const complex<T>& z)
{
    return T(2) * z;
}
```

works with all complex types—but only with complex types. In contrast, the following:

适用于所有复数类型——但仅适用于复数类型。相比之下，以下代码：

```cpp
template <typename T>
inline T twice(const T& z)
{
    return T(2) * z;
}
```

compiles with complex and non-complex types. However, when T is a complex type, 2 is unnecessarily converted into a complex and four multiplications plus two additions are performed where only half of them are needed. A possible solution is to overload the last two implementations. Alternatively, we can write type traits to deal with it.

可与复数和非复数类型一起编译。但是，当 T 是复数类型时，2 会被不必要地转换为复数，并且执行了四次乘法和两次加法，而实际上只需要其中一半。一种可能的解决方案是重载最后两个实现。或者，我们可以编写类型特征来处理它。

The programming becomes more challenging when multiple arguments of different types are involved, some of them possibly complex numbers. The Matrix Template Library (MTL4, Section 4.7.3) provides mixed arithmetic for complex numbers. We are committed to incorporate this feature into future standards.

当涉及多个不同类型的参数（其中一些可能是复数）时，编程变得更加具有挑战性。矩阵模板库（MTL4，第 4.7.3 节）为复数提供了混合运算。我们承诺将此功能纳入未来的标准。

## 4.2.2 随机数生成器

Many application domains—like computer simulation, game programming, or cryptography—use random numbers. Every serious programming language thus offers generators for them. Such generators produce sequences of numbers that appear random. A random generator may depend on physical processes like quantum phenomena. However, most generators are based on pseudo-random calculations. They have an internal state—called a Seed—that is transformed by deterministic computation each time a pseudo-random number is requested. Thus, a pseudo-random number generator (PRNG) always emits the same sequence when started with the same seed.

许多应用领域——如计算机模拟、游戏编程或密码学——都使用随机数。因此，每种严肃的编程语言都为其提供生成器。此类生成器产生看似随机的数字序列。随机生成器可能依赖于量子现象等物理过程。然而，大多数生成器基于伪随机计算。它们具有一个内部状态——称为种子（Seed）——每次请求伪随机数时，该状态都会通过确定性计算进行转换。因此，伪随机数生成器（PRNG）在使用相同种子启动时，始终会发出相同的序列。

Before C++11, there were only the rand and srand functions from C with very limited functionality. More problematic is that there are no guarantees for the quality of generated numbers and it is indeed quite low on some platforms. Therefore, a high-quality <random> library was added in C++11. It was even considered to deprecate rand and srand altogether in C++. They are still around but should really be avoided where the quality of random numbers is important.

在 C++11 之前，只有来自 C 的 rand 和 srand 函数，功能非常有限。更成问题的是，生成数字的质量没有保证，在某些平台上确实相当低。因此，C++11 添加了高质量的 <random> 库。甚至曾考虑在 C++ 中彻底弃用 rand 和 srand。它们仍然存在，但在随机数质量很重要的地方，确实应该避免使用它们。

### 4.2.2.1 保持简单

The random number generators in C++11 provide a lot of flexibility which is very useful for experts but somewhat overwhelming for beginners. Walter Brown proposed a set of novice-friendly functions [6]. Slightly adapted, 4 they are:

C++11 中的随机数生成器提供了大量灵活性，这对专家非常有用，但对初学者来说有些令人不知所措。Walter Brown 提出了一组对新手友好的函数 [6]。经过略微调整，4 它们是：

```
#include <random>

std::default_random_engine& global_urng()
{
    static std::default_random_engine u{};
    return u;
}

void randomize()
{
    static std::random_device rd{};
    global_urng().seed(rd());
}

int pick(int from, int thru)
{
    static std::uniform_int_distribution<> d{};
    using param_t = decltype(d)::param_type;
    return d(global_urng(), param_t{from, thru});
}

double pick(double from, double upto)
{
    static std::uniform_real_distribution<> d{};
    using param_t = decltype(d)::param_type;
    return d(global_urng(), param_t{from, upto});
}
```

To start with random numbers, you could just copy these three function into the project and look at the details later. Walter's interface is pretty simple and nonetheless sufficient for many practical purposes like code testing. We only need to remember the following three functions:

要开始使用随机数，你可以将这三个函数复制到项目中，稍后再查看细节。Walter 的接口非常简单，但对于代码测试等许多实际用途来说已经足够。我们只需要记住以下三个函数：

- randomize: Make the following numbers really random by initializing the generator's seed.
- pick(int a, int b): Give me an int in the interval [a, b] when a and b are int.
- pick(double a, double b): Give me an double in the right-open interval [a, b) when a and b are double.

- randomize：通过初始化生成器的种子，使后续数字真正随机。
- pick(int a, int b)：当 a 和 b 为 int 时，给我一个在区间 [a, b] 中的 int。
- pick(double a, double b)：当 a 和 b 为 double 时，给我一个在右开区间 [a, b) 中的 double。

4. Walter used return type deduction of non-lambda functions which is only available in C++14 and higher. We further shortened the function name from pick_a_number to pick.

4. Walter 使用了非 lambda 函数的返回类型推导，这仅在 C++14 及更高版本中可用。我们还将函数名从 pick_a_number 进一步缩短为 pick。

Without calling randomize, the sequence of generated numbers is equal each time which is desirable in certain situations: finding bugs is much easier with reproducible behavior. Note that pick includes the upper bound for int but not for double to be consistent with standard functions. global_urng can be considered as an implementation detail for the moment. With those functions, we can easily write loops for rolling dice:

如果不调用 randomize，生成的数字序列每次都相同，在某些情况下这是可取的：可重复的行为使查找 bug 更容易。请注意，pick 对于 int 包含上界，但对于 double 不包含，以保持与标准函数的一致性。目前，global_urng 可以被视为实现细节。有了这些函数，我们可以轻松编写掷骰子的循环：

```
randomize();
cout << "Now, we roll dice:\n";
for (int i = 0; i < 15; ++i)
    cout << pick(1, 6) << endl;

cout << "\nLet's roll continuous dice now: :-)\n";
for (int i = 0; i < 15; ++i)
    cout << pick(1.0, 6.0) << endl;
```

In fact, this is even simpler than the old C interface. Apparently it is too late for C++14, but the author would be glad to see these functions in future standards. In the following section, we will use this interface for testing.

事实上，这甚至比旧的 C 接口更简单。显然，为 C++14 加入这些函数为时已晚，但作者很高兴在未来的标准中看到这些函数。在下一节中，我们将使用此接口进行测试。

### 4.2.2.2 随机测试

Say we want to test whether our complex implementation from Chapter 2 is distributive:

假设我们想测试第 2 章中的复数实现是否满足分配律：

\(a(b+c) = ab + ac \quad \forall a,b,c.\) (4.1)

The multiplication is canonically implemented as

乘法的规范实现如下：

```
inline complex operator*(const complex& c1, const complex& c2)
{
    return complex(real(c1) * real(c2) - imag(c1) * imag(c2),
                   real(c1) * imag(c2) + imag(c1) * real(c2));
}
```

To cope with rounding errors we introduce a function similar that checks relative difference:

为了应对舍入误差，我们引入一个名为 similar 的函数来检查相对差异：

```
#include <limits>

const double eps = 10 * numeric_limits<double>::epsilon();

inline bool similar(complex x, complex y)
{
    double sum= abs(x) + abs(y);
    if (sum < 1000 * numeric_limits<double>::min())
        return true;
    return abs(x - y) / sum <= eps;
}
```

To avoid divisions by zero we treat two complex numbers as similar if their magnitudes are both very close to zero (the sum of magnitudes smaller than 1000 times the minimal value representable as double). Otherwise, we relate the difference of the two values to the sum of their magnitudes. This should not be larger than 10 times epsilon, the difference between

为了避免除以零，如果两个复数的模都非常接近零（模之和小于 1000 倍的 double 可表示的最小值），则我们将这两个复数视为相似。否则，我们将两个值的差与它们的模之和相关联。这不应大于 10 倍的 epsilon，即

