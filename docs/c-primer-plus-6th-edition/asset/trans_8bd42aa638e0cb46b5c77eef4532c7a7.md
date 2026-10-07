

# 1318 附录 G 标准模板库方法与函数

max_element() 函数返回一个对对象，其中包含范围 `[first, last)` 内的第一个迭代器 `it1`（使得该范围内没有元素小于 `*it1`），以及范围 `[first, last]` 内的最后一个迭代器 `it2`（使得该范围内没有元素小于 `*it2`*）。第一个版本使用 `<` 来确定顺序，第二个版本使用 `comp` 比较对象。

## lexicographical_compare()

```cpp
template<class InputIterator1, class InputIterator2>
bool lexicographical_compare(
    InputIterator first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2);
```

```cpp
template<class InputIterator1, class InputIterator2, class Compare>
bool lexicographical_compare(
    InputIterator first1, InputIterator1 last1,
    InputIterator2 first2, InputIterator2 last2,
    Compare comp);
```

如果范围 `[first1, last1)` 内的元素序列在字典序上小于范围 `[first2, last2)` 内的元素序列，则 lexicographical_compare() 返回 true；否则——也就是说，它比较 `*first1` 和 `*first2`。如果 `*first1` 小于 `*first2`，返回 true。如果 `*first2` 小于 `*first1`，函数返回 false。如果两者相等，则继续比较每个序列中的下一个元素。此过程一直持续到两个元素不相等或到达序列末尾。较短的序列较小。如果两个序列相等且长度相同，则没有一个更小，因此函数返回 false。函数的第一个版本使用 `<` 比较元素，第二个版本使用 `comp` 比较对象。字典序比较是字母顺序比较推广。

## 处理排列

序列的排列是元素的重新排序。例如，一个包含三个元素的序列有六种可能的排序，因为我们对第一个元素有三个选择。为第一个位置选择一个特定元素后，第二个位置剩下两个选择，第三个也是如此。例如，数字 1, 2, 3 的排列如下：

123 132 213 232 312 321

通常，一个包含 n 个元素的序列有 n! 种可能的排列。字典序比较是字母顺序比较的推广。lexicographical_compare() 函数如果范围 `[first1, last1)` 内的元素序列在字典序上小于范围 `[first2, last2)` 内的元素序列，则返回 true；否则——也就是说，它比较 `*first1` 和 `*first2`。如果 `*first1` 小于 `*first2`，返回 true。如果 `*first2` 小于 `*first1`，函数返回 false。如果两者相等，则继续比较每个序列中的下一个元素。此过程一直持续到两个元素不相等或到达序列末尾。较短的序列较小。如果两个序列相等且长度相同，则没有一个更小，因此函数返回 false。函数的第一个版本使用 `<` 比较元素，第二个版本使用 `comp` 比较对象。

序列的排列是元素的重新排序。例如，一个包含三个元素的序列有六种可能的排序，因为我们对第一个元素有三个选择。为第一个位置选择一个特定元素后，第二个位置剩下两个选择，第三个也是如此。例如，数字 1, 2, 3 的排列如下：

123 132 213 232 312 321

通常，一个包含 n 个元素的序列有 n! 种可能的排列。字典序比较是字母顺序比较的推广。lexicographical_compare() 函数如果范围 `[first1, last1)` 内的元素序列在字典序上小于范围 `[first2, last2)` 内的元素序列，则返回 true；否则——也就是说，它比较 `*first1` 和 `*first2`。如果 `*first1` 小于 `*first2`，返回 true。如果 `*first2` 小于 `*first1`，函数返回 false。如果两者相等，则继续比较每个序列中的下一个元素。此过程一直持续到两个元素不相等或到达序列末尾。较短的序列较小。如果两个序列相等且长度相同，则没有一个更小，因此函数返回 false。函数的第一个版本使用 `<` 比较元素，第二个版本使用 `comp` 比较对象。

序列的排列是元素的重新排序。例如，一个包含三个元素的序列有六种可能的排序，因为我们对第一个元素有三个选择。为第一个位置选择一个特定元素后，第二个位置剩下两个选择，第三个也是如此。例如，数字 1, 2, 3 的排列如下：

123 132 213 232 312 321

通常，一个包含 n 个元素的序列有 n! 种可能的排列。字典序比较是字母顺序比较的推广。lexicographical_compare() 函数如果范围 `[first1, last1)` 内的元素序列在字典序上小于范围 `[first2, last2)` 内的元素序列，则返回 true；否则——也就是说，它比较 `*first1` 和 `*first2`。如果 `*first1` 小于 `*first2`，返回 true。如果 `*first2` 小于 `*first1`，函数返回 false。如果两者相等，则继续比较每个序列中的下一个元素。此过程一直持续到两个元素不相等或到达序列末尾。较短的序列较小。如果两个序列相等且长度相同，则没有一个更小，因此函数返回 false。函数的第一个版本使用 `<` 比较元素，第二个版本使用 `comp` 比较对象。

## next_permutation()

```cpp
template<class BidirectionalIterator>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last);
```

```cpp
template<class BidirectionalIterator, class Compare>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

next_permutation() 函数将范围 `[first, last)` 转换为下一个字典序更大的排列。如果存在这样的排列，则返回 true；否则，它将范围转换为最小的排列（元素按递增排序）并返回 false。

## prev_permutation()

```cpp
template<class BidirectionalIterator>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last);
```

```cpp
template<class BidirectionalIterator, class Compare>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

```

prev_permutation() 函数将范围 `[first, last)` 转换为下一个字典序更小的排列。如果存在这样的排列，则返回 true；否则，它将范围转换为最大的排列（元素按递减排序）并返回 false。

## 数值操作

| 函数 | 描述 |
| :--- | :--- |
| accumulate() | 计算范围内元素的和。 |
| inner_product() | 计算两个指定范围的内积。 |
| partial_sum() | 计算范围内元素的部分和。 |
| adjacent_difference() | 计算范围内相邻元素之间的差。 |
| iota() | 用顺序递增的值填充范围。 |

