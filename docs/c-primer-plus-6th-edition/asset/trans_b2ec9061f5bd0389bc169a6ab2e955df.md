

# 表 G.15 排序及相关操作

| Function | Description |
|---|---|
| merge() | 将两个已排序的范围合并到第三个范围中。 |
| inplace_merge() | 原地合并连续的已排序范围。 |
| includes() | 如果一个集合中的每个元素也在另一个集合中找到，则返回 true。 |
| set_union() | 构造两个集合的并集——即包含每个集合中存在的所有元素的集合。 |
| set_intersection() | 构造两个集合的交集——即仅包含同时存在于两个集合中的元素的集合。 |
| set_difference() | 构造两个集合的差集——即仅包含存在于第一个集合但不存在于第二个集合中的元素的集合。 |
| set_symmetric_difference() | 构造一个集合，其中包含存在于其中一个集合或另一个集合中但不同时存在的元素。 |
| make_heap() | 将范围转换为堆。 |
| push_heap() | 向堆中添加一个元素。 |
| pop_heap() | 从堆中移除最大元素。 |
| sort_heap() | 对堆进行排序。 |
| is_heap() | 如果范围是堆则返回 true。 (C++11) |
| is_heap_until() | 返回范围为堆的最后一个迭代器。 (C++11) |
| min() | 返回两个值中较小者或 initializer_list 对象中的最小项。 (C++11) |
| max() | 返回两个值中较大者或 initializer_list 参数中的最大项。 (C++11) |
| minmax() | 返回一个包含两个参数值按递增大小顺序的 pair，或 initializer_list 范围中最小和最大项。 (C++11) |
| min_element() | 在范围内查找最小值的第一次出现。 |
| max_element() | 在范围内查找最大值的第一次出现。 |
| minmax_element() | 返回一个包含指向范围内最小值第一次出现的迭代器和指向最大值最后一次出现的迭代器的 pair。 (C++11) |
| lexicographic_compare() | 按字典顺序比较两个序列，如果第一个序列字典顺序小于第二个序列则返回 true，否则返回 false。 |
| next_permutation() | 生成序列中的下一个排列。 |
| previous_permutation() | 生成序列中的前一个排列。 |

本节中的函数使用 < 运算符确定两个元素的顺序，或使用模板类型指定的比较运算符。如果 comp 是 Compare 类型的对象，则 comp(a,b) 是 a < b 的泛化，并在 a 在排序方案中先于 b 时返回 true。如果 a < b 为 false 且 b < a 也为 false，则 a 和 b 是等价的。比较对象必须至少提供严格排序。这意味着以下内容：

- 表达式 comp(a,a) 必须为 false，这是 a 值不能是其自身这一事实的泛化。 (这是严格的部分)
- 如果 comp(a,b) 为 true 且 comp(b,c) 为 true，则 comp(a,c) 为 true (即比较是传递关系)。
- 如果 a 等价于 b 且 b 等价于 c，则 a 等价于 c (即等价是传递关系)。

如果你想到将 < 应用于整数，则等价意味着相等，但对于更一般的情况不必如此。例如，你可以定义一个具有多个成员的结构来描述邮寄地址，并定义一个比较对象按邮政编码对其进行排序。那么具有相同邮政编码的两个地址将相等但不相等。

让我们更详细地查看这些排序及相关操作。对于每个函数，讨论显示原型(s)，随后是简要说明。本节分为几个子节。如你之前所见，迭代器对带有选择的模板参数指示迭代器类型。如往常一样，形式为 [first, last) 的范围从 first 开始到不包括 last。传递为参数的函数是函数对象，可以是指针或为其定义了 () 操作的对象。如你在第 16 章中所学，谓词是一个具有一个参数的布尔函数，二元谓词是一个具有两个参数的布尔函数。 (函数不必是 bool 类型，只要它们对 false 返回 0，对 true 返回非零值即可。) 同样在第 16 章中，一元函数对象是接受单个参数的，二元函数对象是接受两个参数的。

## Sorting

首先，让我们检查排序算法。

### sort()

```
template<class RandomAccessIterator>
void sort(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void sort(RandomAccessIterator first, RandomAccessIterator last,
          Compare comp);
```

sort() 函数按递增顺序对范围 [first, last) 进行排序，使用值类型的 < 运算符进行比较。第一个版本使用 <，第二个版本使用比较对象 comp 来确定顺序。

### stable_sort()

```
template<class RandomAccessIterator>
void stable_sort(RandomAccessIterator first, RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void stable_sort(RandomAccessIterator first, RandomAccessIterator last,
          Compare comp);
```

stable_sort() 函数对范围 [first, last) 进行排序，保持等价元素的相对顺序。第一个版本使用 <，第二个版本使用比较对象 comp 来确定顺序。

### partial_sort()

```
template<class RandomAccessIterator>
void partial_sort(RandomAccessIterator first, RandomAccessIterator middle,
                  RandomAccessIterator last);

template<class RandomAccessIterator, class Compare>
void partial_sort(RandomAccessIterator first, RandomAccessIterator middle,
                  RandomAccessIterator last, Compare comp);
```

partial_sort() 函数部分排序范围 [first, last)。已排序范围的第一个元素被放置在范围 [first, middle) 中，其余元素保持未排序。第一个版本使用 <，第二个版本使用比较对象 comp 来确定顺序。

### partial_sort_copy()

```
template<class InputIterator, class RandomAccessIterator>
RandomAccessIterator partial_sort_copy(InputIterator first,
                  InputIterator last,
                  RandomAccessIterator result_first,
                  RandomAccessIterator result_last);

template<class InputIterator, class RandomAccessIterator, class Compare>
RandomAccessIterator
partial_sort_copy(InputIterator first, InputIterator last,
RandomAccessIterator result_first,
RandomAccessIterator result_last,
Compare comp);
```

partial_sort_copy() 函数将已排序范围 [first, last] 的前 n 个元素复制到范围 [result_first, result_first + n)。n 的值是 last - first 和 result_last - result_first 中较小者。函数返回 result_first + n。第一个版本使用 <，第二个版本使用比较对象来确定顺序。

## Appendix G The Standard Template Library Methods and Functions

### is_sorted() (C++11)

```
template<ForwardIterator>
bool is_sorted(ForwardIterator first, ForwardIterator last);

template<ForwardIterator, class Compare>
bool is_sorted(ForwardIterator first, ForwardIterator last,
Compare comp);
```

is_sorted() 函数如果范围 [first, last] 已排序则返回 true，否则返回 false。第一个版本使用 <，第二个版本使用比较对象来确定顺序。

### is_sorted_until() (C++11)

```
template<ForwardIterator>
ForwardIterator is_sorted_until(ForwardIterator first, ForwardIterator last);

template<ForwardIterator, class Compare>
ForwardIterator is_sorted_until(ForwardIterator first, ForwardIterator last,
Compare comp);
```

is_sorted_until() 如果范围 [first, last] 包含少于两个元素则返回 last。否则，它返回使范围 [first, comp] 已排序的迭代器。第一个版本使用 <，第二个版本使用比较对象来确定顺序。

### nth_element()

```
template<class RandomAccessIterator>
void nth_element(RandomAccessIterator first, RandomAccessIterator nth,
RandomAccessIterator last);
```
