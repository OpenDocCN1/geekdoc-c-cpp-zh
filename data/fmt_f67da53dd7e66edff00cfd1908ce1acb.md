
Replace 意味着“就地放置”或“定位”。

注意，`pop` 操作不返回值。如果它们这样做了，抛出异常的复制构造函数可能会使实现变得非常复杂。使用 `front()` 和 `back()`（§B.4.5）来访问堆栈和队列元素。我们在此未记录完整的要求集；请自由猜测（如果你猜错了，编译器通常会告诉你）并查阅更详细的文档。

### B.4.7 列表操作

容器提供列表操作：

| 列表操作 | 描述 |
| :--- | :--- |
| `q=c.insert(p,x)` | 在 `p` 之前添加 `x`。 |
| `q=c.insert(p,n,x)` | 在 `p` 之前添加 `n` 个 `x` 的副本。 |
| `q=c.insert(p,first,last)` | 在 `p` 之前添加 `[first:last)` 中的元素。 |
| `q=c.emplace(p,args)` | 在 `p` 之前添加 `T(args)`；`T` 是 `c` 的值类型。 |
| `q=c.erase(p)` | 从 `c` 中移除位于 `p` 的元素。 |
| `q=c.erase(first,last)` | 擦除 `c` 的 `[first:last)`。 |
| `c.clear()` | 擦除 `c` 的所有元素。 |

对于 `insert()` 函数，结果 `q` 指向最后一个插入的元素。对于 `erase()` 函数，`q` 指向被擦除的最后一个元素之后的元素。

### B.4.8 大小和容量

大小是容器中的元素数量；容量是容器在分配更多内存之前可以持有的元素数量：

| 大小和容量 | 描述 |
| :--- | :--- |
| `x=c.size()` | `x` 是 `c` 的元素数量。 |
| `c.empty()` | `c` 是否为空？ |

### B.4.9 其他操作

容器可以被复制（参见 §B.4.3）、比较和交换：

| 比较和交换 |  |
| :-- | :-- |
| `c1==c2` | `c1` 和 `c2` 的所有对应元素是否都相等？ |
| `c1!=c2` | `c1` 和 `c2` 的任意对应元素是否不相等？ |
| `c1<c2` | `c1` 是否在字典序上先于 `c2`？ |
| `c1<=c2` | `c1` 是否在字典序上先于或等于 `c2`？ |
| `c1>c2` | `c1` 是否在字典序上后于 `c2`？ |
| `c1>=c2` | `c1` 是否在字典序上后于或等于 `c2`？ |
| `swap(c1, c2)` | 交换 `c1` 和 `c2` 的元素 |
| `c1.swap(c2)` | 交换 `c1` 和 `c2` 的元素 |

当使用运算符（例如 `<`）比较容器时，其元素会使用相应的元素运算符（即 `<`）进行比较。

### B.4.10 关联容器操作

关联容器提供基于键的查找：

| 关联容器操作 |  |
| :-- | :-- |
| `c[k]` | 引用键为 `k` 的元素（仅适用于具有唯一键的容器） |
| `p=c.find(k)` | `p` 指向键为 `k` 的第一个元素 |
| `p=c.lower_bound(k)` | `p` 指向键为 `k` 的第一个元素 |
| `p=c.upper_bound(k)` | `p` 指向键大于 `k` 的第一个元素。 |
| `pair(p1,p2)=c.equal_range(k)` | `(p1:p2)` 是键为 `k` 的元素。 |
| `r=c.key_comp()` | `r` 是键比较对象的副本。 |
| `r=c.value_comp()` | `r` 是映射值比较对象的副本。如果未找到键，则返回 `c.end()`。 |

`equal_range` 返回的迭代器对中，第一个是 `lower_bound`，第二个是 `upper_bound`。你可以像这样打印 `multimap<string,int>` 中所有键为 "Marian" 的元素的值：

```cpp
string k = "Marian";

auto pp = m.equal_range(k);

if (pp.first!=pp.second)
  cout << "elements with value " << k << "\n";
else
  cout << "no element with value " << k << "\n";

for (auto p = pp.first; p!=pp.second; ++p)
  cout << p->second << '\n';
```

我们也可以用等价的方式：

```cpp
auto pp = make_pair(m.lower_bound(k),m.upper_bound(k));
```

然而，这会使执行时间大约翻倍。`equal_range`、`lower_bound` 和 `upper_bound` 算法也适用于有序序列（§ B.5.4）。`pair` 的定义在 § B.6.3 中。

## B.5 算法

`<algorithm>` 中定义了大约 60 个标准算法。它们都操作于由一对迭代器（用于输入）或单个迭代器（用于输出）定义的序列。

在复制、比较等两个序列时，第一个序列由一对迭代器 `[b:e]` 表示，而第二个序列仅由单个迭代器 `b2` 表示，`b2` 被视为一个包含足够元素（例如，与第一个序列相同数量的元素）的序列的起点：`[b2:b2+(e-b)]`。

某些算法，如 `sort`，需要随机访问迭代器；而许多算法，如 `find`，只是按顺序读取元素，因此可以使用前向迭代器。

许多算法遵循通常的惯例，通过返回序列的末尾来表示“未找到”。我们不会在每个算法的描述中提及这一点。

### B.5.1 非修改序列算法

非修改算法仅读取序列的元素；它不重新排列序列，也不改变元素的值：

| 非修改序列算法 |  |
| :-- | :-- |
| `f=i=for_each(b,e,f)` | 对 `[b:e)` 中的每个元素执行 `f`；返回 `f`。 |
| `p=find(b,e,v)` | `p` 指向 `v` 在 `[b:e)` 中的第一次出现位置。 |
| `p=find_if(b,e,f)` | `p` 指向 `[b:e)` 中满足 `f(*p)` 的第一个元素。 |
| `p=find_first_of(b,e,b2,e2)` | `p` 指向 `[b:e)` 中满足 `*p==*q` 的第一个元素，其中 `q` 是 `[b2:e2)` 中的某个元素。 |
| `p=find_first_of(b,e,b2,e2,f)` | `p` 指向 `[b:e)` 中满足 `f(*p,*q)` 的第一个元素，其中 `q` 是 `[b2:e2)` 中的某个元素。 |
| `p=adjacent_find(b,e)` | `p` 指向 `[b:e)` 中满足 `*p==*(p+1)` 的第一个 `p`。 |
| `p=adjacent_find(b,e,f)` | `p` 指向 `[b:e)` 中满足 `f(*p,*(p+1))` 的第一个 `p`。 |
| `equal(b,e,b2)` | `[b:e)` 和 `[b2:b2+(e-b))` 的所有元素是否都相等？ |
| `equal(b,e,b2,f)` | 使用 `f(*p,*q)` 作为测试，`[b:e)` 和 `[b2:b2+(e-b))` 的所有元素是否都相等？ |
| `pair(p1,p2)=mismatch(b,e,b2)` | `(p1,p2)` 指向 `[b:e)` 和 `[b2:b2+(e-b))` 中第一个不满足 `!(*p1==*p2)` 的元素对。 |
| `pair(p1,p2)=mismatch(b,e,b2,f)` | `(p1,p2)` 指向 `[b:e)` 和 `[b2:b2+(e-b))` 中第一个不满足 `!f(*p1,*p2)` 的元素对。 |
| `p=search(b,e,b2,e2)` | `p` 指向 `[b:e)` 中第一个满足 `*p` 等于 `[b2:e2)` 中某个元素的 `*p`。 |
| `p=search(b,e,b2,e2,f)` | `p` 指向 `[b:e)` 中第一个满足 `f(*p,*q)` 的 `*p`，其中 `*q` 是 `[b2:e2)` 中的某个元素。 |
| `p=find_end(b,e,b2,e2)` | `p` 指向 `[b:e)` 中最后一个满足 `*p` 等于 `[b2:e2)` 中某个元素的 `*p`。 |
| `p=find_end(b,e,b2,e2,f)` | `p` 指向 `[b:e)` 中最后一个满足 `f(*p,*q)` 的 `*p`，其中 `*q` 是 `[b2:e2)` 中的某个元素。 |
| `p=search_n(b,e,n,v)` | `p` 指向 `[b:e]` 中的第一个元素，使得 `[p:p+n]` 中的每个元素值都为 `v`。 |
| `p=search_n(b,e,n,v,f)` | `p` 指向 `[b:e]` 中的第一个元素，使得对于 `[p:p+n]` 中的每个元素 `*q`，都有 `f(*q,v)`。 |
| `x=count(b,e,v)` | `x` 是 `v` 在 `[b:e]` 中出现的次数。 |
| `x=count_if(b,e,v,f)` | `x` 是 `[b:e]` 中满足 `f(*p,v)` 的元素数量。 |

请注意，传给 `for_each` 的操作并没有阻止其修改元素；这被视为可接受的。将改变其检查元素的操作传递给其他算法（例如 `count` 或 `==`）是不可接受的。

一个例子（正确用法）：

```cpp
bool odd(int x) { return x&1; }

int n_even(const vector<int>& v) // 计算 v 中偶数值的数量
{
    return v.size()-count_if(v.begin(),v.end(),odd);
}
```

### B.5.2 修改序列算法

修改算法（也称为可变序列算法）可以（并且通常确实）修改其参数序列的元素。

| 修改序列算法 |  |
| :-- | :-- |
| `p=transform(b,e,out,f)` | 对 `[b:e]` 中的每个 `*p1` 应用 `*p2=f(*p1)`，写入对应的 `[out:out+(e-b)]` 中的 `*p2`；`p=out+(e-b)`。 |
| `p=transform(b,e,b2,out,f)` | 对 `[b:e]` 中的每个元素 `*p1` 和 `[b2:b2+(e-b))` 中对应的元素 `*p2` 应用 `*p3=f(*p1, *p2)`，写入 `[out:out+(e-b)]` 中的 `*p3`；`p=out+(e-b)`。 |
| `p=copy(b,e,out)` | 将 `[b:e]` 复制到 `[out:p)`。 |
| `p=copy_backward(b,e,out)` | 从最后一个元素开始，将 `[b:e]` 复制到 `[p:out)`。 |
| `p=unique(b,e)` | 移动 `b:e` 中的元素，使得 `b:p` 删除了相邻的重复项（`==` 定义“重复”）。 |
| `p=unique(b,e,f)` | 移动 `b:e` 中的元素，使得 `b:p` 删除了相邻的重复项（`f` 定义“重复”）。 |
| `p=unique_copy(b,e,out)` | 将 `b:e` 复制到 `out:p`；不复制相邻的重复项。 |
| `p=unique_copy(b,e,out,f)` | 将 `b:e` 复制到 `out:p`；不复制相邻的重复项（`f` 定义“重复”）。 |
| `replace(b,e,v1,v2)` | 将 `b:e` 中满足 `*q==v1` 的元素 `*q` 替换为 `v2`。 |
| `replace(b,e,f,v2)` | 将 `b:e` 中满足 `f(*q)` 的元素 `*q` 替换为 `v2`。 |
| `p=replace_copy(b,e,out,v1,v2)` | 将 `b:e` 复制到 `out:p`，将满足 `*q==v1` 的元素 `*q` 替换为 `v2`。 |
| `p=replace_copy(b,e,out,f,v2)` | 将 `b:e` 复制到 `out:p`，将满足 `f(*q)` 的元素 `*q` 替换为 `v2`。 |
| `p=remove(b,e,v)` | 移动 `b:e` 中的元素 `*q`，使得 `b:p` 变为满足 `!(*q==v)` 的元素。 |
| `p=remove(b,e,v,f)` | 移动 `b:e` 中的元素 `*q`，使得 `b:p` 变为满足 `!f(*q)` 的元素。 |
| `p=remove_copy(b,e,out,v)` | 将满足 `!(*q==v)` 的 `b:e` 中的元素复制到 `out:p`。 |
| `p=remove_copy_if(b,e,out,f)` | 将满足 `!f(*q,v)` 的 `b:e` 中的元素复制到 `out:p`。 |
| `reverse(b,e)` | 反转 `b:e` 中元素的顺序。 |
| `p=reverse_copy(b,e,out)` | 将 `b:e` 以反转顺序复制到 `out:p`。 |
| `rotate(b,m,e)` | 旋转元素：将 `b:e` 视为一个圆圈，第一个元素紧跟最后一个元素之后。将 `*b` 移动到 `*m`，通常将 `*(b+i)` 移动到 `*((b+(i+(e-m))%(e-b)))`。 |
| `p=rotate_copy(b,m,e,out)` | 将 `b:e` 复制到一个旋转序列 `out:p` 中。 |
| `random_shuffle(b,e)` | 使用默认均匀随机数生成器，将 `b:e` 中的元素洗牌成一种分布。 |
| `random_shuffle(b,e,f)` | 使用 `f` 作为随机数生成器，将 `b:e` 中的元素洗牌成一种分布。 |

shuffle 算法洗牌其序列的方式，就像我们洗牌一副扑克牌一样；也就是说，洗牌后，元素处于随机顺序，其中“随机”是由随机数发生器产生的分布来定义的。

请注意，这些算法并不知道其参数序列是否是一个容器，因此它们没有添加或删除元素的能力。因此，像 `remove` 这样的算法不能通过删除（擦除）元素来缩短其输入序列；相反，它将其保留的元素（重新）移动到序列的前部：

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
