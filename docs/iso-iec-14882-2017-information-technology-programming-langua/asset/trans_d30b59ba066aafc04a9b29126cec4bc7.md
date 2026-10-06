

# ISO/IEC 14882:2017(E)

## 28.6.8 Remove [alg.remove]

```cpp
template<class ForwardIterator, class T>
ForwardIterator remove(ForwardIterator first, ForwardIterator last,
    const T& value);
template<class ExecutionPolicy, class ForwardIterator, class T>
ForwardIterator remove(ExecutionPolicy&& exec,
                               ForwardIterator first, ForwardIterator last,
                               const T& value);

template<class ForwardIterator, class Predicate>
ForwardIterator remove_if(ForwardIterator first, ForwardIterator last,
    Predicate pred);
template<class ExecutionPolicy, class ForwardIterator, class Predicate>
ForwardIterator remove_if(ExecutionPolicy&& exec,
                               ForwardIterator first, ForwardIterator last,
                               Predicate pred);
```

- 1 需求：*first* 的类型必须满足移动赋值要求（表 25）。
- 2 效果：遍历范围 [first, last) 中所有由 *i* 指向的元素，对于满足以下条件：*i == value, pred(*i) != false*。
- 3 返回：范围的末尾。
- 4 备注：稳定（20.5.5.7）。
- 5 复杂度：恰好调用相应的谓词 last - first 次。
- 6 注意：范围 [ret, last) 中的每个元素（其中 ret 是返回的值）都处于一个有效但未指定的状态；算法可以从原始范围内的元素中移除元素。-- 注意结束

```cpp
template<class InputIterator, class OutputIterator, class T>
OutputIterator
remove_copy(InputIterator first, InputIterator last,
    OutputIterator result, const T& value);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class T>
ForwardIterator2
remove_copy(ExecutionPolicy&& exec, ForwardIterator1 first, ForwardIterator1 last,
                               ForwardIterator2 result, const T& value);

template<class InputIterator, class OutputIterator, class Predicate>
OutputIterator
remove_if(InputIterator first, InputIterator last,
    OutputIterator result, Predicate pred);
template<class ExecutionPolicy, class ForwardIterator1, class ForwardIterator2, class Predicate>
ForwardIterator2
remove_if(ExecutionPolicy&& exec, ForwardIterator1 first, ForwardIterator1 last,
                               ForwardIterator2 result, Predicate pred);
```

- 7 需求：范围 [first, last) 和 [result, result + (last - first)) 不应重叠。表达式 *result = *first* 应该是有效的。| 注意：对于 ExecutionPolicy 的重叠，如果 iterator_traits<ForwardIterator1>::value_type 是可移动构造的（表 23），可能会有性能代价。-- 注意结束
- 8 效果：拷贝范围 [first, last) 中所有由 *i* 指向的元素，当这些元素不满足以下对应条件：*i == value, pred(*i) != false*。
- 9 返回：结果范围的末尾。
- 10 复杂度：恰好调用相应的谓词 last – first 次。
- 11 备注：稳定（20.5.5.7）。

## 28.6.9 Unique [alg.unique]

```cpp
template<class ForwardIterator>
ForwardIterator unique(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator unique(ExecutionPolicy&& exec, ForwardIterator first);
```

```cpp
template<class ForwardIterator, class BinaryPredicate>
ForwardIterator unique(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);
template<class ExecutionPolicy, class BinaryPredicate>
ForwardIterator unique(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, BinaryPredicate pred);
```

- 1 需求：该函数应该是一个等价关系。*first* 的类型必须满足移动赋值要求（表 25）。
- 2 效果：对于非空范围，对于范围 [first + 1, last) 中由迭代器指向的每组连续等价元素，移除除第一个元素以外的所有元素，这些元素满足条件：*(i - 1) == *i && pred(*i) != false*。
- 3 返回：范围的末尾。
- 4 复杂度：对于非空范围，恰好调用相应的谓词 (last – first) – 1 次。

```cpp
template<class InputIterator, class OutputIterator>
OutputIterator unique_copy(InputIterator first, InputIterator last, OutputIterator result);
template<class ExecutionPolicy, class InputIterator, class ForwardIterator2>
ForwardIterator2 unique_copy(ExecutionPolicy&& exec, InputIterator first, InputIterator last, ForwardIterator2 result);
```

```cpp
template<class InputIterator, class BinaryPredicate>
OutputIterator unique_copy(InputIterator first, InputIterator last, OutputIterator result, BinaryPredicate pred);
template<class ExecutionPolicy, class InputIterator, class ForwardIterator2>
ForwardIterator2 unique_copy(ExecutionPolicy&& exec, InputIterator first, InputIterator last, ForwardIterator2 result, BinaryPredicate pred);
```

- 5 需求：
(5.1) 比较函数应该是等价的。
(5.2) 范围 [first, last) 和 [result, result+(last-first)) 不应重叠。
(5.3) 表达式 *result = *first* 应该是有效的。
(5.4) 对于带有 ExecutionPolicy 的重载，令 T 为 InputIterator 的值类型。如果 InputIterator 满足向前迭代器要求，则对 T 没有额外要求。否则，如果 InputIterator 满足向前迭代器要求，则 T 等同于可赋值的（表 36）。对于带有 ExecutionPolicy 的重载，T 应该是可构造的（表 24）。-- 注意
- 6 效果：对于范围 [first, last) 中由迭代器指向的每组连续等价元素，保留第一个元素，满足条件：*i == value, pred(*i) != false*。
- 7 返回：结果范围的末尾。
- 8 复杂度：相应的谓词。

## 28.6.10 Reverse

```cpp
template<class BidirectionalIterator>
void reverse(BidirectionalIterator first, BidirectionalIterator last);
template<class ExecutionPolicy, class BidirectionalIterator>
void reverse(ExecutionPolicy&& exec, BidirectionalIterator first);
```

- 1 需求：BidirectionalIterator 必须满足可交换要求（20.5.3）。
- 2 效果：对于非负整数 i < (last – first)，交换对应位置的元素。
- 3 返回：无（void）。
- 4 复杂度：(last – first) / 2。

```cpp
template<class BidirectionalIterator, class OutputIterator>
OutputIterator reverse_copy(BidirectionalIterator first, BidirectionalIterator last, OutputIterator result);
template<class ExecutionPolicy, class BidirectionalIterator, class OutputIterator>
OutputIterator reverse_copy(ExecutionPolicy&& exec, BidirectionalIterator first, BidirectionalIterator last, OutputIterator result);
```

- 5 需求：BidirectionalIterator 必须满足向前迭代器要求（27.2.5）。
- 6 效果：对于非负整数 i < (last – first) / 2，交换对应位置的元素。
- 7 返回：结果范围的末尾。
- 8 复杂度。

## 28.6.11 Rotate

```cpp
template<class ForwardIterator>
void rotate(ForwardIterator first, ForwardIterator middle, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
void rotate(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator middle, ForwardIterator last);
```

- 1 需求：ForwardIterator 必须满足向前迭代器要求（27.2.6）。
- 2 效果：对于每个非负整数 i < (last - first)，将 first + i 元素移动到位置 (i + (middle - first)) % (last - first)。
- 3 返回：first + (last - first)。
- 4 备注：这是一个左旋转。
- 5 复杂度：最多 last - first 次交换。

```cpp
template<class ForwardIterator, class OutputIterator>
OutputIterator rotate_copy(ForwardIterator first, ForwardIterator middle, ForwardIterator last, OutputIterator result);
template<class ExecutionPolicy, class ForwardIterator, class OutputIterator>
OutputIterator rotate_copy(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator middle, ForwardIterator last, OutputIterator result);
```

- 6 需求：ForwardIterator 必须满足向前迭代器要求（27.2.6）。
- 7 效果：对于每个非负整数 i < (last - first)，将 first + i 元素移动到位置 (i + (middle - first)) % (last - first)。
- 8 返回：result + (last - first)。
- 9 复杂度：恰好 last - first 次赋值。

## 28.6.12 Sample [alg.random.sample]

```cpp
template<class PopulationIterator, class SampleIterator,
class Distance, class UniformRandomGenerator>
SampleIterator sample(PopulationIterator first, PopulationIterator last,
SampleIterator out, Distance n,
UniformRandomGenerator& g);
```

- 1 需求：
(1.1) PopulationIterator 必须满足输入迭代器要求（27.2.3）。
(1.2) SampleIterator 必须满足输出迭代器要求（27.2.4）。
(1.3) 除非 PopulationIterator 满足向前迭代器要求，否则 SampleIterator 必须满足访问迭代器的额外要求（27.2.7）。
(1.4) PopulationIterator 的值类型对 out 可写入（27.2.1）。
(1.5) Distance 必须是整数。
(1.6) remove_reference_t<UniformRandomGenerator> 应当满足均匀随机数生成器的要求（29.6.1.3），其返回类型可转换为 Distance。
(1.7) out 不在范围 [first, last] 中。

