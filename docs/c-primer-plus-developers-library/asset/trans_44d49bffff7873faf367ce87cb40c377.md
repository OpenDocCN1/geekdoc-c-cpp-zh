
### sort_heap()

```cpp
template<class RandomAccessIterator>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last,
               Compare comp);
```

sort_heap() 函数假定范围 [first,last) 是一个堆，并对其进行排序。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

### is_heap() (C++11)

```cpp
template<class RandomAccessIterator>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
bool is_heap(RandomAccessIterator first, RandomAccessIterator last,
             Compare comp);
```

如果范围 [first,last) 是一个堆，则 is_heap() 函数返回 true，否则返回 false。第一个版本使用 <，第二个版本使用比较对象 comp 来确定顺序。

### is_heap_until() (C++11)

```cpp
template<class RandomAccessIterator>
RandomAccessIterator is_heap_until(RandomAccessIterator first,
                                   RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
RandomAccessIterator is_heap_until(
                       RandomAccessIterator first, RandomAccessIterator last,
                       Compare comp);
```

如果范围 [first,last) 中的元素少于两个，则 is_heap_until() 函数返回 last。否则，它返回最后一个迭代器 it，使得范围 [first,it) 是一个堆。第一个版本使用 <，第二个版本使用比较对象 comp 来确定顺序。

## 查找最小值和最大值

minimum 和 maximum 函数返回值对以及值序列中的最小值和最大值。

### min()

```cpp
template<class T> const T& min(const T& a, const T& b);

template<class T, class Compare>
const T& min(const T& a, const T& b, Compare comp);
```

这些版本的 min() 函数返回两个值中较小的值。如果两个值等价，则返回第一个值。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

```cpp
template<class T> T min(initializer_list<T> t);

template<class T, class Compare>
T min(initializer_list<T> t, Compare comp);
```

这些版本的 min() 函数（C++11）返回初始化列表 t 中的最小值。如果两个或多个值等价，则返回具有该值的第一个出现项的副本。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

### max()

```cpp
template<class T> const T& max(const T& a, const T& b);

template<class T, class Compare>
const T& max(const T& a, const T& b, Compare comp);
```

这些版本的 max() 函数返回两个值中较大的值。如果两个值等价，则返回第一个值。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

```cpp
template<class T> T max(initializer_list<T> t);

template<class T, class Compare>
T max(initializer_list<T> t, Compare comp);
```

这些版本的 max() 函数（C++11）返回初始化列表 t 中的最大值。如果两个或多个值等价，则返回具有该值的第一个出现项的副本。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

### minmax() (C++11)

```cpp
template<class T>
    pair<const T&,const T&> minmax(const T& a, const T& b);

template<class T, class Compare>
    pair<const T&,const T&> minmax(const T& a, const T& b,
                                   Compare comp);
```

这些版本的 minmax() 函数在 b 小于 a 时返回 pair (b,a)，否则返回 pair (a,b)。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

```cpp
template<class T> pair<T,T> minmax(initializer_list<T> t);

template<class T, class Compare>
pair<T,T> minmax(initializer_list<T> t, Compare comp);
```

这些版本的 minmax() 函数返回初始化列表 t 中最小元素和最大元素的副本。如果多个元素与最小值等价，则返回第一个出现的元素。如果多个元素与最大值等价，则返回最后一个出现的元素。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

### min_element()

```cpp
template<class ForwardIterator>
ForwardIterator min_element(ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
ForwardIterator min_element(ForwardIterator first, ForwardIterator last,
Compare comp);
```

min_element() 函数返回范围 [first, last) 中的第一个迭代器 it，使得该范围中没有元素小于 *it。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

### max_element()

```cpp
template<class ForwardIterator>
ForwardIterator max_element(ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
ForwardIterator max_element(ForwardIterator first, ForwardIterator last,
Compare comp);
```

max_element() 函数返回范围 [first,last) 中的第一个迭代器 it，使得不存在 *it 小于的元素。第一个版本使用 < 确定顺序，第二个版本使用 comp 比较对象。

### minmax_element() (C++11)

```cpp
template<class ForwardIterator>
  pair<ForwardIterator,ForwardIterator>
    minmax_element(ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
  pair<ForwardIterator,ForwardIterator>
    minmax_element(ForwardIterator first, ForwardIterator last,
                   Compare comp);
```

`minmax_element()` 函数返回一个 pair 对象，其中包含范围 `[first, last)` 中的第一个迭代器 `it1`，使得不存在 `*it1` 小于的元素，以及范围 `[first, last)` 中的最后一个迭代器 `it2`，使得不存在 `*it2` 小于的元素。第一个版本使用 `<` 确定顺序，第二个版本使用 `comp` 比较对象。

### lexicographical_compare()

```cpp
template<class InputIterator1, class InputIterator2>
bool lexicographical_compare(
    InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2);

template<class InputIterator1, class InputIterator2, class Compare>
bool lexicographical_compare(
    InputIterator1 first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2,
    Compare comp);
```

如果范围 `[first1, last1)` 中的元素序列按字典序小于范围 `[first2, last2)` 中的元素序列，则 `lexicographical_compare()` 函数返回 `true`；否则返回 `false`。字典序比较将一个序列的第一个元素与第二个序列的第一个元素进行比较——即比较 `*first1` 和 `*first2`。如果 `*first1` 小于 `*first2`，函数返回 `true`。如果 `*first2` 小于 `*first1`，函数返回 `false`。如果两者等价，则继续比较每个序列中的下一个元素。此过程持续到两个对应元素不等价或到达某个序列的末尾。如果两个序列在到达其中一个末尾之前都等价，则较短的序列较小。如果两个序列等价且长度相同，则两者都不小于对方，因此函数返回 `false`。该函数的第一个版本使用 `<` 比较元素，第二个版本使用 `comp` 比较对象。字典序比较是字母顺序比较的推广。

## 处理排列

序列的一个*排列*是元素的重排。例如，由三个元素组成的序列有六种可能的顺序，因为第一个元素有三种选择。为第一个位置选择特定元素后，第二个位置有两种选择，第三个位置有一种选择。例如，数字 1、2、3 的六种排列如下：

123 132 213 231 312 321

一般而言，由 *n* 个元素组成的序列有 *n* × (*n*−1) × ... × 1，即 *n*! 种可能的排列。排列函数假定所有可能排列的集合可以按字典序排列，如前面的六种排列示例所示。也就是说
