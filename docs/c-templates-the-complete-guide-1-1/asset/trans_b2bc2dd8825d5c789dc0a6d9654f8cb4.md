

```cpp
std::forward_iterator_tag;
```

这样一来，`std::iterator_traits<>` 就会假定 `InputIterator<T>`，我们现在可以为受这两种迭代器类别约束的模板进行重载。

## E.4 概念提示

尽管 C++ 概念已经被研究了很多年，而且实验性实现以某种形式出现已有十多年，但关于它们的广泛经验才刚刚开始积累。我们希望本书的后续版本能够提供更多关于如何设计受约束模板库的实用指导。不过，与此同时，我们给出三点观察。

### E.4.1 测试概念

概念是作为有效常量表达式的布尔谓词。因此，给定一个概念 C 以及一些符合该概念的模型类型 T1、T2、……，我们可以静态断言这一观察结果：

*单击此处查看代码图像*

```cpp
static_assert(C<T1, T2, ...>, "model failure");
```

因此，在设计概念时，建议也设计一些以这种方式测试它们的类型。这包括那些会推动概念所涵盖边界的类型，用来回答如下问题：

- 接口和/或算法是否需要复制和/或移动所建模类型的对象？
- 哪些转换是可接受的？需要哪些转换？
- 模板所假定的基本操作集合是否唯一？例如，某个类型的运算符可以是 `++` 或 `--` 吗？

在这里，原型（archetypes）的概念（见第 653 页第 18.3 节）也可能有用。

### E.4.2 概念粒度

随着概念成为 C++ 语言的一部分，人们自然希望构建“概念库”，就像这些特性一出现我们就会构建类库和模板库一样。与其他库一样，人们自然也希望通过各种方式偏爱自己的概念。我们简要讨论了迭代器类别的例子，不难设想，我们可以与这些概念并列构建“范围类别”，也许还可以在这些类别之上构建“序列概念”，如此等等。

另一方面，我们可能倾向于将所有这些概念都构建在“基本语法”概念之上。例如，我们可以设想：

*单击此处查看代码图像*

```cpp
template<typename T>
concept Addable =
  requires (T a, T b) {
    a + b;
  };
```

然而，并不推荐这样做，因为这是一个没有其他语义内涵的概念，而且互不相同的类型也会满足它。例如，当 `T` 和 `U` 都是 `std::string` 时，或者当一个类型是指针而另一个是整型时，它都会被满足；当然，算术类型也会满足它。然而在这三种情况下，Addable 这一概念的含义有根本不同（分别是拼接、迭代器位移以及算术加法的各种变体）。因此，引入这样的概念，往往会导致库中出现相当有趣、且很可能触发奇怪歧义的情况。

相反，概念最好被设计为对问题域中真实语义概念的建模。以严谨的方式这样做，必然会改善我们库的总体设计，因为它会让呈现给客户的接口内在且清晰地体现这一点。

### E.4.3 二进制兼容性

有经验的 C++ 程序员知道，当某些实体（尤其是函数和成员函数）被编译为低级机器码时，会为它们关联一个名称，该名称将实体的声明名称与类型和作用域组合在一起。这个名称通常称为实体的修饰名（mangled name），目标代码链接器用它来解析对该实体的引用（例如，来自其他目标文件的引用）。例如，按如下方式定义的函数的修饰名是

*单击此处查看代码图像*

```cpp
template<typename T>
concept HasPlus = requires(T a, T b) {
    a + b;
};

template<typename T>
int f(T a) requires HasPlus<T> {
    std::cout << "T\n";
}

void g()
{
    int a, b;
    f(a);
    f(b);
}
```

[单击此处查看代码图像](#)

```cpp
#include <iostream>

template<typename T>
concept HasPlus = requires(T a, T b) {
    a * b;
};

template<typename T>
int f(T a) requires HasPlus<T> {
    std::cout << "T\n";
}

template <int I>
void g() {
    f(I);
}
```

该程序必须输出

```
T
T
```

这意味着 f() 的两个定义必须经过不同的名称修饰。

1. 连续迭代器是 C++17 引入的随机访问迭代器的细化。没有为它们添加 `std::contiguous_iterator` 标签，因为如果更改该标签，依赖 `std::ranges::contiguous_range` 的现有算法将更难扩展。
2. 正在提议标准化的规范比这更强大一些。它将容器分解为若干组“领域概念”（包括正则表达式的要点，以及被发送到其中一个概念、或显然是一个概念的直接子集的分析）。
3. 已知 GCC 7.1 中概念的实验性实现在这方面存在缺陷。

# 代码片段

```cpp
template<typename T> requires LessThanComparable<T>
T max(T a, T b) {
    return a > b ? a : b;
}
```

```cpp
requires LessThanComparable<T>
```

```cpp
class Person
{
private:
    std::string name;
public:
    template <typename T>
    explicit Person(T&& str)
        : name(std::forward<T>(str)) {
            std::cout << "EMPL constructor for " << name << "\n";
        }
};
```

```cpp
template<typename Seq>
    requires Sequence<Seq>
class Sequence
{
public:
    using value_type = typename Seq::value_type;
    Sequence(Seq value) : value_(value) {}

    bool contains(const value_type& val) const {
        return std::find(begin(), end(), val);
    }
};
```

```cpp
template<typename T>
    requires Integral<T> ||
             FloatingPoint<T>
T power(T b, T p);
```

```cpp
template<typename T, typename U>
requires SomeConcept<T, U>
auto f(T x, U y) -> decltype(x+y);
```

```cpp
template<LessThanComparable T>
T max(T a, T b) {
    return b < a ? a : b;
}
```

```cpp
template<typename Seq>
requires EqualityComparable<Seq::value_type>
typename Seq::iterator find(Seq const& seq,
                            typename Seq::value_type const& val)
{
    return std::find(seq.begin(), seq.end(), val);
}
```

```cpp
template<typename T> concept LessThanComparable = ...;
```

```cpp
template<typename T>
concept LessThanComparable = requires(T x, T y) {
    { x < y } -> Bool;
};
```

```cpp
{ x < y } -> bool;
```

```cpp
template<typename T>
concept Swappable = requires(T x, T y) {
  swap(x, y);
};
```

```cpp
...
typename IteratorFor<Seq>;
...
```

```cpp
template<typename Seq>
concept Sequence = requires(Seq seq) {
    typename Seq::iterator;
    requires Iterator<decltype(seq.iterator)>;
    { seq.begin() } -> Seq::iterator;
};
```

```c
int main()
{
    printf(1);        // selects template #1
    printf("1%s");    // selects template #2
}
```

```cpp
template<typename T>
    concept ForwardIterator = ...;
```

```cpp
template<typename T>
concept BidirectionalIterator =
  ForwardIterator<T> &&
  requires (T it) {
    { --it } -> T&;
  };
```

```cpp
template<ForwardIterator T, typename D>
void advance(T& it, D n)
{
    assert(n >= 0);
    for (; n != 0; --n) { ++it; }
}

template<BidirectionalIterator T, typename D>
void advance(T& it, D n)
{
    if (n > 0) {
        for (; n != 0; --n) { ++it; }
    } else if (n < 0) {
        for (; n != 0; ++n) { --it; }
    }
}
```

```cpp
template<typename T>
concept ForwardIterator =
    std::input_iterator<T> &&
    requires {
        typename std::iterator_traits<T>::iterator_category;
        std::is_base_of_v<std::forward_iterator_tag,
                          typename std::iterator_traits<T>::iterator_category>;
    };
```

