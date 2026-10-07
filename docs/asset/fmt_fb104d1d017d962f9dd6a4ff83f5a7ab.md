
`InputIterator2` `first2`, `InputIterator2` `last`);

```cpp
11 last,
2 first2, 2 last);
```

- 1 返回：如果 `[first2,last2)` 为空，或者 `[first2,last2)` 范围内的每个元素都在 `[first,last1)` 范围内，则返回 `true`。否则返回 `false`。

- 2 复杂度：最多 `2 * ((last1 - first1) + (last2 - first2)) - 1` 次比较。

### 25.4.5.2 set_union [set_union]

```cpp
template<class InputIterator1, class InputIterator2, class OutputIterator>
OutputIterator set_union(InputIterator1 first, InputIterator1 last,
                         InputIterator2 first2, InputIterator2 last,
                         OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2, class OutputIterator,class Compare>
OutputIterator set_union(InputIterator1 first, InputIterator1 last,
                         InputIterator2 first2, InputIterator2 last);
```

- 1 影响：构造两个范围的排序并；即存在于一个或两个范围中的元素。
- 2 要求：结果范围不应与任何原始范围重叠。
- 3 返回：所构造范围的末尾。
- 4 复杂度：最多 `2 * ((last1 - first1) + (last2 - first2)) - 1` 次比较。
- 5 备注：如果 `[first1,last1)` 包含 `m` 个相互相等的元素，而 `[first2,last2)` 包含 `n` 个与它们相等的元素，则从第一个范围的所有 `m` 个元素应当被拷贝到输出顺序中，然后从第二个范围将 `max(n-m, 0)` 个元素按顺序拷贝到输出范围。

### 25.4.5.3 set_intersection [set_intersection]

# ISO/IEC 14882:2011(E)

```cpp
template<class InputIterator1, class InputIterator2,
class OutputIterator>
OutputIterator
set_intersection(InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2,
class OutputIterator, class Compare>
OutputIterator
set_intersection(InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
OutputIterator result, Compare comp);
```

- 1 效果：构造来自两个范围的元素的排序后的交集；即同时存在于两个范围中的元素集合。
- 2 要求：结果范围不应与原始范围的任何一个重叠。
- 3 返回：所构造范围的末尾迭代。
- 4 复杂度：最多 `2 * ((last1 - first1) + (last2 - first2)) - 1` 次比较。
- 5 备注：如果 `[first1, last1)` 包含 `m` 个相互等价元素，且 `[first2, last2)` 包含 `n` 个相互等价元素，则将 `[first1, last1)` 中的前 `max(m-n,0)` 个元素按顺序从该范围拷贝到输出范围。

## 25.4.5.4 set_difference [set.difference]

```cpp
template<class InputIterator1, class InputIterator2,
class OutputIterator>
OutputIterator
set_difference(InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2,
class OutputIterator, class Compare>
OutputIterator
set_difference(InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
OutputIterator result, Compare comp);
```

- 1 效果：将范围 `[first1, last1)` 中不存在于范围 `[first2, last2)` 中的元素拷贝到从 `last2` 开始的范围。所构造范围中的元素是排序的。
- 2 要求：结果范围不应与原始范围的任何一个重叠。
- 3 返回：所构造范围的末尾迭代。
- 4 复杂度：最多 `2 * ((last1 - first1) + (last2 - first2)) - 1` 次比较。
- 5 备注：如果 `[first1, last1)` 包含 `m` 个相互等价元素，且 `[first2, last2)` 包含 `n` 个相互等价元素，则将 `[first1, last1)` 中的最后 `max(m-n,0)` 个元素拷贝到输出范围。

## 25.4.5.5 set_symmetric_difference [set.symmetric.difference]

```cpp
template<class InputIterator1, class InputIterator2,
             class OutputIterator,
             class OutputIterator>
set_symmetric_difference(InputIterator1 first1, InputIterator1 last1,
                               InputIterator2 first2, InputIterator2 last2,
                               OutputIterator result);
```

```cpp
template<class InputIterator1, class InputIterator2,
             class OutputIterator,
             class Compare>
set_symmetric_difference(InputIterator1 first1, InputIterator1 last1,
                               InputIterator2 first2, InputIterator2 last2,
                               OutputIterator result, Compare comp);
```

- 1. 效果：将范围 `[first1,last1)` 中不存在于范围 `[first2,last2)` 中的元素，以及范围 `[first2,last2)` 中不存在于范围 `[first1,last1)` 中的元素拷贝到从 `result` 开始的位置。所构造范围中的元素是排序的。
- 2. 要求：该范围不应与原始范围的任何一个重叠。
- 3. 返回：所构造范围的末尾迭代。
- 4. 复杂度：最多 `2*(last1 - first1) + (last2 - first2)` 次比较。
- 5. 备注：如果 `[first1,last1)` 包含相互等等的元素，或者 `[first2,last2)` 包含 `n` 个与它们等等的元素，则将这些元素中的 `|m-n|` 个拷贝到输出范围：如果 `m > n`，则拷贝 `[first1,last1)` 中的最后 `m-n` 个元素；如果 `m < n`，则拷贝 `[first2,last2)` 中的最后 `n-m` 个元素。

## 25.4.6 Heap operations [alg.heap_operations]

- 1 堆是两个随机迭代器之间范围 `[a,b)` 内元素的一种特殊组织形式。它的两个属性是：
  (1) 范围内没有比 `*a` 更大的元素，且
  (2) `*a` 可以在 `O(log(N))` 时间内通过 `pop_heap()` 移除，或通过 `push_heap()` 添加新元素。
- 2 这些属性使得堆成为非常有用的优先级队列。
- 3 `make_heap()` 将范围转换为堆，`sort_heap()` 将堆转换为排序序列。

### 25.4.6.1 push_heap [push.heap]

```cpp
template<class RandomAccessIterator>
void push_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void push_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1 效果：将 `[first, last)` 中的最后一个元素提升到堆的位置，使得 `[first, last)` 成为堆。
- 2 要求：`[first, last)` 已经是一个堆。
- 3 复杂度：`O(log N)`，其中 `N = (last - first)`。

### 25.4.6.2 pop_heap

```cpp
template<class RandomAccessIterator>
void pop_heap(RandomAccessIterator first, RandomAccessIterator last);
```

- 1 效果：将 `[first, last)` 堆中的最大元素与最后一个元素交换，并对 `[first, last)` 重新调整。
- 2 要求：`[first, last)` 已经是一个堆。
- 3 复杂度：`O(log N)`，其中 `N = (last - first)`。

### 25.4.6.3 make_heap

```cpp
template<class RandomAccessIterator>
void make_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void make_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1 效果：在 `[first, last)` 中构造一个堆。
- 2 复杂度：`O(N)`，其中 `N = (last - first)`。

### 25.4.6.4 sort_heap

```cpp
template<class RandomAccessIterator>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1 效果：将堆 `[first, last)` 转换为排序序列。
- 2 要求：`[first, last)` 已经是一个堆。
- 3 复杂度：`O(N log N)`。

### 25.4.6.5 is_heap [is.heap]

```cpp
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class Compare>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

- 1 返回：如果 `[first, last)` 是堆则返回 `true`，否则返回 `false`。
- 2 复杂度：`O(N)`。

## 25.4.7 Minimum and maximum [alg.min.max]

```cpp
template<class T>
T min(const T& a, const T& b);
```

```cpp
template<class T, class Compare>
T min(const T& a, const T& b, Compare comp);
```

- 1 要求：`T` 是 `LessComparable`（18）。
- 2 返回：较小的值。
- 3 备注：当参数相等时，返回第一个参数。

```cpp
template<class T>
T min(initializer_list<T> t);
```

```cpp
template<class T, class Compare>
T min(initializer_list<T> t, Compare comp);
```

- 4 要求：`T` 是 `LessThanComparable` 和 `CopyConstructible`，且 `t.size() > 0`。
- 5 返回：初始化列表中的最小值。
- 6 备注：当有多个参数等于最小值时，返回最左侧参数的拷贝。

```cpp
template<class T>
T max(const T& a, const T& b);
```

```cpp
template<class T, class Compare>
T max(const T& a, const T& b, Compare comp);
```

```cpp
const T& max(const T& a, const T& b, Compare comp);
```

- 7 要求：`T` 是 `LessThanComparable`（18）。
- 8 返回：较大的值。
- 9 备注：当参数相等时，返回第一个参数。

```cpp
template<class T>
T max(initializer_list<T> t);
```

```cpp
template<class T, class Compare>
```

# ISO/IEC 14882:2011(E)

`T max(initializer_list<T> t, Compare comp);`

- 10 要求：`T` 满足 `LessThanComparable`（小于可比较）和 `CopyConstructible`（可拷贝构造），且 `t.size() > 0`。
- 11 返回：`initializer_list` 中的最大值。
- 12 返回：当多个参数等于最大值时，返回最左侧参数的拷贝。

```cpp
template<class T> pair<const T&, const T&> minmax(const T& a, const T& b);
template<class T, class Compare>
pair<const T&, const T&> minmax(const T& a, const T& b, Compare comp);
```

- 13 要求：类型 `T` 为 `LessThanComparable`（小于可比较）（表 18）。
- 14 返回：如果 `b` 小于 `a`，返回 `pair<const T&, const T&> a`；否则返回 `pair<const T&, const T&>(a, b)`。
- 15 返回：当参数等等时，返回 `pair<const T&, const T&>(a, b)`。

```cpp
template<class T>
T max(initializer_list<T> t);
template<class T, class Compare>
pair<T, T> max(initializer_list<T> t, Compare comp);
```
