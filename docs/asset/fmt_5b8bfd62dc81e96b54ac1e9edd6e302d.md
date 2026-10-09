
- `2.` 令 `a` 和 `b` 为可引用迭代器，`c` 为 `I` 的非引用类型，使得 `b` 从 `a` 可达且 `c` 从 `b` 可达，并令 `D` 为 `difference_t<I>`。仅当满足以下条件时模型 `contiguous_iterator`：
`address(a) == address(*b)`
`address(b) == to_address(a) + D(c - a)`.

# 23.3.5 C++17 器要求

## 通用
在以下意义下，`a` 和 `b` 表示类型 `X` 或 `const X` 的值，`difference_type` 和 `reference` 分别引用 `iterator_traits<X>::difference_type` 和 `iterator_traits<X>::reference`，`n` 表示 `difference_type` 的值，`u`, `t` 和 `m` 表示迭代器，`r` 表示 `X` 的值，`T` 表示某些与输出迭代器可交换的值。
> [注：对于迭代器类型 `X`，必须是 `iterator_traits<X>` 的实例化 (23.3.2)。-- 结束注]

### 23.3.5.2 C++17Iterator
`C++17` 要求遵循迭代器的基本事实；该要求允许对迭代器进行操作和增加迭代器。大多数算法需要额外的操作来使用 (23.3.5.5, 23.3.5.6) 或 (23.3.5.4) 值，或者提供更丰富的迭代器移动。

类型满足 `C++17Iterator` 要求：
- `X` 满足 `C++17Constructible`、`C++17CopyAssignable` 以及 `C++17Destructible` 要求 (16.4.2)，且类型 `X` 的值可交换 (16.4.4)，并且
- `iterator_traits<X>::difference_type` 是符号整数类型或 `void`，表 84 中的表达式有效且具有指定的语义。

表 84: `C++17Iterator` 要求 [iterator]

| 表达式 | 返回类型 | 操作语义 | 断言/注前提/后条件 |
| --- | --- | --- | --- |
| `*r` | 未指定 | | 前提：`r` 是可引用的。 |
| `++r` | | | |

### 23.3.5.3 输入迭代器
如果类或指针类型 `X` 满足值 `T` 的输入迭代器 `C++17Iterator` (23.3.5.2) 要求以及 `C++17EqualityComparable` (表 25) 要求，且表 85 中的表达式有效并具有指定的语义。

在表 85 中，`==` 的域在普通意义下表示定义定义的值集合。这会随时间变化。每个算法对其使用的迭代器值的 `==` 域提出要求。这些要求可以通过使用 `==` 和 `!=` 的算法推断出来。

> [示例：1：`find(a,b,x)` 仅当值 `x` 如下属性 `p` 时才定义：`b` 有属性 `p` 且当 `(*x==b)` 或 `(*++x` 和 `++i` 有 `p`) 时 `a` 有属性 `p` -- 结束示例]

表 85: `C++17Input` 要求（`C++17Iterator` 之外）

| 表达式 | 返回类型 | 操作语义 | 断言/注前提/后条件 |
| --- | --- | --- | --- |
| `a == b` | | | 前提：`a` 在 `==` 的域内 |
| `*a` | `reference`, 可转换为 `T` | | 前提：`a` 是可引用的。 |
| `*r` | | | 前提：`a` 在 `==` 的域内 |
| `++r` | | | 前提：`r` 是可引用的。后条件：`r` 是可引用的或 `r` 在末尾。 |
| `*r++` | 可转换为 `T` | `{ T tmp = *r; ++r; return tmp; }` | |

### 23.3.5.4 输出迭代器
- 如果类或指针类型 `X` 满足 `C++17Iterator` 要求 (23.3.5.2)，且表 86 中的表达式有效并具有指定的语义，则 `X` 满足输出迭代器的要求。

表 86: `C++17OutputIterator` 要求（`C++17Iterator` 之外）[taboutiterator]

| 表达式 | 返回类型 | 操作语义 | 断言/注前提/后条件 |
| --- | --- | --- | --- |
| `*r = o` | 结果未使用 | | 备注：此操作后 `r` 不需要是可引用的。后条件：`r` 是可增的。 |
| `++r` | `X&` | | `address_of() == address(++r)`。备注：此操作后 `r` 不需要是可引用的。后条件：`r` 是可增的。 |
| `r++` | 可转换为 `const X&` | `{ X tmp = r; ++r; return tmp; }` | 备注：此操作后 `r` 不需要是可引用的。后条件：`r` 是可增的。 |
| `*r++ = o` | 结果未使用 | | 备注：此操作后 `r` 不需要是可引用的。后条件：`r` 是可增的。 |

# ISO/IEC 14882:2020(E)

2 建议：在输出迭代器上实现算法时不应尝试多次通过同一个迭代器；此类算法应为单次通过算法（single-pass algorithm）。

> [注 1：运算符 `=*` 使用在赋值语句的左侧。相等和不相等关系不一定定义。]

## 23.3.5.5 前向迭代器 [forward.iterators]

1 如果类或指针类型 `x` 满足前向迭代器的要求，如果：

- (1.1) `x` 满足 `Cpp17InputIterator` 的要求 (23.3.5.5)。
- (1.2) `x` 满足 `Cpp17ForwardConstructible` 的要求 (16.4.4.2)。
- (1.3) 如果 `x` 是可变迭代器，引用为 `T`；如果 `x` 是常量迭代器，引用为 `const T`；
- (1.4) 表格 87 中的表达式是有效的且具有指示的语义，并且
- (1.5) 类型为 `X` 的对象提供下述的多通过保证（multi-pass guarantee）。

2 `==` 的域确保两个迭代器都指向同一个底层序列。然而，值初始化的迭代器可以与相同类型的其他值初始化迭代器进行比较并相等。

> [注 1：值初始化的迭代器的行为就像它们指向了同一序列的末尾之后。]

类型为 `X` 的两个解引用迭代器 `a` 和 `b` 满足多通过保证，如果：

- (3.1) `a == b++ == ++b`
- (3.2) `x` 是指针或表达式 `(void++)*x` 的类型，相当于表达式 `*a`。

> [注 2：对 `a == b++ == ++b` 的要求（这在输出迭代器和前向迭代器上不成立）以及对可变迭代器非 const 部分限制的移除（适用于输出迭代器），允许了多通过单向前向迭代器的使用。]

表格 87：`Cpp17ForwardIterator` 的要求（除 `Cpp17InputIterator` 之外）[tab:forwardIterator]

| 表达式 | 返回类型 | 操作语义 | 断言/注 前/后置条件 |
|---|---|---|---|
| `r++` | 可转换为 `const X` | `{ X tmp = r; ++tmp; return tmp; }` | |
| `*r` | 引用 | | |

5 如果 `a` 和 `b` 相等，则要么 `a` 和 `b` 都是可解引用的，或者都是不可解引用的，

6 如果 `a` 和 `b` 都是可解引用的，则 `a == b` 当且仅当 `*a` 和 `*b` 绑定到同一个对象上。

## 23.3.5.6 双向迭代器 [bidirectional.iterators]

1 如果类或指针类型 `x` 满足双向迭代器的要求，除了满足 `Cpp17ForwardIterator` 的要求外，表 88 所示的以下表达式是有效的。

> [注 2：双向迭代器允许算法向后移动与向前移动等量的距离。]

## 23.3.5.7 随机访问迭代器 [random.access.iterators]

1 如果类或指针类型 `x` 满足随机访问迭代器的要求，除了满足 `Cpp17BidirectionalIterator` 的要求外，表 89 所示的以下表达式是有效的。

表格 88：`Cpp17BidirectionalIterator` 的要求（除 `Cpp17ForwardIterator` 之外）[tab:bidirectionaliterator]

| 表达式 | 返回类型 | 操作语义 | 断言/注 前/后置条件 |
|---|---|---|---|
| `--r` | `X&` | | 前置条件：存在 `s` 使得 `r == ++s`。后置条件：`r` 是 `--((++)) = r`。`--r == --s` 意味着 `r == s`。`address(r) = address(--r)`。 |
| `r--` | 可转换为 `const X&` | `{ X tmp = r; --; return tmp; }` | | |
| `*--` | 引用 | | |

表格 89：`Cpp17RandomAccessIterator` 的要求（除 `Cpp17BidirectionalIterator` 之外）[tab:randomiterator]

| 表达式 | 返回类型 | 操作语义 | 断言/注 前/后置条件 |
|---|---|---|---|
| `r += n` | `X&` | `{ difference_type m = n; if (m--) ++r; else while (m++); --r; return r; }` | | |
| `a + n` | `X` | `{ X tmp = a; tmp += n; return tmp; }` | `a + n == n + a.` |
| `r = n` | `X&` | `r += -n;` | | 前置条件：`n` 的绝对值在 `difference_type` 的表示范围内。 |
| `a - n` | `X` | `{ X tmp = a; tmp -= n; return tmp; }` | 前置条件：存在 `difference_type` `n` 使得 `a + n == b`。 |
| `a[n]` | 可转换为引用 | `*(a + n)` | |
| `a < b` | 可转换为 `bool` | `b - a > 0` | 是全序关系 |
| `a > b` | 可转换为 `bool` | `b < a` | 是全序关系的反向 |
| `a >= b` | 可转换为 `bool` | `!(a < b)` | |

表格 89（续）：`Cpp17RandomAccessIterator` 的要求（除 `Cpp17BidirectionalIterator` 之外）

| 表达式 | 返回类型 | 断言/注 前/后置条件 |
|---|---|---|
| `a == b` | 可转换为 `bool`。 | `!(a > b)` |

### 23.3.5.6 间调用要求 [indirectcallable]

#### 23.3.5.6.1 General [indirectcallable.general]

- 有若干额外的概念用于对将调用对象作为参数的算法分组。

#### 23.3.5.6.2 Indirect callables [indirectcallable]

- 间接调用概念用于约束接受调用对象的算法。

```cpp
namespace std {
template<class F>
concept indirectly_unary_invocable =
indirectly_readable<F> &&
invocable<copy_constructible<F>, iter_value_t<I>> &&
invocable<F&, iter_reference_t<I>> &&
invocable<F&, common_reference_t<I>> &&
common_reference_t<
invoke_result<F, iter_value_t<I>>,
invoke_result<F, iter_reference_t<I>>>
template<class F, class I>
concept indirectly_unary_invocable =
indirectly_readable<F> &&
copy_constructible<F> &&
regular_invocable<F, iter_value_t<I>> &&
regular_invocable<F, iter_reference_t<I>> &&
regular_invocable<F, common_reference_t<I>> &&
common_reference_t<
invoke_result<F, iter_value_t<I>>,
invoke_result<F, iter_reference_t<I>>>
template<class F>
concept indirectly_unary_predicate =
indirectly_readable<F> &&
copy_constructible<F> &&
predicate<F, iter_value_t<I>> &&
predicate<F, iter_reference_t<I>> &&
predicate<F, common_reference_t<I>>;
template<class F, class I1, class I2>
concept indirectly_binary_predicate =
indirectly_readable<I1> && indirectly_readable<I2> &&
copy_constructible<F> &&
predicate<F, iter_value_t<I1>, iter_value_t<I2>> &&
predicate<F, iter_value_t<I1>, iter_reference_t<I2>> &&
predicate<F, iter_reference_t<I1>, iter_value_t<I2>> &&
predicate<F, iter_reference_t<I1>, iter_reference_t<I2>> &&
predicate<F, common_reference_t<I1>, common_reference_t<I2>>;
template<class F, class I1, class I2 = I1>
concept indirectly_equivalence_relation =
indirectly_readable<I1> && indirectly_readable<I2> &&
copy_constructible<F> &&
equivalence_relation<F, iter_value_t<I1>, iter_value_t<I2>>;
}
```

```cpp
equivalence_relation<P8, iter_reference_t<I1>, iter_reference_t<I2>> &&
equality_relation<P8, iter_value_t<I1>, iter_value_t<I2>> &&
equality_relation<P8, iter_reference_t<I1>, iter_reference_t<I2>> &&
equivalence_relation<P8, common_reference_t<I1>, common_reference_t<I2>>;
template<class F, class I1, class I2 = I
concept indirect_direct_work_order =
indirectly_readable<I1> && indirectly_readable<I2> &&
copy_constructible<F>
strict_weak_order<P8, iter_value_t<I1>, iter_value_t<I2>> &&
strict_weak_order<P8, iter_value_t<I1>, iter_reference_t<I2>> &&
strict_weak_order<P8, iter_reference_t<I1>, iter_value_t<I2>> &&
strict_weak_order<P8, iter_reference_t<I1>, iter_reference_t<I2>> &&
strict_weak_order<P8, common_reference_t<I1>, common_reference_t<I2>>;
```

## 23.6.3 Class template projected [projected]

1 类模板 `projected` 用于约束接受类对象和投影的算法 (3.39)。它结合了间接读取类型 `I` 可以接受类对象 `Pro`；其引用类型是 `Pro` 作用于 `I` 的 `iter_reference_t` 的结果。

```cpp
namespace std {
template<indirectly_readable<I>
```

3 让 `i` 为类型为 `In` 的可解引用值。`In` 和 `Out` 满足 `indirectly_movable_storage<In, Out>`，当且仅当在对象 `obj` 初始化后：
`iter_value_t<In> obj(ranges::iter_move(i));`

`obj` 等于之前由 `*i` 所指代的值。如果 `iter_reference_t<In>` 是引用类型，则 `*i` 指代的值的最终状态是有效的，除非满足 (16.4.6.16)。

## 23.7.3.7 Concept indirectly_copable

`indirectly_copable` 概念规定了间接可读类型与直接可写类型之间的关系，这些类型的值可以被拷贝。

```cpp
template<class In, class Out>
concept indirectly_copable =
indirectly_readable<In> &&
directly_writable<Out, iter_reference<In>>;
```

`indirectly_copable_storage` 概念在 `indirectly_copable` 的基础上增加了额外的要求，允许转移通过 `indirectly_readable` 类型的值类型的中间对象进行。它还要求具备创建值拷贝的能力。

```cpp
template<class In, class Out>
```
