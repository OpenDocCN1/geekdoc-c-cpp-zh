
```cpp
std::cout << "std::vector<int>::size: "
          << HasMemberT_size<std::vector<int>>::value << '\n';
std::cout << "std::pair<int,int>::first: "
          << HasMemberT_first<std::pair<int,int>>::value << '\n';
}
```

修改偏特化以排除 `&T::Member` 不是指向成员的指针类型的情况（相当于排除静态数据成员）并不困难。类似地，也可以排除或要求指向成员函数的指针，从而将特征限制为数据成员或成员函数。

### 19.6.2 检测成员函数

注意，`HasMemberT` 特征只检查是否存在一个具有相应名称的成员。如果存在两个成员（例如，当我们检查重载成员函数时可能会出现这种情况），该特征也会失败。例如：

```cpp
DEFINE_HAS_MEMBER(begin);
std::cout << HasMemberT_begin<std::vector<int>>::value; // false
```

然而，正如第133页第8.4.1节所解释的，SFINAE 原则可以防止在函数模板声明中创建无效类型和表达式的尝试，从而使上述重载技术能够扩展到测试任意表达式是否良构。

也就是说，我们可以简单地检查是否能够以特定方式调用某个我们关注的函数，即使该函数被重载，这种检查也可能成功。与第428页第19.5节中的 `IsConvertibleT` 特征一样，诀窍在于构造一个表达式，在附加函数模板参数的默认值的 `decltype` 表达式中检查我们能否调用 `begin()`：

`traits/hasbegin.hpp`

```cpp
#include <utility>        // for declval
#include <type_traits>    // for true_type, false_type, and void_t

// primary template:
template<typename, typename = std::void_t<>>
struct HasBeginT : std::false_type {
};

// partial specialization (may be SFINAE'd away):
template<typename T>
struct HasBeginT<T, std::void_t<decltype(std::declval<T>().begin())>>
: std::true_type {
};
```

在这里，我们使用 `decltype(std::declval<T>().begin())` 来测试：给定类型 T 的一个值/对象（使用 `std::declval` 以避免需要任何构造函数），调用成员 `begin()` 是否有效。²²

### 19.6.3 检测其他表达式

我们可以将上述技术用于其他类型的表达式，甚至组合多个表达式。例如，我们可以测试：给定类型 T1 和 T2，对于这些类型的值，是否定义了合适的 `<` 运算符：

`traits/hasless.hpp`

```cpp
#include <utility>        // for declval
#include <type_traits>    // for true_type, false_type, and void_t

// primary template:
template<typename, typename, typename = std::void_t<>>
struct HasLessT : std::false_type
{};

// partial specialization (may be SFINAE'd away):
template<typename T1, typename T2>
struct HasLessT<T1, T2, std::void_t<decltype(std::declval<T1>() < std::declval<T2>())>>
: std::true_type
{};
```

与以往一样，关键之处在于为要检查的条件定义一个有效表达式，并用 `decltype` 将其置于 SFINAE 上下文中；如果表达式无效，则会回退到主模板：`decltype(std::declval<T1>() < std::declval<T2>())`。以这种方式检测有效表达式的特征相当健壮：只有当表达式良构时它们才会求值为 true，而当 `<` 运算符具有歧义、被删除或不可访问时，它们会正确返回 false。²³

我们可以如下使用该特征：

```cpp
HasLessT<int, char>::value                                // yields true
HasLessT<std::string, std::string>::value                 // yields true
HasLessT<std::string, int>::value                         // yields false
HasLessT<std::string, char*>::value                       // yields true
HasLessT<std::complex<double>, std::complex<double>>::value // yields false
```

如第30页第2.3.1节所介绍，我们可以使用这个特征来要求模板参数 T 支持 `operator <`：

```cpp
template<typename T>
class C
{
    static_assert(HasLessT<T>::value,
                  "Class C requires comparable elements");
};
```

注意，由于 `std::void_t` 的特性，我们可以在一个特征中组合多个约束：

`traits/hasvarious.hpp`

```cpp
#include <utility>        // for declval
#include <type_traits>    // for true_type, false_type, and void_t

// primary template:
template<typename, typename = std::void_t<>>
struct HasVariousT : std::false_type
{
};

// partial specialization (may be SFINAE'd away):
template<typename T>
struct HasVariousT<T, std::void_t<decltype(std::declval<T>().begin()),
                                  typename T::difference_type,
                                  typename T::iterator>>
: std::true_type
{
};
```

能够检测特定语法是否有效的特征非常强大，它们允许模板根据特定操作是否存在来自定义行为。这些特征将再次被用于定义对 SFINAE 友好的特征（第424页第19.4.4节），并辅助基于类型属性的重载（第20章）。

### 19.6.4 使用泛型 Lambda 检测成员

第421页第19.4.3节引入的 `isValid` lambda 提供了一种更紧凑的技术来定义检查成员的特征，帮助我们避免使用宏来处理任意名称的成员。

下面的示例说明了如何定义特征，以检查数据成员或类型成员（如 `first` 或 `size_type`）是否存在，或者是否为两个不同类型的对象定义了 `operator<`：

`traits/isvalid1.cpp`

```cpp
#include "isvalid.hpp"
#include <iostream>
#include <string>
#include <utility>

int main()
{
    using namespace std;
    cout << boolalpha;

    // define to check for data member first:
    constexpr auto hasFirst
        = isValid([](auto x) -> decltype((void)valueT(x).first) {});

    cout << "hasFirst: " << hasFirst(type<pair<int,int>>) << '\n'; // true

    // define to check for member type size_type:
    constexpr auto hasSizeType
        = isValid([](auto x) -> typename decltype(valueT(x))::size_type {});

    struct CX {
        using size_type = std::size_t;
    };
    cout << "hasSizeType: " << hasSizeType(type<CX>) << '\n'; // true

    if constexpr (!hasSizeType(type<int>)) {
        cout << "int has no size_type\n";
    }

    // define to check for <:
    constexpr auto hasLess
        = isValid([](auto x, auto y) -> decltype(valueT(x) < valueT(y)) {});

    cout << hasLess(42, type<char>) << '\n';               // yields true
    cout << hasLess(type<string>, type<string>) << '\n';   // yields true
    cout << hasLess(type<string>, type<int>) << '\n';      // yields false
    cout << hasLess(type<string>, "hello") << '\n';        // yields true
}
```

再次注意，`hasSizeType` 使用 `std::decay` 从传入的 `x` 中移除引用，因为你无法从引用访问类型成员。如果跳过这一步，特征将始终产生 `false`，因为会使用 `isValidImpl<>()` 的第二个重载。

为了能够使用常见的泛型语法（将类型作为模板参数），我们可以再次定义额外的辅助函数。例如：

`traits/isvalid2.cpp`

```cpp
#include "isvalid.hpp"
#include <iostream>
#include <string>
#include <utility>

constexpr auto hasFirst
    = isValid([](auto&& x) -> decltype((void)&x.first) {});

template<typename T>
using HasFirstT = decltype(hasFirst(std::declval<T>()));

constexpr auto hasSizeType
    = isValid([](auto&& x)
              -> typename std::decay_t<decltype(x)>::size_type {});

template<typename T>
using HasSizeTypeT = decltype(hasSizeType(std::declval<T>()));

constexpr auto hasLess
    = isValid([](auto&& x, auto&& y) -> decltype(x < y) {});

template<typename T1, typename T2>
using HasLessT = decltype(hasLess(std::declval<T1>(), std::declval<T2>()));

int main()
{
    using namespace std;

    cout << "first: " << HasFirstT<pair<int,int>>::value << '\n'; // true
    struct CX {
        using size_type = std::size_t;
    };
    cout << "size_type: " << HasSizeTypeT<CX>::value << '\n'; // true
    cout << "size_type: " << HasSizeTypeT<int>::value << '\n'; // false

    cout << HasLessT<int, char>::value << '\n'; // true
    cout << HasLessT<string, string>::value << '\n'; // true
    cout << HasLessT<string, int>::value << '\n'; // false
    cout << HasLessT<string, char*>::value << '\n'; // true
}
```

现在，`template<typename T> using HasFirstT = decltype(hasFirst(std::declval<T>()));` 允许我们调用 `HasFirstT<std::pair<int,int>>::value`，这将导致针对一个由两个 int 组成的 pair 调用 `hasFirst`，其求值方式如上所述。

## 19.7 其他特征技术

最后，让我们介绍并讨论一些其他定义特征的方法。

### 19.7.1 If-Then-Else

在上一节中，`PlusResultT` 特征的最终定义根据另一个类型特征 `HasPlusT` 的结果而采用了完全不同的实现。我们可以使用一个特殊的类型模板 `IfThenElse` 来表述这种 if-then-else 行为，该模板接受一个布尔非类型模板参数，用于从两个类型参数中选择一个：

`traits/ifthenelse.hpp`

```cpp
#ifndef IFTHENELSE_HPP
#define IFTHENELSE_HPP

// primary template: yield the second argument by default and rely on
// a partial specialization to yield the third argument
// if COND is false
```

