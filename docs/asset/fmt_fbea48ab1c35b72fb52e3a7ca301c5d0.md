
### B.5.3 实用算法

从技术上讲，这些实用算法也是修改序列算法，但我们认为将它们单独列出来是个好主意，以免它们被遗漏。

| 实用算法 | 描述 |
| :--- | :--- |
| `swap(x, y)` | 交换 x 和 y。 |
| `iter_swap(p, q)` | 交换 `*p` 和 `*q`。 |
| `swap_ranges(b, e, b2)` | 交换 `[b : e]` 和 `[b2 : b2 + (e-b)]` 中的元素。 |
| `fill(b, e, v)` | 将 v 赋给 `[b : e]` 中的每个元素。 |
| `fill_n(b, n, v)` | 将 v 赋给 `[b : b + n]` 中的每个元素。 |
| `generate(b, e, f)` | 将 `f()` 赋给 `[b : e]` 中的每个元素。 |
| `generate_n(b, n, f)` | 将 `f()` 赋给 `[b : b + n]` 中的每个元素。 |
| `uninitialized_fill(b, e, v)` | 用 v 初始化 `[b : e]` 中的所有元素。 |
| `uninitialized_copy(b, e, out)` | 用 `[b : e]` 中对应的元素初始化 `[out : out + (e-b)]` 中的所有元素。 |

请注意，未初始化的序列应仅出现在编程的最底层，通常是在容器的实现内部。作为 `uninitialized_fill` 或 `uninitialized_copy` 目标的元素必须是内置类型或未初始化的。

### B.5.4 排序和搜索

排序和搜索是基础，程序员的需求也各不相同。默认情况下，比较是使用 `<` 运算符完成的，并且一对值 `a` 和 `b` 的等价性是通过 `!(a < b) && !(b < a)` 来确定的，而不是要求运算符 `==`。

| 排序和搜索 | 描述 |
| :--- | :--- |
| `sort(b, e)` | 对 `[b:e]` 进行排序。 |
| `sort(b, e, f)` | 使用 `f(*p,*q)` 作为排序标准对 `[b:e]` 进行排序。 |
| `stable_sort(b, e)` | 对 `[b:e]` 进行排序，保持等价元素的顺序。 |
| `stable_sort(b, e, f)` | 使用 `f(*p,*q)` 作为排序标准对 `[b:e]` 进行排序，保持等价元素的顺序。 |
| `partial_sort(b, m, e)` | 对 `[b:e]` 进行排序以得到 `[b:m]` 有序；`[m:e]` 无需排序。 |
| `partial_sort(b, m, e, f)` | 使用 `f(*p,*q)` 作为排序标准对 `[b:e]` 进行排序以得到 `[b:m]` 有序；`[m:e]` 无需排序。 |
| `partial_sort_copy(b,e,b2,e2)` | 对 `[b:e)` 进行足够的排序，以便将 `e2-b2` 个元素复制到 `[b2:e2)`。 |
| `partial_sort_copy(b,e,b2,e2,f)` | 使用 `f` 作为比较标准，对 `[b:e)` 进行足够的排序，以便将 `e2-b2` 个元素复制到 `[b2:e2)`。 |
| `nth_element(b,p,e)` | 将 `[b:e)` 中的第 n 个元素放到其正确的位置；`[b:p)` 是排序的。 |
| `nth_element(b,p,e,f)` | 使用 `f` 进行比较，将 `[b:e)` 中的第 n 个元素放到其正确的位置；`[b:p)` 是排序的。 |
| `p=lower_bound(b,e,v)` | `p` 指向 `[b:e)` 中 `v` 的第一次出现。 |
| `p=lower_bound(b,e,v,f)` | 使用 `f` 进行比较，`p` 指向 `[b:e)` 中 `v` 的第一次出现；`[b:p)` 是排序的。 |
| `p=upper_bound(b,e,v)` | `p` 指向 `[b:e)` 中大于 `v` 的第一个值。 |
| `p=upper_bound(b,e,v,f)` | 使用 `f` 进行比较，`p` 指向 `[b:e)` 中大于 `v` 的第一个值。 |
| `binary_search(b,e,v)` | `v` 是否在排序后的序列 `[b:e)` 中？ |
| `binary_search(b,e,v,f)` | 使用 `f` 进行比较，`v` 是否在排序后的序列 `[b:e)` 中？ |
| `pair(p1,p2)=equal_range(b,e,v)` | `[p1,p2)` 是 `[b:e)` 中值为 `v` 的子序列；基本上是对 `v` 的二分查找。 |
| `pair(p1,p2)=equal_range(b,e,v,f)` | 使用 `f` 进行比较，`[p1,p2)` 是 `[b:e)` 中值为 `v` 的子序列；基本上是对 `v` 的二分查找。 |
| `p=merge(b,b2,e2,e2,out)` | 将两个排序后的序列 `[b2:e2)` 和 `[b:e)` 合并到 `[out:p)`。 |
| `p=merge(b,b2,e2,e2,out,f)` | 使用 `f` 作为比较标准，将两个排序后的序列 `[b2:e2)` 和 `[b:e)` 合并到 `[out:+p)`。 |
| `inplace_merge(b,m,e)` | 将两个排序后的子序列 `[b:m)` 和 `[m:e)` 合并为一个排序后的序列 `[b:e)`。 |
| `inplace_merge(b,m,e,f)` | 使用 `f` 作为比较标准，将两个排序后的子序列 `[b:m)` 和 `[m:e)` 合并为一个排序后的序列 `[b:e)`。 |
| `p=partition(b,e,f)` | 将 `f(*p)` 为真的元素放在 `[b:p)` 中，其他元素放在 `[p:e)` 中。 |
| `p=stable_partition(b,e,f)` | 将 `f(*p)` 为真的元素放在 `[b:p)` 中，其他元素放在 `[p:e)` 中，并保持相对顺序。 |

例如：

```cpp
vector<int> v {3,1,4,2};

list<double> lst {0.5,1.5,3,2.5};         // lst 是有序的

sort(v.begin(),v.end());                   // 将 v 排序

vector<double> v2;

merge(v.begin(),v.end(),lst.begin(),lst.end(),back_inserter(v2));

for (auto x : v2) cout << x << ", ";
```

有关插入器，请参阅 § B.6.1。输出是

0.5, 1, 1.5, 2, 2, 2.5, 3, 4,

`equal_range`、`lower_bound` 和 `upper_bound` 算法的使用方式与它们的关联容器等价物相同；请参阅 § B.4.10。

### B.5.5 集合算法

这些算法将序列视为一组元素，并提供基本的集合操作。输入序列假定为已排序，输出序列也是已排序的：

| 集合算法 | 描述 |
| :--- | :--- |
| `includes(b,e,b2,e2)` | `[b2:e2]` 中的所有元素是否也在 `[b:e]` 中？ |
| `includes(b,e,b2,e2,f)` | 使用 `f` 进行比较，`[b2:e2]` 中的所有元素是否也在 `[b:e]` 中？ |
| `p=set_union(b,e,b2,e2,out)` | 构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 或 `[b2:e2]` 中的元素。 |
| `p=set_union(b,e,b2,e2,out,f)` | 使用 `f` 进行比较，构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 或 `[b2:e2]` 中的元素。 |
| `p=set_intersection(b,e,b2,e2,out)` | 构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 和 `[b2:e2]` 中均存在的元素。 |
| `p=set_intersection(b,e,b2,e2,out,f)` | 使用 `f` 进行比较，构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 和 `[b2:e2]` 中均存在的元素。 |
| `p=set_difference(b,e,b2,e2,out)` | 构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 中但不在 `[b2:e2]` 中的元素。 |
| `p=set_difference(b,e,b2,e2,out,f)` | 使用 `f` 进行比较，构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 中但不在 `[b2:e2]` 中的元素。 |
| `p=set_symmetric_difference(b,e,b2,e2,out)` | 构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 或 `[b2:e2]` 中但不同时在两者中的元素。 |
| `p=set_symmetric_difference(b,e,b2,e2,out,f)` | 使用 `f` 进行比较，构造一个排序后的序列 `[out:p]`，包含 `[b:e]` 或 `[b2:e2]` 中但不同时在两者中的元素。 |

### B.5.6 堆

堆是一种数据结构，它将具有最高值的元素放在首位。堆算法允许程序员将随机访问序列视为堆：

| 堆操作 | 描述 |
| :--- | :--- |
| `make_heap(b,e)` | 使序列准备好被用作堆。 |
| `make_heap(b,e,f)` | 使用 `f` 进行比较，使序列准备好被用作堆。 |
| `push_heap(b,e)` | 向堆中添加一个元素（放在其正确的位置）。 |
| `push_heap(b,e,f)` | 使用 `f` 进行比较，向堆中添加一个元素。 |
| `pop_heap(b,e)` | 从堆中移除最大（第一个）元素。 |
| `pop_heap(b,e,f)` | 使用 `f` 进行比较，从堆中移除一个元素。 |
| `sort_heap(b,e)` | 对堆进行排序。 |
| `sort_heap(b,e,f)` | 使用 `f` 进行比较，对堆进行排序。 |

堆的意义在于提供快速的元素添加和对具有最高值的元素的快速访问。堆的主要用途是实现优先级队列。

### B.5.7 排列

排列用于生成序列元素的组合。例如，`abc` 的排列是 `abc`、`acb`、`bac`、`bca`、`cab` 和 `cba`。

### B.5.7 排列

| 函数 | 描述 |
| :--- | :--- |
| `x = next_permutation(b, e)` | 将 `b:e` 调整为字典序中的下一个排列。 |
| `x = next_permutation(b, e, f)` | 使用 `f` 进行比较，将 `b:e` 调整为字典序中的下一个排列。 |
| `x = prev_permutation(b, e)` | 将 `b:e` 调整为字典序中的上一个排列。 |
| `x = prev_permutation(b, e, f)` | 使用 `f` 进行比较，将 `b:e` 调整为字典序中的上一个排列。 |

对于 `next_permutation`，如果 `b:e` 已经包含最后一个排列（例如示例中的 `cba`），则其返回值 (`x`) 为 `false`；在这种情况下，它返回第一个排列（例如示例中的 `abc`）。对于 `prev_permutation`，如果 `b:e` 已经包含第一个排列（例如示例中的 `abc`），则其返回值为 `false`；在这种情况下，它返回最后一个排列（例如示例中的 `cba`）。

### B.5.8 min 和 max

值比较在许多上下文中都非常有用：

### min 和 max

| 函数 | 描述 |
| :--- | :--- |
| `x = max(a, b)` | `x` 是 `a` 和 `b` 中较大的一个。 |
| `x = max(a, b, f)` | 使用 `f` 进行比较，`x` 是 `a` 和 `b` 中较大的一个。 |
| `x = max({elems})` | `x` 是 `{elems}` 中的最大元素。 |
| `x = max({elems}, f)` | 使用 `f` 进行比较，`x` 是 `{elems}` 中的最大元素。 |
| `x = min(a, b)` | `x` 是 `a` 和 `b` 中较小的一个。 |
| `x = min(a, b, f)` | 使用 `f` 进行比较，`x` 是 `a` 和 `b` 中较小的一个。 |
| `x = min({elems})` | `x` 是 `{elems}` 中的最小元素。 |
| `x = min({elems}, f)` | 使用 `f` 进行比较，`x` 是 `{elems}` 中的最小元素。 |
| `pair(x, y) = minmax(a, b)` | `x` 是 `max(a, b)`，`y` 是 `min(a, b)`。 |
| `pair(x, y) = minmax(a, b, f)` | `x` 是 `max(a, b, f)`，`y` 是 `min(a, b, f)`。 |
| `pair(x, y) = minmax({elems})` | `x` 是 `max({elems})`，`y` 是 `min({elems})`。 |
| `pair(x, y) = minmax({elems}, f)` | `x` 是 `max({elems}, f)`，`y` 是 `min({elems}, f)`。 |

### min 和 max（续）

| 函数 | 描述 |
| :--- | :--- |
| `p = max_element(b, e)` | `p` 指向 `[b, e)` 中的最大元素。 |
| `p = max_element(b, e, f)` | 使用 `f` 作为元素比较，`p` 指向 `[b, e)` 中的最大元素。 |
| `p = min_element(b, e)` | `p` 指向 `[b, e)` 中的最小元素。 |
| `p = min_element(b, e, f)` | 使用 `f` 作为元素比较，`p` 指向 `[b, e)` 中的最小元素。 |
| `lexicographical_compare(b, e, b2, e2)` | `[b, e) < [b2, e2]` 是否成立？ |
| `lexicographical_compare(b, e, b2, e2, f)` | 使用 `f` 作为元素比较，`[b, e) < [b2, e2]` 是否成立？ |

## B.6 STL 工具

标准库提供了一些机制，以简化标准库算法的使用。

### B.6.1 插入迭代器

通过迭代器向容器产生输出意味着迭代器所指向的元素及其后续元素可能会被覆盖。这也意味着可能会发生溢出以及随之而来的内存损坏。例如：

```cpp
void f(vector<int>& vi)
{
	fill_n(vi.begin(), 200, 7);	// 将 vi[0]..[199] 赋值给 7
}
```

如果 `vi` 的元素少于 200 个，我们就陷入了困境。

在 `<iterator>` 中，标准库提供了三个迭代器，通过向容器添加（插入）元素而不是覆盖旧元素来处理这个问题。提供了三个函数来生成这些插入迭代器：

### 插入迭代器

| 函数 | 描述 |
| :--- | :--- |
| `r = back_inserter(c)` | `*r = x` 会导致执行 `c.push_back(x)`。 |
| `r = front_inserter(c)` | `*r = x` 会导致执行 `c.push_front(x)`。 |
| `r = inserter(c, p)` | `*r = x` 会导致执行 `c.insert(p, x)`。 |

对于 `inserter(c, p)`，`p` 必须是容器 `c` 的有效迭代器。当然，每次通过插入迭代器向其写入值时，容器的大小都会增加一个元素。当写入发生时，插入器使用 `c.push_back(x)`、`c.push_front()` 或 `c.insert()` 将新元素插入到序列中，而不是覆盖现有元素。例如：

```cpp
void g(vector<int>& vi)
{
    fill_n(back_inserter(vi), 200, 7); // 在 vi 的末尾添加 200 个 7
}
```

### B.6.2 函数对象

许多标准算法接受函数对象（或函数）作为参数，以控制其工作方式。常见的用途包括比较准则、谓词（返回 `bool` 的函数）以及算术运算。在 `<functional>` 中，标准库提供了一些常用的函数对象。

### 谓词

| 函数 | 描述 |
| :--- | :--- |
| `p = equal_to<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x == y`。 |
| `p = not_equal_to<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x != y`。 |
| `p = greater<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x > y`。 |
| `p = less<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x < y`。 |
| `p = greater_equal<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x >= y`。 |
| `p = less_equal<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x <= y`。 |
| `p = logical_and<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x && y`。 |
| `p = logical_or<T>{}` | 当 `x` 和 `y` 为类型 `T` 时，`p(x, y)` 意味着 `x || y`。 |
| `p = logical_not<T>{}` | 当 `x` 为类型 `T` 时，`p(x)` 意味着 `!x`。 |

例如：

```cpp
vector<int> v; // ...
```
