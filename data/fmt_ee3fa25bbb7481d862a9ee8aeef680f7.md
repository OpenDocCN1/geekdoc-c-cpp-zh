
13 当通过传递比较对象构造关联容器时，容器不应存储对所传递对象的指针或引用，即使该对象是通过引用传递的。当通过拷贝构造函数或赋值运算符拷贝关联容器时，如果该比较对象在构造函数中已传递给目标容器，则目标容器应使用从拷贝而来的比较对象。

14 当 `qualified-id::is_transparent` 有效且派生出类型（13.10.3）时，成员函数模板 `find`, `contains`, `lower_bound`, `upper_bound` 和 `equal_range` 不参与重载解析。

15 如果以下任一情况为真，则关联容器的推导不参与重载解析：

- (15.1) 它有一个 `Allocator` 模板参数，且推导出的类型不符合该参数的输入迭代器。
- (15.2) 它有一个 `Allocator` 模板参数，且推导出的类型不符合分配器的要求。
- (15.3) 它有一个 `Compare` 模板参数，且推导出的类型符合分配器的要求。

## 22.2.6 异常保证 [associative.req.except]

- 1 对于关联容器，`clear()` 不抛出异常，除非容器的比较操作器抛出异常。
- 2 对于关联容器，`erase` 不抛出异常，除非插入操作 `insert` 抛出异常。
- 3 对于关联容器，`swap` 不抛出异常，除非容器的比较操作器抛出异常。

## 22.2.7 无序容器

### 22.2.7.1 通用 [unord.req]

- 1 无序容器提供了基于键的快速检索能力。操作的最坏情况复杂度是线性的，但平均情况要快。
- 2 无序容器符合 (22.2) 的要求，对于 `unordered_set` 和 `unordered_multiset`，`value_type` 的要求适用于 `key_type`。
- 5 两个 `k1` 和 `k2` 被视为相等，如果无序容器的谓词 `pred(k1, k2)` 有效且返回 true。
> 注意：当无序容器使用非默认哈希函数实例化时，通常需要

- 6 无序容器每个哈希支持最多一个元素，否则支持等价键。
- 7 对于 `unordered_set` 和 `unordered_multiset`，值即键。
- 8 对于同一容器中的任意两个键 `k1` 和 `k2`，`hash(k1)` 和 `hash(k2)` 应返回相同的值。
- 9 无序容器的元素与桶（buckets）相关。具有相同哈值的键放置在一起。重哈（Rehashing）使迭代器失效。
- 10 无序容器满足所有分配器感知 (22.1) 的要求，对于 `unordered_map` 和 `unordered_multimap`。
- 11 在表 81 中：
  - `X` 关联容器类
  - `a` `X` 的值
  - `a2` 与类型 `X` 兼容的类型（表 79）
  - `b` `X` 的可能常量值
  - `a_unique` `X` 支持唯一键时 的 的
  - `a_tran` 当 `X::key::is_transparent` 和 `X::hasher` 均有效时 `X` 的可能常量值（13.10.3）
  - `i` 和 `j` 指向 `value_type` 的迭代器
  - `[i, j]` 有效范围
  - `p` 和 `q2` 指向 `a` 的迭代器
  - `q` 和 `q1` 指向 `a` 的常量迭代器
  - `r` 指向 `a` 的迭代器
  - `[q1, q2]` `a` 中的有效范围
  - `el` `initializer_list<value_type>` 的值
  - `t` 类型 `X::value_type` 的值
  - `k` `key_type` 的值
  - `hf` `hasher` 的可能常量值
  - `eqq` `key_equal` 的可能常量值
  - `ke` 是满足 `eqq(r1, ke) == eq(ke, r1)` 的值，当 `eq(r1, ke)` 为真时，`h(r1) == hf(ke)`，且当 `eq(r1, ke) && eq(r1, r2)` 时，`eq(r2, ke)`，其中 `r1` 和 `r2` 是 `a` 中元素的键
  - `dotes` `size_type` 类型的值
  - `dotes` `float` 类型的值
  - `nh` `X::node_type` 类型的非常量值。

## 表 81: 无序关联容器要求（除 container 之外）[tab:container.hash.req]

| 表达式 | 返回类型 | 断言/备注前/后置 | 复杂度 |
|---|---|---|--|
| `X::key_type` | `Key` | | |
| `X::mapped_type` (仅限 `unordered_map` 和 `unordered_multimap`) | `T` | | 编译时 |
| `X::value_type` (仅限 `unordered_set` 和 `unordered_multiset`) | `Key` | 前置条件：`value_type` 是 `X` 的 `Cpp17Erasable` | 编译时 |
| `X::value_type` (限 `unordered_map` 和 `unordered_multimap`) | `pair<const Key, T>` | 前置条件：`value_type` 是 `X` 的 `Cpp17Erasable` | 编译时 |
| `X::hasher` | `Hash` | 前置条件：`Hash` 是一个元函数类型，使得表达式 `hf (k)` 的大小为 `size_t` | 编译时 |
| `X::key_equal` | `Pred` | 前置条件：`Pred` 满足 `Cpp17Constructible` 要求。`Pred` 是一个接受两个 `Key` 类型参数的二元谓词。`Pred` 是等价关系。 | | |
| `X::local_iterator` | 一个类别、值类型、差值类型和指针引用类型与 `X::iterator` 相同的迭代器 | `local_iterator` 对象可用于遍历单个桶，但不能用于跨桶遍历。 | 编译时 |
| `X::const_iterator` | 一个类别、值类型、差值类型和指针引用类型与 `X::const_iterator` 相同的迭代器 | `const_local_iterator` 对象可用于遍历单个桶，但不能用于跨桶遍历。 | 编译时 |
| `X::node_type` | 节点句柄句模板的特化版本，其公共嵌套类型与 `X` 中对应的类型相同。 | 见 22.2.4 | 编译时 |
| `X(n, hf, eq)` `X a(n, hf, eq);` | `X` | 影响：构造函数构造一个包含至少 `n` 个桶的空容器，使用 `hf` 作为哈希函数，`eq` 作为键谓词。 | `O(n)` |

## 表 81: 无序关联容器要求（除 container 之外）（续）

| 表达式 | 返回类型 | 断言/备注前/后置 | 复杂度 |
|---|---|---|n|
| `X(n, hf)` `X a(n, hf);` | `X` | 前置条件：`key_equal` 满足 `CDefaultConstructible` 要求。影响：构造一个包含至少 `n` 个桶的空容器，使用 `h` 作为哈希函数，`key_equal()` 作为键等价谓词。 | `O(n)` |
| `X(n)` `X a(n);` | `X` | 前置条件：`hasher` 和 `key_equal` 满足 `C17DefaultConstructible` 要求。影响：构造一个包含至少 `n` 个桶的空容器，使用 `hasher()` 作为哈希函数，`key_equal()` 作为键等价谓词。 | `O(n)` |
| `X()` `X a;` | `X` | 前置条件：`hasher` 和 `key_equal` 满足 `C17DefaultConstructible` 要求。影响：构造一个具有未数量桶的空容器，使用 `hasher()` 和 `key_equal()` 作为键等价谓词。 | 常数 |
| `X(i, j, n, hf, eq)` `X a(i, j, n, hf, eq);` | `X` | 前置条件：`value_type` 可从 `*1*` 处替换到 `X` 中。影响：构造一个包含至少 `n` 个桶的空容器，使用 `hf` 作为哈希函数，`eq` 作为等价谓词，并将元素 `(i, j)` 插入其中。 | 平均情况 `O(N)` (`N` 是 `distance(i, j)`), 最坏情况 `O(N^2)` |
| `X(i, j, n, hf)` `X a(i, j, n, hf);` | `X` | 前置条件：`key_equal` 满足 `C1DefaultConstructible` 要求。`value_type` 可从 `*1*` 处替换到 `X` 中。 影响：构造一个包含至少 `n` 个桶的空容器，使用 `hf` 作为哈希函数，`key_equal()` 作为键等价谓词，并将元素 `(i, j)` 插入其中。 | 平均情况 `O(N)` (`N` 是 `distance(i, j)`), 最坏情况 `O(N^2)` |

## 22.2.7.2 异常安全性

对于无序关联容器，`clear()` 函数抛出异常。`erase(k)` 不抛出异常，除非容器的 `Hash` 或 `Pred` 对象抛出了异常。

对于无序关联容器，如果插入元素时，除容器哈希函数以外的操作抛出异常，则插入操作无效。

对于无序关联容器，`swap` 函数抛出异常，除非容器的 `Hash` 或 `Pred` 对象抛出了异常。

对于无序关联容器，如果 `rehash()` 函数内部由除容器哈希函数或比较函数以外的代码抛出异常，则 `rehash()`无效。

## 22.3 序列容器

### 22.3.1 通用

`<array>`22.3)、`<deque>`22.3)、`<forward_list>`22.4)、`<list>`22.5) 和 `<vector>`22.6) 定义了满足序列容器要求的类模板。

以下异常别名模板可能出现在序列容器的推导指南中：

```cpp
```
