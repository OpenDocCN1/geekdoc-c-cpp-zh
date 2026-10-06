

ISO/IEC 14882:2017(E)

- 11 返回：当多个参数等效时，返回第一个参数。
- 12 复杂度：恰好执行一次比较。

```cpp
template<class T>
constexpr T max(initializer_list<T> t);
template<class T, class Compare> max(initializer_list<T> t, Compare comp);
```

- 13 要求：T 必须是可拷贝构造（CopyConstructable）且 t.size() > 0。对于第一种形式，类型 T 必须是可比较的（LessThanComparable）。
- 14 返回：初始化列表中的最大值。
- 15 返回：当多个参数与最大值等效时，返回最左参数的拷贝。
- 16 复杂度：恰好为 t.size() - 1。

```cpp
template<class T> constexpr min(const T& a, const T& b);
template<class T, class Compare> min(const T& a, const T& b);
constexpr pair<const T&, const T&> min(const T& a, b);
```

- 17 要求：对于第一种形式，类型 T 必须是可比较的（表 21）。
- 18 返回：如果 b 小于 a，返回 pair<const T&, const T&>；否则返回 pair<const T&, const T&>(a, b)。
- 19 备注：当参数等效时，返回 pair<const T&, const T&>(a, b)。
- 20 复杂度：恰好执行一次比较。

```cpp
template<class T> min(initializer_list<T> t);
template<class T, class Compare> min(initializer_list<T> t, Compare comp);
```

- 21 要求：T 必须是可拷贝构造且 t.size() > 0。对于第一种形式，类型 T 必须是可比较的。
- 22 返回：pair<T, T>(x, y)，其中 x 拥有初始化列表中的最小值，y 拥有最大值。当多个参数与最小值等效时，y 是最右参数的拷贝。
- 23 复杂度：执行 (3/2).size() 次相应的谓词应用。

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

- 25 返回：范围 [first, last) 中的第一个迭代器 i，使得对于范围 [first, last) 中的每一个迭代器 j，满足以下条件：!(*j < *i) 或 comp(*j, *i) == false。

如果 first == last，则返回 last。
复杂度：恰好执行 max(last - first, 1.0) 次相应的比较。

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

返回：范围 [first, last) 中的第一个迭代器，使得对于范围 [first, last) 中的每一个 j，满足以下条件：!(*i < j) 或 comp(*i,j) == false。
如果 first == last，则返回 last。
复杂度：恰好执行 max(last - first, 1.0) 次相应的比较。

```cpp
template<class ForwardIterator>
const pair<ForwardIterator, ForwardIterator>
max_element(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
pair<ForwardIterator, ForwardIterator>
max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
const pair<ForwardIterator, ForwardIterator>
max_element(ForwardIterator first, ForwardIterator last, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class Compare>
pair<ForwardIterator, ForwardIterator>
max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, Compare comp);
```

返回：如果 [first, last) 为空，则返回 max_pair(first, first)；否则返回 make_pair(m, M)，其中 m 是 [first, last) 中第一个迭代器，使得范围内没有迭代器指向更小的元素，而 M 是 [first, last) 中最后一个指向更大元素的迭代器。
复杂度：最多执行 max(|N-1|, 1.0) 次相应的谓词，其中 N 为 last - first。

## 28.9. 有边界值 [alg.clamp]

```cpp
template<class T>
const T& clamp(const T& v, const T& lo, const T& hi);
template<class Compare>
const T& clamp(const T& v, const T& lo, const T& hi, Compare comp);
```

- 要求：lo 的值不大于 hi。对于第一种形式，类型 T 必须是可比较的（表 21）。
- 此行为与 max_element() 不同。
- 返回：如果 v 小于 lo，返回 lo；如果 hi 小于 v，返回 hi。
- 备注：避免了 NaN，T 可以是浮点类型。
复杂度：最多两次比较。

## 28.7.10 字典序比较 [alg.comparison]

```cpp
template<class InputIterator, class InputIterator>
bool lexicographical_compare(InputIterator first1, InputIterator last1, InputIterator first2, InputIterator last2);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator>
bool lexicographical_compare(ExecutionPolicy&& exec, ForwardIterator first1, ForwardIterator last1, ForwardIterator first2, ForwardIterator last2);
template<class InputIterator, class InputIterator, class Compare>
bool lexicographical_compare(InputIterator first1, InputIterator last1, InputIterator first2, InputIterator last2, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator, class Compare>
bool lexicographical_compare(ExecutionPolicy&& exec, ForwardIterator first1, ForwardIterator last1, ForwardIterator first2, ForwardIterator last2, Compare comp);
```

返回：如果范围 [first1, last1) 定义的序列字典序小于范围 [first2, last2) 定义的序列，则返回 true；否则返回 false。
复杂度：如果两个序列元素数量相同且对应的元素（如果有）等效，则两者都不小于另一个。如果一个序列是另一个的前缀，则较短的序列字典小于较长的序列。否则，字典序的结果与第一对不相等元素的比较相同。
示例：以下实现满足这些要求：
```cpp
for (; first1 != last1 && first2 != last2; ++first1, ++first2) {
    if (*first1 < *first2) return false;
    if (*first2 < *first1) return true;
}
return first1 == last1 && first2 == last2;
```
备注：空序列字典序小于任何非空序列，但不小于任何。

## 28.7.11 排生成器 [alg.permutation.generators]

```cpp
template<class BidirectionalIterator>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last);
```

## ISO/IEC 14882:2017(E)

```cpp
template<class BidirectionalIterator, class Compare>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

- 1 要求：BidirectionalIterator 必须满足可交换（ValueSwapable）（20.5.3.2）。
- 2 影响：取范围 [first, last] 定义的序列并转换为下一个排列。下一个排列通过假设所有排列相对于 operator< 或 comp 是字典序排序。
- 3 返回：如果存在这样的排列，则返回 true。否则，将序列转换为降序排序的最大排列并返回 false。
- 4 复杂度：最多 (last - first) / 2 次交换。

```cpp
template<class BidirectionalIterator>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last);
template<class BidirectionalIterator, class Compare>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

- 5 要求：BidirectionalIterator 必须满足可交换（ValueSwapable）（20.5.3.2）。
- 6 影响：取范围 [first, last] 定义的序列并转换为上一个排列。上一个排列通过假设所有排列相对于 operator< 或 comp 是字典序排序。
- 7 返回：如果存在这样的排列，则返回 true。否则，将序列转换为降序排序的最小排列并返回 false。
- 8 复杂度：最多 (last - first) / 2 次交换。

## 28.8 C 算法

备注：头文件 <cstdlib> (21.2.2) 声明了本子句描述的函数。结束

```c
void* search(const void* key, const void* base, size_t nemb, size_t size,
               int (*compare_pred)(const void*, const void*));
void qsort(void* base, size_t nemb, size_t size, int (*compare_pred)(const void*, const void*));
```

- 2 影响：这些函数具有 C 标准库指定的语义。
- 3 备注：除非由 base 指向的数组对象是平凡类型，否则行为是未定义的。
- 4 抛出：任何由 compare() (20.5.12) 抛出的异常。

另另：ISO C 7.22.5.

