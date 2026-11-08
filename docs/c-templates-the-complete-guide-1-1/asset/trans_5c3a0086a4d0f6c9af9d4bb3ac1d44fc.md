
在 C++ 语境中，泛型编程有时被定义为使用模板进行编程（而面向对象编程则被认为是使用虚函数进行编程）。从这个意义上说，几乎任何对 C++ 模板的使用都可以被视为泛型编程的一个实例。然而，实践者通常认为泛型编程还有一个额外的基本要素：必须在一个框架中设计模板，以便支持大量有用的组合。

迄今为止，该领域最重要的贡献是标准模板库（STL），它后来被改编并纳入 C++ 标准库。STL 是一个框架，为若干种用于对象集合的线性数据结构——称为容器——提供了许多有用的操作，称为算法。算法和容器都是模板。然而，关键在于算法不是容器的成员函数。相反，算法以泛型方式编写，因此可被任何容器（以及元素的线性集合）使用。为此，STL 的设计者定义了一个抽象迭代器概念，可为任何类型的线性集合提供。本质上，容器操作中与具体集合相关的方面被分离出来，放到了迭代器的功能中。

因此，我们可以实现诸如计算序列中最大值这样的操作，而无需知道值在该序列中如何存储的细节。

```cpp
template<typename Iterator>
Iterator max_element(Iterator begin,  // reference to start
                     // of collection
                     Iterator end)    // reference to end of
                                      // collection
{
    // use only iterator operations to traverse
    // all elements
    // of the collection to find the element with the maximum value
    // and return its position as iterator
}
```

每个线性容器并没有提供所有有用的操作（例如 `max_element()`），而是只提供了一种迭代器类型，用于遍历其包含的值序列，以及用于创建此类迭代器的各种函数。

```cpp
namespace std {
    template<class T, ...>
    class vector {
    public:
        using const_iterator = ...;  // implementation-specific
        ...
        const_iterator begin() const; // iterator for
                                       // start of collection
        const_iterator end() const;   // iterator for
                                       // end of collection
    };

    template<class T, ...>
    class list {
    public:
        using const_iterator = ...;  // implementation-specific
        ...
        const_iterator begin() const; // iterator for
                                       // start of collection
        const_iterator end() const;   // iterator for
                                       // end of collection
    };
}
```

现在，我们可以通过调用泛型 `max_element()` 操作，并将集合的开头和结尾作为参数传入，来找到任何集合中的最大值（此处省略了对空集合的特殊处理）：

```cpp
int main()
{
    std::vector<int> c;
    std::list<int> l;

    max_element(c.begin(), c.end());
    max_element(l.begin(), l.end());
}
```

`poly/printmax.cpp`

```cpp
#include <vector>
#include <list>
#include <algorithm>
#include "MyClass.hpp"

...
{
    // compute position of maximum value
    auto pos = std::max_element(col.begin(), col.end());

    // print value of maximum element of col (if any)
    if (pos != col.end()) {
        std::cout << *pos << '\n';
    }
    else {
        std::cout << "empty" << '\n';
    }
}

int main()
{
    std::vector<int> c1;
    std::list<int> c2;

    ...

    printMax(c1);
    printMax(c2);
}
```

通过根据迭代器对其操作进行参数化，STL 避免了操作定义数量的爆炸式增长。我们不必为每个容器实现每种操作，而是只实现一次算法，使其可用于每个容器。因此，泛型算法对迭代器而言是通用适配的；迭代器由容器提供，并由算法使用。这之所以可行，是因为迭代器具有某种接口，该接口由容器提供并由算法使用。这个接口通常称为概念（concept），它表示模板为了融入该框架而必须满足的一组约束。此外，这个概念常常就是传统的操作和数据结构。

你会记得，我们在前面第 377 页的 18.4 节中描述过概念（concepts）语言特性，并在附录 E 中做了更详细的说明；事实上，该语言特性恰好对应这里的这一概念。实际上，此语境中的术语 concept 最初由 STL 的设计者引入，以将其工作形式化。此后不久，人们便开始尝试在模板中显式表达概念。

即将推出的语言特性将帮助我们指定并复核对迭代器的要求（由于存在不同的迭代器类别，例如前向迭代器和双向迭代器，现在可以结合使用多种操作；见第 744 页的 E.1.2 节）。然而，在当今的 C++ 中，概念隐含在示例库（以及一般而言的标准 C++ 库）的规范中。不过，一些特性和技术（例如 static_assert 和 SFINAE）确实允许进行一定程度的自动检查。

原则上，类似 STL 的方法这类功能可以用动态多态来实现。然而在实践中，它的用途有限，因为与虚函数调用机制相比，迭代器概念过于轻量。增加一个基于虚函数的接口层，很可能会使我们的操作慢一个数量级（甚至更多）。

泛型编程之所以实用，正是因为它依赖静态多态，而静态多态在编译时解析接口。另一方面，接口必须在编译时解析这一要求，也呼唤新的设计原则，这些原则在许多方面不同于面向对象设计原则。其中许多最重要的泛型设计原则将在本书余下部分描述。此外，附录 E 通过描述对概念这一观念的直接语言支持，更深入地探讨了作为开发范式的泛型编程。

## 18.7 后记

容器类型是将模板引入 C++ 编程语言的主要动机。在模板出现之前，多态层次结构是容器的一种流行实现方法。一个著名的例子是美国国家卫生研究院的类库（National Institute of Health’s Class Library，NIHCL），它在很大程度上移植了 Smalltalk 的容器类层次结构（见图 18.5）。

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_262_0.png)

图 18.5：NIHCL 的类层次结构

与 C++ 标准库非常相似，NIHCL 支持丰富多样的容器以及迭代器。然而，其实现遵循 Smalltalk 风格的动态多态：迭代器使用通用的基类 Collection 来操作不同类型的集合：

```cpp
Bag c1;
Set c2;
...
Iterator i1(c1);
Iterator i2(c2);
...
```

不幸的是，这种方法在运行时间和内存使用方面的代价都很高。运行时间通常比使用 C++ 标准库的等效代码差几个数量级，因为最终有更多操作需要虚调用（而在 C++ 标准库中，许多操作是内联的，虚函数只出现在迭代器和容器接口中）。此外，与 Smalltalk 不同，由于接口是有限的，内置类型必须包装在大量使用多态的类中（这类包装器由 NIHCL 提供），这反过来又可能导致存储需求急剧增加。

即使在当今的模板时代，许多项目在处理多态的方法上仍会做出重大选择。显然，在很多情况下，动态多态是正确的选择。异构容器就是一个例子。然而，同样地，许多编程任务可以通过模板自然且高效地解决，同构容器就是这方面的一个例子。

静态多态很适合核心基础计算结构。相反，需要选择公共基类型意味着动态多态库通常必须做出特定于领域的抉择。因此，C++ 标准库中的 STL 部分从未包含多态容器，而是包含一组丰富的、使用静态多态的容器和迭代器（如第 1.6 节或第 9.5 节所示），这并不奇怪。

中型和大型 C++ 程序通常需要处理本章讨论的两种多态。在某些情况下，甚至可能需要将它们非常紧密地结合起来。在许多情况下，根据我们的讨论，最佳设计选择是明确的，但花些时间思考长期的潜在演进总是值得的。

- 1. *多态*（Polymorphism）字面上指具有多种形式或形态的状态（源自希腊语 *polymorph*）。
- 2. 严格来说，宏也可以被视为静态多态的一种早期形式。然而，这里不考虑它们，因为它们与其他语言机制大多是正交的。
- 3. 也就是说，多态基类子对象的编码包含一些通常隐藏的数据，这些数据使这种运行时分派成为可能。
- 4. 关于多态的一般性详细讨论，另见本书第 6.6.2 节。
- 5. 例如，GCC 7 提供了选项 `-fconcepts`。

