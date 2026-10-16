
`p=replace_copy_if(b,e ,out,f,v2)` `replace` (§iso.25.3.5)

将 `[b:e)` 中满足 `*p==v` 的元素 `*p` 替换为 `v2`。将 `[b:e)` 中满足 `f(*p)` 的元素 `*p` 替换为 `v2`。复制 `[b:e)` 到 `[out:p)`，并将满足 `*p==v` 的元素替换为 `v2`。复制 `[b:e)` 到 `[out:p)`，并将满足 `f(*p,v)` 的元素替换为 `v2`。

这些算法无法改变输入序列的大小，因此即使是 `remove()` 也会保持输入序列的大小不变。与 `unique()` 一样，它通过向左移动元素来“移除”。例如：

```cpp

string s {" *CamelCase*IsUgly*"};

cout << s << '\n'; // *CamelCase*IsUgly*

auto p = remove(s.begin(),s.end(),'*');

```

```cpp

copy(s.begin(),p,ostream_iterator<char>{cout}); // CamelCaseIsUgly

cout << s << '\n'; // CamelCaseIsUglyly*

```

# 32.5.4 rotate()、random_shuffle() 与 partition()

`rotate()`、`random_shuffle()` 和 `partition()` 算法提供了在序列中有序移动元素的系统方法：

## rotate()（§iso.25.3.11）

- `p = rotate(b, m, e)` — 左旋元素：将 `[b:e)` 视为一个圆环，最后一个元素后面紧跟着第一个元素；将 `*(b+i)` 移动到 `*(b + ((i + (e - m)) % (e - b)))`；注意：`*b` 移动到 `*p`；`p = b + (e - m)`。
- `p = rotate_copy(b, m, e, out)` — 将 `[b:e)` 复制到旋转后的序列 `[out:p)` 中。`rotate()`（以及 shuffle 和 partition 算法）所进行的元素移动通过 `swap()` 完成。

## random_shuffle() 与 shuffle()（§iso.25.3.12）

- `random_shuffle(b, e)` — 使用默认随机数生成器打乱 `[b:e)` 中的元素。
- `random_shuffle(b, e, f)` — 使用随机数生成器 `f` 打乱 `[b:e)` 中的元素。
- `shuffle(b, e, f)` — 使用均匀随机数生成器 `f` 打乱 `[b:e)` 中的元素。

`shuffle` 算法打乱序列的方式与我们洗一副牌非常相似。也就是说，打乱后，元素处于随机顺序，其中“随机”由随机数生成器产生的分布来定义。

默认情况下，`random_shuffle()` 使用均匀分布的随机数生成器来打乱其序列。也就是说，它选择序列元素的一个排列，使得每个排列被选中的概率相同。如果你想要不同的分布或更好的随机数生成器，可以自行提供。对于调用 `random_shuffle(b, e, r)`，生成器以序列（或子序列）的元素个数作为参数进行调用。例如，调用 `r(e - b)` 时，生成器必须返回 `[0, e - b)` 范围内的值。如果 `My_rand` 是这样一个生成器，我们可以像这样洗一副牌：

```cpp

void f(deque<Card>& dc, My_rand& r)

{

    random_shuffle(dc.begin(), dc.end(), r);

    //...

}

```

`partition` 算法根据分区标准将序列分为两部分：

## partition()（§iso.25.3.13）

- `p = partition(b, e, f)` — 将满足 `f(*p)` 为真的元素放在 `[b:p)` 中，其余元素放在 `[p:e)` 中。
- `p = stable_partition(b, e, f)` — 将满足 `f(*p)` 为真的元素放在 `[b:p)` 中，其余元素放在 `[p:e)` 中；保持相对顺序。
- `pair(p1, p2) = partition_copy(b, e, out1, out2, f)` — 将 `[b:e)` 中满足 `f(*p)` 的元素复制到 `[out1:p1)`，将 `[b:e)` 中满足 `!f(*p)` 的元素复制到 `[out2:p2)`。
- `p = partition_point(b, e, f)` — 对于 `[b:e)`，`p` 是满足 `all_of(b, p, f)` 且 `none_of(p, e, f)` 的点。
- `is_partitioned(b, e, f)` — `[b:e)` 中每个满足 `f(*p)` 的元素是否都先于每个满足 `!f(*p)` 的元素？

# 32.5.5 排列

排列算法提供了一种系统生成序列所有排列的方法。

## 排列（§iso.25.4.9, §iso.25.2.12）

- `x = next_permutation(b, e)` — 将 `[b:e)` 变为字典序下的下一个排列。
- `x = next_permutation(b, e, f)` — 使用 `f` 进行比较，将 `[b:e)` 变为下一个排列。
- `x = prev_permutation(b, e)` — 将 `[b:e)` 变为字典序下的上一个排列。
- `x = prev_permutation(b, e, f)` — 使用 `f` 进行比较，将 `[b:e)` 变为上一个排列。
- `is_permutation(b, e, b2)` — 是否存在 `[b2:b2 + (e - b))` 的一个排列与 `[b:e)` 比较相等？
- `is_permutation(b, e, b2, f)` — 是否存在 `[b2:b2 + (e - b))` 的一个排列与 `[b:e)` 比较相等，使用 `f(*p, *q)` 作为元素比较方式？

如果 `next_*` 操作成功，则 `x` 为 `true`，否则为 `false`。

排列用于生成序列元素的组合。例如，`abc` 的排列有 `abc`、`acb`、`bac`、`bca`、`cab` 和 `cba`。

`next_permutation()` 接收一个序列 `[b:e)` 并将其转换为下一个排列。下一个排列的确定基于所有排列按字典序排序的假设。如果这样的排列存在，`next_permutation()` 返回 `true`；否则，它将序列转换为最小的排列，即升序排列（示例中的 `abc`），并返回 `false`。因此，我们可以像这样生成 `abc` 的所有排列：

```cpp

vector<char> v {'a', 'b', 'c'};

while (next_permutation(v.begin(), v.end()))

    cout << v[0] << v[1] << v[2] << ' ';

```

类似地，如果 `[b:e)` 已经包含第一个排列（示例中的 `abc`），`prev_permutation()` 的返回值为 `false`；在这种情况下，它返回最后一个排列（示例中的 `cba`）。

# 32.5.6 fill()

`fill()` 算法族提供了对序列元素进行赋值和初始化的方法：

## fill 家族（§iso.25.3.6, §iso.25.3.7, §iso.20.6.12）

- `fill(b, e, v)` — 将 `v` 赋给 `[b:e)` 中的每个元素。
- `p = fill_n(b, n, v)` — 将 `v` 赋给 `[b:b + n)` 中的每个元素；`p = b + n`。
- `generate(b, e, f)` — 将 `f()` 的结果赋给 `[b:e)` 中的每个元素。
- `p = generate_n(b, n, f)` — 将 `f()` 的结果赋给 `[b:b + n)` 中的每个元素；`p = b + n`。
- `uninitialized_fill(b, e, v)` — 使用 `v` 初始化 `[b:e)` 中的每个元素。
- `p = uninitialized_fill_n(b, n, v)` — 使用 `v` 初始化 `[b:b + n)` 中的每个元素；`p = b + n`。
- `p = uninitialized_copy(b, e, out)` — 使用 `[b:e)` 中对应的元素初始化 `[out:out + (e - b))` 中的每个元素；`p = out + (e - b)`。
- `p = uninitialized_copy_n(b, n, out)` — 使用 `[b:b + n)` 中对应的元素初始化 `[out:out + n)` 中的每个元素；`p = out + n`。

`fill()` 算法重复地赋给指定值，而 `generate()` 通过反复调用其函数参数来获取值并赋值。例如，使用 §40.7 中的随机数生成器 `Randint` 和 `Urand`：

```cpp

int v1[900];

array<int, 900> v2;

vector<int> v3;

void f()

{

    fill(begin(v1), end(v1), 99); // 将 v1 的所有元素设置为 99

    generate(begin(v2), end(v2), Randint{}); // 设置为随机值（§40.7）

    // 输出 [0:100) 区间内的 200 个随机整数：

    generate_n(ostream_iterator<int>{cout}, 200, Urand{100}); // 参见 §40.7

    fill_n(back_inserter(v3), 20, 99); // 向 v3 添加 20 个值为 99 的元素

}

```

`generate()` 和 `fill()` 函数是赋值而非初始化。如果你需要操作原始存储，例如将一段内存转换为具有明确类型和状态的对象，则应使用 `uninitialized_` 版本（在 `<memory>` 中提供）。

未初始化的序列只应出现在最低层次的编程中，通常是在容器的实现内部。`uninitialized_fill()` 或 `uninitialized_copy()` 的目标元素必须是内建类型或未初始化的。例如：

```cpp

vector<string> vs {"Breugel", "El Greco", "Delacroix", "Constable"};

vector<string> vs2 {"Hals", "Goya", "Renoir", "Turner"};

copy(vs.begin(), vs.end(), vs2.begin()); // 正确

uninitialized_copy(vs.begin(), vs.end(), vs2.begin()); // 泄漏！

```

更多处理未初始化内存的工具将在 §34.6 中描述。

# 32.5.7 swap()

`swap()` 算法交换两个对象的值：

## swap 家族（§iso.25.3.3）

- `swap(x, y)` — 交换 `x` 和 `y` 的值。
- `p = swap_ranges(b, e, b2)` — 交换 `[b:e)` 和 `[b2:b2 + (e - b))` 中对应的元素。
- `iter_swap(p, q)` — `swap(*p, *q)`。

例如：

```cpp

void use(vector<int>& v, int* p)

{

    swap_ranges(v.begin(), v.end(), p); // 交换值

}

```

指针 `p` 最好指向一个至少包含 `v.size()` 个元素的数组。

`swap()` 算法可能是标准库中最简单、也可以说是最关键的一个算法。它被用作许多最广泛使用算法的实现部分。其实现作为示例出现在 §7.7.2 中，标准库版本在 §35.5.2 中介绍。

# 32.6 排序与查找

排序和在已排序序列中查找是基础操作，程序员的需求多种多样。默认使用 `<` 运算符进行比较，值 `a` 和 `b` 的等价性由 `!(a < b) && !(b < a)` 确定，而不要求使用 `operator ==`。

## sort 家族（§iso.25.4.1）

- `sort(b, e)` — 对 `[b:e)` 进行排序。
- `sort(b, e, f)` — 使用 `f(*p, *q)` 作为排序标准，对 `[b:e)` 进行排序。

除了“普通排序”之外，还有许多变体：

- `stable_sort(b, e)` — 对 `[b:e)` 进行排序，保持相等元素的顺序。
- `stable_sort(b, e, f)` — 使用 `f(*p, *q)` 作为排序标准，对 `[b:e)` 进行排序，保持相等元素的顺序。
- `partial_sort(b, m, e)` — 对 `[b:e)` 中足够多的元素进行排序，使 `[b:m)` 有序；`[m:e)` 不必排序。
- `partial_sort(b, m, e, f)` — 使用 `f(*p, *q)` 作为排序标准，对 `[b:e)` 中足够多的元素进行排序，使 `[b:m)` 有序；`[m:e)` 不必排序。
- `p = partial_sort_copy(b, e, b2, e2)` — 对 `[b:e)` 中足够多的元素进行排序，将前 `e2 - b2` 个元素复制到 `[b2:e2)`；`p` 是 `e2` 和 `b2 + (e - b)` 中较小的一个。
- `p = partial_sort_copy(b, e, b2, e2, f)` — 使用 `f(*p, *q)` 作为排序标准，对 `[b:e)` 中足够多的元素进行排序，将前 `e2 - b2` 个元素复制到 `[b2:e2)`；`p` 是 `e2` 和 `b2 + (e - b)` 中较小的一个。
- `is_sorted(b, e)`
- `is_sorted(b, e, f)`
- `p = is_sorted_until(b, e)`

对 `[b:e)` 进行足够的排序，以便将前 `e2–b2` 个元素复制到 `[b2:e2)` 中，使用 `f` 进行比较；`p` 是 `b2` 与 `b2+(e–b)` 中较小的一个。
`[b:e)` 是否已排序？
使用 `f` 进行比较，`[b:e)` 是否已排序？
`p` 指向 `[b:e)` 中第一个未按顺序排列的元素

`p=is_sorted_until(b,e,f)` `p` 指向 `[b:e)` 中第一个未按顺序排列的元素，使用 `f` 进行比较

`nth_element(b,n,e)` 如果 `[b:e)` 已排序，`*n` 将位于其应有位置；`[b:n)` 中的元素 `<= *n`，且 `*n <= [n:e)` 中的元素

`nth_element(b,n,e,f)` 如果 `[b:e)` 已排序，`*n` 将位于其应有位置；`[b:n)` 中的元素 `<= *n`，且 `*n <= [n:e)` 中的元素，使用 `f` 进行比较

`sort()` 算法需要随机访问迭代器（§33.1.2）。
尽管名称如此，`is_sorted_until()` 返回的是迭代器，而不是 `bool`。
标准 `list`（§31.3）不提供随机访问迭代器，因此对列表排序应该

使用特定的列表操作（§31.4.2），或者将其元素复制到一个 `vector` 容器中，对该 `vector` 容器排序，然后再将元素复制回列表：

```cpp

template<typename List> void sort_list(List& lst) {

vector v {lst.begin(),lst.end()}; sort(v);

copy(v,lst);

}

// initialize from lst

// use container sort(§32.2)

```

基本 `sort()` 是高效的（平均 `N*log(N)`）。如果需要稳定排序，应使用 `stable_sort()`，即一种 `N*log(N)*log(N)` 的算法，当系统有足够额外内存时会趋近于 `N*log(N)`。`get_temporary_buffer()` 函数可用于获取这种额外内存（§34.6）。比较相等的元素的相对顺序由 `stable_sort()` 保留，而 `sort()` 不保留。

有时，只需要一个已排序序列的前几个元素。在这种情况下，只需对序列进行必要的排序，使前一部分有序即可，也就是部分排序。普通的 `partial_sort(b,m,e)` 算法将 `[b:m)` 范围内的元素按顺序排列。`partial_sort_copy()` 算法产生 `N` 个元素，其中 `N` 是输出序列中元素个数与输入序列中元素个数中的较小值。我们需要同时指定结果序列的起点和终点，因为这决定了我们需要排序多少个元素。例如：

```cpp

void f(const vector<Book>& sales) // find the top ten books

{

vector<Book> bestsellers(10);

partial_sort_copy(sales.begin(),sales.end(),

bestsellers.begin(),bestsellers.end(),

[](const Book& b1, const Book& b2) { return b1.copies_sold()>b2.copies_sold(); });

```

```cpp

copy(bestsellers.begin(),bestsellers.end(),ostream_iterator<Book>{cout,"\n"});

}

```

由于 `partial_sort_copy()` 的目标必须是随机访问迭代器，我们不能直接排序到 `cout`。

如果 `partial_sort()` 所需排序的元素数量相对于总元素数量很小，这些算法可能显著快于完整排序。此时，它们的复杂度接近 `O(N)`，而 `sort()` 的复杂度为 `O(N*log(N))`。

`nth_element()` 算法只进行必要的排序，使第 `N` 个元素到达其正确位置，并且序列中没有比第 `N` 个元素小的元素被放置在它后面。例如：

```cpp

vector<int> v;
