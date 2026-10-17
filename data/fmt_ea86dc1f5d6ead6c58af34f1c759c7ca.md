
# 24 迭代器库

## 24.1 通用

1 本节描述了 C++ 程序可能用于对容器进行迭代的组件（第 23 节、流 `27.7` 和流缓冲区 `27.6`）。

2 后子节描述了迭代器要求以及迭代器原语、预定义迭代器和流迭代器的组件，如表 104 所示。

表 104 — 迭代器库摘要

| 子节 | 头文件(s) | |
|---|---|---|
| 24.2 | 要求 | |
| 24.4 | 迭代器原语 | `<iterator>` |
| 24.5 | 预定义迭代器 | |
| 24.6 | 流迭代器 | |

## 24.2 迭代器要求

### 24.2.1 一般地

1 迭代器是指针的泛化，允许 C++ 程序以统一的方式处理不同的数据结构（容器）。为了能够构建在不同类型数据上正确且高效运行的模板算法，库不仅形式化了迭代器的接口，还形式化了其语义和复杂性假设。所有迭代器支持表达式 `*`，结果为 `a = o`，其中 `o` 是某种类型的值的迭代器的类型。所有输出迭代器支持表达式 `i = o`，其中 `o` 是某种类型的值的可写入 `i` 的特定迭代器类型。所有表达式 `(*i)==j` 定义良好的迭代器都支持表达式 `i!=j`。对于每个定义了相等性的迭代器类型 `i`，都有对应 `i` 的比较运算符。

2 由于迭代器是指针的抽象，它们的语义是 C++ 中大多数指针语义的泛化。这确保了每个接收迭代器的函数模板都能像普通指针一样工作。本国际标准根据在它们上定义的操作将迭代器分为五类：输入迭代器、前向迭代器、双向迭代器和随机访问迭代器，如表 105 所示。

表 105 — 迭代器类别之间的关系

| 随机访问 | 双向 | 前向 | 输入 |
|---|---|---|---|
| | | | 输出 |

3 前向迭代器满足输入迭代器的所有要求，并在指定输入迭代器时均可以使用；双向迭代器也满足前向迭代器的所有要求，并在指定前向迭代器时均可以使用；随机访问迭代器也满足双向迭代器的所有要求，并在指定双向迭代器时均可以使用。

4 进一步满足输出迭代器要求的迭代器称为可变迭代器。不可变迭代器称为常量迭代器。

5 进一步满足以下要求的：对于整数值 `n` 和可解引用迭代器值 `a` 以及 `(a + n)`，`*(a + n)` 等于 `*address(*a + n)` 的迭代器被称为连续迭代器。[注：例如，类型为连续迭代器，使用 `reverse_iterator<int>`。对于具有可解引用 `a` 的有效范围 `[a,b]`，指针表示的相应范围 `*address(*a),*address(*a + (b - a))` 可能不可解引用。——结束]

指向数组的普通指针保证有一个通过数组最后一个元素的指针值，因此对于任何其他序列，都有一个指向序列最后一个元素的迭代器。这些值被称为*尾部之后*（past-end）。对于序列定义的迭代器 `i` 的值是连续的。通过了*尾部之后*值的迭代器是可解引用的。[示例：在声明未初始化的指针 `x (with int x)` 后，`x` 必须赋值为一个有效指针。——结束] 大多数赋值的结果对于值是未定义的；迭代器持有一个值，对于默认构造（DefaultConstructible）要求，使用值初始化的迭代器作为源或拷贝操作的非单一值的赋值是未定义的。[注：`j` 被称为从迭代器 `i` *可达的*（reachable），如果存在有限的 `+i` 应用序列使得 `i` 变为 `j`。如果 `j` 可达，`i` 指向同一序列的元素。

库的大多数算法对指针操作，要求迭代器具有可使用的接口。指向迭代器的指针范围定义了容器的开始和结束。范围 `(i,j)` 是空范围；通常情况下，范围 `{i,j}` 指数据结构中从 `i` 开始但不包含元素 `j` 的元素。仅当 `j` 从 `i` 可达时，范围 `{i,j}` 才是有效的。如果未定义，库中函数的应用结果是无效的。

### 24.2.3 头文件 `<iterator>` 概要

```cpp
namespace std {
// 原生类型：
template<class Iterator> struct iterator_traits;
template<class T> struct iterator_traits<T*>;

template<class Category, class T, class Distance = ptrdiff_t,
    class Pointer = T*, class Reference = T&> struct iterator;
```

```cpp
struct input_iterator_tag {};
struct output_iterator_tag {};
struct forward_iterator_tag : public input_iterator_tag {};
struct bidirectional_iterator_tag : public forward_iterator_tag {};
struct random_access_iterator_tag : public bidirectional_iterator_tag {};
```

### 24.2.4 迭代器操作

```cpp
template <class Iterator, class Distance>
void advance(Iterator i, Distance n);
template <class Iterator>
typename iterator_traits<Iterator>::difference_type
distance(Iterator first, Iterator last);
template <class ForwardIterator>
ForwardIterator next(ForwardIterator x);
typename std::traits<ForwardIterator>::difference_type n = 1);
template <class BidirectionalIterator>
BidirectionalIterator prev(BidirectionalIterator x);
typename std::traits<BidirectionalIterator>::difference_type n = 1);
```

### 24.2.4 输出迭代器 [output.iterators]

如果类或指针类型 `X` 满足迭代器要求 `24.2.2` 且表 108 中的表达式有效并具有指示的语义，则该类型 满足输出迭代器的要求。

表 108 — 输出要求（除迭代器要求外）

| 表达式 | 返回类型 | 操作语义 | 断言/备注前置/后置条件 |
| :--- | :--- | :--- | :--- |
| *r = o | 结果不使用 | | 备注：执行此操作后，r 不要求可解引用，后置：r 是可递增的。 |
| ++r | X& | | 备注：执行此操作后，r 不要求可解引用，后置：r == k++r。 |
| r++ | 可转换为 const X& | { X tmp = r; ++ return tmp; } | 备注：执行此操作后，r 不要求可解引用，后置：r 是可递增的。 |
| *r++ = o | 结果不使用 | | 备注：执行此操作后，r 不要求可解引用，后置：r 是可递增的。 |

[注：运算符 `*` 的唯一用法是在赋值语句的左侧。通过迭代器的相同值进行赋值仅发生一次。处理输出迭代器的算法不应尝试多次通过同一个迭代器。它们应该是单次通过迭代器。等等和不等关系可能未定义。输出迭代器的算法可以通过通过 `ostream_iterator` 类以及插入迭代器指针与 `istreams` 作为目标来配合使用。 — 结束注]

### 24.2.5 前向迭代器 [forward.iterators]

如果满足以下条件，则类或指针类型 `X` 满足前向迭代器的要求：

- `X` 满足输入迭代器的要求 `24.2.3`，
- `X` 满足默认构造要求 `17.6.3.1`，
- 如果 `X` 是可变迭代器，则引用指向 `T`；如果 `X` 是常数迭代器，则引用指向 `const T`，
- 表 109 中的表达式有效并具有指示的语义，
- 类型为 `X` 的对象提供多次通过保证（下文所述）。

前向迭代器的 `==` 域是相同序列的迭代器域。然而，值初始化的迭代器可以进行比较，并且应当与相同类型的其他值初始化迭代器相等。[注：值初始化迭代器的行为表现为它们指向相同序列的末尾之后 — 结束注 ]

如果满足以下条件，类型为 `X` 的两个可解引用迭代器 `a` 和 `b` 提供了多次通过保证：

- `a == b` 意味着 `a == ++b`
- `X` 是指针或类型 `X (void)++X(a)` 等价于表达式 `*`。

[注：`a == b` 意味着 `a == b` 的要求（这在输入和输出迭代器中是不成立的）以及移除可变迭代器赋值次数的限制（这适用于输出迭代器），允许在前向迭代器上使用多次通过的单向算法。 — 结束注 ]

表 109 — 前向迭代器要求（除输入要求外）

| 表达式 | 返回类型 | 操作语义 | 断言/备注前/后置条件 |
| :--- | :--- | :--- | :--- |
| r++ | 可转换为 const X& | { X tmp = r; ++r; return tmp; } | |
| *r++ | | | |

如果 `a` 和 `b` 相等，则 `a` 和 `b` 均可解引用，或者两者均不可解引用。

如果 `a` 和 `b` 均可解引用，那么 `a == b` 当且且仅当 `*a` 和 `*b` 绑定到同一个对象。

### 24.2.6 双向迭代器 [bidirectional.iterators]

如果类或指针类型 `X` 在满足前向迭代器要求的基础上，还满足表 110 所示的表达式，则其满足双向迭代器的要求。

表 110 — 双向迭代器要求（除前向迭代器要求外）

| 表达式 | 返回类型 | 操作语义 | 断言/备注前/后置条件 |
| :--- | :--- | :--- | :--- |
| --r | X& | | 前置：存在 x 使得 r == ++x；后置：r 是可解引用的。r == s。 |
| r-- | 可转换为 const X& | { X tmp = r; --r; return tmp; } | --r == s 意味着 r == s。 |
| *r-- | 引用 | | [注：双向迭代器允许算法向后以及向前移动迭代器。 — 结束注 ]

### 24.2.7 随机访问迭代器 [random.access.iterators]

如果类或指针类型 `X` 在满足双向迭代器要求的基础上，满足表 111 所示的有效表达式，则其满足随机访问迭代器的要求。

表 111 — 随机访问迭代器要求（除双向迭代器要求外）

| 表达式 | 返回类型 | 操作语义 | 断言/备注前/后置条件 |
| :--- | :--- | :--- | :--- |
| r += n | X& | { difference_type m = n; if (m > 0) while (m--) ++r; else while (m++) --r; return r; } | |
| a + n | X | { X tmp = a + n; } | a + n == n + a. |
| n + a | X | | |
| r -- n | X& | { X tmp = r; r -= n; } | |
| a - n | X | { X tmp = a - n; } | a - a b == a + (b - a). |
| a[n] | 引用 | *(a + n) | |
| a < b | 可转换为 bool | b - a > 0 | 一个全序关系。 |
| a > b | 可转换为 bool | b < a | 与 < 符号的反全序关系。 |
| a >= b | 可转换为 bool | !(a < b) | |
| a <= b | 可转换为 bool | !(a > b) | |

### 24.2.3 定义迭代器：

```cpp
template <class Iterator1, class Iterator2>
bool operator==(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator<(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator>(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator<=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator>=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator!==(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
auto operator-(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y) -> decltype(y.base() - x.base());
template <class Iterator>
reverse_iterator<Iterator>
operator+(typename reverse_iterator<Iterator>::difference_type n,
const reverse_iterator<Iterator&> x);
```

```cpp
template <class Iterator>
reverse_iterator<Iterator> make_reverse_iterator(Iterator i);
```

```cpp
template <class Container> back_insert_iterator;
template <class Container>
back_insert_iterator(Container& x);
```

```cpp
template <class Container> front_insert_iterator;
template <class Container>
front_insert_iterator(Container& x);
```

```cpp
template <class Container> insert_iterator;
template <class Container, typename Container::iterator Iterator>
insert_iterator(Container& x, Iterator i);
```
