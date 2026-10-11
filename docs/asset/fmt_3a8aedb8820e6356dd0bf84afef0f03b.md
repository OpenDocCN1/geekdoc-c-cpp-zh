
- 1. 要求：结果范围不应与任何原始范围重叠。
- 2. 复制：将范围 `[first1, last1)` 中不存在于 `[first2, last2)` 中的元素，以及范围 `[first2, last2)` 中不存在于 `[first1, last1)` 中的元素复制到 `result` 范围。所构建范围内的元素是排序的。
- 3. 返回：所构建范围的末尾。
- 4. 复杂度：最多 `2 * (last1 - first1) + (last2 - first2)` 次比较。
- 5. 奖励：如果 `[first1, last1)` 包含 `m` 个相互等等的元素，且 `[first2, last2)` 包含 `n` 个与它们等等的元素，如果 `m > n`，则从 `[first1, last1)` 复制 `m-n` 个元素；如果 `m < n`，则从 `[first2, last2)` 复制 `n-m` 个元素。

# 27.8 堆操作

> `[operations]`

- 1 堆是两个随机访问迭代器 `(a, b)` 之间元素的一种特定组织形式使得：
    (1.1) 对于 `N = b - a`，所有 `0 ≤ i < N`，`comp(a[i], a[j])` 均为假。
    (1.2) *元素*可以通过 `pop_heap()` 移除，或通过 `push_heap()` 在 `O(log N)` 时间内添加。
- 2 这些属性使得堆作为优先级队列非常有用。
- 3 `make_heap()` 将范围转换为堆，`sort_heap()` 将堆转换为有序范围。

## 27.8.7.1 pop_heap

> `[pop.heap]`

```cpp
template<class RandomAccessIterator>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1. 要求：范围 `[first, last)` 应该是一个有效的堆。`*first` 应满足构造（表 23）和移动赋值（表 25）。
- 2. 效果：将位置 `last - 1` 处的值放入结果堆 `[first, last]` 中。
- 3. 复杂度：最多 `log(last - first)` 次比较。

## 27.8.7.2 pop_heap

> `[pop.heap]`

```cpp
template<class RandomAccessIterator>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1. 要求：范围 `[first, last)` 应该是一个有效的非空堆。`RandomIterator` 应满足 `ValueSwappable(20.5.3.2)`。`*first` 的类型应满足移动构造（表 23）和移动赋值（表 25）的要求。
- 2. 效果：交换堆中第一个值与位置 `last - 1` 处的值，并使 `[first, last)` 变为堆。
- 3. 复杂度：`log(last - first)`。

## 27.7.3 make_heap

```cpp
template<class RandomAccessIterator>
void make_heap(RandomAccessIterator first);
```

```cpp
template<class RandomAccessIterator, class Compare>
void make_heap(RandomAccessIterator first, Compare comp);
```

- 1. 要求：`*first` 的类型应满足移动构造（表 23）和移动赋值（表 25）的要求。
- 2. 效果：从范围 `[first, last)` 创建一个堆。
- 3. 复杂度：线性。

## 27.7.4 sort_heap

```cpp
template<class RandomAccessIterator>
void sort_heap(RandomAccessIterator first);
```

```cpp
template<class RandomAccessIterator, class Compare>
void sort_heap(RandomAccessIterator first, Compare comp);
```

- 1. 要求：范围 `[first, last)` 应该是一个有效的堆。`RandomIterator` 应满足 `ValueSwappable(20.5.3.2)`。`*first` 应满足构造（表 23）和移动赋值（表 25）的要求。
- 2. 效果：排序范围 `[first, last)`。
- 3. 复杂度：`N log N`，其中 `N = last - first`。

## 27.7.5 is_heap

```cpp
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first);
```

```cpp
template<class ExecutionPolicy, class RandomAccessIterator>
bool is_heap(ExecutionPolicy&& exec, RandomAccessIterator first);
```

```cpp
template<class RandomAccessIterator, class Compare>
bool is_heap(RandomAccessIterator first, Compare comp);
```

```cpp
template<class ExecutionPolicy, class RandomAccessIterator, class Compare>
bool is_heap(ExecutionPolicy&& exec, RandomAccessIterator first, Compare comp);
```

- 1. 要求：范围 `[first, last)` 是是一个有效的堆。`RandomIterator` 应满足 `ValueSwappable(20.5.3.2)`。
- 2. 效果：如果范围 `[first, last)` 是堆，则返回 `true`。
- 3. 复杂度：线性。

## 27.7.8 Minimum and maximum

```cpp
template<class T>
const T min(const T& a, const T& b);
```

```cpp
template<class T>
const T min(const T& a, const T& b, T (*comp));
```

```cpp
template<class T>
const T min(initializer_list<T> t);
```

```cpp
template<class T>
const T min(initializer_list<T> t, T (*comp));
```

```cpp
template<class T>
const T max(const T& a, const T& b);
```

```cpp
template<class T>
const T max(const T& a, const T& b, T (*comp));
```

```cpp
template<class T>
const T max(initializer_list<T> t);
```

- 1. 要求：对于第一个类型，类型 `T` 应满足 `LessThanComparable`（表 21）。
- 2. 返回：较小的值。
- 3. 备注：当参数相等时，返回第一个参数。
- 4. 复杂度：一次比较。
- 1. 要求：`T` 应是 `CopyConstructible` 且 `t.size() > 0`。对于第一个类型，`T` 应满足 `LessThanComparable`。
- 2. 返回：`iterator_list` 中的最小值。
- 3. 备注：当多个参数等同于最小值时，返回最左侧的参数。
- 4. 复杂度：`t.size() - 1` 次比较。

ISO/IEC 14882:2017(E)

- 11 返回：当多个参数等效时，返回第一个参数。
- 12 复杂度：恰好执行一次比较。

```cpp
template<class T>
constexpr T max(initializer_list<T> t);
template<class T, class Compare> max(initializer_list<T> t, Compare comp);
```

- 13 要求：`T` 必须是可拷贝构造（`CopyConstructable`）且 `t.size() > 0`。对于第一种形式，类型 `T` 必须是可比较的（`LessThanComparable`）。
- 14 返回：初始化列表中的最大值。
- 15 返回：当多个参数与最大值等效时，返回最左参数的拷贝。
- 16 复杂度：恰好为 `t.size() - 1`。

```cpp
template<class T> constexpr min(const T& a, const T& b);
template<class T, class Compare> min(const T& a, const T& b);
constexpr pair<const T&, const T&> min(const T& a, b);
```

- 17 要求：对于第一种形式，类型 `T` 必须是可比较的（表 21）。
- 18 返回：如果 `b` 小于 `a`，返回 `pair<const T&, const T&>`；否则返回 `pair<const T&, const T&>(a, b)`。
- 19 备注：当参数等效时，返回 `pair<const T&, const T&>(a, b)`。
- 20 复杂度：恰好执行一次比较。

```cpp
template<class T> min(initializer_list<T> t);
template<class T, class Compare> min(initializer_list<T> t, Compare comp);
```

- 21 要求：`T` 必须是可拷贝构造且 `t.size() > 0`。对于第一种形式，类型 `T` 必须是可比较的。
- 22 返回：`pair<T, T>(x, y)`，其中 `x` 拥有初始化列表中的最小值，`y` 拥有最大值。当多个参数与最小值等效时，`y` 是最右参数的拷贝。
- 23 复杂度：执行 `(3/2).size()` 次相应的谓词应用。

```cpp
template<class Forwarditerator>
constexpr Forwarditerator min_element(Forwarditerator first, Forwarditerator last);
```

```cpp
template<class Forwarditerator, class ExecutionPolicy>
Forwarditerator min_element(ExecutionPolicy&& exec, Forwarditerator first, Forwarditerator last);
```

```cpp
template<class Forwarditerator, class Compare>
constexpr Forwarditerator min_element(Forwarditerator first, Forwarditerator last, Compare comp);
```

```cpp
template<class Forwarditerator, class ExecutionPolicy, class Compare>
Forwarditerator min_element(ExecutionPolicy&& exec, Forwarditerator first, Forwarditerator last, Compare comp);
```

- 25 返回：范围 `[first, last)` 中的第一个迭代器 `i`，使得对于范围 `[first, last)` 中的每一个迭代器 `j`，满足以下条件：`!(*j < *i)` 或 `comp(*j, *i) == false`。
如果 `first == last`，则返回 `last`。
复杂度：恰好执行 `max(last - first, 1.0)` 次相应的比较。

```cpp
template<class ForwardIterator>
const& ForwardIterator max_element(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last);
template<class Compare>
const& ForwardIterator max_element(ForwardIterator first, ForwardIterator last, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class Compare>
ForwardIterator max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, Compare comp);
```

返回：范围 `[first, last)` 中的第一个迭代器，使得对于范围 `[first, last)` 中的每一个 `j`，满足以下条件：`!(*i < j)` 或 `comp(*i,j) == false`。
如果 `first == last`，则返回 `last`。
复杂度：恰好执行 `max(last - first, 1.0)` 次相应的比较。

```cpp
template<class ForwardIterator>
const pair<ForwardIterator, ForwardIterator> max_element(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
pair<ForwardIterator, ForwardIterator> max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last);
template<class ForwardIterator, class Compare>
const pair<ForwardIterator, ForwardIterator> max_element(ForwardIterator first, ForwardIterator last, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class Compare>
pair<ForwardIterator, ForwardIterator> max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, Compare comp);
```

返回：如果 `[first, last)` 为空，则返回 `max_pair(first, first)`；否则返回 `make_pair(m, M)`，其中 `m` 是 `[first, last)` 中第一个迭代器，使得范围内没有迭代器指向更小的元素，而 `M` 是 `[first, last)` 中最后一个指向更大元素的迭代器。
复杂度：最多执行 `max(|N-1|, 1.0)` 次相应的谓词，其中 `N` 为 `last - first`。

## 28.9. 有边界值 [alg.clamp]

```cpp
template<class T>
const T& clamp(const T& v, const T& lo, const T& hi);
template<class Compare>
const T& clamp(const T& v, const T& lo, const T& hi, Compare comp);
```

- 要求：`lo` 的值不大于 `hi`。对于第一种形式，类型 `T` 必须是可比较的（表 21）。
- 此行为与 `max_element()` 不同。
- 返回：如果 `v` 小于 `lo`，返回 `lo`；如果 `hi` 小于 `v`，返回 `hi`。
- 备注：避免了 NaN，`T` 可以是浮点类型。
复杂度：最多两次比较。

## 28.7.10 字典序比较 [alg.comparison]
