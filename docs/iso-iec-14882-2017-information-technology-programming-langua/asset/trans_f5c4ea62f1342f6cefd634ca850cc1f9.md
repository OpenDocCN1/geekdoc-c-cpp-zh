

# ISO/IEC 14882:2017(E)

```cpp
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
bool equal(ExecutionPolicy&& exec,
ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2, ForwardIterator2 last2);

template<class InputIterator1, class InputIterator2,
class BinaryPredicate>
bool equal(InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
BinaryPredicate pred);

template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
bool equal(ExecutionPolicy&& exec,
ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2, ForwardIterator2 last2,
BinaryPredicate pred);
```

- 1. 如果参数列表中没有给出 last2，则它表示下方的 `first2 + (last1 - first1)`。
- 2. 返回：如果 `last1 == last2` 则返回 false。否则如果范围 `[first, last1)` 中的每个迭代器 `i` 满足以下条件：*i == *(first2 + (i - first1)), pred(i, *(first2 + (i - first1))) == false*，则返回 true。否则返回 false。
- 3. 复杂度：
    - (3.1) 对于带有 ExecutionPolicy 的重载。
    如果 `InputIterator1` 和 `InputIterator2` 满足随机访问迭代器 (27.2) 的要求且 `last1 - first1 == last2`，则不应用相应的谓词；
    - (3.2) 至少有 `min(last1 - first1, last2 - first2)` 次相应谓词的应用。
    - (3.2.1) 对于带有 ExecutionPolicy 的重载。
    如果 `ForwardIterator1` 和 `ForwardIterator2` 满足随机访问迭代器的要求且 `last1 - first1 == last2`，则不应用相应的谓词；
    - (3.2.2) `min(last1 - first1, last2 - first2)` 次相应谓词的应用。

# 28.5.12 是否为排列 [alg.is_permutation]

```cpp
template<class ForwardIterator1, class ForwardIterator2>
bool is_permutation(ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2, ForwardIterator2 last2);

template<class ForwardIterator1, class ForwardIterator2, class BinaryPredicate>
bool is_permutation(ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2, ForwardIterator2 last2, BinaryPredicate pred);
```

- 1. 要求：`ForwardIterator1` 和 `ForwardIterator2` 具有相同的值类型。比较函数应该是一个等价关系。
- 2. 备注：如果参数列表中没有给出 last2，则它表示下方的 `first2 + (last1 - first1)`。
- 返回：如果 `last1 - first1 = last2 - first2`，返回 false。否则，如果存在范围 `[first2, first2 + (last1 - first1))` 中的元素的排列，且以 `ForwardIterator2` 开始，使得 `equal(first1, last1, pred)` 或 `equal(first1, last2, pred)` 返回 true，则返回 true；否则返回 false。
- 复杂度：如果 `ForwardIterator1` 和 `ForwardIterator2` 满足随机访问迭代器的要求且 `last1 - last2 = first2`，则应用谓词的顺序。否则，如果 pred 在列表中给出时 `equal(first1, last2, pred)` 会返回 true，或者如果 pred 在参数列表中给出时 `equal(first1, last2, pred)` 会返回 true，则应用 `last1 - first1` 次相应谓词的应用；否则为 O(N)，其中 N 的值类似于 `first1` 的值。

# 28.5.13 搜索

```cpp
template<class ForwardIterator1, class ForwardIterator2>
search(ForwardIterator1 first1, ForwardIterator1 last1,
      ForwardIterator2 first2, ForwardIterator2 last2);

template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2>
search(ExecutionPolicy&& exec, pred,
      ForwardIterator1 first1, ForwardIterator1 last1,
      ForwardIterator2 first2, ForwardIterator2 last2);

template<class ForwardIterator1, class ForwardIterator2,
      class BinaryPredicate>
search(ForwardIterator1 first1, ForwardIterator1 last1,
      ForwardIterator2 first2, ForwardIterator2 last2,
      BinaryPredicate pred);

template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2,
      class BinaryPredicate>
search(ExecutionPolicy&& exec, pred,
      ForwardIterator1 first1, ForwardIterator1 last1,
      ForwardIterator2 first2, ForwardIterator2 last2,
      BinaryPredicate pred);
```

- 影响：在序列中找到相等值的子序列。
- 返回：迭代器返回 `[first1, last1 - (last2-first2))` 范围内的 `i`，使得对于每个不小于 `last2` 的非负整数 `n`，满足以下条件：*(i + n) == *(first2 + n)*，且 `pred*(i + n) != false`。如果 `[first1, last2]` 为空，则返回 true；否则如果没有找到迭代器，则返回 `last1`。
- 复杂度：最多有 `(last1 - first1) * (last2 - first2)` 次相应谓词的应用。

```cpp
template<class ForwardIterator, class Size, class T>
search(ForwardIterator first, ForwardIterator last, Size count,
      const T& value);

template<class ForwardIterator, class Size, class T,
      class BinaryPredicate>
search(ForwardIterator first, ForwardIterator last, Size count,
      const T& value, BinaryPredicate pred);
```

- 4. 要求：`Size` 必须可积分。
- 5. 影响：在序列中找到相等子序列。
- 6. 返回：返回 `[first, last)` 范围内的 `i`，使得对于每个小于 `count` 的非负整数 `n`，满足 `*(i + n) == value` 且 `pred*(i + n) != false`。如果没有找到迭代器，则返回 `last`。
- 7. 复杂度：最多 `first` 次谓词的应用。

```cpp
template<class ForwardIterator, class Searcher>
search(ForwardIterator first, ForwardIterator last,
      Searcher searcher);
```

- 8. 影响：等价于 `search(first, last)`。
- 9. 备注：`Searcher` 必须可拷贝。

# 28.6 复制 [alg.copy]

```cpp
template<class InputIterator, class OutputIterator>
copy(InputIterator first, InputIterator last,
      OutputIterator result);
```

- 1. 要求：`result` 不在 `[first, last]` 范围内。
- 2. 影响：将 `[first, last)` 中的元素复制到 `[result, result + (last - first))`。对于每个小于 `last - first` 的整数 `n`，执行 `*(result + n) = *(first + n)`。
- 3. 返回：`result + (last - first)`。
- 4. 复杂度：`first`。

```cpp
template<class ExecutionPolicy, class ForwardIterator, class OutputIterator>
copy(ExecutionPolicy&& exec,
      ForwardIterator first, ForwardIterator last,
      OutputIterator result);
```

- 5. 要求：范围不重叠。
- 6. 影响：将 `[first, last]` 中的元素复制到 `[result, result + (last - first))`。对于每个小于 `last - first` 的整数 `n`，执行 `*(result + n) = *(first + n)`。
- 7. 返回：`result + (last - first)`。
- 8. 复杂度：`first`。

```cpp
template<class InputIterator, class Size, class OutputIterator>
copy_n(InputIterator first, Size count,
      OutputIterator result);
```

- 1. 要求：`Size` 可积分。
- 2. 影响：对于每个小于 `count` 的整数 `i`，执行 `*(result + i) = *(first + i)`。
- 3. 返回：`result + count`。
- 4. 复杂度：`count`。

```cpp
template<class ExecutionPolicy, class ForwardIterator, class Size, class OutputIterator>
copy_n(ExecutionPolicy&& exec,
      ForwardIterator first, Size count,
      OutputIterator result);
```

- 5. 影响：对于每个小于 `count` 的整数 `i`，执行 `*(result + i) = *(first + i)`。
- 6. 返回：`result + count`。
- 7. 复杂度：`count`。

```cpp
template<class InputIterator, class OutputIterator, class BinaryPredicate>
copy_if(InputIterator first, InputIterator last,
      OutputIterator result, BinaryPredicate pred);
```

- 1. 要求：范围 `[first, last]` 和 `[result, result + (last - first))` 不重叠。
- 2. 注意：对于 `ExecutionPolicy` 的重叠，如果 `iterator_traits<InputIterator>::value_type` 不可构造，可能会有性能开销。
- 3. 影响：`[first, last)` 范围内所有满足 `pred(i)` 的元素。
- 4. 返回：结果范围的结束。
- 5. 复杂度：`first`。

```cpp
template<class ExecutionPolicy, class ForwardIterator, class OutputIterator, class BinaryPredicate>
copy_if(ExecutionPolicy&& exec,
      ForwardIterator first, ForwardIterator last,
      OutputIterator result, BinaryPredicate pred);
```

- 6. 要求：范围 `[first, last]` 和 `[result, result + (last - first))` 不重叠。
- 7. 影响：`[first, last)` 范围内所有满足 `pred(i)` 的元素。
- 8. 返回：结果范围的结束。
- 9. 复杂度：`first`。

```cpp
template<class BidirectionalIterator, class OutputIterator>
backward(BidirectionalIterator first, BidirectionalIterator last,
      OutputIterator result);
```

- 1. 要求：`result` 不在 `[first, last)` 范围内，也不在 `[result - (last-first), first)` 范围内，从 `last - 1` 开始一直到 `last`。
- 2. 影响：对于每个小于 `last - first` 的正整数 `n`，执行 `*(result - n) = *(last - n)`。
- 3. 返回：`result - (last - first)`。
- 4. 复杂度：`first`。

```cpp
template<class BidirectionalIterator, class Size, class OutputIterator>
copy_backward(BidirectionalIterator first, BidirectionalIterator last,
      OutputIterator result);
```

- 1. 要求：`result` 不在 `[first, last]` 范围内。
- 2. 影响：对于每个小于 `last - first` 的整数 `n`，执行 `*(result - n) = *(last - n)`。
- 3. 返回：`result - (last - first)`。
- 4. 复杂度：`first`。

```cpp
template<class InputIterator, class OutputIterator>
move(InputIterator first, InputIterator last, OutputIterator result);
```

- 1. 要求：`result` 不在 `[first, last]` 范围内。
- 2. 影响：将 `[first, last)` 中的元素移动到 `[result, result + (last - first))`。
- 3. 当 `last` 在范围 `[result - (last - first), result)` 内时，应该使用 `copy_backward` 而不是 `copy`。

