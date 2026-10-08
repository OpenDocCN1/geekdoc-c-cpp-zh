
```cpp
template<class InputIterator1, class InputIterator2, class OutputIterator>
OutputIterator set_union(InputIterator1 first, InputIterator1 last,
    InputIterator2 first, InputIterator2 last,
    OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2, class Compare>
OutputIterator set_union(InputIterator1 first, InputIterator1 last,
    InputIterator2 first, InputIterator2 last,
    OutputIterator result, Compare comp);
```

```cpp
template<class InputIterator1, class InputIterator2, class OutputIterator>
OutputIterator set_intersection(
    InputIterator1 first, InputIterator1 last,
    InputIterator2 first, InputIterator2 last,
    OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2, class OutputIterator, class Compare>
OutputIterator set_intersection(
    InputIterator1 first, InputIterator1 last,
    InputIterator2 first, InputIterator2 last,
    OutputIterator result, Compare comp);
```

```cpp
template<class InputIterator1, class InputIterator2, class OutputIterator>
OutputIterator set_difference(
    InputIterator1 first, InputIterator1 last,
    InputIterator2 first, InputIterator2 last,
    OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2, class OutputIterator, class Compare>
OutputIterator set_difference(
    InputIterator1 first, InputIterator1 last,
    InputIterator2 first, InputIterator2 last);
```

# ISO/IEC N4296

```cpp
template<class Iterator1, class Iterator2, class OutputIterator>
OutputIterator set_symmetric_difference(
InputIterator1 first, InputIterator1 last1,
InputIterator2 first, InputIterator2 last2,
OutputIterator result);
template<class InputIterator1, class InputIterator2, class OutputIterator,
class Compare>
OutputIterator set_symmetric_difference(
InputIterator1 first, InputIterator1 last1,
InputIterator2 first, InputIterator2 last2,
OutputIterator result, Compare comp);
```

// 25.4.6.堆操作：

```cpp
template<class RandomAccessIterator>
void push_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare>
void push_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

```cpp
template<class RandomAccessIterator>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

```cpp
template<class RandomAccessIterator>
void make_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare>
void make_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

```cpp
template<class RandomAccessIterator>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

```cpp
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
template<class RandomAccessIterator>
RandomAccessIterator is_heap_until(RandomAccessIterator first, RandomAccessIterator last);
template<class RandomAccessIterator, class Compare>
RandomAccessIterator is_heap_until(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

// 25.4.7.最小与最大值：

```cpp
template<class T>
const T min(const T& a, const T& b);
template<class T, class Compare>
const T min(const T& a, const T& b, Compare comp);
template<class T>
const T min(initializer_list<T> l);
```

```cpp
template<class T, class Compare>
const T min(initializer_list<T> l, Compare comp);
```

```cpp
template<class T>
const T max(const T& a, const T& b);
template<class T, class Compare>
const T max(const T& a, const T& b, Compare comp);
template<class T>
const T max(initializer_list<T> l);
```

```cpp
template<class T, class Compare>
const T max(initializer_list<T> l, Compare comp);
```

```cpp
template<class T>
const T& min(initializer_list<T> l);
template<class T, class Compare>
const T& min(initializer_list<T> l, Compare comp);
```

```cpp
template<class T>
const T& max(initializer_list<T> l);
template<class T, class Compare>
const T& max(initializer_list<T> l, Compare comp);
```

# ISO/IEC N4296

在 `binary_pred(*first1, *first2)` 构造上下文中转换为 bool（第 4 节）中正常工作。`BinaryPredicate` 总是将第一个迭代器的 `value_type` 作为其第一个参数，也就是说，当 T 为其签名时，在 `binary_pred(*first, value)` 构造上下文中转换为 bool（第 4 节）中正常工作。`binary_pred` 不应通过解引用迭代器应用任何非常数函数。

- 10. [注] 另有规定的情况下，将函数对象作为参数的算法允许自由拷贝这些函数对象。为了对象的等标识性，程序员应考虑使用指向非拷贝对象的封装类，例如 `reference_wrapper<T>` (20.9.4) 或某些等价物。 — 注结束

- 11 当算法描述给出诸如 *first == value* 的表达式作为条件时，该表达式在布尔上下文中应求值为真或假。

- 12 在算法描述中，运算符 `+` 和 `-` 用于某些迭代器类别，而这些类别并不一定定义了这些运算符。在这种情况下，`a+n` 的语义等于：

```cpp
Type tmp =
advance(tmp, n);
return tmp;
```

且 `b-b` 等于：

```cpp
return distance(a, b);
```

## 25.2 非修改序列操作

### 25.2.1 All_of

template<class Iterator, class Predicate>

bool all_of(InputIterator first, InputIterator last, Predicate pred);

- 1 返回：如果 `[first, last)` 为空，或者范围 `[first, last)` 中的每一个迭代器的 `pred(*i)` 都为真，则返回 true，否则返回 false。

- 2 复杂度：最多 `last — first` 次谓词调用。

### 25.2.2 Any_of

template<class Iterator, class Predicate>

bool any_of(InputIterator first, InputIterator last, Predicate pred);

- 1 返回：如果 `[first, last)` 为空或者范围 `[first, last)` 中没有迭代器使得 `pred(*i)` 为真，则返回 false（此处原文逻辑可能有误，通常为真时返回true），否则返回 false。

- 2 复杂度：最多 `last — first` 次谓词调用。

### 25.2.3 None_of

template<class Iterator, class Predicate>

bool none_of(InputIterator first, InputIterator last, Predicate pred);

- 1 返回：如果 `[first, last)` 为空，或者范围 `[first, last)` 中的每一个迭代器的 `pred(*i)` 都为假，则返回 true，否则返回 false。

- 2 复杂度：最多 `last — first` 次谓词调用。

### 25.2.4 For_each

template<class Iterator, class Function>

Function for_each(InputIterator first, InputIterator last, Function f);

要求：`Function` 应当满足 `MoveConstructible` 的要求（表 20）。[注：`Function` 不满足 `CopyConstructible` 的要求（表 21）。 — 注结束

影响：将 `f` 赋值给范围 `[first, last)` 中从 `first` 到 `last - 1` 的每一个迭代器的解引用结果。[注：如果 `first` 满足修改迭代器的要求，`f` 可以通过解引用迭代器调用函数。 — 注结束

返回：`std::move(f)`。

复杂度：恰好 `last - first` 次。

备注：如果 `f` 返回了结果，则该结果被忽略。

### 25.2.5 Find

```cpp
template<class InputIterator, class T>
InputIterator find(InputIterator first, InputIterator last, const T& value);

template<class InputIterator, class Predicate>
InputIterator find_if(InputIterator first, InputIterator last, Predicate pred);

template<class InputIterator, class Predicate>
InputIterator find_if_not(InputIterator first, InputIterator last, Predicate pred);
```

返回：范围 `[first, last)` 中第一个满足对应条件的迭代器：*i = value(*i) != false, pred(*i) == false*。如果未找到此类迭代器，则返回 `last`。

复杂度：最多 `– first` 次对应谓词的调用。

### 25.2.6 Find end

```cpp
template<class ForwardIterator, class ForwardIterator2>
ForwardIterator1 find_end(ForwardIterator1 first, ForwardIterator1 last1, ForwardIterator2 first2, ForwardIterator2 last2);
```

```cpp
template<class ForwardIterator1, class ForwardIterator2, class BinaryPredicate>
ForwardIterator1 find_end(ForwardIterator1 first, ForwardIterator1 last1, ForwardIterator2 first2, ForwardIterator2 last2, BinaryPredicate pred);
```

影响：在序列中寻找等值的子序列。

返回：范围 `[first1, last1] – (last2 – first2)` 中的迭代器，使得对于非负的 `n <= (last2 – first2)`，满足以下条件：*(i + n) == *(first2 + n), pred(i + n), *(first2 + n) != false*。如果 `[first2,last2)` 为空或未找到此类迭代器，则返回 `last`。

复杂度：最多 `(last2 – first2) * (last1 – first1 + 1)` 次对应谓词的调用。

### 25.2.7 Find first

```cpp
template<class InputIterator, class ForwardIterator>
InputIterator find_first_of(InputIterator first1, InputIterator last1, ForwardIterator first2, ForwardIterator last2);
```

template<class Iterator, class ForwardIterator, class BinaryPredicate>
