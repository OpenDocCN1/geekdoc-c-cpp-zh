
这并不明确说明这在程序员的日常工作中究竟意味着什么。此外，在撰写本文时，没有编译器支持此功能²，因此我们只能将来再尝试。

- 2. 更具体地说，尝试用 clang++-13、g++-11 和 VS19 编译 c++20/constexpr_vector_string.cpp 失败了。

语言标准试图定义类型在 constexpr 函数中可用的条件。结果发现，这无法作为类型属性来定义，因为它取决于类型的使用方式——更准确地说，取决于所考虑的 constexpr 函数中调用的是哪个构造函数。因此，相应的类型特征 is_literal_type 注定无用，并自 C++14 起被声明为弃用。³

- 3. 尽管如此，人们仍注意到无用的结果是明确定义的。

constexpr 函数一个非常好的特性是它们既可在编译时也可在运行时使用：

点击此处查看代码图像

```
long n = atoi(argv[1]);
cout << "fibonacci(" << n << ") = " << fibonacci(n) << '\n';
```

这里我们传递了命令行的第一个参数（在编译时肯定未知）。因此，每当有一个或多个参数仅在运行时才知晓时，函数就无法在编译时求值。只有当所有函数参数在编译时都可用时，函数才能在编译期间计算。

constexpr 函数的混合适用性反过来意味着，它们的参数只能传递给 constexpr 函数。将参数传递给普通函数会阻碍在编译时使用。反之，我们不能将函数参数传递给像 static_assert 这样的编译时求值，因为这会阻止运行时调用。因此，我们无法在 C++11 的 constexpr 函数中表达断言。

语言标准规定标准库中哪些函数必须实现为 constexpr。某些库实现将额外的函数实现为 constexpr。例如，以下函数：

点击此处查看代码图像

```
constexpr long floor_sqrt(long n)
{
    return floor(sqrt(n));
}
```

g++ 支持（尽管不是所有版本都支持）。相比之下，floor 和 sqrt 在 clang++ 中不是 constexpr 函数，因此代码在那里无法编译。

=> c++20/fibonacci.cpp

C++20 为了强制在编译时对函数求值，我们可以在 C++20 中将其声明为 consteval：

点击此处查看代码图像

```
consteval long fibonacci(long n)
{
    return n <= 2 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
}
```

使用运行时参数调用此函数会导致错误。

## C++14 5.1.2 扩展的编译时函数

C++14 和 C++20 放宽了对编译时函数的限制。这使我们可以额外使用：

- void 函数，例如：

点击此处查看代码图像

```
constexpr void square(int &x) { x *= x; }
```

- 自 C++20 起的虚函数（§6.1.3）；
- 自 C++20 起的协程（§4.6.8）；
- 局部变量，只要它们
  - 已初始化（C++20 之前）；
  - 既没有静态存储持续期也没有线程存储持续期；并且
  - 具有字面量类型。
- 控制结构，但以下除外：
  - goto（我们反正也不想使用）；
  - 汇编代码，即 asm 块（在 C++20 中已解除限制）；并且
  - try-catch 块（在 C++20 中已解除限制）。

以下示例在 C++14 中允许，但在 C++11 中不允许（出于多种原因）：

点击此处查看代码图像

```
template <typename T>
constexpr T power(const T& x, int n)
{
    T r{1};
    for (; n > 0; --n)
        r *= x;
    return r;
}
```

=> c++14/popcount.cpp

有了这些扩展，编译时函数几乎和普通函数一样富有表现力。作为一个更技术性的示例，我们还将实现 popcount（population count 的缩写），它用于计算二进制数据中 1 比特的数量：

点击此处查看代码图像

```
constexpr size_t popcount(size_t x)
{
    size_t count = 0;
    for (; x != 0; ++count)
        x &= x - 1;
    return count;
}
```

分析此算法也有助于更好地理解二进制算术。这里的关键思想是，x &= x - 1 将最低有效位设置为零，并保持所有其他位不变。

=> c++11/popcount.cpp

[C++11] 该函数也可以在 C++11 中表示为 constexpr，并且在递归表达中更短：

点击此处查看代码图像

```
constexpr size_t popcount(size_t x)
{
    return x == 0 ? 0 : popcount(x & x-1) + 1;
}
```

这种无状态的递归计算对某些读者来说可能不太容易理解，而对另一些读者来说可能更清晰。据说，发现迭代或递归程序更容易理解取决于它们向程序员介绍的顺序。幸运的是，C++ 允许我们同时实现两者。

## C++14 5.1.3 素性

我们已经提到过，素数是第一个严肃元程序的主题，尽管不可编译。现在我们想演示，我们可以在（可编译的）现代 C++ 中计算它们。更准确地说，我们将实现一个函数，在编译时告诉我们给定的数字是否为素数。你可能会问：“我编译期间到底需要这些信息干什么？”这是个公正的问题。实际上，作者曾在他的研究中使用过这个编译时函数，用于对带有语义概念的循环群进行分类（§3.10）。当群的大小是素数时，它是一个域，否则是一个环。一个实验性编译器（ConceptGCC [24]）在 C++ 中启用了这样的代数概念，它们的模型声明包含了素性的编译时检查（不幸的是，在 `constexpr` 可用之前）。

=> c++14/is_prime.cpp

我们重用第 4.6.3 节的算法思路：1 不是素数，偶数除了 2 都不是素数，对于所有其他数字，我们检查它们是否不能被任何大于 1 且小于其自身的奇数整除：

点击此处查看代码图像

```
constexpr bool is_prime(int i)
{
  if (i == 1)
    return false;
  if (i % 2 == 0)
    return i == 2;
  for (int j = 3; j < i; j+= 2)
    if (i % j == 0)
        return false;
  return true;
}
```

实际上，我们只需要测试参数 i 的平方根以下的奇数的整除性：

![](img/5682e787fc967e93d7e33e8bac5f58a0_451_0.png)

```
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    int max_check= static_cast<int>(sqrt(i)) + 1;
    for (int j = 3; j < max_check; j+= 2)
        if (i % j == 0)
            return false;
    return true;
}
```

不幸的是，此版本仅适用于 `sqrt` 是 `constexpr` 的标准库（大多数 4.7 及以上版本的 g++）。否则，我们必须提供自己的 `constexpr` 实现。例如，我们可以使用第 4.3.1 节中的定点算法：

![](img/5682e787fc967e93d7e33e8bac5f58a0_451_1.png)

```
constexpr int const_abs(int i) { return i < 0 ? -i : i; }

constexpr int square_root(int x)
{
    double r= x, dx= x;
    while (const_abs(r * r - dx) > 0.1) {
        r = (r + dx/r) / 2;
    }
    return static_cast<int>(r);
}
```

这里我们以 `double` 执行迭代方法，仅在返回结果时将其转换为 `int`。这得出了一个（足够）高效且可移植的实现：

![](img/5682e787fc967e93d7e33e8bac5f58a0_451_2.png)

```
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    int max_check= square_root(i) + 1;
    for (int j = 3; j < max_check; j+= 2)
        if (i % j == 0)
            return false;
    return true;
}
```

通过这个示例，我们看到了编译时求值性能的提升。大约在 2006 年，该函数对接近 100 万的素数耗时约 18 秒，对接近 1000 万的素数耗时约一分钟。在 g++-10 上使用 `constexpr` 时，测试接近 10 亿的素数使编译时间增加了约 0.02 秒。

=> c++11/is_prime.cpp

最后，我们喜欢接受挑战，使用 C++11 中受限的 `constexpr` 来实现这个（嗯，它的第一个版本）：

点击此处查看代码图像

```
constexpr bool is_prime_aux(int i, int div)
{
    return div >= i ? true :
           (i % div == 0 ? false : is_prime_aux(i, div + 2));
}

constexpr bool is_prime(int i)
{
    return i == 1 ? false :
           (i % 2 == 0 ? i == 2 : is_prime_aux(i, 3));
}
```

这里我们需要两个函数：一个用于特殊情况，另一个用于检查从 3 开始的奇数的整除性。

**向后兼容性：** 在引入 `constexpr` 之前，编译时计算是通过模板 _元函数_ 实现的。它们更难实现，并且在 C++20 之前，它们的适用性也更受限制（既不支持 `float` 也不支持用户定义的类型）。如果你无法使用 C++11
