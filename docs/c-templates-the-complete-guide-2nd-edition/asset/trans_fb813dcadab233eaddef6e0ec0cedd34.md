

Advance<Iterator> 类似于前面章节中使用的 advanceIter() 算法，用于将迭代器推进若干步。我们同时提供了通用实现（针对输入迭代器）以及针对双向迭代器和随机访问迭代器的专用实现，依赖于辅助特性 BestMatchInSet（下面描述）来为迭代器的类别标签选择最佳匹配：

```
// primary template (intentionally undefined):
template<typename Iterator,
typename Tag =
BestMatchInSet<
typename std::iterator_traits<Iterator>
::iterator_category,
std::input_iterator_tag,
std::bidirectional_iterator_tag,
std::random_access_iterator_tag>>
class Advance;

// general, linear-time implementation for input iterators:
template<typename Iterator>
class Advance<Iterator, std::input_iterator_tag>
{
public:
using DifferenceType =
typename std::iterator_traits<Iterator>::difference_type;

void operator() (Iterator& x, DifferenceType n) const
{
while (n > 0) {
++x;
--n;
}
}
};

// bidirectional, linear-time algorithm for bidirectional iterators:
template<typename Iterator>
class Advance<Iterator, std::bidirectional_iterator_tag>
{
```

EnableIf 技术的基本思想是，仅当模板参数满足特定条件时才启用某个模板或偏特化。例如，advanceIter() 算法的最高效形式会检查迭代器参数的类别是否可转换为 std::random_access_iterator_tag，这意味着算法可以使用各种随机访问迭代器操作。

如果我们将这一概念推向极致，并将模板对其模板参数执行的每个操作都编码为 EnableIf 条件的一部分呢？此类模板的实例化永远不会失败，因为不提供所需操作的模板参数会导致推导失败（通过 EnableIf），而不是允许实例化继续进行。我们将此类模板称为“实例化安全”模板，并在下面概述其实现。

我们从一个非常基础的模板 min() 开始，它计算两个值的最小值。我们通常会这样实现该模板：

```
template<typename T>
T const& min(T const& x, T const& y)
{
if (y < x) {
return y;
}
return x;
}
```

该模板要求类型 T 具有 < 运算符，能够比较两个 T 值（具体为两个 T const 左值），然后将比较结果隐式转换为 bool 以供 if 语句使用。检查 < 运算符并计算其结果类型的特性类似于第 19.4.4 节第 424 页讨论的 SFINAE 友好的 PlusResultT 特性，但我们在这里为方便起见展示 LessResultT 特性：

typeoverload/lessresult.hpp

```
#include <utility> // for declval()
#include <type_traits> // for true_type and false_type

template<typename T1, typename T2>
class HasLess {
template<typename T> struct Identity;
template<typename U1, typename U2> static std::true_type
test(Identity<decltype(std::declval<U1>() < std::declval<U2>())>*);
template<typename U1, typename U2> static std::false_type
test(...);
public:
static constexpr bool value = decltype(test<T1, T2>(nullptr))::value;
};

template<typename T1, typename T2, bool HasLess>
class LessResultImpl {
public:
using Type = decltype(std::declval<T1>() < std::declval<T2>());
};

template<typename T1, typename T2>
class LessResultImpl<T1, T2, false> {
};

template<typename T1, typename T2>
class LessResultT
: public LessResultImpl<T1, T2, HasLess<T1, T2>::value> {
};

template<typename T1, typename T2>
using LessResult = typename LessResultT<T1, T2>::Type;
```

然后可以将该特性与 IsConvertible 特性组合，使 min() 成为实例化安全的：

typeoverload/min2.hpp

```
#include "isconvertible.hpp"
#include "lessresult.hpp"

template<typename T>
EnableIf<IsConvertible<LessResult<T const&, T const&>, bool>,
T const&>
min(T const& x, T const& y)
{
if (y < x) {
return y;
}
return x;
}
```

尝试使用具有不同 < 运算符的各种类型（或完全缺少该运算符）调用此 min() 函数是有启发性的，如以下示例所示：

typeoverload/min.cpp

```
#include "min.hpp"

struct X1 { };
bool operator< (X1 const&, X1 const&) { return true; }

struct X2 { };
bool operator<(X2, X2) { return true; }

struct X3 { };
bool operator<(X3&, X3&) { return true; }

struct X4 { };

struct BoolConvertible {
operator bool() const { return true; } // implicit conversion to bool
};
struct X5 { };
BoolConvertible operator< (X5 const&, X5 const&)
{
return BoolConvertible();
}

struct NotBoolConvertible { // no conversion to bool
};
struct X6 { };
NotBoolConvertible operator< (X6 const&, X6 const&)
{
return NotBoolConvertible();
}

struct BoolLike {
explicit operator bool() const { return true; } // explicit conversion to bool
};
struct X7 { };
BoolLike operator< (X7 const&, X7 const&) { return BoolLike(); }

int main()
{
min(X1(), X1()); // X1 can be passed to min()
min(X2(), X2()); // X2 can be passed to min()
min(X3(), X3()); // ERROR: X3 cannot be passed to min()
min(X4(), X4()); // ERROR: X4 cannot be passed to min()
min(X5(), X5()); // X5 can be passed to min()
min(X6(), X6()); // ERROR: X6 cannot be passed to min()
min(X7(), X7()); // UNEXPECTED ERROR: X7 cannot be passed to min()
}
```

编译此程序时，请注意，虽然对 X3、X4、X6 和 X7 的四次不同 min() 调用存在错误，但错误并非来自 min() 的函数体，如非实例化安全变体中那样。相反，它们抱怨没有合适的 min() 函数，因为唯一的选择已被 SFINAE 消除。Clang 产生的诊断如下：

```
template<typename T>
class IsContextualBoolT {
private:
template<typename T> struct Identity;
template<typename U> static std::true_type
test(Identity<decltype(std::declval<U>() ? 0 : 1)>*);
template<typename U> static std::false_type
test(...);
public:
static constexpr bool value = decltype(test<T>(nullptr))::value;
};

template<typename T>
constexpr bool IsContextualBool = IsContextualBoolT<T>::value;
```

有了这个新特性，我们就可以提供一个实例化安全的 min()，其 EnableIf 中的要求集是正确的：

typeoverload/min3.hpp

```
#include "iscontextualbool.hpp"
#include "lessresult.hpp"

template<typename T>
EnableIf<IsContextualBool<LessResult<T const&, T const&>>,
T const&>
min(T const& x, T const& y)
{
if (y < x) {
return y;
}
return x;
}
```

这里用于使 min() 实例化安全的技术可以扩展到通过将各种需求检查组合成描述某类类型的特性的方式来描述非平凡模板的需求，例如前向迭代器，并在 EnableIf 中组合这些特性。这样做的好处是重载行为更好，并且消除了编译器在打印嵌套模板实例化深处的错误时产生的“错误噪音”。另一方面，所提供的错误消息往往缺乏关于哪个特定操作失败的具体信息。此外，正如我们用小的 min() 示例所示，准确确定和编码模板的确切要求可能是一项艰巨的任务。我们在第 28.2 节第 654 页探讨了使用这些特性进行调试的技术。

## 20.6 在标准库中

C++ 标准库为输入、输出、前向、双向和随机访问迭代器提供了迭代器标签，我们在介绍中使用了它们。这些迭代器标签是标准迭代器特性（`std::iterator_traits`）的一部分，也是对迭代器的要求，因此可以安全地用于标签分发目的。

C++11 标准库 `std::enable_if` 类模板提供了与本文介绍的 EnableIfT 类模板相同的行为。唯一的区别是标准使用小写的成员类型名为 `type`，而不是我们的大写 `Type`。

算法特化在 C++ 标准库的许多地方使用。例如，`std::advance()` 和 `std::distance()` 都有几个基于其迭代器参数的迭代器类别的变体。大多数标准库实现倾向于使用标签分发，尽管最近有些实现采用了 `std::enable_if` 来实现这种算法特化。此外，许多 C++ 标准库实现也在内部使用这些技术来实现各种标准算法的算法特化。例如，`std::copy()` 可以特化为在迭代器引用连续内存且其值类型具有平凡的复制赋值运算符时调用 `std::memcpy()` 或 `std::memmove()`。同样，`std::fill()` 可以优化为调用 `std::memset()`，并且各种算法可以在类型已知具有平凡析构函数时避免调用析构函数。这些算法特化并不像 `std::advance()` 或 `std::distance()` 那样由 C++ 标准强制规定，但实现者出于效率原因选择提供它们。

如第 8.4 节第 131 页所述，C++ 标准库还强烈暗示在其要求中使用 `std::enable_if<>` 或类似的基于 SFINAE 的技术。例如，`std::vector` 具有构造函数模板，允许从迭代器序列构建向量：

```
template<typename InputIterator>
vector(InputIterator first, InputIterator second,
       allocator_type const& alloc = allocator_type());
```

其要求为“如果构造函数使用不满足输入迭代器资格的类型 InputIterator 调用，则构造函数不得参与重载决议”（参见 [C++11] 的 §23.2.3 第 14 段）。这种表述足够模糊，允许最有效

