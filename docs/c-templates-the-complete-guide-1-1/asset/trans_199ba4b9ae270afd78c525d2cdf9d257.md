

```cpp
template<typename T>
struct IsSame<T, T> : TrueType
{
};
```

现在，`IsSame<T, T>` 的结果类型可以隐式转换为其基类 `TrueType`，该基类不仅提供相应的 `value` 成员，还允许我们在编译期分派到不同的函数实现或类模板偏特化。例如：

**单击此处查看代码图像**

`traits/2.3/isame.cpp`

```cpp
#include <iostream>
#include <ostream>

template<typename T>
void fooImpl(T, TrueType)
{
    std::cout << "fooImpl(true) for int called\n";
}

template<typename T>
void fooImpl(T, FalseType)
{
    std::cout << "fooImpl(false) for other type called\n";
}

template<typename T>
void foo(T t)
{
    fooImpl(t, IsSame<T,int>{});  // choose impl, depending on type
}

int main()
{
    foo(42);  // calls fooImpl(42, TrueType)
    foo(7.0); // calls fooImpl(7.0, FalseType)
}
```

这种技术称为标签分派，第 467 页的 20.2.3 节介绍了它。

注意，我们的 `IsSame` 实现包含一个 `Type` 成员，这使我们能够重新为 `IsSame<T>` 引入别名模板。

**单击此处查看代码图像**

```cpp
template<typename T>
using IsSameT = typename IsSame<T>::Type;
```

该别名模板可以与变量模板 `IsSame` 共存。

一般来说，产生布尔值的特征应通过派生自 `TrueType` 和 `FalseType` 之类的类型来支持标签分派。然而，为了尽可能通用，任何种类的布尔特征中都应只有一个表示 `true` 的类型和一个表示 `false` 的类型（因此，任何此类特征都应为布尔常量定义自己的类型）。

幸运的是，自 C++11 起，C++ 标准库在 `<type_traits>` 中提供了对应类型：`std::true_type` 和 `std::false_type`。在 C++11 和 C++14 中，它们定义如下：

```cpp
namespace std {
    using true_type = integral_constant<bool, true>;
    using false_type = integral_constant<bool, false>;
}
```

元编程的语境。第 23 章将详细讨论元编程。（这些便利类模板对于像这样的多级嵌套特别有帮助。没有它们，我们就必须在每一层都添加一个类型名和一个 `::Type` 类型。）

此时，数组加法运算符在相加两个可能具有不同元素类型的数组时，能够正确计算结果类型。然而，我们对 `PlusResult<T>` 的表述对元素类型 `T1` 和 `T2` 施加了一个不理想的限制：因为表达式 `T1() + T2()` 试图对 `T1` 和 `T2` 类型的值进行值初始化，所以这两种类型都必须具有可访问的、未删除的默认构造函数（或者必须是非类类型）。`Array` 类的默认构造函数会对其元素类型使用值初始化，因此这是一个额外且不必要的限制。

## decltype

幸运的是，通过使用一个产生给定类型 `T` 值的函数，可以相当容易地为 `T` 表达式产生值，而不需要构造函数。为此，C++ 标准提供了 `std::declval<T>`，如第 965 页的 11.2.3 节所介绍。它在 `<utility>` 中的定义很简单，如下所示：

**单击此处查看代码图像**

```cpp
template<typename T>
add_rvalue_reference_t<T> declval() noexcept;
```

表达式 `declval<T>()` 产生一个 `T` 类型的值，而不需要默认构造函数（或任何其他操作）。

这个函数模板被有意保留为未定义，因为它只打算在 `decltype`、`sizeof` 或某些其他从不要求求值的上下文中使用。它还有两个有趣的属性：

- 对于引用类型，返回类型始终是该类型的右值引用，这使得 `declval<T>` 甚至能用于通常无法从函数返回的类型，例如抽象类类型（具有纯虚函数的类）或数组类型。除此之外，从 `T` 到 `T&&` 的转换在 `declval<T>()` 作为表达式使用时对其行为没有实际影响：两者都是右值（如果 `T` 是对象类型），而左值引用类型由于引用折叠（见第 483 页的 19.7.2 节）保持不变。
- `noexcept` 异常规范表明，`declval` 本身不会导致表达式被视为抛出异常。当 `declval<T>` 在 `decltype` 或其他表达式的上下文中使用时，这一点会很有用（见第 483 页的 19.7.2 节）。

借助 `declval`，我们可以消除 `PlusResult<T>` 对值初始化的要求：

**单击此处查看代码图像**

```cpp
template<typename T1, typename T2>
struct PlusResult {
  using Type = decltype(std::declval<T1>() + std::declval<T2>());
};

template<typename T1, typename T2>
using PlusResultT = typename PlusResult<T1, T2>::Type;
```

结果类型特征提供了一种确定特定操作精确返回类型的方法，并且在描述函数模板的结果类型时通常很有用。

## 19.4 基于 SFINAE 的特征

SFINAE 原则（替换失败并非错误；见第 132 页的 8.4 节和第 250 页的 10.2 节）允许你在模板实参推导期间控制无效类型和表达式形成过程中的错误（这些错误原本会使程序非良构），把它们变成简单的函数失败，从而让重载解析可以选择另一个实体。虽然 SFINAE 最初旨在避免函数模板重载中的虚假失败，但它还支持一些非凡的编译期技术，这些技术可以确定某个特定类型或表达式是否有效。这使我们能够编写特征，以确定例如某个类型是否具有特定成员、是否支持特定操作，或者是否为类。基于 SFINAE 的特征的两种主要方法是：用 SFINAE 排除函数重载，以及用 SFINAE 排除偏特化。

### 19.4.1 用 SFINAE 排除函数重载

我们对基于 SFINAE 的特征的第一次探索，展示了将 SFINAE 与函数重载结合使用的基本技术，以查明某个类型是否可默认构造，从而可以在没有任何初始化值的情况下创建对象。也就是说，对于给定类型 `T`，诸如 `T()` 这样的表达式必须是有效的。

一个基本实现如下所示：

```cpp
#include "Lesson.hpp"

template<typename T>
struct IsDefaultConstructible {
 private:
   // test() trying substitute call of a default constructor
   template<typename U, typename = decltype(U())>
   static char test(void*);

   // test() fallback
   template<typename>
   static long test(...);

 public:
   static constexpr bool value
     = sizeof(test<T>(nullptr)) == sizeof(char);
};
```

使用函数重载实现基于 SFINAE 的特征的通常做法是声明两个名为 `test()`、返回类型不同的重载函数模板：

**单击此处查看代码图像**

```cpp
template<class T> static char test(T*);
template<class> static long test(...);
```

第一个重载被设计为仅在所请求的检查成功时才匹配（我们将在下面讨论如何实现这一点）。第二个重载是回退方案。它始终能匹配该调用，但由于它通过省略号（可变参数）进行匹配，任何其他匹配都会被优先选择（见第 86 页的 C.2 节）。

我们的返回值“value”取决于选择哪个重载的 `test()` 成员：

**单击此处查看代码图像**

```cpp
static constexpr bool value
  = IsSame<decltype(test<T>(nullptr)), char>::value;
```

如果选择第一个 `test()` 成员——当返回类型为 `char` 时——那么由于 `sizeof(char) == sizeof(char)`，`value` 将被初始化为 `true`。否则，由于 `sizeof(long) != sizeof(char)`，它将被初始化为 `false`。

现在，我们必须处理想要测试的特定属性。目标是使第一个 `test()` 重载当且仅当我们要检查的条件成立时才有效。在这种情况下，我们想查明是否可以默认构造传入类型 `T` 的对象。为此，我们将 `T` 和一个 `void*` 作为 `test()` 的第一个声明实参传入（即用实参进行模板实参初始化，该实参当且仅当转换有效时才有效）。在这种情况下，我们使用仅当存在隐式或显式默认构造函数时才有效的表达式：`U()`。该表达式被 `decltype` 包围，以使其成为可用于初始化类型参数的有效表达式。

第二个模板参数无法被推导，因此不会传入对应的实参。而且我们也不会为它提供显式模板实参。因此，它将被替换；如果替换失败，根据 SFINAE，该 `test()` 声明将被丢弃，从而只有回退函数会匹配。

因此，我们可以如下使用该特征：

**单击此处查看代码图像**

```cpp
IsDefaultConstructible<int>::value  // yields true

struct S {
  S() = delete;
};

IsDefaultConstructible<S>::value    // yields false
```

注意，我们可以直接在第一个 `test()` 中使用模板参数 `T`：

