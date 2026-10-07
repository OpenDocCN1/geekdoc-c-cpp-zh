
## 25.5.6 Fill

```cpp
template<class ForwardIterator, class T>
void fill(ForwardIterator first, ForwardIterator last, const T& value);
```

```cpp
template<class OutputIterator, class Size, class T>
OutputIterator fill_n(OutputIterator first, Size n, const T& value);
```

- 要求：表达式 `value` 必须可写入输出迭代器。类型 `Size` 应能转换为整数类型 (`4.7`, `12.3`)。
- 影响：第一个算法通过范围 `[first,last)` 内的所有迭代器赋值 `value`。第二个算法在 `n` 为正数时，通过范围 `[first,first + n)` 内的所有迭代器赋值 `value`；否则什么都不做。
- 返回：`fill_n` 在 `n` 为非负值时返回 `first + n`，在 `n` 为负时返回 `first`。
- 复杂度：分别为恰好执行 `last — first`、`n` 或 `0` 次赋值。

## 25.3.7 Generate [alg.generate]

```cpp
template<class ForwardIterator, class Generator>
void generate(ForwardIterator first, ForwardIterator last, Generator gen);

template<class OutputIterator, class Size, class Generator>
OutputIterator generate_n(OutputIterator first, Size n, Generator gen);
```

- 1 影响：第一个算法调用函数 `gen`，并通过范围 `[first,last)` 内的所有迭代器赋值 `gen` 对象的返回值。第二个算法在 `n` 为正数时，调用 `gen` 并通过范围 `[first,first + n]` 内的所有迭代器赋值；否则什么都不做。
- 2 要求：`gen` 不接受参数。`Size` 应能转换为整数类型 (`4.7`, `12.3`)。
- 3 返回：`generate_n` 在 `n` 为非负值时返回 `first + n`，在 `n` 为负时返回 `first`。
- 4 复杂度：分别为恰好执行 `last — first`、`n` 或 `0` 次 `gen` 调用和赋值。

## 25.3.8 Remove [alg.remove]

```cpp
template<class ForwardIterator, class T>
remove(ForwardIterator first, ForwardIterator last, const T& value);

template<class ForwardIterator, class Predicate>
remove_if(ForwardIterator first, ForwardIterator last, Predicate pred);
```

- 1 要求：第一个 `first` 应满足移动赋值的要求（表 `22`）。
- 2 影响：消除范围 `[first,last]` 内所有由迭代器指的且满足以下条件的元素：`*i == value`, `pred(*i) != false`。
- 3 返回：结果范围的末尾。
- 4 备注：稳定的。
- 5 复杂度：恰好调用了 `last — first` 次相应的谓词。
- 6 注意：范围 `[ret,last)` 内（其中 `ret` 是返回的值）的每个元素都有一个有效但未指定的状态，因为算法可以通过交换或移动从原先在该范围内的元素来消除元素。

```cpp
template<class InputIterator, class OutputIterator, class T>
OutputIterator copy(InputIterator first, InputIterator last, OutputIterator result, const T& value);

template<class InputIterator, class OutputIterator, class Predicate>
OutputIterator copy_if(InputIterator first, InputIterator last, OutputIterator result, Predicate pred);
```

### 25.3.8 copy

要求：范围 `[first,last)` 和 `[result,result + (last - first)]` 不重叠。表达式 `result = *first` 必须有效。
- 影响：复制范围 `[first,last)` 内所有由迭代器指的且满足以下条件的元素：`*i == value`, `pred(*i) != false`。
- 返回：结果范围的末尾。
- 复杂度：`last - first` 次相应的谓词。

## 25.3.9 Unique [alg.unique]

```cpp
template<class ForwardIterator>
ForwardIterator unique(ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class BinaryPredicate>
ForwardIterator unique(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);
```

- 影响：消除范围 `[first,last)` 内连续的且满足以下条件的元素：`pred(*(i-1), *i)`。
- 要求：`first` 应满足移动赋值的要求（表 `22`）。
- 返回：结果范围的末尾。
- 复杂度：`last - first` 次相应的谓词。

```cpp
template<class InputIterator, class OutputIterator>
OutputIterator unique_copy(InputIterator first, InputIterator last);

template<class InputIterator, class OutputIterator, class BinaryPredicate>
OutputIterator unique_copy(InputIterator first, InputIterator last, BinaryPredicate pred);
```

- 要求：范围 `[first,last)` 和 `[result,result + (last - first))` 不重叠。表达式 `result = *first` 必须有效。
- 影响：复制范围 `[first,last)` 内所有满足以下条件的元素：`pred(*(i-1), *i)`。
- 返回：结果范围的末尾。
- 复杂度：`last - first` 次相应的谓词。

## 25.3.10 Reverse [alg.reverse]

```cpp
template<class BidirectionalIterator>
void reverse(BidirectionalIterator first, BidirectionalIterator last);
```

- 影响：反转范围 `[first,last)` 内由迭代器指的元素。
- 要求：`first` 应满足交换的要求 (`17.6.3.2`)。
- 复杂度：恰好 `(last - first)/2` 次交换。

```cpp
template<class BidirectionalIterator, class OutputIterator>
OutputIterator reverse_copy(BidirectionalIterator first, BidirectionalIterator last, OutputIterator result);
```

- 影响：将范围 `[first,last)` 反序复制到范围 `[result,result+(last - first))`。
- 要求：范围 `[first,last)` 和 `[result,result + (last - first))` 不重叠。表达式 `result = *first` 必须有效。
- 复杂度：恰好 `(last - first)/2` 次交换。

## 25.3.11 Rotate [alg.rotate]

```cpp
template<class ForwardIterator>
ForwardIterator rotate(ForwardIterator first, ForwardIterator middle, ForwardIterator last);
```

- 影响：旋转范围 `[first,last)` 内由迭代器指的元素，使 `middle` 指的元素成为第一个元素。
- 要求：`[first,last)` 有效。
- 返回：原先 `last` 处的元素之后的迭代器。
- 复杂度：`last - first` 次交换。

```cpp
template<class ForwardIterator, class OutputIterator>
OutputIterator rotate_copy(ForwardIterator first, ForwardIterator middle, ForwardIterator last, OutputIterator result);
```

- 影响：将范围 `[first,last)` 旋转到范围 `[result,result+(last - first))`，使 `middle` 指的元素成为第一个元素。
- 要求：范围 `[first,last)` 和 `[result,result + (last - first))` 不重叠。表达式 `result = *first` 必须有效。
- 返回：原先 `last` 处的元素之后的迭代器。
- 复杂度：`last - first` 次交换。

## 25.3.12 随机洗牌

> [alg.random.shuffle]

```cpp
template<class RandomAccessIterator>
void random_shuffle(RandomAccessIterator first, RandomAccessIterator last);
```

```cpp
template<class RandomAccessIterator, class RandomNumberGenerator>
void random_shuffle(RandomAccessIterator first, RandomAccessIterator last, RandomNumberGenerator&& rand);
```

```cpp
template<class RandomAccessIterator, class UniformRandomNumberGenerator>
void random_shuffle(RandomAccessIterator first, RandomAccessIterator last, UniformRandomNumberGenerator&& g);
```

- 1. 效果：置乱范围 `[first,last)` 内的元素，使得这些元素的每种排列组合出现的概率相等。
- 2. 要求：`RandomAccessIterator` 应当满足 `ValueAndSwapable(17.6.3.2)` 的要求。随机数生成对象 `rand` 的返回类型应可转换为 `iterator_traits<RandomAccessIterator>::difference_type`，且当 `n > 0` 时，调用 `rand(n)` 应返回范围 `[0,n)` 内一个随机选择的类型为 `iterator_traits` 的值。`UniformRandomNumberGenerator` 类型应满足均匀随机数生成器 (`26.5.1.3`) 的要求，其类型返回可转换为 `iterator_traits<RandomAccessIterator>::difference_type`。
- 3. 复杂度：恰好为 `(last - first)` 次交换。
- 4. 备注：为了确保这些函数的实现使用了随机数，实现应当是良定义的。实现可以使用标准 C 库中的 `rand` 函数。

第一种形式函数的随机数底层源是由实现定义的。实现可以使用标准 C 库中的 `rand` 函数。

在函数的第二种形式中，函数对象 `g` 应当是该实现的随机性源。

在函数的第三种形式中，对象 `g` 应当作为该实现的随机性源。

## 25.3.13 分区

> [alg.partitions]

```cpp
template<class InputIterator, class Predicate>
bool is_partitioned(InputIterator first, InputIterator last, Predicate pred);
```

- 1. 要求：`InputIterator` 的值应可转换为 `Predicate` 的参数类型。
- 2. 返回：如果 `[first,last)` 为空或如果 `[first,last)` 被 `pred` 分区（即所有满足 `pred` 的元素都出现在不满足 `pred` 的元素之前），则返回 `true`。
- 3. 复杂度：线性。最多应用 `last - first` 次 `pred`。

```cpp
template<class ForwardIterator, class Predicate>
ForwardIterator partition(ForwardIterator first, ForwardIterator last, Predicate pred);
```

- 要求：`ForwardIterator` 的值类型必须必须可转换为 `Predicate` 的参数。类型 `[first,last)` 应当被 `pred` 分区，即所有满足 `pred` 的元素都出现在不满足 `pred` 的元素之前。
- 返回：一个迭代器 `mid`，使得 `all_of(first, mid, pred)` 和 `none_of(mid, last, pred)` 均为真。
- 复杂度：`O(log(last - first))` 次 `pred` 应用。

## 25.4 排序及相关操作 [alg.sorting]

`25.4` 中的所有操作都有两个版本：一个接受类型为 `Compare` 的函数对象，另一个使用运算符 `<`。

`Compare` 是一个函数对象类型 (`20.8`)。当应用于类型为 `Compare` 的函数调用时，其返回值在上下文中转换为 `bool(i)`，如果调用的第一个参数小于第二个参数，则返回 `true`，否则返回 `false`。`comp` 是用于使用排序关系的算法的函数对象。假设 `comp` 不会通过解引用迭代器应用任何非常数函数。

对于所有接受 `Compare` 的算法，都有一个使用运算符的版本。即 `comp(i, *j)` 默认为 `i < j`。对于其他使用 `25.4.3` 以确保正确工作的算法，`comp` 在值上具有严格弱序。

严格序指的是不可归约反射的要求（对于所有 `x`，`!comp(x, x)` 成立），而弱序指的是其强度不强于全序，但强于偏序的要求。如果我们定义 `equiv(a, b)` 为 `!comp(a, b) && !comp(b, a)`，那么这些要求是 `comp` 和 `equiv` 必须是传递关系。

```cpp
comp(a, b) && equiv(b, c) implies comp(a, c)
```

```cpp
equiv(a, b) && equiv(b, c) implies equiv(a, c)
```

注: 在这些条件下，可以证明

```cpp
equiv 是一个等价关系
```

```cpp
comp 在 equiv 确定的等价类上诱导出一个良定义的关系
```
