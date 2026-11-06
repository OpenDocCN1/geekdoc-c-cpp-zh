
```cpp
        }
    inline Lines::Proxy::operator std::string const &() const
    {
        return d_str;
    }
```

成员 `Lines::operator[]` 也可以内联实现：它仅返回一个 `Proxy` 对象，该对象用与索引 `idx` 关联的字符串初始化。

既然 `Proxy` 类已经开发完成，就可以在程序中使用它。下面是一个将 `Proxy` 对象用作左值或右值的示例。从表面上看，`Lines` 对象的行为不会与使用原始实现的 `Lines` 对象有所不同，但通过向 `Proxy` 的成员添加一条用于标识的 `cout` 语句，可以表明 `operator[]` 在用作左值或右值时行为不同：

```cpp
int main()
{
    ifstream in("lines.cc");
    Lines lines(in);

    string s = lines[0];        // rvalue use
    lines[0] = s;               // lvalue use
    cout << lines[0] << '\n';   // rvalue use
    lines[0] = "hello world";   // lvalue use
    cout << lines[0] << '\n';   // rvalue use
}
```

## 23.8 实现一个‘reverse_iterator’

第 21.13.1 节讨论了迭代器和反向迭代器的构造。在该节中，迭代器被构造为某个类的内部类，而该类派生自一个字符串指针 vector。这个嵌套迭代器类的对象负责解引用存储在 vector 中的指针。这使我们能够对 vector 元素所指向的*字符串*进行排序，而不是对*指针*排序。

这样做的一个缺点是，实现迭代器的类与派生类紧密绑定，因为迭代器类是实现为嵌套类的。如果我们希望为任何派生自存储指针的容器类的类提供一个处理指针解引用的迭代器，那该怎么办？

本节讨论先前（嵌套类）方法的一种变体。这里迭代器类被定义为类模板，不仅将容器元素所指向的数据类型参数化，还将容器自身的迭代器类型参数化。我们再次集中开发一个*RandomIterator*，因为它是最复杂的迭代器类型。

我们的类命名为 `RandomPtrIterator`，表示它是一个作用于指针值的随机迭代器。该模板定义了三个模板类型参数：

-   第一个参数指定派生类类型（`Class`）。和之前一样，`RandomPtrIterator` 的构造函数是私有的。因此需要友元声明来允许客户端类构造 `RandomPtrIterators`。但是，不能使用友元类 `Class`，因为模板参数类型不能用于友元类声明。不过这是一个小问题，因为并非客户端类的每个成员都需要构造迭代器。事实上，只有 `Class` 的 `begin` 和 `end` 成员必须构造迭代器。使用模板的第一个参数，可以为客户端的 `begin` 和 `end` 成员指定友元声明。
-   第二个模板参数将容器的迭代器类型参数化（`BaseIterator`）；
-   第三个模板参数指示指针所指向的数据类型（`Type`）。

`RandomPtrIterator` 有一个私有数据成员，一个 BaseIterator。下面是类的接口和构造函数的实现：

```cpp
#include <iterator>

template <typename Class, typename BaseIterator, typename Type>
class RandomPtrIterator:
    public std::iterator<std::random_access_iterator_tag, Type>
{
    friend RandomPtrIterator<Class, BaseIterator, Type> Class::begin();
    friend RandomPtrIterator<Class, BaseIterator, Type> Class::end();

    BaseIterator d_current;

    RandomPtrIterator(BaseIterator const &current);

public:
    bool operator!=(RandomPtrIterator const &other) const;
    int operator-(RandomPtrIterator const &rhs) const;
    RandomPtrIterator operator+(int step) const;
    Type &operator*() const;
    bool operator<(RandomPtrIterator const &other) const;
    RandomPtrIterator operator--();
    RandomPtrIterator operator--(int);
    RandomPtrIterator operator++();
    RandomPtrIterator operator++(int);
    bool operator==(RandomPtrIterator const &other) const;
    RandomPtrIterator operator-(int step) const;
    RandomPtrIterator operator-=(int step);
    RandomPtrIterator &operator+=(int step);
    Type *operator->() const;
};

template <typename Class, typename BaseIterator, typename Type>
RandomPtrIterator<Class, BaseIterator, Type>::RandomPtrIterator(
                                BaseIterator const &current)
    :
    d_current(current)
{}
```

查看它的友元声明，我们可以看到，类 Class 的成员 begin 和 end 被授予访问 RandomPtrIterator 私有构造函数的权限，这两个成员返回针对类型 Class、BaseIterator 和 Type 的 RandomPtrIterator 对象。这正是我们想要的。Class 的 begin 和 end 成员被声明为绑定友元。

`RandomPtrIterator` 的所有其余成员都是公有的。由于 `RandomPtrIterator` 只是第 21.13.1 节中开发的嵌套类迭代器的泛化，重新实现所需的成员函数很容易，只需将 iterator 改为 `RandomPtrIterator`，并将 `std::string` 改为 `Type`。例如，在类 iterator 中定义的 operator< 如下：

```cpp
inline bool StringPtr::iterator::operator<(iterator const &other) const
{
    return d_current < other.d_current;
}
```

现在实现为：

```cpp
template <typename Class, typename BaseIterator, typename Type>
bool RandomPtrIterator<Class, BaseIterator, Type>::operator<(
            RandomPtrIterator const &other) const
{
    return **d_current < **other.d_current;
}
```

一些额外示例：在类 iterator 中定义的 operator* 如下：

```cpp
inline std::string &StringPtr::iterator::operator*() const
{
    return **d_current;
}
```

现在实现为：

```cpp
template <typename Class, typename BaseIterator, typename Type>
Type &RandomPtrIterator<Class, BaseIterator, Type>::operator*() const
{
    return **d_current;
}
```

前缀和后缀递增运算符现在实现为：

```cpp
template <typename Class, typename BaseIterator, typename Type>
RandomPtrIterator<Class, BaseIterator, Type> &
RandomPtrIterator<Class, BaseIterator, Type>::operator++()
{
    ++d_current;
    return *this;
}
template <typename Class, typename BaseIterator, typename Type>
RandomPtrIterator<Class, BaseIterator, Type>
RandomPtrIterator<Class, BaseIterator, Type>::operator++(int)
{
    return RandomPtrIterator(d_current++);
}
```

其余成员可以相应地实现，其实际实现留给读者作为练习（当然，也可以从 cplusplus.yo.zip 归档中获得）。

重新实现第 21.13.1 节中开发的类 StringPtr 也不困难。除了包含定义类模板 RandomPtrIterator 的头文件之外，它只需要一处修改。其 iterator typedef 现在必须与一个 RandomPtrIterator 关联。下面是完整的类接口和该类的内联成员定义：

```cpp
#ifndef INCLUDED_STRINGPTR_H_
#define INCLUDED_STRINGPTR_H_

#include <vector>
#include <string>
#include "iterator.h"

class StringPtr: public std::vector<std::string *>
{
    public:
        typedef RandomPtrIterator
        <
            StringPtr,
            std::vector<std::string *>::iterator,
            std::string
        >
        iterator;

        typedef std::reverse_iterator<iterator> reverse_iterator;

        iterator begin();
        iterator end();
        reverse_iterator rbegin();
        reverse_iterator rend();
};

inline StringPtr::iterator StringPtr::begin()
{
    return iterator(this->std::vector<std::string *>::begin());
}
inline StringPtr::iterator StringPtr::end()
{
    return iterator(this->std::vector<std::string *>::end());
}
inline StringPtr::reverse_iterator StringPtr::rbegin()
{
    return reverse_iterator(end());
}
inline StringPtr::reverse_iterator StringPtr::rend()
{
    return reverse_iterator(begin());
}
#endif
```

将 StringPtr 修改后的头文件包含到第 21.13.2 节给出的程序中，会得到一个行为与先前版本完全相同的程序。在这种情况下，StringPtr::begin 和 StringPtr::end 返回由模板定义构造的迭代器对象。

## 23.9 使用 'bisonc++' 和 'flex'

下面讨论的示例深入探讨使用解析器和扫描器生成器生成 C++ 源代码的特殊之处。一旦程序的输入超过一定复杂程度，使用扫描器和解析器生成器来生成执行实际输入识别的代码就变得很有吸引力。

当前示例假设读者知道如何使用扫描器生成器 flex 和解析器生成器 bison。bison 和 flex 在其他地方都有很好的文档。bison 和 flex 的原始前身称为 yacc 和 lex，在多本书中有所描述，例如 O'Reilly 的书 'lex & yacc'^3。

扫描器和解析器生成器也可以作为自由软件获得。bison 和 flex 通常都是软件发行版的一部分，或者可以从 ftp://prep.ai.mit.edu/pub/non-gnu 获得。当指定 %option c++ 时，Flex 会创建一个 C++ 类。

对于解析器生成器，可以使用程序 bison。在 90 年代早期，Alain Coetmeur（coetmeur@icdc.fr^4）创建了一个 C++ 变体（bison++），用于生成解析器类。尽管 bison++ 程序生成的代码可以在 C++ 程序中使用，但它也表现出许多更像是 C 的特征
