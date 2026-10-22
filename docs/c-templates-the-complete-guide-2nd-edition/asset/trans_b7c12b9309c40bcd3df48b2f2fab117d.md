
参数。（在我们的第一种方法中，静态数据成员必须嵌入到成员类模板中。）然而，模板模板参数方法的一个缺点是，策略类现在必须写成模板，并且模板参数集必须与我们的接口定义完全一致。这可能会使得特征（traits）本身的表达比简单的非模板类更加冗长，也不那么自然。

## 19.2.3 组合多个策略和/或特征

正如我们的开发过程所示，特征和策略并不能完全消除多个模板参数的存在。然而，它们确实将参数数量减少到了可控的程度。那么，一个有趣的问题是如何对这些多个参数进行排序。

一种简单的策略是按照其默认值被选中的可能性递增的顺序来排列参数。通常，这意味着特征参数位于策略参数之后，因为策略参数在客户端代码中更常被覆盖。（细心的读者可能已经在我们前面的开发中注意到了这一策略。）如果我们愿意为代码增加大量复杂性，还有一种替代方案，它本质上允许我们以任意顺序指定非默认参数。详情请参阅第512页的21.4节。

## 19.2.4 使用通用迭代器进行累加

在结束对特征和策略的介绍之前，看一下`accum()`的一个版本是很有启发性的，该版本增加了处理通用迭代器（而不仅仅是指针）的能力，这正是工业级泛型组件所应具备的。有趣的是，这仍然允许我们使用指针调用`accum()`，因为C++标准库提供了*迭代器特征*。（特征无处不在！）因此，我们可以将`accum()`的初始版本定义如下（忽略我们后续的改进）：⁷

```cpp
#ifndef ACCUM_HPP
#define ACCUM_HPP

#include <iterator>

template<typename Iter>
auto accum (Iter start, Iter end)
{
    using VT = typename std::iterator_traits<Iter>::value_type;

    VT total{}; // assume this actually creates a zero value
    while (start != end) {
        total += *start;
        ++start;
    }
    return total;
}

#endif // ACCUM_HPP
```

`std::iterator_traits`结构封装了迭代器的所有相关属性。由于存在针对指针的偏特化，这些特征可以方便地用于任何普通指针类型。以下是标准库实现可能实现此支持的方式：

```cpp
namespace std {
template<typename T>
struct iterator_traits<T*> {
    using difference_type = ptrdiff_t;
    using value_type = T;
    using pointer = T*;
    using reference = T&;
    using iterator_category = random_access_iterator_tag;
};
}
```

然而，并没有一个类型来表示迭代器所指值的累加结果；因此我们仍然需要设计自己的`AccumulationTraits`。

## 19.3 类型函数

最初的特征示例表明，我们可以定义依赖于类型的行为。传统上，在C和C++中，我们定义的函数更具体地可以称为值函数：它们以某些值作为参数，并返回另一个值作为结果。借助模板，我们还可以定义类型函数：以某种类型作为参数，并产生一个类型或常量作为结果的函数。

一个非常有用的内置类型函数是`sizeof`，它返回一个常量，描述给定类型参数的大小（以字节为单位）。类模板也可以充当类型函数。类型函数的参数就是模板参数，结果则作为成员类型或成员常量来提取。例如，`sizeof`运算符可以具有以下接口：

```cpp
#include <cstddef>
#include <iostream>

template<typename T>
struct TypeSize {
    static std::size_t const value = sizeof(T);
};

int main()
{
    std::cout << "TypeSize<int>::value = "
              << TypeSize<int>::value << '\n';
}
```

这可能看起来不是很有用，因为我们已经有了内置的`sizeof`运算符，但请注意，`TypeSize<T>`是一个类型，因此它本身可以作为类模板参数传递。或者，`TypeSize`是一个模板，可以作为模板模板参数传递。

接下来，我们将开发一些更通用的类型函数，它们可以以这种方式用作特征类。

### 19.3.1 元素类型

假设我们有许多容器模板，例如`std::vector<>`和`std::list<>`，以及内置数组。我们希望有一个类型函数，给定这样的容器类型，能够产生元素类型。这可以通过偏特化来实现：

```cpp
#include <vector>
#include <list>

template<typename T>
struct ElementT; // primary template

template<typename T>
struct ElementT<std::vector<T>> { // partial specialization for std::vector
    using Type = T;
};

template<typename T>
struct ElementT<std::list<T>> { // partial specialization for std::list
    using Type = T;
};
...

template<typename T, std::size_t N>
struct ElementT<T[N]> { // partial specialization for arrays of known bounds
    using Type = T;
};

template<typename T>
struct ElementT<T[]> { // partial specialization for arrays of unknown bounds
    using Type = T;
};
...
```

注意，我们应该为所有可能的数组类型提供偏特化（详见第71页的5.4节）。

我们可以如下使用这个类型函数：

```cpp
#include "elementtype.hpp"
#include <vector>
#include <iostream>
#include <typeinfo>

template<typename T>
void printElementType (T const& c)
{
    std::cout << "Container of "
              << typeid(typename ElementT<T>::Type).name()
              << " elements.\n";
}

int main()
{
    std::vector<bool> s;
    printElementType(s);
    int arr[42];
    printElementType(arr);
}
```

使用偏特化使我们能够在不要求容器类型了解该类型函数的情况下实现它。然而，在许多情况下，类型函数是与适用的类型一起设计的，因此实现可以简化。例如，如果容器类型定义了成员类型`value_type`（就像标准容器那样），我们可以编写以下代码：

```cpp
template<typename C>
struct ElementT {
    using Type = typename C::value_type;
};
```

这可以作为默认实现，并且它不排除为那些没有定义适当成员类型`value_type`的容器类型提供特化。

尽管如此，通常建议为类模板类型参数提供成员类型定义，以便在泛型代码中更容易地访问它们（就像标准容器模板所做的那样）。下面勾勒了这一思想：

```cpp
template<typename T1, typename T2, ...>
class X {
public:
    using Type1 = T1;
    using Type2 = T2;
    ...
};
```

类型函数有什么用处？它允许我们仅根据容器类型来参数化模板，而无需同时为元素类型和其他特性提供参数。例如，与其使用

```cpp
template<typename T, typename C>
T sumOfElements (C const& c);
```

这种写法需要类似`sumOfElements<int>(list)`的语法来显式指定元素类型，我们可以声明

```cpp
template<typename C>
typename ElementT<C>::Type sumOfElements (C const& c);
```

其中元素类型由类型函数确定。

请注意，这些特征是如何作为现有类型的扩展来实现的；也就是说，即使对于基本类型和封闭库中的类型，我们也可以定义这些类型函数。

在这种情况下，类型`ElementT`被称为特征类（traits class），因为它用于访问给定容器类型`C`的某个特征（通常，这样的类中可以收集多个特征）。因此，特征类不仅限于描述容器参数的特征，而是可以描述任何种类的“主参数”的特征。

为了方便起见，我们可以为类型函数创建别名模板。例如，我们可以引入

```cpp
template<typename T>
using ElementType = typename ElementT<T>::Type;
```

这使我们能够进一步简化上面`sumOfElements`的声明，变为

```cpp
template<typename C>
ElementType<C> sumOfElements (C const& c);
```

### 19.3.2 转换特征

除了提供对主参数类型特定方面的访问之外，特征还可以对类型执行转换，例如添加或移除引用，或`const`和`volatile`限定符。

#### 移除引用

例如，我们可以实现一个`RemoveReferenceT`特征，它将引用类型转换为其底层的对象或函数类型，并保持非引用类型不变：

```cpp
template<typename T>
struct RemoveReferenceT {
    using Type = T;
};

template<typename T>
struct RemoveReferenceT<T&> {
    using Type = T;
};

template<typename T>
struct RemoveReferenceT<T&&> {
    using Type = T;
};
```
