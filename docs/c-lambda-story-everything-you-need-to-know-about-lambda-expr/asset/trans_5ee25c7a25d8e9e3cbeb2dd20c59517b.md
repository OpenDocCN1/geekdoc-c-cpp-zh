

```cpp
std::cout << lamOnePlus(10) << " " << lamMinusOne(10) << '\n';
```

Lambda 版本要更加简洁且更具可读性。在下面更复杂的示例中，这一点会更加明显。

## 函数组合

作为最后一个示例，让我们来看下面这段使用函数组合的代码：

```cpp
Function composition with std::bind. Live code @Compiler Explorer
#include <algorithm>
#include <functional>
#include <vector>

int main() {
    using std::placeholders::_1;
    const std::vector<int> v { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    const auto val = std::count_if(v.begin(), v.end(),
        std::bind(std::logical_and<bool>(), std::placeholders::_1,
        std::bind(std::greater<int>)(_, _1, 2),
        std::bind(std::less<int>)(_, _1, 6))));

    return val;
}
```

你能立即看懂那里发生了什么吗？

现在，让我们用一个简单的 lambda 表达式重写这个复杂的组合：

```cpp
std::vector<int> v { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
const auto more2less6 = std::count_if(v.begin(), v.end(),
    [](int x) { return x > 2 && x < 6; });
```

这不是更好吗？

> 你可以在以下资源中了解更多关于 std::bind 和 lambdas 使用的指南：“Effective Modern C++”，第 34 节：优先使用 lambdas 而非 std::bind，以及 Google Abseil 博客上的：Tip of the Week #108：避免 std::bind。

## 使用 lambda 进行 LIFTing

虽然标准库中的算法非常方便，但某些问题是很难解决的。其中之一是将函数重载传递到接收可调用对象的函数模板中。

例如：

### 调用函数重载

```cpp
#include <algorithm>
#include <vector>

// 两个重载：
void foo (int ) {}
void foo (float) {}

int main() {
    const std::vector<int> vi = {1, 2, 3, 4, 5, 6, 7, 8, 9 };
    std::for_each(vi.begin(), vi.end(), foo);
}
```

在上面的示例中，我们尝试使用 int 和 float 的两个重载并将它们传递给 for_each。遗憾的是，我们从 GCC 9 (trunk) 处收到了以下错误：

```cpp
error: no matching function for call to
for_each(std::vector<int>::iterator, std::vector<int>::iterator,
<unresolved overloaded function type>)
std::for_each(vi.begin(), vi.end(), foo);
                       ^^^^
```

主要问题在于，编译器将 foo 视为一个模板参数，它需要解析它的类型。但要这样做，它必须检查 foo 接受什么类型，这是不可能的。

然而，有一个技巧，我们可以使用 lambda，然后调用所需的函数重载。

对于简单值类型的基本形式，对于我们的两个函数，我们可以写以下代码：

```cpp
std::for_each(vi.begin(), vi.end(), [](auto x) { return foo(x); });
```

现在，我们有一个包装器（一个泛型 lambda），它处理重载解析并调用 foo() 的适当重载。

我们可以通过完美转发（perfect forwarding）来改进它：

```cpp
std::for_each(vi.begin(), vi.end(), [](auto && x) {
  return foo(std::forward<decltype(x)>(x));
});
```

这里是一个可以运行的示例：

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

void foo (int i) { std::cout << "int: " << i << " n"; };
void foo (float f) { std::cout << "float: " << f << " n"; };

int main() {
  const std::vector<int> vi = {1, 2, 3, 4, 5, 6, 7, 8, 9 };
  std::for_each(vi.begin(), vi.end(), [](auto && x) {
    return foo(std::forward<decltype(x)>(x));
  });
}
```

然而，对于更高级场景，这可能不是首选方案，因为我们没有变变参数和异常说明。如果你需要一个泛型的解决方案，那么你需要写更多的代码：

```cpp
#define LIFT(foo) \
[(auto&&... args) noexcept(foo(args)...) -> decltype(foo(args)...) { \
  return foo
```

看起来很复杂，对吧？让我们尝试解析它。它有三个部分：

- `return foo(std::forward<decltype(args)>(args)...)` - 这是完美转发。
- `noexcept(foo(args)...)` - 使用 noexcept 运算符检查可调用对象的异常说明。根据结果，它将产生 true 或 false。
- `decltype(foo(args)...)` - 用于推导包装 lambda 的返回类型。LIFT 被定义为宏，否则你每次想创建这样的 lambda 都要写这段代码。

## 递归 Lambda

如果你有一个普通的函数，递归调用它是很容易的。一个常见的例子是阶乘计算：

```cpp
int factorial(int n) {
    return n > 1 ? factorial(n - 1) : 1;
}
```

```cpp
int main() {
    return factorial(5);
}
```

然而，使用 lambda 直接是不可能的：

递归 Lambda 的错误：

```cpp
int main() {
    auto factorial = [](int n) {
        return n > 1 ? factorial(n - 1) : 1;
    };
    return factorial(5);
}
```

这段代码无法编译！这里是 GCC 的错误：

`error: use of 'factorial' before deduction of 'auto'`

这是因为我们无法在 lambda 体内部访问 factorial，因为它还没有完全求值。为了说明这个问题，我们可以代码“展开”为简化的函数对象（functor）：

```cpp
struct fact {
    int operator()(int n) const {
        return n > 1 ? n - 1 : 1;
    };
};
```
如你所见，在 `operator()` 内部没有访问函数对象类型的方法。如果你需要递归调用 lambda，至少可以使用两个技巧：

- 使用 std::function 并将其捕获。
- 使用内部 lambda 并将其作为泛型参数。

### 使用 std::function

主要思想是将 lambda 赋值给 std::function，然后将其捕获到 lambda 体中。

```cpp
#include <functional>
int main() {
    const std::function<int(int)> factorial = [&factorial](int n) {
        return n > 1 ? factorial(n - 1) : 1;
    };
    return factorial(5);
}
```

在之前的代码中，内部是一个捕获的 std::function 对象。这个对象是完全定义的，这就是为什么编译器在访问和调用它时没有问题。如果你只想使用无状态的 lambda，你甚至可以使用函数指针而不是 std::function，因为它的内存消耗低。

### 内部 lambda 和泛型参数

使用 C++14 可以使用以下替代方案：

```cpp
int main() {
    const auto factorial = [](int n) noexcept {
        const auto f_impl = [](int n, const auto& impl) noexcept -> int {
          return n > 1 ? n * impl(n - 1, impl) : 1;
        };
        return f_impl(n, f_impl); // 等等，这里有逻辑错误
    };
```

这次我们创建了一个执行主要处理（f_impl）的内部 lambda。稍后，我们传递一个泛型参数（const auto& impl）。这个参数是一个我们可以递归调用的可调用对象。感谢 C++14 的泛型 lambda，我们可以避免 std::function 的开销并依赖 auto 类型推导。

## 更多技巧

如果你想看更多技巧，也可以查看以下资源：

- c++ - Recursive lambda functions in C++11 - Stack Overflow
- Recursive lambdas in C++(14) - Pedro Melendez

## 递归 lambda 是最佳替代方案吗？

在本节中，你可以看到一些关于 lambda 表达式的技巧。尽管如此，这些技术的复杂性远高于只有递归函数调用的简单解决方案。这就是为什么在某些情况下，递归 lambda 不是最佳且最直接的选择。另一方面，复杂的递归 lambda 的优点是它的局部性以及接受 auto 参数的能力。

