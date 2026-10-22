

};

template<typename R, typename Visitor, typename... ElementTypes>
using VisitResult = typename VisitResultT<R, Visitor, ElementTypes...>::Type; VisitResultT 的主定义处理显式指定 R 参数的情况，因此 Type 被定义为 R。当 R 接收其默认参数时，会应用一个单独的偏特化，
ComputedResultType: 点击此处查看代码图片

```
template<typename Visitor, typename... ElementTypes>
class VisitResultT<ComputedResultType, Visitor, ElementTypes...>
{
...
}
```

该偏特化负责为常见情况计算合适的结果类型，这将是下一节的主题。

## 26.5.2 公共结果类型

当调用一个访问器（visitor）时，它可能为 variant 的每个元素类型产生不同的类型，我们如何将这些类型组合成 visit() 的单一结果类型？有一些明显的情况——如果访问器对每个元素类型返回相同的类型，那么该类型就应该是 visit() 的结果类型。

C++ 已经有一个合理结果类型的概念，在第 12 页的 1.3.3 节中介绍过：在三元表达式 b ? x : y 中，表达式的类型是 x 和 y 类型之间的公共类型。例如，如果 x 的类型是 int，y 的类型是 double，那么公共类型是 double，因为 int 可以提升为 double。我们可以将这种公共类型的概念捕获到一个类型萃取（type trait）中：点击此处查看代码图片

variant/common type.hpp

```
using std::declval;
```

```
template<typename T, typename U>
class CommonTypeT
{
public:
using Type = decltype(true? declval<T>() : declval<U>());
};
```

```
template<typename T, typename U>
using CommonType = typename CommonTypeT<T, U>::Type; The notion of a
```

公共类型可扩展到一组类型：公共类型是该组中所有类型都能提升到的类型。对于我们的访问器，我们希望计算访问器在分别以 variant 中的每种类型调用时所产生的各结果类型的公共类型：点击此处查看代码图片

## variant/variantvisitresultcommon.hpp

```
#include "accumulate.hpp"
#include "commontype.hpp"
// the result type produced when calling a visitor with a value of type T:
template<typename Visitor, typename T>
using VisitElementResult = decltype(declval<Visitor>()(declval<T>()));

// the common result type for a visitor called with each of the given element types:
template<typename Visitor, typename... ElementTypes>
class VisitResultT<ComputedResultType, Visitor, ElementTypes...>
{
using ResultTypes =
Typelist<VisitElementResult<Visitor, ElementTypes>...>;

public:
using Type =
Accumulate<PopFront<ResultTypes>, CommonTypeT, Front<ResultTypes>>;
};
```

VisitResult 的计算分两个阶段进行。首先，VisitElementResult 计算以类型 T 的值调用访问器时产生的结果类型。这个元函数被应用于每个给定的元素类型，以确定访问器可能产生的所有结果类型，并将结果捕获在类型列表 ResultTypes 中。

接下来，计算使用第 560 页 24.2.6 节描述的 Accumulate 算法，将公共类型计算应用于结果类型列表。其初始值（Accumulate 的第三个参数）是第一个结果类型，通过 CommonTypeT 与 ResultTypes 类型列表中剩余的后继值进行组合。最终结果是访问器的所有结果类型都能转换到的公共类型，如果结果类型不兼容，则会产生错误。

自 C++11 起，标准库提供了相应的类型萃取 std::common_type<>，它使用这种方法来产生任意数量传入类型的公共类型（参见第 732 页的 D.5 节），实际上结合了 CommonTypeT 和 Accumulate。通过使用 std::common_type<>，VisitResultT 的实现更简单：点击此处查看代码图片

## variant/variantvisitresultstd.hpp

```
template<typename Visitor, typename... ElementTypes>
class VisitResultT<ComputedResultType, Visitor, ElementTypes...>
{
public:
using Type =
std::common_type_t<VisitElementResult<Visitor, ElementTypes>...>;
};
```

下面的示例程序打印出传入一个泛型 lambda（将收到的值加 1）所产生的类型：点击此处查看代码图片

## variant/visit.cpp

```
#include "variant.hpp"
#include <iostream>
#include <typeinfo>

int main()
{
Variant<int, short, double, float> v(1.5);
auto result = v.visit([](auto const& value) {
return value + 1;
});
std::cout << typeid(result).name() << '\n';
}
```

该程序的输出将是 double 的 type_info 名称，因为所有结果类型都能转换到该类型。

## 26.6 Variant 的初始化与赋值

Variant 可以通过多种方式进行初始化和赋值，包括默认构造、拷贝构造和移动构造，以及拷贝赋值和移动赋值。本节将详细介绍这些 Variant 操作。

### 默认初始化

Variant 是否应该提供默认构造函数？如果不提供，Variant 可能会变得不必要地难以使用，因为人们总是必须凭空构造一个初始

默认构造的 v2 存储 double 类型的 0

### 拷贝/移动初始化

拷贝和移动初始化更有趣。要拷贝一个源 variant，我们需要确定它当前存储的是哪种类型，将该值拷贝构造到缓冲区中，并设置判别式。幸运的是，visit() 负责解码源 variant 的活动值，而从 VariantChoice 继承的拷贝赋值运算符会将值拷贝构造到缓冲区中，从而得到一个紧凑的实现：⁹

variant/variantcopyctor.hpp

```
template<typename... Types>
Variant<Types...>::Variant(Variant const& source) {
if (!source.empty()) {
source.visit([&](auto const& value) {
*this = value;
});
}
}
```

移动构造函数类似，不同之处仅在于访问源 variant 时使用 std::move，并从源值进行移动赋值：点击此处查看代码图片

variant/variantmovector.hpp

```
template<typename... Types>
Variant<Types...>::Variant(Variant&& source) {
if (!source.empty()) {
std::move(source).visit([&](auto&& value) {
*this = std::move(value);
});
}
}
```

基于访问器的实现有一个特别有趣的方面：它也适用于拷贝和移动操作的模板化形式。例如，模板化的拷贝构造函数可以定义如下：点击此处查看代码图片

variant/variantcopyctortmpl.hpp

```
template<typename... Types>
template<typename... SourceTypes>
Variant<Types...>::Variant(Variant<SourceTypes...> const& source) {
if (!source.empty()) {
source.visit([&](auto const& value) {
*this = value;
});
}
}
```

由于这段代码会访问源 variant，因此对 *this 的赋值将针对源 variant 的每种类型进行。该赋值操作的重载决议会为每个源类型找到最合适的目标类型，并在必要时执行隐式转换。下面的示例演示了从不同的 variant 类型进行构造和赋值：点击此处查看代码图片

## variant/variantpromote.cpp

```
#include "variant.hpp"
#include <iostream>
#include <string>

int main()
{
Variant<short, float, char const*> v1((short)123);

Variant<int, std::string, double> v2(v1);
std::cout << "v2 contains the integer " << v2.get<int>() << '\n';

v1 = 3.14f;
Variant<double, int, std::string> v3(std::move(v1));
std::cout << "v3 contains the double " << v3.get<double>() << '\n';

v1 ="hello";
Variant<double, int, std::string> v4(std::move(v1));
std::cout << "v4 contains the string " << v4.get<std::string>() <<
'\n';
}
```

从 v1 构造或赋值给 v2 或 v3 涉及整型提升（short 到 int）、浮点提升（float 到 double）以及用户定义转换（char const* 到 std::string）。该程序的输出如下：
v2 contains the integer 123
v3 contains the double 3.14
v4 contains the string hello

