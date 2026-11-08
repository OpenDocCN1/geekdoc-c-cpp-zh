
1)，我们只为第二个 `test()` 重载创建特定的 SFINAE 上下文。

## 基于 SFINAE 的特性的替代实现策略

基于 SFINAE 的特性自 1998 年首个 C++ 标准发布之前就已经可以实现。这种方法的关键始终在于声明两个返回不同类型的重载函数模板。

```cpp
template <typename T> static char test(T*);
template <typename> static long test(...);
```

然而，最初发布的技术利用返回类型的大小来确定选择哪个重载（还使用了枚举，因为当时还没有空指针和常量）。

```cpp
enum { value = sizeof(test<T>(...)) == 1 };
```

在某些平台上，可能会发生 `sizeof(char) == sizeof(long)` 的情况（例如，在数字信号处理器（DSP）或 C++ 机器上，所有基本整型类型可能具有相同的大小）。根据定义，`sizeof(char)` 等于 1，因此在这些机器上 `sizeof(long)` 可以等于 1，甚至 `sizeof(long) == sizeof(char)`。

鉴于这一观察，我们希望确保 `test()` 函数的返回类型在所有平台上都具有不同的大小。例如，在定义以下内容之后：

```cpp
using SizeT = char;
using SizeT2 = struct { char a[2]; };
```

或

```cpp
using SizeT = char[6];
using SizeT2 = char[6][2];
```

我们可以如下定义 `test()` 重载：

```cpp
template <typename T> static SizeT test(void*);  // checking
template <typename> static SizeT2 test(...);     // fallback
```

还要注意，传递给 `test()` 的调用参数的类型无关紧要。重要的是传递的参数与期望类型匹配。例如，您也可以定义传递整数 42：

```cpp
template <typename T> SizeT test(int);     // checking
template <typename> SizeT2 test(...);      // fallback

return sizeof(test<T>(42)) == 1;
```

## 让基于 SFINAE 的特性可预测

如第 410 页的 19.3.3 节所介绍的，返回布尔值的谓词特性（predicate trait）应该返回派生自 `std::true_type` 或 `std::false_type` 的值。这样，我们还可以解决在某些平台上 `sizeof(char) == sizeof(long)` 的问题。

为此，我们需要一个 `is-type()` 构造的隐式定义。该特性本身应该派生自辅助类的类型，该辅助类提供必要的基类。幸运的是，我们可以直接将匹配核心特性的基类作为 `test()` 重载的返回类型：

```cpp
template <typename T> static std::true_type test(T*);    // checking
template <typename> static std::false_type test(...);    // fallback

template<typename T>
using is_default_constructible = decltype(test<T>(nullptr));
```

这样，基类的 `Type` 成员可以直接声明如下：

```cpp
using Type = decltype(SFINAE<...>);
```

并且我们不再需要 `isSameT` 特性。

因此，`isDefaultConstructible` 的完整改进实现如下：

traits/is_defaultconstructible.hpp

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_285_0.png)

```cpp
private:

  // test() trying substitute call of a default constructor
  template<typename T, typename = decltype(T())>
    static std::true_type test(void*);

  // test() fallback:
  template<typename>
    static std::false_type test(...);

public:
  using Type = decltype(test<T>(nullptr));
};

template<typename T>
struct IsDefaultConstructible : IsDefaultConstructibleT<T> {};
```

现在，如果第一个 `test()` 函数模板有效，则它是首选重载，因此成员 `IsDefaultConstructible::Type` 由其返回类型 `std::true_type` 初始化。从而 `IsDefaultConstructible<T>` 派生自 `std::true_type`。

如果第一个 `test()` 函数模板无效，则它因 SFINAE 而被禁用，并且 `IsDefaultConstructible<T>` 由 `test()` 回退的返回类型（即 `std::false_type`）初始化。结果是 `IsDefaultConstructible<T>` 派生自 `std::false_type`。

### 9.4.2 SFINAE 剔除部分特化

实现基于 SFINAE 的特性的第二种方法使用部分特化。同样，我们可以使用该示例来检查类型是否默认可构造：

traits/isdefaultconstructible3.hpp

```cpp
#include "isdefaultconstructible.hpp"
#include <type_traits>   // define true_type and false_type

// helper to ignore any number of template parameters:
template<typename...>
using void_t = void;

// primary template:
template<typename T, typename = void>
struct IsDefaultConstructibleT : std::false_type
{
};

// partial specialization (may be SFINAE'd away):
template<typename T>
struct IsDefaultConstructibleT<T, void_t<decltype(T{})>>
  : std::true_type
{
};
```

与上面谓词特性的 `IsDefaultConstructible<T>` 实现一样，我们将一般情况定义为从 `std::false_type` 派生，因为默认类型具有成员 `value`。

这里有趣的特点是第二个模板参数默认为辅助类型 `void_t`。它使我们能够提供使用任意数量编译期类型构造的部分特化。

在这种情况下，我们只需要一个构造：

```cpp
decltype(T{})
```

用于再次检查 `T` 的默认构造函数是否有效。如果对于特定的 `T`，该构造无效，这一次 SFINAE 会导致整个部分特化被丢弃，并回退到主模板。否则，部分特化有效且是首选。

在 C++17 中，C++ 标准库引入了一个类型特性 `std::void_t`：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_287_0.png)

```cpp
#include <type_traits>

#ifndef __cpp_lib_void_t
namespace std {
    template<typename...> using void_t = void;
}
#endif
```

从 C++14 开始，C++ 标准化委员会建议编译器和标准库通过定义约定的特性宏来指示它们已实现标准的哪些部分。这不是符合标准的要求，但实现通常会遵循该建议以便对用户有所帮助。宏 `__cpp_lib_void_t` 是用于指示库实现具有 `std::void_t` 的推荐宏，因此我们上面的代码以它为条件。

显然，这种定义类型特性的方式比第一种重载函数模板的方法看起来更简洁。但它要求能够在模板参数的声明中表述条件。使用带有函数重载的类模板使我们能够使用额外的辅助函数或辅助类型。

### 9.4.3 使用泛型 Lambda 进行 SFINAE

无论我们使用哪种技术，定义特性总是需要一些样板代码；重载和调用必须通过多个部分特化来实现。接下来，我们将展示在 C++17 中，如何通过在泛型 lambda 中指定要检查的条件来最小化这些样板代码。

首先，我们介绍一个由两个嵌套泛型 lambda 表达式构建的工具：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_287_1.png)

traits/is_valid.hpp

```cpp
#include <utility>

// helper: checking validity of f (arg...) for F and Args
template<typename F, typename... Args>
constexpr auto is_valid_impl(int)
    -> decltype(std::declval<F>()(std::declval<Args>()...), std::true_type{});

// fallback if helper SFINAEd out
template<typename F, typename... Args>
constexpr std::false_type is_valid_impl(...);

// define a lambda that takes a lambda f and returns a lambda
inline constexpr auto is_valid = [](auto f) {
    return [f](auto&&... args) {
        return decltype(is_valid_impl<decltype(f), decltype(args)...>(0))::value;
    };
};

// helper template to represent a type as a value
template<typename T>
struct TypeT {
    using Type = T;
};

// helper to map a type as a value
template<typename T>
constexpr auto type = TypeT<T>{};
```
