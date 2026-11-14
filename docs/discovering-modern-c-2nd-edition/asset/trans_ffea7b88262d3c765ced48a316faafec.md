

归根结底，我们的核心计算仅用三行代码即可实现，而其他约 50 行代码都用于绘制一张漂亮的图片，尽管我们已经使用了一个非常简单的图形库。不幸的是，这种情况并不少见：许多现实世界的应用程序用于文件 I/O、数据库访问、图形、Web 界面等的代码，远多于用于科学核心功能的代码。

自 C++14 起，我们可以使用用户自定义字面量来表示虚数。例如，`3i` 是 `complex<double>{0, 3}` 的简写。`float` 和 `long double` 字面量的后缀也已添加。现在，针对 `complex` 实例的函数 `f` 可以用更简洁的方式调用，以表示 `3.2 + 4.3i` 的不同类型：

- 5. 该特性被称为用户自定义字面量，尽管我们在字面量中使用的后缀并非由用户定义，而是由标准库定义。

点击此处查看代码图像

```
f(3.2f + 4.3if) // As float
f(3.2 + 4.3i)   // As double
f(3.2L + 4.3il) // As long double
```

这种记法相比构造函数调用并没有短多少，但它肯定更接近数学原始形式。

![](img/5682e787fc967e93d7e33e8bac5f58a0_377_0.png)

图 4-7：曼德勃罗集

### 4.2.1.2 混合复数计算

如前所示，复数可以由大多数数值类型构建。在这方面，库非常通用。但对于其运算则不那么通用：类型 complex<T> 的值只能与类型 complex<T> 或 T 的值相加（相减等）。因此，简单的代码：

```
complex<double> z(3, 5), c = 2 * z;
```

无法编译，因为未定义 int 和 complex<double> 之间的乘法。将 2 替换为 2.0 即可轻松解决此问题。然而，在泛型函数中，此问题更令人烦恼，例如：

点击此处查看代码图像

```
template <typename T>
inline T twice(const T& z)
{ return 2 * z; }
int main()
{
    complex<double> z(3, 5), c;
    c = twice(z);
}
```

函数 twice 出于与之前相同的原因无法编译。如果我们写 2.0 * z，它对于 complex<double> 可以编译，但对于 complex<float> 或 complex<long double> 则不行。函数

点击此处查看代码图像

```
template <typename T>
complex<T> twice(const complex<T>& z)
{ return T{2} * z; }
```

适用于所有复数类型——但仅适用于复数类型。相比之下，以下代码：

```
template <typename T>
inline T twice(const T& z)
{ return T{2} * z; }
```

可与复数和非复数类型一起编译。但是，当 T 是复数类型时，2 会被不必要地转换为复数，并且会执行四次乘法和两次加法，而实际上只需要其中一半。一种可能的解决方案是相应地重载实现。或者，我们可以使用类型特性或概念来区分 complex 的实例和其他类型。

当涉及多个不同类型的参数（其中一些可能是复数）时，编程变得更具挑战性。矩阵模板库（MTL4，第 4.7.3 节）为复数提供了混合运算。我们承诺将此功能纳入未来的标准。

## C++11 4.2.2 随机数生成器

许多应用领域——如计算机模拟、游戏编程和密码学——都使用随机数。因此，每种严肃的编程语言都为其提供生成器。此类生成器产生看似随机的数字序列。随机生成器可能依赖于量子现象等物理过程。然而，大多数生成器基于伪随机计算。它们具有一个内部状态——称为 *种子*——每次请求伪随机数时，该状态都会通过确定性计算进行转换。因此，伪随机数生成器（PRNG）在使用相同种子启动时，始终会发出相同的序列。

在 C++11 之前，只有来自 C 的 `rand` 和 `srand` 函数，功能非常有限。更成问题的是，生成的数字质量没有保证，在某些平台上确实相当低。因此，C++11 添加了高质量的 `<random>` 库。甚至曾考虑在 C++ 中彻底废弃 `rand` 和 `srand`。它们仍然存在，但在随机数质量很重要的地方，确实应该避免使用它们。

### 4.2.2.1 保持简单

=> c++11/simple_random.hpp

C++11 的随机数生成器提供了大量灵活性，这对专家非常有用，但对初学者来说有些令人不知所措。Walter Brown 提出了一组对新手友好的函数 [8]。经过略微调整，⁶ 它们是：

点击此处查看代码图像

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
    static std::uniform_int_distribution<> d();
    using param_t = decltype(d)::param_type;
    return d(global_urng(), param_t(from, thru));
}

double pick(double from, double upto)
{
    static std::uniform_real_distribution<> d{};
    using param_t = decltype(d)::param_type;
    return d(global_urng(), param_t(from, upto));
}
```

要开始使用随机数，你可以将这三个函数复制到项目中，稍后再查看细节。Walter 的接口非常简单，但对于代码测试等许多实际用途来说仍然足够。我们只需要记住以下三个函数：

- `randomize`: 通过初始化生成器的种子，使数字真正随机。
- `pick(int a, int b)`: 当 `a` 和 `b` 为 `int` 时，返回区间 `[a, b]` 中的一个 `int`。
- `pick(double a, double b)`: 当 `a` 和 `b` 为 `double` 时，返回右开区间 `[a, b)` 中的一个 `double`。

6. Walter 使用了非 lambda 函数的返回类型推导，这仅在 C++14 及更高版本中可用。我们进一步将函数名从 `pick_a_number` 缩短为 `pick`。

如果不调用 `randomize`，生成的数字序列每次都相同，这在某些情况下是可取的：可重复的行为使查找 bug 更容易。请注意，`pick` 对于 `int` 包含上界，但对于 `double` 不包含，以与标准函数保持一致。目前，`global_urng` 可以被视为实现细节。有了这些函数，我们可以轻松编写掷骰子的循环：

点击此处查看代码图像

```
randomize();
cout << "Now, we roll dice:\n";
for (int i = 0; i < 15; ++i)
    cout << pick(1, 6) << endl;

cout << "\nLet's roll continuous dice now: ;-)\n";
```

```
for (int i = 0; i < 15; ++i)
cout << pick(1.0, 6.0) << endl;
```

事实上，这比旧的 C 接口更简单。但尽管如此，它并未进入标准。也许对于强悍的 C++ 程序员来说，这太简单了。我们仍将在下一节中使用此接口进行测试。

### 4.2.2.2 随机化测试

=> c++11/random_testing.cpp

假设我们想测试第 2 章中的复数实现是否满足分配律：

a (b + c) = ab + ac 对所有 a, b, c 成立。(4.1)

乘法的标准实现如下

点击此处查看代码图像

```
inline complex operator*(const complex& c1, const complex& c2)
{
    return complex(real(c1) * real(c2) - imag(c1) * imag(c2),
                   real(c1) * imag(c2) + imag(c1) * real(c2));
}
```

为了应对舍入误差，我们引入一个检查相对差异的类似函数：

点击此处查看代码图像

```
#include <limits>

inline bool similar(complex x, complex y)
{
    const double eps = 10 * numeric_limits<double>::epsilon();
    double sum = abs(x) + abs(y);
    if (sum < 1000 * numeric_limits<double>::min())
        return true;
    return abs(x - y) / sum <= eps;
}
```

为了避免除以零，如果两个 `complex` 数的模都非常接近零（模之和小于可表示为 `double` 的最小值的 1,000 倍），则我们将它们视为相似。否则，我们将两个值的差与它们的模之和相关联。这不应大于 10 倍的 `epsilon`，即 1 与下一个可表示为 `double` 的值之间的差。此信息由稍后在第 4.3.1 节中介绍的 `<limits>` 库提供。

接下来，我们需要一个测试，它为 (4.1) 中的变量获取一组三个 `complex` 数，然后检查两边各项的相似性：

点击此处查看代码图像

```
struct distributivity_violated {};

inline void test(complex a, complex b, complex c)
{
  if (!similar(a * (b + c), a * b + a * c)) {
    cerr << "Test detected that " << a << ...
         throw distributivity_violated();
  }
}
```

如果检测到违规，关键值将在错误流上报告，并抛出用户定义的异常。最后，我们实现随机 `complex` 数的生成以及对测试集的循环：

点击此处查看代码图像

```
const double from = -10.0, upto = 10.0;

inline complex mypick()
{
  return complex(pick(from, upto), pick(from, upto));
}

int main()
{
  const int max_test = 20;
  randomize();
  for (int i = 0; i < max_test; ++i) {
    complex a = mypick();
    for (int j = 0; j < max_test; ++j) {
      complex b = mypick();
      for (int k = 0; k < max_test; ++k) {
        complex c = mypick();
        test(a, b, c);
      }
    }
  }
}
```

