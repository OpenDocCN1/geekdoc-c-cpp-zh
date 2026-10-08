
shuffle 算法洗牌其序列的方式，就像我们洗牌一副扑克牌一样；也就是说，洗牌后，元素处于随机顺序，其中“随机”是由随机数发生器产生的分布来定义的。

请注意，这些算法并不知道其参数序列是否是一个容器，因此它们没有添加或删除元素的能力。因此，像 **remove** 这样的算法不能通过删除（擦除）元素来缩短其输入序列；相反，它将其保留的元素（重新）移动到序列的前部：

```cpp
template<typename Iter>
void print_digits(const string& s, Iter b, Iter e)
{
    cout << s;
    while (b!=e) { cout << *b; ++b; }
    cout << "\n";
}

void ff()
{
    vector<int> v {1,1,1, 2,2, 3, 4,4,4, 3,3,3, 5,5,5,5, 1,1,1};
    print_digits("all: ", v.begin(), v.end());

    auto pp = unique(v.begin(), v.end());
    print_digits("head: ", v.begin(), pp);
    print_digits("tail: ", pp, v.end());

    pp=remove(v.begin(), pp, 4);
    print_digits("head: ", v.begin(), pp);
    print_digits("tail: ", pp, v.end());
}
```

产生的输出是

```
all:  1112234443335555111
head: 1234351
tail: 443335555111
head: 123351
tail: 1443335555111
```

### B.5.3 实用算法

从技术上讲，这些实用算法也是修改序列算法，但我们认为将它们单独列出来是个好主意，以免它们被遗漏。

| 实用算法 | 描述 |
| :--- | :--- |
| `swap(x, y)` | 交换 x 和 y。 |
| `iter_swap(p, q)` | 交换 \*p 和 \*q。 |
| `swap_ranges(b, e, b2)` | 交换 [b : e] 和 [b2 : b2 + (e-b)] 中的元素。 |
| `fill(b, e, v)` | 将 v 赋给 [b : e] 中的每个元素。 |
| `fill_n(b, n, v)` | 将 v 赋给 [b : b + n] 中的每个元素。 |
| `generate(b, e, f)` | 将 f() 赋给 [b : e] 中的每个元素。 |
| `generate_n(b, n, f)` | 将 f() 赋给 [b : b + n] 中的每个元素。 |
| `uninitialized_fill(b, e, v)` | 用 v 初始化 [b : e] 中的所有元素。 |
| `uninitialized_copy(b, e, out)` | 用 [b : e] 中对应的元素初始化 [out : out + (e-b)] 中的所有元素。 |

请注意，未初始化的序列应仅出现在编程的最底层，通常是在容器的实现内部。作为 **uninitialized_fill** 或 **uninitialized_copy** 目标的元素必须是内置类型或未初始化的。

### B.5.4 排序和搜索

排序和搜索是基础，程序员的需求也各不相同。默认情况下，比较是使用 **<** 运算符完成的，并且一对值 **a** 和 **b** 的等价性是通过 **!(a < b) && !(b < a)** 来确定的，而不是要求运算符 **==**。

| 排序和搜索 | 描述 |
| :--- | :--- |
| `sort(b, e)` | 对 [b:e] 进行排序。 |
| `sort(b, e, f)` | 使用 f(\*p,\*q) 作为排序标准对 [b:e] 进行排序。 |
| `stable_sort(b, e)` | 对 [b:e] 进行排序，保持等价元素的顺序。 |
| `stable_sort(b, e, f)` | 使用 f(\*p,\*q) 作为排序标准对 [b:e] 进行排序，保持等价元素的顺序。 |
| `partial_sort(b, m, e)` | 对 [b:e] 进行排序以得到 [b:m] 有序；[m:e] 无需排序。 |
| `partial_sort(b, m, e, f)` | 使用 f(\*p,\*q) 作为排序标准对 [b:e] 进行排序以得到 [b:m] 有序；[m:e] 无需排序。 |
| `partial_sort_copy(b,e,b2,e2)` | 对 [b:e) 进行足够的排序，以便将 e2-b2 个元素复制到 [b2:e2)。 |
| `partial_sort_copy(b,e,b2,e2,f)` | 使用 f 作为比较标准，对 [b:e) 进行足够的排序，以便将 e2-b2 个元素复制到 [b2:e2)。 |
| `nth_element(b,p,e)` | 将 [b:e) 中的第 n 个元素放到其正确的位置；[b:p) 是排序的。 |
| `nth_element(b,p,e,f)` | 使用 f 进行比较，将 [b:e) 中的第 n 个元素放到其正确的位置；[b:p) 是排序的。 |
| `p=lower_bound(b,e,v)` | p 指向 [b:e) 中 v 的第一次出现。 |
| `p=lower_bound(b,e,v,f)` | 使用 f 进行比较，p 指向 [b:e) 中 v 的第一次出现；[b:p) 是排序的。 |
| `p=upper_bound(b,e,v)` | p 指向 [b:e) 中大于 v 的第一个值。 |
| `p=upper_bound(b,e,v,f)` | 使用 f 进行比较，p 指向 [b:e) 中大于 v 的第一个值。 |
| `binary_search(b,e,v)` | v 是否在排序后的序列 [b:e) 中？ |
| `binary_search(b,e,v,f)` | 使用 f 进行比较，v 是否在排序后的序列 [b:e) 中？ |
| `pair(p1,p2)=equal_range(b,e,v)` | [p1,p2) 是 [b:e) 中值为 v 的子序列；基本上是对 v 的二分查找。 |
| `pair(p1,p2)=equal_range(b,e,v,f)` | 使用 f 进行比较，[p1,p2) 是 [b:e) 中值为 v 的子序列；基本上是对 v 的二分查找。 |
| `p=merge(b,b2,e2,e2,out)` | 将两个排序后的序列 [b2:e2) 和 [b:e) 合并到 [out:p)。 |
| `p=merge(b,b2,e2,e2,out,f)` | 使用 f 作为比较标准，将两个排序后的序列 [b2:e2) 和 [b:e) 合并到 [out:+p)。 |
| `inplace_merge(b,m,e)` | 将两个排序后的子序列 [b:m) 和 [m:e) 合并为一个排序后的序列 [b:e)。 |
| `inplace_merge(b,m,e,f)` | 使用 f 作为比较标准，将两个排序后的子序列 [b:m) 和 [m:e) 合并为一个排序后的序列 [b:e)。 |
| `p=partition(b,e,f)` | 将 f(\*p) 为真的元素放在 [b:p) 中，其他元素放在 [p:e) 中。 |
| `p=stable_partition(b,e,f)` | 将 f(\*p) 为真的元素放在 [b:p) 中，其他元素放在 [p:e) 中，并保持相对顺序。 |

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

equal_range、lower_bound 和 upper_bound 算法的使用方式与它们的关联容器等价物相同；请参阅 § B.4.10。

### B.5.5 集合算法

这些算法将序列视为一组元素，并提供基本的集合操作。输入序列假定为已排序，输出序列也是已排序的：

| 集合算法 | 描述 |
| :--- | :--- |
| `includes(b,e,b2,e2)` | [b2:e2] 中的所有元素是否也在 [b:e] 中？ |
| `includes(b,e,b2,e2,f)` | 使用 f 进行比较，[b2:e2] 中的所有元素是否也在 [b:e] 中？ |
| `p=set_union(b,e,b2,e2,out)` | 构造一个排序后的序列 [out:p]，包含 [b:e] 或 [b2:e2] 中的元素。 |
| `p=set_union(b,e,b2,e2,out,f)` | 使用 f 进行比较，构造一个排序后的序列 [out:p]，包含 [b:e] 或 [b2:e2] 中的元素。 |
| `p=set_intersection(b,e,b2,e2,out)` | 构造一个排序后的序列 [out:p]，包含 [b:e] 和 [b2:e2] 中均存在的元素。 |
| `p=set_intersection(b,e,b2,e2,out,f)` | 使用 f 进行比较，构造一个排序后的序列 [out:p]，包含 [b:e] 和 [b2:e2] 中均存在的元素。 |
| `p=set_difference(b,e,b2,e2,out)` | 构造一个排序后的序列 [out:p]，包含 [b:e] 中但不在 [b2:e2] 中的元素。 |
| `p=set_difference(b,e,b2,e2,out,f)` | 使用 f 进行比较，构造一个排序后的序列 [out:p]，包含 [b:e] 中但不在 [b2:e2] 中的元素。 |
| `p=set_symmetric_difference(b,e,b2,e2,out)` | 构造一个排序后的序列 [out:p]，包含 [b:e] 或 [b2:e2] 中但不同时在两者中的元素。 |
| `p=set_symmetric_difference(b,e,b2,e2,out,f)` | 使用 f 进行比较，构造一个排序后的序列 [out:p]，包含 [b:e] 或 [b2:e2] 中但不同时在两者中的元素。 |

### B.5.6 堆

堆是一种数据结构，它将具有最高值的元素放在首位。堆算法允许程序员将随机访问序列视为堆：

| 堆操作 | 描述 |
| :--- | :--- |
| `make_heap(b,e)` | 使序列准备好被用作堆。 |
| `make_heap(b,e,f)` | 使用 f 进行比较，使序列准备好被用作堆。 |
| `push_heap(b,e)` | 向堆中添加一个元素（放在其正确的位置）。 |
| `push_heap(b,e,f)` | 使用 f 进行比较，向堆中添加一个元素。 |
| `pop_heap(b,e)` | 从堆中移除最大（第一个）元素。 |
| `pop_heap(b,e,f)` | 使用 f 进行比较，从堆中移除一个元素。 |
| `sort_heap(b,e)` | 对堆进行排序。 |
| `sort_heap(b,e,f)` | 使用 f 进行比较，对堆进行排序。 |

堆的意义在于提供快速的元素添加和对具有最高值的元素的快速访问。堆的主要用途是实现优先级队列。

### B.5.7 排列

排列用于生成序列元素的组合。例如，**abc** 的排列是 **abc**、**acb**、**bac**、**bca**、**cab** 和 **cba**。

