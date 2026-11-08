

## 第19章 实现 Traits

模板使我们能够为各种类型参数化类和函数。人们可能会倾向于引入尽可能多的模板参数，以便对类型或算法的每个方面都进行定制。通过这种方式，我们的“模板化”组件可以被实例化，以满足客户端代码的确切需求。然而，从实际角度看，为了实现最大限度的参数化而引入数十个模板参数通常并不可取。在客户端代码中必须指定所有相应的参数过于繁琐，而且每增加一个模板参数都会使组件与其客户端之间的契约变得更加复杂。

幸运的是，事实证明，我们想引入的大多数额外参数都有合理的默认值。在某些情况下，这些额外参数完全由少数几个主要参数决定，而且我们将看到，每个额外参数都可以完全省略。另一些参数可以赋予依赖于主要参数的默认值，并能满足大多数情况的需求，但这些默认值偶尔必须被覆盖（用于特殊应用）。还有一些参数与主要参数无关：从某种意义上说，它们本身就是主要参数，只不过它们的默认值属于明智默认值的范畴。

Traits（或 traits 模板）是一种 C++ 编程装置，它们极大地简化了在设计工业级模板时出现的那类额外参数的管理。在本章中，我们将展示它们有用的一些场景，并演示各种技术，使你能为自己的用途编写健壮且无缺陷的代码。

这里介绍的大多数 traits 在 C++ 标准库中都以某种形式存在。然而，为了清晰起见，我们通常会给出简化的实现，省略工业级实现（如标准库中的实现）中的某些细节。出于这个原因，我们也使用自己的命名方案，不过该方案很容易映射到标准 traits。

### 19.1 示例：累加一个序列

计算一个值序列的总和是一项相当常见的计算任务。然而，这个看似简单的问题为我们提供了一个极好的示例，用来介绍策略类和 traits 可以在哪些不同层面上提供帮助。

#### 19.1.1 固定 Traits

首先假设我们要计算的总和值存储在一个数组中，并给定一个指向第一个待累加元素的指针，以及一个指向最后一个待累加元素之后位置的指针。由于本书是关于模板的，我们希望编写一个适用于多种类型的模板。下面这个写法现在看起来可能很直接：

```cpp
#ifndef ACCUM_HPP
#define ACCUM_HPP

template<typename T>
T accum (T const* beg, T const* end)
{
    T total{};
    while (beg != end) {
        total += *beg;
        ++beg;
    }
    return total;
}

#endif // ACCUM_HPP
```

这里唯一稍微微妙的地方在于，如何创建正确类型的零值来开始求和。我们使用带有`{}`记号的空初始化；这在第5.2节（第68页）中介绍过。它意味着标量对象类型会被初始化：double 类型初始化为零，指针类型初始化为空指针，布尔值初始化为 false。

为了引出我们的第一个 traits 模板，请看下面使用`accum()`的代码。

```cpp
#include <iostream>
#include <numeric>

int main()
{
    // create array of 5 integer values
    int num[] = { 1, 2, 3, 4, 5 };

    // print average value
    std::cout << "the average value of the integer values is "
              << accum(num, num+5) / 5
              << '\n';

    // create array of character values
    char name[] = "template";

    int length = sizeof(name)-1;

    // (try to) print average character value
    std::cout << "the average value of the characters in \""
              << name << "\" is "
              << accum(name, name+length) / length
              << '\n';
}
```

程序的前半部分使用`accum()`对五个整数值求和。

```text
the average value of the integer values is 3
```

然后通过简单地将结果总和除以数组中的值个数，即可得到整数平均值。

程序的后半部分尝试对单词`template`中的所有字符做同样的处理（前提是实际字符集中从`a`到`z`的字符构成一个连续序列；这在 ASCII 中成立，但在 EBCDIC 中不成立）。结果按理应当介于`a`的值和`z`的值之间。在当今大多数平台上，这些值由 ASCII 码决定：`a`编码为97，`z`编码为122。因此，我们可能期望结果在97到122之间。然而，在我们的平台上，程序的输出如下：

```text
the average value of the integer values is 3
the average value of the characters in "template" is -5
```

这并非异常结果，但它是可以避免的。

处理额外参数的一种替代方法是在每个调用`accum()`的类型与相应的累加类型之间建立关联。事实上，我们的关联可以被编码为模板的特化：

```cpp
template<typename T>
struct AccumulationTraits;

template<>
struct AccumulationTraits<char> {
    using AccT = int;
};

template<>
struct AccumulationTraits<short> {
    using AccT = int;
};

template<>
struct AccumulationTraits<int> {
    using AccT = long;
};

template<>
struct AccumulationTraits<unsigned int> {
    using AccT = unsigned long;
};

template<>
struct AccumulationTraits<float> {
    using AccT = double;
};
```

模板`AccumulationTraits`被称为 traits 模板，因为它保存了其参数类型的一个 trait。（一般来说，可能不止一个 trait，也不止一个参数。）我们选择不提供这个模板的通用定义，因为在不知道类型是什么的情况下，没有一种很好的方法来选择一个好的关联类型。不过，也可以认为`T`本身通常是这样一个类型的好候选（尽管在我们前面的例子中不是）。

考虑到这一点，我们可以将`accum()`模板重写如下：

```cpp
#ifndef ACCUM_HPP
#define ACCUM_HPP

#include "accumtraits1.hpp"

template<typename T>
auto accum (T const* beg, T const* end)
{
    // result type is trait of the element type
    using AccT = typename AccumulationTraits<T>::AccT;

    AccT total{};  // assume this actually creates a zero value
    while (beg != end) {
        total += *beg;
        ++beg;
    }
    return total;
}
#endif // ACCUM_HPP
```

这样，示例程序的输出就变成了我们所期望的结果：

```text
the average value of the integer values is 3
the average value of the characters in "template" is 109
```

总的来说，考虑到我们添加了一种非常有用的机制来自定义算法，这些改动并不算很大。此外，如果出现新的类型要与`accum()`一起使用，只需为`AccumulationTraits`模板声明一个额外的显式特化，就可以为其关联一个合适的`AccT`。请注意，这可以针对任何类型完成：基本类型、在其他库中声明的类型，等等。

#### 19.1.2 值 Traits

到目前为止，我们已经看到 traits 表示与给定“主”类型相关的额外类型信息。在本节中，我们将展示这些额外信息不必仅限于类型。常量和其他类别的值也可以与类型相关联。

我们最初的`accum()`模板使用返回值的默认构造函数来初始化结果值，希望它是一个类似零的值：

```cpp
AccT total{};  // assume this actually creates a zero value

return total;
```

显然，这并不能保证产生一个适合开始累加循环的良好值。类型`AccT`甚至可能没有默认构造函数。

同样，traits 可以前来解围。对于我们的示例，可以向`AccumulationTraits`添加一个新的值 trait：

*traits/accumcreate.cpp*

```cpp
template<typename T>
struct AccumulationTraits;

template<>
struct AccumulationTraits<char> {
    using AccT = int;
    static AccT const zero = 0;
};

template<>
struct AccumulationTraits<short> {
    using AccT = int;
    static AccT const zero = 0;
};

template<>
struct AccumulationTraits<int> {
    using AccT = long;
    static AccT const zero = 0;
};
```

在这种情况下，我们的新 trait 提供了一个`zero`元素，它是一个可以在编译时求值的常量。于是，`accum()`变成下面这样：

*traits/accumaccu.cpp*

```cpp
#ifndef ACCUM_HPP
#define ACCUM_HPP
```

