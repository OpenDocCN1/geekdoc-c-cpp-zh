

```cpp
template<typename... Types>
void Variant<Types...>::destroy()
{
    (VariantChoice<Types, Types...>::destroy(), ...);
    // indicate that the variant does not store a value
    this->setDiscriminator(0);
}
```

## 26.4.3 赋值

赋值基于初始化和销毁，如赋值运算符所示：

**variant/variantchoiceassign.hpp**

```cpp
template<typename T, typename... Types>
auto VariantChoice<T, Types...>::operator= (T const& value) -> Derived&
{
  if (getDerived().getDiscriminator() == Discriminator) {
    // assign new value of same type:
    *getDerived().template getBufferAs<T>() = value;
  }
  else {
    // assign new value of different type:
    getDerived().destroy(); // try destroy() for all types
    new(getDerived().getRawBuffer()) T(value); // place new value
    getDerived().setDiscriminator(Discriminator);
  }
  return getDerived();
}

template<typename T, typename... Types>
auto VariantChoice<T, Types...>::operator= (T&& value) -> Derived& {
  if (getDerived().getDiscriminator() == Discriminator) {
    // assign new value of same type:
    *getDerived().template getBufferAs<T>() = std::move(value);
  }
  else {
    // assign new value of different type:
    getDerived().destroy(); // try destroy() for all types
    new(getDerived().getRawBuffer()) T(std::move(value)); // place new value
    getDerived().setDiscriminator(Discriminator);
  }
  return getDerived();
}
```

与从存储的值类型之一进行初始化时的情况一样，每个尝试复制其复制构造函数会抛异常的类型的值的尝试都会失败：

**variant/variantexception.cpp**

```cpp
#include "variant.hpp"
#include <exception>
#include <iostream>
#include <string>

class CopiedNonCopyable : public std::exception
{
};

class NonCopyable
{
public:
    NonCopyable()
    {
    }

    NonCopyable(NonCopyable const&)
    {
        throw CopiedNonCopyable();
    }

    NonCopyable(NonCopyable&&) = default;

    NonCopyable& operator= (NonCopyable const&)
    {
        throw CopiedNonCopyable();
    }

    NonCopyable& operator= (NonCopyable&&) = default;
};

int main()
{
    Variant<int, NonCopyable> v(17);
    try {
        NonCopyable nc;
        v = nc;
    }
    catch (CopiedNonCopyable) {
        std::cout << "Copy assignment of NonCopyable failed." << '\n';
        if (!v.is<int>() && !v.is<NonCopyable>()) {
            std::cout << "Variant has no value." << '\n';
        }
    }
}
```

该程序的输出是：

要将此推广到打印任意变体中存储的值，需要一个递归实例化的函数模板和一个辅助函数。例如：

**variant/printrec.cpp**

```cpp
#include "variant.hpp"
#include <iostream>

template<typename V, typename Head, typename... Tail>
void printImpl(V const& v)
{
    if (v.template is<Head>()) {
        std::cout << v.template get<Head>();
    }
    else if constexpr (sizeof...(Tail) > 0) {
        printImpl<V, Tail...>(v);
    }
}

template<typename... Types>
void print(Variant<Types...> const& v)
{
    printImpl<Variant<Types...>, Types...>(v);
}

int main()
{
    Variant<int, short, float, double> v(1.5);
    print(v);
}
```

对于一个相对简单的操作来说，这代码量相当大。为了简化这一点，我们换个思路，为 `Variant` 扩展一个 `visit()` 操作。客户端随后传入一个访问器函数对象，其 `operator()` 将使用当前活动值来调用。由于活动值可能是变体的任意潜在类型，因此这个 `operator()` 很可能要么被重载，要么本身就是一个函数模板。例如，泛型 lambda 提供了模板化的 `operator()`，使我们能够简洁地表示变体 `v` 的打印操作：

```cpp
v.visit([](auto const& value) {
    std::cout << value;
});
```

这个泛型 lambda 大致等价于以下函数对象，该对象对于尚不支持泛型 lambda 的编译器也很有用：

```cpp
class VariantPrinter {
public:
    template<typename T>
    void operator()(T const& value) const
    {
        std::cout << value;
    }
};
```

`visit()` 操作的核心类似于递归的 `print` 操作：它遍历 `Variant` 的类型，检查活动值是否具有给定类型（通过 `is<T>()`），然后在找到适当类型时执行操作：

**variant/variantvisitimpl.hpp**

```cpp
template<typename R, typename V, typename Visitor,
typename Head, typename... Tail>
R variantVisitImpl(V&& variant, Visitor&& vis, Typelist<Head, Tail...>)
{
    if (variant.template is<Head>()) {
        return static_cast<R>(
            std::forward<Visitor>(vis)(
                std::forward<V>(variant).template get<Head>()));
    }
    else if constexpr (sizeof...(Tail) > 0) {
        return variantVisitImpl<R>(std::forward<V>(variant),
            std::forward<Visitor>(vis),
            Typelist<Tail...>());
    }
    else {
        throw EmptyVariant();
    }
}
```

`variantVisitImpl()` 是一个非成员函数模板，带有若干模板参数。模板参数 `R` 描述了访问操作的结果类型，我们稍后会回到这一点。`V` 是变体的类型，`Visitor` 是访问器的类型。`Head` 和 `Tail` 用于分解 `Variant` 中的类型以实现递归。

第一个 `if` 执行（运行时）检查，以确定给定变体的活动值是否为 `Head` 类型。如果是，则通过 `get<Head>()` 从变体中提取该值并传递给访问器，从而终止递归。第二个 `if` 在还有更多元素需要考虑时执行递归。如果没有一个类型匹配，则变体不包含值，⁸ 此时实现会抛出 `EmptyVariant` 异常。

除了由 `VisitResult` 提供的结果类型计算（将在下一节讨论）之外，`visit()` 的实现很直接：

**variant/variantvisit.hpp**

```cpp
template<typename... Types>
template<typename R, typename Visitor>
VisitResult<R, Visitor, Types&...>
Variant<Types...>::visit(Visitor&& vis) & {
using Result = VisitResult<R, Visitor, Types&...>;
return variantVisitImpl<Result>(*this, std::forward<Visitor>(vis),
TypeList<Types...>());
}

template<typename... Types>
template<typename R, typename Visitor>
VisitResult<R, Visitor, Types const&...>
Variant<Types...>::visit(Visitor&& vis) const& {
using Result = VisitResult<R, Visitor, Types const&...>;
return variantVisitImpl<Result>(*this, std::forward<Visitor>(vis),
TypeList<Types...>());
}

template<typename... Types>
template<typename R, typename Visitor>
VisitResult<R, Visitor, Types&&...>
Variant<Types...>::visit(Visitor&& vis) && {
using Result = VisitResult<R, Visitor, Types&&...>;
return variantVisitImpl<Result>(std::move(*this),
std::forward<Visitor>(vis),
TypeList<Types...>());
}
```

这些实现直接委托给 `variantVisitImpl`，传递变体本身、转发访问器，并提供完整的类型列表。三个实现之间唯一的区别在于它们将变体本身作为 `Variant&`、`Variant const&` 还是 `Variant&&` 传递。

## 26.5.1 访问结果类型

`visit()` 的结果类型仍然是个谜。给定的访问器可能有不同的 `operator()` 重载，产生不同的结果类型；也可能有模板化的 `operator()`，其结果类型取决于其参数类型；或者是这些情况的某种组合。例如，考虑以下泛型 lambda：

```cpp
[](auto const& value) {
    return value + 1;
}
```

这个 lambda 的结果类型取决于输入类型：给定 `int`，它产生 `int`；但给定 `double`，它产生 `double`。如果这个泛型 lambda 被传递给 `variant<int, double>` 的 `visit()` 操作，结果应该是什么？

没有唯一正确的答案，因此我们的 `visit()` 操作允许显式提供结果类型。例如，可能有人想要将结果捕获到另一个 `variant<int, double>` 中。可以将结果类型作为第一个模板参数显式指定给 `visit()`：

```cpp
v.visit<variant<int, double>>([](auto const& value) { return value + 1; });
```

当没有放之四海而皆准的解决方案时，显式指定结果类型的能力很重要。然而，要求在所有情况下都显式指定结果类型可能过于冗长。因此，`visit()` 通过默认模板参数和简单元程序的组合提供了两种选项。回忆一下 `visit()` 的声明：

```cpp
template<typename R = ComputedResultType, typename Visitor>
VisitResult<R, Visitor, Types&...> visit(Visitor&& vis) &;
```

模板参数 `R` 在我们上面的示例中显式指定，它也有一个默认参数，因此不必总是显式指定。该默认参数是一个不完整的哨兵类型 `ComputedResultType`：`class ComputedResultType;` 为了计算其结果类型，`visit` 将其所有模板参数传递给 `VisitResult`，这是一个别名模板，提供对新型特征 `VisitResultT` 的访问：

**variant/variantvisitresult.hpp**

```cpp
// an explicitly-provided visitor result type:
template<typename R, typename Visitor, typename... ElementTypes>
class VisitResultT
{
public:
using Type = R;
};
```

