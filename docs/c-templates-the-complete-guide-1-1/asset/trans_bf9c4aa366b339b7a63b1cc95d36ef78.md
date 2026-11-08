

```
T value(Type<T>) // no definition needed
```

让我们从 `isValid` 的定义开始：它是一个 constexpr 变量，其类型是 lambda 的闭包类型。该声明必须使用占位符类型（在我们的代码中是 `auto`），因为 C++ 无法直接表达闭包类型。C++17 之前，lambda 表达式不能出现在常量表达式中。到了 C++17，这种能力在常量表达式中也可用。在 C++17 中，由于 `isValid` 具有闭包类型，因此它可以被调用（即被调用），但它返回的对象本身是一个 lambda 闭包类型的对象，由内层 lambda 表达式产生。

在深入这个内层 lambda 表达式的细节之前，让我们看看 `isValid` 的一个典型用法：

```
constexpr auto isDefaultConstructible
    = isValid([] (auto x) -> decltype(std::declval<decltype(x)>())
        { return {}; });
```

我们已经知道 `isDefaultConstructible` 具有 lambda 闭包类型，而且顾名思义，它是一个函数对象，用于检查某个类型是否可默认构造这一 trait（我们将在后文看到原因）。换句话说，`isValid` 是一个 trait 工厂。一个根据其参数生成 trait 检查对象的组件。

类型辅助变量模板允许我们将类型表示为值。我使用一个 `type` 变量，你可以用 `decltype(value)` 将其还原为原始类型，而这正是上面传给 `isValid` 的内容。如果提取出的类型不能默认构造，那么 `decltype(value)` 就是无效的，我们要么得到编译器错误，要么替换出一个关联的默认函数；由于 `isValid` 定义的细节，我们将实现后一种效果。

`isDefaultConstructible` 可以如下使用：

```
isDefaultConstructible(type<int>)                 // true (int is
                                                     // default-constructible)
isDefaultConstructible(type<std::unique_ptr<int>&>)   // false (references
                                                     // are not default-constructible)
```

现在所有部分协同工作，考虑当 `isValid` 中的内层 lambda 表达式被调用时，参数 `t` 绑定到 `isDefaultConstructible` 定义中指定的泛型 lambda 参数后，它会变成什么。通过在 `isValid` 的定义中执行替换，我们得到等价于

```
constexpr auto isDefaultConstructible
    = [] (auto... args) {
        return decltype([] (auto x) -> decltype(std::declval<
            decltype(args)>()); 
        });
      };
```

如果我们回看上面 `isValid` 的第一个声明，会注意到它包含一个如下形式的默认模板实参

```
decltype([](decltype(auto) t) -> decltype(std::declval<T>()));
```

它试图用参数类型的值（`decltype(std::declval<...>())`）调用其第一个模板实参类型的值，而该类型是 `isDefaultConstructible` 定义中 lambda 的闭包类型。在 `isValid` 的第一个实参的类型中，创建了一个常规 lambda 表达式；其返回类型指定为 `decltype(std::declval<...>)`，如上所示。当替换该表达式时，如果 `isDefaultConstructible` 的第一个声明是良构的，则调用有效。如果不是，则表达式替换失败，并被 SFINAE 淘汰。这样就只剩下第二个声明，否则它的匹配程度较低，会产生 false 值。此外，当传入 `type<T&>` 时，`isDefaultConstructible` 会产生 false 类型。如果改为传入 `type<T>`，则替换不会失败，并选择 `isValid<T>()` 的第一个声明，产生 true 值。

回想一下，要让 SFINAE 起作用，替换必须发生在被替换模板的立即上下文中。在这种情况下，替换模板是 `isValid<T>` 的第一个声明和传给 `isValid` 的泛型 lambda 的调用运算符。因此，要测试的构造必须出现在该 lambda 的返回类型中，而不是其函数体中！

我们的 `isDefaultConstructible` trait 与之前的 trait 实现略有不同，因为它要求函数对象实例，而不是指定模板实参。这可以说是一种更易用的写法，但也可以获得之前的风格：

```
template<typename T>
using isDefaultConstructible = decltype(isValid(type<T>{}));
```

块作用域。

到目前为止，这种技术可能看起来很有吸引力，因为实现中涉及的表达式和使用风格都比之前的技术更复杂。然而，一旦放置并理解了 `yield`，许多 trait 只需一个声明就能实现。例如，测试对名为 `first` 的成员的访问就相当简洁（完整示例见第 438 页的 19.6.1 节）：

```
template<typename T>
struct HasFirst {
  template<typename U>
  static auto test(U* u) -> decltype(u->first);
};
```

### 19.9.4 对 SFINAE 友好的 trait

一般来说，类型 trait 应当能够回答特定查询，而不使程序变为非良构。基于 SFINAE 的 trait 通过将潜在问题小心地捕获在 SFINAE 上下文中来解决这个问题，从而把那些本会成为错误的情况转化为否定结果。

然而，到目前为止介绍的一些 trait（例如第 434 页 19.3.4 节描述的 `PlusResultT` trait）在出现错误时表现不佳。回想该节中 `PlusResultT<>` 的定义：

```
template<typename T1, typename T2>
struct PlusResult {
  using Type = decltype(std::declval<T1>() + std::declval<T2>());
};

template<typename T1, typename T2>
using PlusResultT = typename PlusResult<T1, T2>::Type;
```

在这个定义中，`+` 用于不受 SFINAE 保护的上下文。因此，如果程序试图对没有合适 `+` 运算符的类型求值 `PlusResult<T>`，那么对 `PlusResult<T>` 本身的求值就会使程序变为非良构，如下面尝试声明两个无关类型 `A` 和 `B` 的数组相加的返回类型时所示：

```
template<typename T>
class Array {
};

template<typename T1, typename T2>
Array<PlusResultT<T1, T2>>
operator+(Array<T1> const&, Array<T2> const&);
```

显然，如果没有为数组元素定义相应的运算符 `+`，在这里使用 `PlusResultT<>` 会导致错误。

```
class A {
};

class B {
};

void add(Array<A> const&, Array<A> const&);

// declare a + for arrays of different element types:
template<typename T1, typename T2>
Array<PlusResultT<T1, T2>>
operator+(Array<T1> const&, Array<T2> const&);

// no int = arrayA + arrayB   // ERROR? depends on
// whether the compiler              // instantiations
// ...
```

如果编译器能够在不进行第一个 `operator+`（模板）声明的推导和替换的情况下确定第二个 `operator+` 声明是有效匹配，它就会接受这段代码。

然而，在推导和替换函数模板候选时，类模板定义实例化期间发生的任何事情都不属于该函数模板替换的立即上下文，SFINAE 也无法保护我们免于在那里形成无效类型或表达式的尝试。此时不会只是丢弃该函数模板候选，而是会立即引发错误，因为我们试图对类型 `T1` 和 `T2` 的两个元素调用 `operator+`。

```
template<typename T1, typename T2>
struct PlusResultT {
    using Type = decltype(std::declval<T1>() + std::declval<T2>());
};
```

要解决这个问题，我们必须让 `PlusResultT` 对 SFINAE 友好，这意味着即使其 `decltype` 表达式非良构，也要通过给它一个合适的定义来使其更合适。

按照上一节描述的 `HasResultT` 示例，我们定义一个 `HasPlusTrait`，它允许我们检测给定类型是否存在合适的 `+` 运算：

```
#include <utility>      // for declval
#include <type_traits>   // for decltype, false_type,
                         // true_type

// primary template
template<typename T1, typename T2, typename = std::void_t<>>
struct HasPlusT : std::false_type
{
};

// partial specialization (may be SFINAE'd away)
template<typename T1, typename T2>
struct HasPlusT<T1, T2, std::void_t<decltype(std::declval<T1>() +
                                             std::declval<T2>())>>
  : std::true_type
{
};
```

如果它产生 true 结果，`PlusResultT` 就可以使用现有实现。否则，`PlusResultT` 需要一个安全的默认值。对于一组模板实参没有有意义结果的 trait，最好的默认值就是根本不提供任何成员 `Type`。这样，如果该 trait 在 SFINAE 上下文中使用——例如错误 `operator+` 的返回类型——缺失的成员 `Type` 将使模板实参推导失败，而这正是数组 `operator+` 模板所期望的行为。

下面 `PlusResultT` 的实现提供了这种行为：

```
#include "HasPlus.hpp"

template<typename T1, typename T2, bool = HasPlusT<T1, T2>::value>
struct PlusResultT {                 // primary template, used ...
    using Type = decltype(std::declval<T1>() + std::declval<T2>());
};

template<typename T1, typename T2>
struct PlusResultT<T1, T2, false> {    // partial specialization
```

