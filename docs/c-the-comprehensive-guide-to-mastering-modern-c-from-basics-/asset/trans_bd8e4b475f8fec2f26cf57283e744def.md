
你不能在不定义 LATE 的情况下声明它——也就是说，在定义的同时对其进行初始化。这确保了你一旦知道它的名称就可以使用该常量。

你几乎可以在任何可以使用 `const` 的地方使用 `constexpr` 变量。尝试习惯在这些情况下使用 `constexpr`。

## “constexpr” 作为返回类型

`constexpr` 的另一个令人兴奋的特性是你也可以对函数进行标记。在返回类型处用 `constexpr` 代替 `const`。事实上，这个 `constexpr` 影响的是整个函数：

```cpp
//://godbolt.org/z/Yv85s9T6v
constexpr size_t doubleIfSmall(size_t value) {
    return value < 100 ? value : 0; // 如果小于 100 则返回 value
}
std::array<int, doubleIfSmall(50)> arr {};
```

这是一个巨大的进步！一个简单返回 `const` 值的自定义函数不能作为常量表达式使用：

```cpp
const size_t doubleIfSmall2(size_t value) {
    return value < 100 ? value*2 : value;
}
std::array<int, doubleIfSmall2(50)> arr {}; // // 不够常量
```

为什么这里又要进行区分呢？原因是为了让编译器确保可以在编译时计算 `doubleIfSmall1(50)`。

以下是 C++23 之前编译器不允许的两个示例：

```cpp
#include <cmath> // sin, cos, sqrt
constexpr unsigned MyLog2(unsigned number) { // 函数具有静态变量
    static int count_calls = 0; // 在 constexpr 中是不允许的
    count_calls += 1;
    unsigned int count = 0;
    while (number > 1) { number /= 2; }
    return count;
}

constexpr double one(double x) { // 使用了非 constexpr 函数
    return sqrt(sin(x)*sin(x) + cos(x)*cos(x));
}
```

从 C++14 开始，特别是从 C++20 和 C++23 开始，关于 `constexpr` 函数中可以内容的规则变得严格严格了。例如，从 C++14 开始，允许简单的 `while` 和 `for` 循环。从 C++20 开始，你甚至可以在它们内部使用 `new` 分配内存。从 C++23 开始，允许静态局部变量。这反过来允许像 `vector` 和 `string` 等许多方法和构造函数被定义为 `constexpr`，因此你可以在 `constexpr` 函数中使用它们——但前提是它们的内存也在编译时被释放。`<algorithm>`、`<numeric>` 和 `<utility>` 中的许多算法现在也是 `constexpr` 了。

方便的是，`constexpr` 对于函数和成员变量意味着 `inline`，而对于成员函数意味着 `const`。

| 13.10.7 用于编译时决策的 "if constexpr" |

有时你希望在编译时而不是在运行时决定执行哪些代码。你通过重载（overloads）一直做到这一点。“如果参数是指针，则对其进行解引用；否则，返回值本身。”这个问题可以通过重载解决，但也可以通过 `constexpr` 实现。

```cpp
// https://godbolt.org/z/zMbnYzo17
template<typename T>
auto deref(T t) {
    if constexpr (std::is_pointer_v<T>) {
        return *t;
    } else {
        return t;
    }
}

int main() {
    int i = 42;
    std::cout << deref(i) << '\n';
    auto p = std::make_unique<int>(73);
    std::cout << deref(p) << '\n'; // 直接解引用指针的值
}
```

列表 13.15 使用 "constexpr"，你可以在编译时决定将执行哪些代码。

在这里是在编译时决定执行哪些代码。对于 i 来说，执行的是 `return t`——因为 `is_pointer_v<int>` 为虚假。对于 `p.get()`，执行的是 `return *`。

重载或模板特化也可以也可以用 `if constexpr` 替换。

```cpp
// https://godbolt.org/z/eo468MvMo
#include <iostream>
#include <string>
struct S {
    int n;
    std::string s;
    float d;
};

template <std::size_t N> auto get(S& s) {
  if constexpr (N == 0) return s.n;
  else if constexpr (N == 1) return s.s;
  else if constexpr (N == 2) return s.d;
}
int main() {
  S obj {0, "hello", "", 10.0f};
  std::cout << get<0>(obj) << " " << get<1>(obj) << "\n"; // 输出:
  0, hello
}
```

### ### 列表 13.16 "if constexpr" 也可以配合 "else" 使用。

在使用 `constexpr if` 之前，你需要编写三个模板特化，例如 `template<> auto& get<0>(S& s)`。新方法可以更简洁。

使用此特性，可以很容易地在编译时计算斐波那契数——这是书中喜爱的示例：

```cpp
// https://godbolt.org/z/44KM1fWr
template<auto N>
constexpr auto fibonacci() {
  if constexpr (N>=2) {
    return fibonacci<N-1>() + fibonacci<N-2>();
  } else {
    return N;
  }
}
int main() {
  std::cout << fibonacci<10>() << "\n"; // 输出: 55
}
```

然而，由于这是写成递归的，取决于实现，可能会导致编译器挂起。但也许你想测试编译器的性能？

## 13.10.8 C++20: "constval"

从 C++20 开始，有了 `constval`。如果你用 `constval` 声明函数，它会在编译时执行。`constexpr` 仅仅提供了可能，而 `constval` 是专门为此目的设计的。

```cpp
// https://godbolt.org/z/Wbr7n4
#include <iostream>
#include <array>
constexpr bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i*i <= n; ++i) {
        if (n % i == 0) return false;
    }
    return true;
}

template<int Num>
constval std::array<int, Num> primeNumbers() {
    std::array<int, Num> primes{0};
    int idx = 0;
    for (int val = 1; val < Num; ++val) {
        if (isPrime(val)) primes[idx++] = val;
    }
    return primes;
}

int main() {
    auto primes = primeNumbers<100>();
    for (auto v : primes) {
        std::cout << v << ' ';
    }
    std::cout << "\n";
}
```

列表 13.17 使用 `constval` 在编译时计算第一个素数。

在这里，包含第一个素数的数组是在编译时计算的。`constval` 函数取决于运行时。可能想将运行时计算很大的的工作转移到编译时，但这并不总是好主意。编译器通常对其编译时计算的表达式有一个限制（标准保证约为百万）。当我尝试用 g++ 13.2 设置计算 1,000,000 个素数时，我得到了这个错误：

```
'constexpr' evaluation operation count exceeds limit of 33554432
use -fconstpr-ops-limit=' to increase the limit
```

所以，你应该在有限范围内将此类初始化工作转移到编译时。

## 13.10.9 "constval" 从 C++23 开始，还有 `constval`。此功能的作用就像它没有包含括号中的条件。相反，`constval` 之后的块只有在调用上下文为 `constexpr` 时才会执行（这通常意味着它可以在编译时求值）。

```cpp
// https://godbolt.org/z/7KWqTPo1K
#include <iostream>
constexpr int get_value() {
    if constval {
        return 42;
    } else {
        return 668;
    }
}
int main() {
    auto a = get_value();
    std::cout << a << '\n';   // 输出: 668
    constexpr auto b = get_value();
}
```
