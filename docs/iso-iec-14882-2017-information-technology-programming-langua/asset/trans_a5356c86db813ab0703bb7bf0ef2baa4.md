

# ISO/IEC 14882:2017(E)

iterator_traits<Iterator>::difference_type
iterator_traits<Iterator>::value_type
iterator_traits<Iterator>::iterator_category
应分别定义为迭代器的差类型（difference type）、值类型（value type）和迭代器类别。此外，
iterator_traits<Iterator>::reference
iterator_traits<Iterator>::pointer
应当定义为迭代器的引用和指针类型，即对于迭代器对象 `a`分别定义为相同类型的 `a*` 和 `a->`。在迭代器的输出中，
iterator_traits<Iterator>::difference_type
iterator_traits<Iterator>::value_type
iterator_traits<Iterator>::reference
iterator_traits<Iterator>::pointer
可以定义为 void。

+ 2 如果 Iterator 拥有 (17.2) 成员类型 `difference_type`、`value_type`、`pointer`、`reference` 和 `iterator_category`，则 `iterator_traits<Iterator>` 应当具有以下公开访问成员：
* `using difference_type = typename Iterator::difference_type;`
* `using value_type = typename Iterator::value_type;`
* `using pointer = typename Iterator::pointer;`
* `using reference = typename Iterator::reference;`
* `using iterator_category = typename Iterator::iterator_category;`
如果是随机访问指针：
* `using iterator_category = random_access_iterator_tag;`
否则，`iterator_traits<Iterator>` 不应具有上述任何名称的成员。

+ 3 它针对指针进行了特化如下：
namespace std {
```cpp
template<class> struct iterator_traits<T*> {
    using difference_type = ptrdiff_t;
    using value_type = T;
    using pointer = T;
    using reference = T&;
    using iterator_category = random_access_iterator_tag;
};
```

+ 并且指向常量的指针的特化如下：
namespace std {
```cpp
template<class> struct iterator_traits<const T*> {
    using difference_type = ptrdiff_t;
    using value_type = T;
    using pointer = const T;
    using reference = const T&;
    using iterator_category = random_access_iterator_tag;
};
```

+ 4 示例：为了实现一个通用的反转函数，C++ 程序可以执行以下操作：
```cpp
template<class BidirectionalIterator>
void reverse(BidirectionalIterator first, BidirectionalIterator last) {
    typename iterator_traits<BidirectionalIterator>::difference_type n =
    distance(first, last);
    ...
```

```cpp
--;
while(n > 0) {
  typename iterator_traits<BidirectionalIterator>::value_type
  tmp = *first;
  *first++ = --last;
  last = tmp;
  n -= 2;
}
```

--- end example[]

## 27.4.2 标准迭代器标签 [std.iterator.tags]

+ 1 模板特化通常希望查明其迭代器最具体的类别，以便函数能够在编译时选择最高效的算法。为了方便这一点，库引入了类别标签，用作算法选择的编译时标签。我们使用了 `input_iterator_tag`、`output_iterator_tag`、`forward_iterator_tag`、`bidirectional_iterator_tag` 和 `random_access_iterator_tag`。对于每一个迭代器类型，`iterator_traits<Iterator>::category` 被定义为描述迭代器行为的最具体的类别标签。

```cpp
namespace std {
  struct input_iterator_tag {};
  struct output_iterator_tag {};
  struct forward_iterator_tag : public input_iterator_tag {};
  struct bidirectional_iterator_tag : public forward_iterator_tag {};
  struct random_access_iterator_tag : public bidirectional_iterator_tag {};
}
```

+ 2 示例：对于一个程序定义的 `BinaryTreeIterator`，可以通过特化 `iterator_traits` 模板将其包含在双向类别中：
```cpp
template<class T> struct iterator_traits<BinaryTreeIterator<T>> {
  using iterator_category = bidirectional_iterator_tag;
  using difference_type = ptrdiff_t;
  using value_type = T;
  using pointer = T*;
  using reference = T&;
};
```

--- example[]

+ 3 示例：如果 `evolve(O)` 对于双向迭代器是良定义的，但对于随机访问迭代器可以更高效地实现，那么实现如下：
```cpp
template<class BidirectionalIterator>
inline void
evolve(BidirectionalIterator first, BidirectionalIterator last) {
  evolve(first, last);
  typename iterator_traits<BidirectionalIterator>::iterator_category();
}
template<class BidirectionalIterator>
void evolve(BidirectionalIterator first, BidirectionalIterator last,
  random_iterator_tag) {
  // 更通用、效率较低的算法

template <class RandomAccessIterator>
void evolve(RandomAccessIterator first, RandomAccessIterator last,
    random_access_iterator_tag) {
  // 更高效、但泛化的算法
}
```
// end example

## 27.4.3 迭代器操作

+ 1. 由于只有随机访问迭代器提供 `+` 和 `-` 运算符，库提供了两个函数模板和 `distance`。这些模板对于随机访问迭代器使用 `+` 和 `-`因此是常数时间的；对于前向和双向迭代器则使用 `++` 的线性时间实现。

```cpp
template <class InputIterator, class Distance>
const void advance(InputIterator i, Distance n);
```

+ 2. 对于双向和随机访问迭代器，`n` 要求为负值。

+ 3. 影响：递增（如果 `n` 为负值则递减）迭代器 `n` 次。
```cpp
template <class InputIterator>
distance(InputIterator first, Input last);
```

+ 4. 影响：如果 `InputIterator` 满足随机访问要求，返回从 `first` 到 `last` 的次数。

+ 5. 要求：如果 `InputIterator` 满足随机访问要求，则 `last` 必须从 `first` 可达；否则。
```cpp
template <class BidirectionalIterator>
typename iterator_traits<BidirectionalIterator>::difference_type
distance(BidirectionalIterator first);
```

+ 6. 影响：`advance(x, n)`。

```cpp
template <class BidirectionalIterator>
typename iterator_traits<BidirectionalIterator>::difference_type
distance(BidirectionalIterator x, int);
```

+ 7. 影响：`advance(x, n)`。

## 27.5 迭代器适配

+ 1 `reverse_iterator` 是一种从序列末尾到起始的迭代器适配。`reverse_iterator` 与相应的迭代器 `i` 之间的基本关系通过 `*reverse_iterator(i) == i` 建立。

```cpp
namespace std {
template <class Iterator>
class reverse_iterator {
public:
  using iterator_type = Iterator;
  using iterator_category = typename iterator_traits<Iterator>::iterator_category;
  using value_type = typename iterator_traits<Iterator>::value_type;
  using difference_type = typename iterator_traits<Iterator>::difference_type;
  using pointer = typename iterator_traits<Iterator>::pointer;
  using reference = typename iterator_traits<Iterator>::reference;

  constexpr reverse_iterator();
  constexpr reverse_iterator(Iterator x);
  template <class U> constexpr reverse_iterator(const reverse_iterator<U>& u);
  template <class U> constexpr reverse_iterator& operator=(const reverse_iterator<U>& u);

  constexpr base() const;
  constexpr reference() const;
  constexpr pointer operator() const;

  constexpr reverse_iterator operator++();
  constexpr reverse_iterator operator++(int);
  constexpr reverse_iterator operator--();
  constexpr reverse_iterator operator--(int);

  constexpr reverse_iterator operator+(difference_type n) const;
  constexpr reverse_iterator operator+=(difference_type n) const;
  constexpr reverse_iterator operator-(difference_type n) const;
  constexpr reverse_iterator operator-=(difference_type n) const;
  constexpr reference operator[](difference_type n) const;

protected:
  Iterator current;
};

template <class Iterator1, class Iterator2>
constexpr bool operator==(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
constexpr bool operator!=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
constexpr bool operator<=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
constexpr bool operator>=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
constexpr bool operator<=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
constexpr bool operator>=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
constexpr bool operator<=(const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
constexpr auto operator-(
const reverse_iterator<Iterator1>& x,
const reverse_iterator<Iterator2>& y);
```
