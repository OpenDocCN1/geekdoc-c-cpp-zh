
现在考虑如果本节开头引入的函数模板不返回 `Type` 值，而是返回 `Type::Ambiguous` 值，会发生什么。这里再次引用了模板类型的子类型，因此必须使用 `typename`：

```cpp
template <typename Type>
typename Type::Ambiguous function(Type t)
{
     return t.ambiguous();
}
```

在返回类型的说明中使用 `typename` 将在第 22.1.1 节进一步讨论。

类型名可以嵌入 `typedef` 中。正如常见情况那样，这降低了其他地方出现的声明和定义的复杂性。在下一个示例中，类型 `Iterator` 被定义为模板类型 `Container` 的子类型。现在使用 `Iterator` 时不再需要使用关键字 `typename`：

```cpp
template <typename Container>
class Handler
{
     typedef typename Container::const_iterator Iterator;

     Iterator d_it;
     ...
};
```

## 21.3 为偏离类型特化类模板

`CirQue` 类可用于许多不同的类型。它们的共同特征是，可以直接由该类的 `d_data` 成员指向它们。但这并不总是像看起来那么简单。如果 `d_data` 实际上是 `vector<int>` 呢？对于这类数据类型，常规的 `CirQue` 实现无法使用，因此可以考虑特化。在考虑特化时，也应当考虑继承。通常可以很容易地设计一个类，它派生自以不兼容的数据结构为参数、但在其他方面与原类模板相同的类模板。继承相对于特化的开发优势很明显：继承的类会继承其基类的成员，而特化不继承任何东西。原类模板定义的所有成员都必须由该类的特化重新实现。

这里考虑的特化是真正的特化，因为该特化所使用的数据成员和表示形式与原 `CirQue` 类模板差异很大。因此，原类模板定义的所有成员都必须修改，以适应特化的数据组织方式。

与函数模板特化类似，类模板特化以模板头开始，该模板头可以具有空的模板参数列表，也可以不具有。如果模板参数由特化直接特化，则模板参数列表保持为空（例如，`CirQue` 的模板类型参数 `Data` 针对 `char *` 数据特化）。但是，当针对 `vector<Data>`（即存储任意类型数据的 vector）特化时，模板参数列表可能显示 `typename Data`。这引出了以下原则：

> 模板特化是通过函数或类模板*名称*后面的模板实参列表来识别的，而*不是*通过空的模板参数列表来识别。类模板特化可以具有非空的模板参数列表。如果是这样，则定义的是*类模板部分特化*。

完全特化的类具有以下特征：

- 类模板特化必须提供在泛型类模板定义之后。由于它是特化，编译器必须首先已经看到原始类模板；
- 完全特化的类模板的模板参数列表为空；
- 该类的所有模板参数都被赋予显式类型名，或（对于非类型参数）显式值。这些显式指定在紧接特化模板的类名之后插入的模板参数说明列表（由尖括号包围）中提供；
- 特化类模板的所有成员在原始模板定义使用原始模板参数的地方使用特化类型和值；
- 原始模板的所有成员（可能某些构造函数除外）都应由特化重新定义。如果某个成员在特化中被遗漏，则它不能用于特化类模板的对象；
- 特化可以定义额外的成员（但也许不应这样做，因为这会破坏原始类模板与特化类模板之间的一一对应关系）；
- 特化类模板的成员函数可以由特化类声明，并在其类接口下方实现。如果其实现跟在类接口之后，则它们*不得*以 `template <>` 头开始，而必须直接以成员函数的头开始。

### 21.3.1 类特化示例

下面是一个完全特化的 `CirQue` 类示例，它针对 `vector<int>` 进行了特化。特化类的所有成员都已声明，但只提供了其成员的非平凡实现。该特化类使用传入构造函数的 vector 的副本，并使用其 vector 数据成员实现循环队列：

```cpp
#ifndef INCLUDED_CIRQUEVECTOR_H_
#define INCLUDED_CIRQUEVECTOR_H_

#include <vector>
#include "cirque.h"

template<>
class CirQue<std::vector<int>>
{
    typedef std::vector<int> IntVect;

    IntVect d_data;
    size_t d_size;

    typedef IntVect::iterator iterator;
    iterator d_front;
    iterator d_back;

public:
    typedef int value_type;
    typedef const value_type & const_reference;

    enum Exception
    {
        EMPTY,
        FULL
    };

    CirQue();
    CirQue(IntVect const &iv);
    CirQue(CirQue<IntVect> const &other);

    CirQue &operator=(CirQue<IntVect> const &other);

    int &back();
    int &front();
    bool empty() const;
    bool full() const;
    size_t maxSize() const;
    size_t size() const;
    void pop_front();
    void push_back(int const &object);
    void swap(CirQue<IntVect> &other);

private:
    iterator inc(iterator const &iter);
};

CirQue<std::vector<int>>::CirQue()
:
    d_size(0)
{}
CirQue<std::vector<int>>::CirQue(IntVect const &iv)
:
    d_data(iv),
    d_size(iv.size()),
    d_front(d_data.begin()),
    d_back(d_data.begin())
{}
CirQue<std::vector<int>>::CirQue(CirQue<IntVect> const &other)
:
    d_data(other.d_data),
    d_size(other.d_size),
    d_front(d_data.begin() + (other.d_front - other.d_data.begin())),
    d_back(d_data.begin() + (other.d_back - other.d_data.begin()))
{}
CirQue<std::vector<int>> &CirQue<std::vector<int>>::operator=(
                                CirQue<IntVect> const &rhs)
{
    CirQue<IntVect> tmp(rhs);
    swap(tmp);
}
void CirQue<std::vector<int>>::swap(CirQue<IntVect> &other)
{
    char tmp[sizeof(CirQue<IntVect>)];
    memcpy(tmp, &other, sizeof(CirQue<IntVect>));
    memcpy(&other, this, sizeof(CirQue<IntVect>));
    memcpy(this, tmp, sizeof(CirQue<IntVect>));
}
void CirQue<std::vector<int>>::pop_front()
{
    if (d_size == 0)
        throw EMPTY;

    d_front = inc(d_front);
    --d_size;
}
void CirQue<std::vector<int>>::push_back(int const &object)
{
    if (d_size == d_data.size())
        throw FULL;

    *d_back = object;
    d_back = inc(d_back);
    ++d_size;
}
inline int &CirQue<std::vector<int>>::back()
{
    return d_back == d_data.begin() ? d_data.back() : d_back[-1];
}
inline int &CirQue<std::vector<int>>::front()
{
    return *d_front;
}
CirQue<std::vector<int>>::iterator CirQue<std::vector<int>>::inc(
    CirQue<std::vector<int>>::iterator const &iter)
{
    iterator tmp(iter + 1);
    tmp = tmp == d_data.end() ? d_data.begin() : tmp;
    return tmp;
}

#endif
```

下一个示例展示如何使用特化的 `CirQue` 类：

```cpp
static int iv[] = {1, 2, 3, 4, 5};

int main()
{
    vector<int> vi(iv, iv + 5);
    CirQue<vector<int>> ci(vi);

    cout << ci.size() << ' ' << ci.front() << ' ' << ci.back() << '\n';
    ci.pop_front();
    ci.pop_front();

    CirQue<vector<int>> cp;

    cp = ci;
    cout << cp.size() << ' ' << cp.front() << ' ' << cp.back() << '\n';
    cp.push_back(6);
    cout << cp.size() << ' ' << cp.front() << ' ' << cp.back() << '\n';
}

/*
    Displays:
        5 1 5
        3 3 5
        4 3 6
*/
```

## 21.4 部分特化

上一节介绍了类模板特化。本节将介绍这种特化的一种变体，它在被特化的模板参数的数量和类型两方面都有所不同。
