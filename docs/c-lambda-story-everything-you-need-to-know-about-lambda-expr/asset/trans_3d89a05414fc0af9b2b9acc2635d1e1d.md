

```cpp
int main () {
  struct PrintFunctor {
    void operator () (int x) const {
      std::cout << x << endl;
    }
  };
  std::vector<int> v(10, 1);
  std::for_each(v.begin(), v.end(), PrintFunctor());
}
```

尝试使用 `-std=c++98` 编译它，你会在 GCC 上看到以下错误：

```text
error: template argument for
'template-class__Iter, class__Funct> _Funct
std::for_each(__Iter, __Iter, __Funct)
uses local type 'Main::PrintFunctor'
```

基本上，在 C++98/03 中，你不能使用局部类型实例化模板。

一旦认识并理解了这些局限性，C++ 程序员就找到了绕过 C++98/03 问题的方法。一种解决方案是准备一组辅助函数。

# 使用函数式辅助函数进行组合

使用一些辅助函数和预定义的函数对象（functors）怎么样？

如果你检查标准库中的 `<functional>` 头文件，你会发现许多可以立即用于标准算法（alg）的类型和函数。

例如：

- `std::plus<T>()` - 接收两个参数并返回它们的和。
- `std::minus<T>()` - 接收两个参数并返回它们的差。
- `std::less<T>()` - 接收两个参数并返回第一个是否小于第二个。
- `std::greater_equal<T>()` - 接收两个参数并返回第一个是否大于第二个。
- `std::bind` - 创建一个可调用对象，将第一个参数固定为给定值。
- `std::bind2nd` - 创建一个可调用对象，将第二个参数固定为给定值。
- 以及许多更多。

让我们写一些受益于这些辅助函数的代码：

使用旧的 C++98/03 函数式辅助函数。在线代码见 @Wandbox

```cpp
#include <algorithm>
#include <functional>
#include <vector>

int main() {
    std::vector<int> v;
    v.push_back(1);
    v.push_back(2);
    // push_back 直到 9...
    const size_t smaller5 = std::count_if(v.begin(), v.end(),
        std::bind2nd(std::less<int>(),), 5));

    return smaller5;
}
```

该示例使用了 `std::bind2nd` 并通过 `std::bind2nd` 固定了它的第二个参数。这整个“组合”被传递给 `count_if`。正如你可能猜到的，代码展开成一个执行简单比较的函数：

```cpp
return x < 5;
```

如果你想要现即用的辅助函数，你也可以查看 boost 库，例如 `boost::bind`。

遗憾的是，这种方法的主要问题是复杂性和难以学习的语法。例如编写组合两个或多个函数的代码并不直观。请看下文：

组合函数式辅助函数。在线代码 @Wandbox

```cpp
std::vector<int> v;
v.push_back(1);
v.push_back(2);
// push_back 直到 9...
const size_t val = std::count_if(v.begin(), v.end(),
    std::bind(std::logical_and<bool>(),),
    std::bind(std::greater<int>(),_1, 2),
    std::bind(std::less_equal<int>(),_1, 6)));
```

```cpp
// _1 来自 std::placeholder 命名空间
```

该组合使用了 `std::bind`（来自 C++11，所以我们稍微作了点弊，它不是 ++98/03）配合 `std::greater` 和 `std::less_equal`，通过 `std::logical_and` 连接起来。此外，代码使用了 `_1`，它是第一个输入参数的占位符。

虽然上面的代码可以工作，但你可以局部定义它，你可能同意这种语法复杂且不自然。需要提到的是这种组合只表示了一个简单的条件：

```cpp
return x > 2 && x <= 6 ;
```

有没有什么更好、更自然的方法呢？

# 新特性的动机

正如你所见，在 C++98/03 中，有多种方法向标准库的算法和工具声明并传递可调用对象。然而，所有这些选项都有些局限。例如，你不能声明局部函数对象对象，或者将函数与函数式辅助对象组合非常复杂。

幸运的是，有了 C++11，我们终于看到了许多改进！

首先，C++ 委员会取消了带有局部类型的模板实例化限制。现在你可以在需要它们的地方局部编写函数对象。

此外，C++11 还实现了一个另一个理念：如果编译器能为开发者“编写”这些短小的函数对象呢？这意味着通过一些新语法，我们可以“就地”创建函数对象，并为更简洁紧凑的语法打开大门。

这就是“Lambda 表达式”（lambda expressions）的诞生！

如果我们看 N3337 —— C++11 的最终草稿，我们可以看到一个专门针对 lambda 的章节：[expr.prim.lambda]。

让我们在下一章来看看这个新特性。

# 2. C++11 中的 Lambdas

万岁！C++ 委员会听取了开发者的声音，从 C++11 开始，我们得到了许多改进！

Lambdas 很快变得非常流行。在 N3337 - C++11 的最终草稿中，我们可以看到一个专门针对 lambda 的章节：[expr.prim.lambda]。

让我们在下一章来看看这个新特性。

# Lambda 的语法

在本章，你将学习：

- Lambda 的基本语法。
- 捕获（capture）。
- 返回类型。
- 修饰符。
- Lambda 如何转换为函数指针。
- IIFE（立即调用函数表达式）。

Lambda 的语法图如下：

```
[] () -> ret {code }
^ ^ ^
| | | return type
| | parameter list
| optional capture list
```

上面的示例显示了在 Lambda 体之前可以使用其他修饰符。

# Lambda 表达式的一些示例

```cpp
// 1. 最简单的 lambda 表达式：
[] {};
```

在第一个示例中，你可以看到一个简单的 lambda 表达式。它只需要 `[]` 然后是函数体的 `{}`。参数列表 `()` 是可选的，在这种情况下不需要。

```cpp
// 2. 带有两个参数：
[](float f, int a) { return a * f; }
[](int a, int b) { return a < b; };
```

在第二个示例中，可能重要的是，你可以看到参数被传递到 `()` 部分，就像普通函数一样。返回类型是不需要的，编译器会自动推导出它。

```cpp
// 3. 尾返回类型：
[](MyClass t) -> int { auto a = t.compute(a); print(a); return a; };
```

在上面的示例中，我们显式设置了返回类型。尾返回类型从 C++11 起也适用于函数声明。

```cpp
// 4. 额外的修饰符：
[x](int a, int b) mutable { return a < b; }
[](float param) noexcept { return param * param; }
[x](int a, int b) mutable noexcept { return a < b; };
```

最后一个示例显示在 Lambda 体之前可以使用其他修饰符。在代码中，我们使用了 `mutable`（以便修改捕获的变量）和 `noexcept`。第三个 lambda 使用了 `mutable` 和 `noexcept`，它们必须按此顺序出现。

