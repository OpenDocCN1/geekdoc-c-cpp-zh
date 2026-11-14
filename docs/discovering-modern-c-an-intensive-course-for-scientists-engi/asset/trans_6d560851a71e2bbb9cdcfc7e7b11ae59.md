

- 局部变量，只要满足以下条件：
  - 已初始化；
  - 既没有静态存储期也没有线程存储期；并且
  - 具有字面量类型。

- 控制结构，但不包括：
  - goto（反正我们也不想使用它）；
  - 汇编代码，即 asm 块；以及
  - try 块。

以下示例在 C++14 中是允许的，但在 C++11 中不允许（出于多种原因）：

```cpp
template <typename T>
constexpr T power(const T& x, int n)
{
    T r(1);
    while (--n > 0)
        r *= x;
    return r;
}
```

有了这些扩展，编译时函数几乎和普通函数一样富有表现力。作为一个更技术性的示例，我们还将实现 popcount（population count 的缩写），用于计算二进制数据中 1 比特的数量：

```cpp
constexpr size_t popcount(size_t x)
{
    int count = 0;
    for ( ; x != 0; ++count)
        x &= x - 1;
    return count;
}
```

分析此算法也有助于更好地理解二进制算术。这里的关键思想是，`x &= x - 1` 将最低有效位置零，并保持所有其他位不变。

该函数也可以用 C++11 constexpr 表达，并且在递归表述中更加简短：

```cpp
constexpr size_t popcount(size_t x)
{
    return x == 0 ? 0 : popcount(x & x - 1) + 1;
}
```

这种无状态的递归计算对某些读者来说可能不太容易理解，而对另一些读者来说可能更清晰。据说，发现迭代或递归程序更容易理解取决于它们向程序员介绍的顺序。幸运的是，C++ 允许我们同时实现两者。

## 5.1.3 素性

我们已经提到过，素数是第一个严肃元程序的主题，尽管不可编译。现在我们想展示，我们可以在（可编译的）现代 C++ 中计算它们。更准确地说，我们将实现一个函数，在编译时告诉我们给定的数字是否为素数。你可能会问：“我究竟为什么在编译期间需要这些信息？”这是个公正的问题。实际上，作者曾在他的研究中使用过这个编译时函数，用于基于语义概念对循环群进行分类（§8.5）。当群的大小是素数时，它是一个域，否则是一个环。一个实验性编译器（ConceptGCC [21]）在 C++ 中启用了这样的代数概念，它们的模型声明包含了素性的编译时检查（不幸的是，在 concepts 可用之前）。

=> c++14/is_prime.cpp

```cpp
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    for (int j = 3; j < i; j += 2)
        if (i % j == 0)
            return false;
    return true;
}
```

实际上，我们只需要测试参数 i 小于其平方根的奇数的可整除性：

```cpp
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    int max_check = static_cast<int>(sqrt(i)) + 1;
    for (int j = 3; j < max_check; j += 2)
        if (i % j == 0)
            return false;
    return true;
}
```

不幸的是，此版本仅适用于 sqrt 为 constexpr 的标准库（如前所述，>= 4.7-4.9）。否则，我们必须提供自己的 constexpr 实现。例如，我们可以使用第 4.3.1 节中的定点算法：

```cpp
constexpr int square_root(int x)
{
    double r = x, dx = x;
    while (std::abs(r * r - dx) > 0.1) {
        r = (r + dx / r) / 2;
    }
    return static_cast<int>(r);
}
```

如你所见，我们以 double 执行迭代方法，仅在返回结果时将其转换为 int。这导致了一个（足够）高效且可移植的实现：

```cpp
constexpr bool is_prime(int i)
{
    if (i == 1)
        return false;
    if (i % 2 == 0)
        return i == 2;
    int max_check = square_root(i) + 1;
    for (int j = 3; j < max_check; j += 2)
        if (i % j == 0)
            return false;
    return true;
}
```

=> c++11/is_prime.cpp

最后，我们喜欢迎接挑战，使用 C++11 中受限的 constexpr 实现这个（好吧，它的第一个版本）：

```cpp
constexpr bool is_prime_aux(int i, int div)
{
    return div >= i ? true :
           (i % div == 0 ? false : is_prime_aux(i, div + 2));
}
```

```cpp
constexpr bool is_prime(int i)
{
    return i == 1 ? false :
           (i % 2 == 0 ? i == 2 : is_prime_aux(i, 3));
}
```

这里我们需要两个函数：一个用于处理特殊情况，另一个用于检查从 3 开始的奇数的可整除性。

在理论上，我们可以使用 C++11 constexpr 实现每一种计算。它提供了 μ-递归函数的所有特性：常数和后继函数、投影和递归。在可计算性理论中，已进一步证明 μ-递归函数等价于图灵机，因此每个可计算函数都可以用 μ-递归函数实现，进而也可以用 C++11 constexpr 实现。理论就是这样。但在实践中，使用这种受限的表现力来实现真正复杂的计算所需的努力（和痛苦）则是另一回事了。

**向后兼容性：** 在引入 `constexpr` 之前，编译时计算是通过模板 _元函数_ 实现的。它们的适用性更有限（不支持浮点数或用户定义的类型），并且更难实现。如果你出于某种原因无法使用 C++11 特性，或者只是对历史编程感兴趣，欢迎阅读附录 5.2.5 中的元函数部分。

## 5.1.4 我们的常量有多恒定？

将（非成员）变量声明为 const：

```cpp
const int i = something;
```

可以建立两个层次的常量性：

- 对象在程序执行期间不能更改（始终如此）。
- 值在编译时已经知晓（有时如此）。

`i` 的值在编译期间是否可用取决于分配给它的表达式。如果 `something` 是字面量：

```cpp
const long i = 7, j = 8;
```

那么我们可以在编译期间使用它，例如，作为模板参数：

```cpp
template <long N>
struct static_long
{
    static const long value = N;
};
```

```cpp
static_long<i> si;
```

编译时常量的简单表达式通常在编译期间可用：

```cpp
const long k = i + j;
static_long<k> sk;
```

当我们将变量分配给 const 对象时，它在编译期间绝对不可用：

```cpp
long ll;
cin >> ll;
const long cl = ll;
static_long<cl> scl; // Error
```

常量 `cl` 在程序中不能更改。另一方面，它不能在编译期间使用，因为它依赖于运行时值。

有些场景中，我们无法从程序源代码中判断拥有哪种常量，例如：

```cpp
const long ri = floor(sqrt(i));
static_long<ri> sri; // compiles with g++ 4.7-4.9
```

这里，当 sqrt 和 floor 在标准库实现中都是 constexpr 时（例如，在 g++ 4.7-4.9 中），ri 在编译期间是已知的；否则，当它作为模板参数使用时会报错。

为了确保常量具有编译时值，我们必须将其声明为 constexpr：

```cpp
constexpr long ri = floor(sqrt(i)); // compiles with g++ 4.7-4.9
```

这保证了 ri 在编译期间是已知的；否则该行无法编译。请注意，constexpr 对变量比对函数更严格。constexpr 变量仅接受编译时值，而 constexpr 函数既接受编译时参数也接受运行时参数。

## 5.2 提供和使用类型信息

在第 3 章中，我们看到了函数和类模板的表现力。然而，所有这些函数和类对所有可能的参数类型都包含完全相同的代码。为了进一步提高模板的表现力，我们将根据参数类型引入大小不一的代码变体。因此，我们首先需要类型信息来进行分发。此类类型信息可以是技术性的——例如 `is_const` 或 `is_reference`——或者是语义/领域特定的——例如 `is_matrix` 或 `is_pressure`。对于大多数技术类型信息，我们将在头文件 `<type_traits>` 和 `<limits>` 中找到库支持，如第 4.3 节所示。领域特定的类型属性正等待我们去实现。

### 5.2.1 类型特征

=> c++11/magnitude_example.cpp

在我们迄今编写的函数模板中，临时变量和返回值的类型等于函数参数之一。不幸的是，这并不总是有效。想象一下，我们实现一个函数，从两个值中返回幅度最小的那个：

```cpp
template <typename T>
T inline min_magnitude(const T& x, const T& y)
{
    using std::abs;
    T ax = abs(x), ay = abs(y);
    return ax < ay ? x : y;
}
```

我们可以针对 int、unsigned 或 double 值调用此函数：

```cpp
double d1 = 3., d2 = 4.;
cout << "min |d1, d2| = " << min_magnitude(d1, d2) << '\n';
```

