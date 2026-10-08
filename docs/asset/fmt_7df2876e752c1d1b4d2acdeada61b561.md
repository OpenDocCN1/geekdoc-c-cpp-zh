
```cpp
template <class C> auto rbegin(C& c) -> decltype(c.rbegin());
template <class C> auto rbegin(const C& c) -> decltype(c.rbegin());
```

返回: `c.rbegin()`;

```cpp
template <class C> auto rend(C& c) -> decltype(c.rend());
template <class C> auto rend(const C& c) -> decltype(c.rend());
```

返回: `c.rend()`;

```cpp
template <class T, size_t N> reverse_iterator<T*> rbegin(array<T, N>);
```

返回: `reverse_iterator<T*>(array + N)`;

```cpp
template <class T, size_t N> reverse_iterator<T*> rend(array<T, N>);
```

返回: `reverse_iterator<T*>(array)`;

```cpp
template <class E> reverse_iterator<const E> rbegin(initializer_list<E> il);
```

返回: `reverse_iterator<const E*>(il.begin())`;

```cpp
template <class E> reverse_iterator<const E> rend(initializer_list<E> il);
```

返回: `reverse_iterator<const E*>(il.begin())`;

```cpp
template <class C> auto crend(const C& c) -> decltype(std::rend(c));
```

返回: `std::crend(c)`;

## 24.8 容器访问

除了可以通过包含 `<iterator>` 头文件可用外，24.8节中的函数模板在包含以下任何头文件时均可用：`<array>, <deque>, <forward_list>, <list>, <map>, <regex>, <set>, <string>, <unordered_map>, <unordered_set> 和 <vector>`。

```cpp
template <class C> constexpr auto size(const C& c) -> decltype(c.size());
```

返回: `c.size()`;

```cpp
template <class T, size_t N> constexpr auto size(const T (&array)[N]) noexcept;
```

返回: `N`.

```cpp
template <class C> constexpr auto empty(const C& c) -> decltype(c.empty());
```

返回: `c.empty()`;

```cpp
template <class T, size_t N> constexpr bool empty(T (&array)[N]) noexcept;
```

返回: `false`.

```cpp
template <class E> constexpr bool empty(initializer_list<E> il) noexcept;
```

返回: `il.size() == 0`.

```cpp
template <class C> constexpr auto data(C& c) -> decltype(c.data());
```

```cpp
template <class C> constexpr auto data(const C& c) -> decltype(c.data());
```

返回: `c.data()`.

```cpp
template <class T, size_t N> constexpr T* data(T (&array)[N]) noexcept;
```

返回: `array`.

```cpp
template <class E> constexpr E* data(initializer_list<E> il) noexcept;
```

返回: `il.begin()`.

# 25 算法库

### 25.1 通用

本节描述了 C++ 程序可能用于对容器（第 23节）和其他序列执行算术操作的组件。以下描述了 ISO 库中的非修改序列操作、修改性序列操作、排序及相关操作以及算法，总结在表 12 中。

### 表 12 — 算法库摘要

| 节 | 头文件(s) |
| :--- | :--- |
| 25.2 非修改性序列操作 | `<algorithm>` |
| 25.3 修改性序列操作 | `<algorithm>` |
| 25.4 排序及相关操作 | `<cstdlib>` |
| 25.5 算法 | `<iterator>` |

`<algorithm>` 概览

```cpp
#include <initializer_list>
namespace std {
// 25.2 非修改性序列操作:
template <class InputIterator, class Predicate>
bool all_of(InputIterator first, InputIterator last, Predicate pred);
template <class InputIterator, class Predicate>
bool any_of(InputIterator first, InputIterator last, Predicate pred);
template <class InputIterator, class Predicate>
bool none_of(InputIterator first, InputIterator last, Predicate pred);

template <class InputIterator, class Function>
void for_each(InputIterator first, InputIterator last, Function f);
template <class InputIterator, class T>
InputIterator find(InputIterator first, InputIterator last, const T& value);
template <class InputIterator, class Predicate>
InputIterator find_if(InputIterator first, InputIterator last, Predicate pred);
template <class InputIterator, class Predicate>
InputIterator find_not(InputIterator first, InputIterator last, Predicate pred);
template <class ForwardIterator1, class ForwardIterator2>
ForwardIterator1 find_end(ForwardIterator1 first, ForwardIterator1 last);
template <class ForwardIterator1, class ForwardIterator2, class BinaryPredicate>
ForwardIterator1 find_end(ForwardIterator1 first, ForwardIterator1 last, ForwardIterator2 first, ForwardIterator2 last, BinaryPredicate pred);

template <class InputIterator, class ForwardIterator>
InputIterator find_first_of(InputIterator first, InputIterator last, ForwardIterator first2, ForwardIterator last2);
template <class InputIterator, class ForwardIterator, class BinaryPredicate>
InputIterator find_first_of(InputIterator first, InputIterator last, ForwardIterator first2, ForwardIterator last2, BinaryPredicate pred);

template <class ForwardIterator>
ForwardIterator adjacent_find(ForwardIterator first, ForwardIterator last);
template <class ForwardIterator, class BinaryPredicate>
ForwardIterator adjacent_find(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);

template <class InputIterator, class T>
typename iterator_traits<InputIterator>::difference_type count(InputIterator first, InputIterator last, const T& value);
template <class InputIterator, class Predicate>
typename iterator_traits<InputIterator>::difference_type count_if(InputIterator first, InputIterator last, Predicate pred);

template <class InputIterator1, class InputIterator2>
pair<InputIterator1, InputIterator2> mismatch(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2);

template <class InputIterator1, class InputIterator2, class BinaryPredicate>
pair<InputIterator1, InputIterator2> mismatch(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, BinaryPredicate pred);

template <class InputIterator1, class InputIterator2>
pair<InputIterator1, InputIterator2> mismatch(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2);

template <class InputIterator1, class InputIterator2, class BinaryPredicate>
pair<InputIterator1, InputIterator2> mismatch(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, BinaryPredicate pred);

template <class InputIterator1, class InputIterator2>
bool equal(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2);
template <class InputIterator1, class InputIterator2, class BinaryPredicate>
equal(InputIterator1 first1, InputIterator1 last1, BinaryPredicate pred);
template <class InputIterator, class InputIterator2>
equal(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last);

template <class InputIterator, class InputIterator2,
class BinaryPredicate>
equal(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last,
BinaryPredicate pred);
```

# ISO/IEC N4296

```cpp
OutputIterator result);
template<class InputIterator, class Size, class OutputIterator>
OutputIterator copy_n(InputIterator first, Size n,
OutputIterator result);
template<class InputIterator, class OutputIterator, class Predicate>
OutputIterator copy_if(InputIterator first, InputIterator last,
OutputIterator result, Predicate pred);
template<class BidirectionalIterator, class Bidirectional2>
Bidirectional2 copy_backwards(
BidirectionalIterator first, BidirectionalIterator last,
Bidirectional2 result);
```

```cpp
// 5.3.2. move;
template<class InputIterator, class OutputIterator>
OutputIterator move(InputIterator first, InputIterator last,
OutputIterator result);
template<class BidirectionalIterator, class Bidirectional2>
Bidirectional2 move_back(
BidirectionalIterator first, BidirectionalIterator last,
Bidirectional2 result);
```

```cpp
// 5.3.3. swap;
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 swap_ranges(ForwardIterator1 first1,
ForwardIterator1 last1, ForwardIterator2 first2);
template<class ForwardIterator, class ForwardIterator2>
void iter_swap(ForwardIterator a, ForwardIterator2 b);
```

```cpp
template<class InputIterator, class UnaryOperation>
OutputIterator transform(InputIterator first, InputIterator last,
OutputIterator result, UnaryOperation op);
template<class InputIterator1, class InputIterator2, class OutputIterator>
OutputIterator transform(InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, OutputIterator result,
BinaryOperation op);
```
