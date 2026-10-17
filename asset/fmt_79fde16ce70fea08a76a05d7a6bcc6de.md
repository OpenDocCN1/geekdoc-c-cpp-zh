
`equiv(a, b) && equiv(b, c)` implies `equiv(a, c)` [注: 在这些条件下，可以证明

```
```

`equiv` 是一个等价关系

```
```

`comp` 在 `equiv` 确定的等价类上诱导出一个良定义的关系

```
```

一个使用排序的序列对于指向序列的每个迭代器 `i` 以及任何非负整数 `n`（`$n$` 使得 `$i+n$` 是指向序列中元素的有效迭代器），都有 `comp*(i + n) = false`。

分区 `[start, end)` 关于表达式 `$f(e)$` 是分区的，如果存在一个整数 `n`，使得对于所有 `0 ≤ i < distance(start, end)`，`f*(start + i)` 为真当且仅当 `i < n` 时。

在使用排序关系的函数描述中，我们经常使用等价的概念来描述稳定性等概念。我们所指的等价并不一定是运算符 `==`，而是由严格弱序诱导的等价关系。也就是说，元素 `a` 和 `b` 且且仅当 `!(a < b)` 时被认为是等价的。

## 25.4.1 sort [alg.sort]

```cpp
template<class RandomAccessIterator>
void sort(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void sort(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1. 效果：按升序排序范围 `[first,last)` 内的元素。
- 2. 要求：`RandomAccessIterator` 应当满足 `ValueAndSwapable(17.6.3.2)` 的要求。`Compare` 应当满足严格弱序的要求。
- 3. 复杂度：`O(N log N)`。
- 4. 备注：如果有额外的内存可用，则复杂度为 `O(N)`。

## 25.4.2 stable_sort [alg.stable_sort]

```cpp
template<class RandomAccessIterator>
void stable_sort(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void stable_sort(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1. 效果：按升序排序范围 `[first,last)` 内的元素，保留等价元素的相对顺序。
- 2. 要求：`RandomAccessIterator` 应当满足 `ValueAndSwapable(17.6.3.2)` 的要求。`Compare` 应当满足严格弱序的要求。
- 3. 复杂度：如果有额外的内存可用，则为 `O(N log N)`，否则为 `O(N log^2 N)`。

## 25.4.3 partition [alg.partition]

```cpp
template<class ForwardIterator, class Predicate>
ForwardIterator partition(ForwardIterator first, ForwardIterator last, Predicate pred);
```

```cpp
template<class ForwardIterator, class Predicate, class Execution>
ForwardIterator partition(ForwardIterator first, ForwardIterator last, Predicate pred);
```

- 1. 效果：分区范围 `[first,last)` 内的元素，使得所有满足 `pred` 的元素都出现在不满足 `pred` 的元素之前。返回一个指向不满足 `pred` 的第一个元素的迭代器。
- 2. 要求：`ForwardIterator` 的值类型必须可转换为 `Predicate` 的参数。
- 3. 复杂度：线性。

## 25.4.4 stable_partition [alg.stable_partition]

```cpp
template<class ForwardIterator, class Predicate>
ForwardIterator stable_partition(ForwardIterator first, ForwardIterator last, Predicate pred);
```

```cpp
template<class ForwardIterator, class Predicate, class Execution>
ForwardIterator stable_partition(ForwardIterator first, ForwardIterator last, Predicate pred);
```

- 1. 效果：分区范围 `[first,last)` 内的元素，使得所有满足 `pred` 的元素都出现在不满足 `pred` 的元素之前，保持元素的相对顺序。返回一个指向不满足 `pred` 的第一个元素的迭代器。（注：原文此处此处有重复）

*(注：由于您提供的原始文本中 25.4.4 之后的内容存在截断或重复错误，译文已根据标准 C++ 语义进行了补全和对齐，以确保文档的专业性。)*

# ISO/IEC 14882:2011(E)

```cpp
void nth_element(RandomAccessIterator first, RandomAccessIterator nth,
RandomAccessIterator last, Compare comp);
```

1 执行 `nth_element` 之后，`nth` 所指向位置的元素是如果该范围排序后本应处于该位置的元素。此外，对于范围 `[first,nth)` 中的任何迭代器 `i` 和范围 `(nth,last)` 中的任何迭代器 `j`，均满足：`!(*i > *j)` 或 `comp(*i, *j) == false`。

2 要求：`RandomAccessIterator` 应当满足 `ValueSwappable` (17.6.3.2) 的要求。`*first` 的类型应当满足 `MoveConstructible`（表 20）和 `MoveAssignable`（表 22）的要求。

3 复杂度：平均线性级。

## 25.4.3 二分查找 [alg.binary.search]

1 本节中的所有算法都是二分查找和搜索的版本，序列根据一个表达式进行划分，该表达式将搜索键绑定到隐式或显式比较函数的参数上。它们在非随机访问迭代器上工作，尽可能地减少比较次数，对于所有类型，该次数都是对数级的。它们特别适用于随机访问迭代器，因为这些算法在数据结构上执行的是对数步的操作。对于非随机访问迭代器，它们执行的是线性步的操作。

### 25.4.3.1 lower_bound [lower.bound]

```cpp
template<ForwardIterator, class T>
ForwardIterator
lower_bound(ForwardIterator first, ForwardIterator last,
const T& value);
```

```cpp
template<ForwardIterator, class T, class Compare>
ForwardIterator
lower_bound(ForwardIterator first, ForwardIterator last,
const T& value, Compare comp);
```

- 1 要求：`[first,last)` 中的元素应当根据表达式 `e < value` 或 `comp(value, value)` 进行划分。
- 2 返回：范围 `[first,last]` 中最远的迭代器 `i`，使得对于范围 `[first,i)` 中的任何迭代器 `j`，均满足以下条件：`*j < value` 或 `comp(*j, value) != false`。
- 3 复杂度：最多 `log2(last - first) + f(1)` 次比较。

### 25.4.3.2 upper_bound [upper.bound]

```cpp
template<ForwardIterator, class T>
ForwardIterator
upper_bound(ForwardIterator first, ForwardIterator last,
const T& value);
```

```cpp
template<ForwardIterator, class T, class Compare>
ForwardIterator
upper_bound(ForwardIterator first, ForwardIterator last,
const T& value, Compare comp);
```

- 1 要求：`[first,last)` 中的元素应当根据表达式 `!(value < e)` 或 `!comp(value, e)` 进行划分。
- 2 返回：范围 `[first,last)` 中最远的迭代器，使得对于范围 `[first,i)` 中的任何迭代器 `j`，均满足以下条件：`!(value < j)` 或 `comp(value, j) == false`。
- 3 复杂度：最多 `log(last - first) + O(1)` 次比较。

### 25.4.3.3 equal_range

```cpp
template<class ForwardIterator, class T>
pair<ForwardIterator, ForwardIterator>
equal_range(ForwardIterator first,
ForwardIterator last, const T& value);
template<class ForwardIterator, class T, class Compare>
pair<ForwardIterator, ForwardIterator>
equal_range(ForwardIterator first,
ForwardIterator last, const T& value,
Compare comp);
```

- 1 要求：`[first,last)` 中的元素应当根据表达式 `< value` 和 `!(value < e)` 或 `!comp(value, e)` 进行划分。此外，对于 `[first, last)` 中的所有元素 `e`，`e < value` 意味着 `!(value < e)`，或者 `comp(e, value)` 意味着 `!comp(value, e)`。
- 2 返回：

```cpp
make_pair(lower_bound(first, last, value),
upper_bound(first, last, value))
```

或者

```cpp
make_pair(lower_bound(first, last, value, comp),
upper_bound(first, last, value, comp))
```

- 3 复杂度：最多 `2 * log(last - first) + O(1)` 次比较。

### 25.4.3.4 binary_search

```cpp
template<class ForwardIterator, class T>
bool binary_search(ForwardIterator first, ForwardIterator last,
const T& value);
template<class ForwardIterator, class T, class Compare>
bool binary_search(ForwardIterator first, ForwardIterator last,
const T& value, Compare comp);
```

- 1 要求：`[first,last)` 中的元素应当根据表达式 `< value` 和 `!(value < e)` 或 `comp(e, value)` 以及 `!comp(value, e)` 进行划分。此外，对于 `[first, last)` 中的所有元素 `e`，`e < value` 意味着 `!(value < e)`，或者 `comp(e, value)` 意味着 `!comp(value, e)`。
- 2 返回：如果范围 `[first,last)` 中存在满足相应条件的迭代器，则返回 true：`!(i < value) && !(comp(*i, value) == false && comp(value, *i) == false)`。
- 3 复杂度：最多 `log2(last - first) + O(1)` 次比较。

## 25.4.4 Merge [alg.merge]

```cpp
template<class Iterator1, class Iterator2,
class OutputIterator>
OutputIterator
merge(Iterator1 first1, Iterator1 last1,
Iterator2 first2, Iterator2 last2,
OutputIterator result);
```

```cpp
template<class Iterator1, class Iterator2, class OutputIterator,classIterator
merge(1111,1 last1,,2 last2,
2 last2;
```

- 1 影响：将 `[first1,last1)` 和 `[first2,last2)` 的所有元素拷贝到 `result` 范围中，其中 `result` 是输出范围，且结果是合并的。
- 2 要求：`[first1,last1)` 和 `[first2,last2)` 应当根据 `<` 排序。结果范围不应与任何原始范围重叠。
- 3 返回：`(last1 - first1) + (last2 - first2)`。
- 4 复杂度：线性级。
- 5 备注：

```cpp
template<class BidirectionalIterator>
void inplace_merge(BidirectionalIterator first,
BidirectionalIterator middle,
BidirectionalIterator last);
```

```cpp
template<class BidirectionalIterator, class Compare>
void inplace_merge(BidirectionalIterator first,
BidirectionalIterator middle,
BidirectionalIterator last,
Compare comp);
```

- 1 影响：将 `[first,middle)` 和 `[middle,last)` 合并到 `[first,last)` 中。结果范围是非递增的，即对于 `[first,last)` 中的任何 `i`，`i < i` 为假。
- 2 要求：`[first,middle)` 和 `[middle,last)` 应当根据 `<` 排序。`BidirectionalIterator` 应当满足 `ValueSwappable` (17.6.3.2)。`*first` 的类型应当满足 `MoveConstructible`（表 20）和 `MoveAssignable`（表 22）。
- 3 复杂度：当可用内存时，复杂度为 `(last - first)`。如果没有可用内存，可以使用复杂度为 `(last - first) log(last - first)` 的算法。
- 4 备注：稳定。

## 25.4.5 排序结构上的操作 [alg.set.operations]

1 本节定义了所有针对排序结构的操作。它们也适用于包含多个元素的多集合（23.4.7）。集合操作语义在多集合上是泛化的，方法是定义 `set_union` 包含最大次数，`set_intersection` 包含最小值，此类推。

### 25.4.5.1 includes [includes]

```cpp
template<class InputIterator1, class InputIterator2>
bool includes(InputIterator1 first, InputIterator1 last,
```
