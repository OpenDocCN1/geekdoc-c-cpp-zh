
n + 1

于是，相应的程序为

```text
1: r ← 0
2: j ← 0
3: while j ≠ n do
4:   r ← r + s_j - max(a[j], s_{j-1})
5:   j ← j + 1
6: end while
```

或者，

```text
1: q ← s_{j-1}
2: r ← 0
3: j ← 0
4: q ← max(q, a[0])
5: while j ≠ n do
6:   p ← s_j
7:   r ← r + p - max(a[j], q)
8:   j ← j + 1
9:   q ← p
10: end while
```

让我们定义

0 ≤ i < 4 : d4_i = t_0

于是有

0 ≤ i < N : s_i = max(a[i], d4_i)

而 d 序列的定义变为

(d4_0, d3_0, d2_0, d1_0) = (t_0, t_0, t_0, t_0)
0 ≤ i < n - 1 : (d4_{i+1}, d3_{i+1}, d2_{i+1}, d1_{i+1}) =
(s_i + b[i], d3_i, d2_i, d1_i) 的非递减排列。

进一步用关系

h_4, h_3, h_2, h_1 = d4_j, d3_j, d2_j, d1_j

加强不变式，便得到我们所认为的最终程序：

```text
1:  r ← 0
2:  j ← 0
3:  q ← a[0]
4:  h₄, h₃, h₂, h₁ ← t₀, t₀, t₀, t₀
5:  while j ≠ n do
6:      p ← max(a[j], h₄)
7:      r ← r + p − max(a[j], q)
8:      q ← p
9:      h₄ ← p + b[j]
10:     loop
11:         if h₄ > h₃ then
12:             h₄ ← h₃
13:             h₃ ← h₄
14:         else if h₃ > h₂ then
15:             h₃ ← h₂
16:             h₂ ← h₃
17:         else if h₂ > h₁ then
18:             h₂ ← h₁
19:             h₁ ← h₂
20:         end if
21:     end loop
22:     j ← j + 1
23: end while
```

## 2.6 插值查找

在二分查找中，搜索空间总是被减半，这保证了对数级性能。然而，如果在查找过程中我们发现一个非常接近所要查找的数（比如 x）的值，那么在该邻域内继续查找似乎比盲目地前往下一个半分割点更合理。特别是，如果 x 很小，我们应当从序列开头附近的某个位置开始查找，而不是从中间位置开始。

插值查找是一种在有序序列中按关键字检索所需记录的方法，它利用关键字的值以及关键字的统计分布。

考虑我们在查找某个页码（比如 200）时翻开一本书的方式，而这本书共有 800 页。因此第 200 页大约在四分之一处，我们利用这一知识来判断应该在哪里翻开书。我们第一次尝试很可能不会正好翻到第 200 页；假设我们翻到了第 250 页。现在我们将查找范围缩小到 250 页，并假定目标页大约位于第 1 页到第 250 页之间 80% 的位置。现在我们尝试往回翻大约 (1/5) 的距离。我们可以继续这一过程，直到足够接近第 200 页，从而可以一页一页地翻。这正是插值查找背后的思想。我们不是按固定的二分之一来划分搜索空间，而是按看起来最有可能成功的比例来划分。这一比例由插值确定。

给定一个包含 1000 条记录的文件，其关键字 X_1 < X_2 < ... < X_1000 均匀分布在 0 和 1 之间，我们的任务是找到一个索引 i | X_i = 0.7。可以合理预期大约有 0.7 × 1000 = 700 个关键字小于或等于 0.7，因此所需记录应当接近第 700 条记录。

然而，查看文件可能会发现 X_700 = 0.68 < 0.7。虽然我们还没有检索到该记录，但可以推断目标索引位于 700 和 1000 之间。相应的关键字均匀分布在 0.68 和 1 之间。新文件包含 300 条记录。P_2 = (0.7−0.68)/(1−0.68) = 0.0675 是这些记录具有更小或相等关键字的概率；因此，我们现在应当查看新文件中的第 300 × 0.0675 ≈ 20 条记录。

使用同样的方法继续这一过程；在每次迭代中，要么找到记录，要么文件长度减少。

插值查找最初由 Peterson 提出，作为一种在存储于连续存储位置的已排序序列中进行查找的方法。

### 算法

```text
Algorithm 45 Interpolation Search Algorithm
1: Input : A (a sorted array) and x (the search key).
2: Output : position (an index i | A[i] = x, or 0 if no such index exists).
3: function INTERPOLATION-SEARCH(A[0..n − 1], x)
4:   if x < A[0] or x > A[n − 1] then
5:     position ← 0 ▷ unsuccessful search
6:   else
7:     position = INTERPOLATION-SEARCH-HELPER(x, 0, n − 1)
8:   end if
9:   return position
10: end function
11: function INTERPOLATION-SEARCH-HELPER(x, l, r)
12:   found ← 0
13:   if A[l] == x then
14:     found = l
15:   else if l == r or A[l] == A[r] then
16:     found = 0
17:   else
18:     next = l + [(x−A[l])(r−l)]/[A[r]−A[l]]
19:     if x < A[next] then
20:       found = INTERPOLATION-SEARCH-HELPER(x, l, next − 1)
21:     else
22:       found = INTERPOLATION-SEARCH-HELPER(x, next, r)
23:     end if
24:   end if
25:   return found
26: end function
```

### 复杂度

插值查找的性能不仅取决于序列的大小，还取决于输入本身。存在一些输入，使得插值查找会检查序列中的每一个数。然而，对于由相对均匀分布的元素组成的输入，插值查找非常高效，例如书页毫无疑问是均匀分布的。可以证明，插值查找执行的平均比较次数（对所有可能的序列取平均）为 O(log log n)。尽管这看起来比二分查找的性能提升了一个数量级，但在实践中插值查找并不比二分查找好多少，因为

- 1. 除非 \(n\) 非常大，\(\log_2 n\) 的值足够小，以至于它的对数并不会小多少。
- 2. 插值查找需要更复杂的算术运算。

### C++ 实现

程序 2.6：插值查找

```cpp
#include <vector>
#include <cassert>

template<typename T>
T interpolation_search_helper(T A[], std::size_t l,
    std::size_t r, T value)
{
    std::size_t found = 0, next;

    if (A[l] == value)
    {
        found = l;
    }
    else if ((l == r) || (A[l] == A[r]))
    {
        found = 0;
    }
    else
    {
        next = l + (value - A[l]) * (r - l) / (A[r] -
            A[l]);

        if (value < A[next])
        {
            found = interpolation_search_helper(A,
                l, next - 1, value);
        }
        else
        {
            found = interpolation_search_helper(A,
                next, r, value);
        }
    }
    return found;
}

template<typename T>
T interpolation_search(T sorted_array[], std::size_t l,
    std::size_t r, T value)
{
    std::size_t position = 0;

    if (value < sorted_array[l] || value >
        sorted_array[r])
    {
        position = 0;
    }
    else
    {
        position = interpolation_search_helper(
            sorted_array, l, r, value);
    }
    return position;
}

int main()
{
    int sorted_array[] = {1, 2, 3, 4, 5, 6, 7, 8,
        9};

    assert(interpolation_search(sorted_array, 0, 8,
        5) == 4);
}
```

### 备注

对于外部查找（文件位于外部设备上），插值查找优于二分查找，因为查找时间由访问次数决定。然而，在内部查找中，还应考虑每次迭代的计算时间。计算机实验表明，插值查找和二分查找所花的时间大致相同。插值查找仅对大于 5000 条记录的文件才略快一些。然而，在二分查找中使用移位运算代替除法，或使用斐波那契查找，会得到更快的内部查找方法。经过插值查找的几次迭代后，我们已经相当接近所需记录。当两次连续迭代的索引之差很小时，切换到顺序查找可能更有利，并能节省计算时间。

## 2.7 机器人行走

### 问题描述

给定两个整数数组 $x[0..46]$ 和 $y[0..46]$。数对 $(x[i], y[i])$ 表示平面中点 $P_i$ 的笛卡尔坐标（$0 ≤ i < 47$）。这些数组使得全部 47 个点互不相同。

一个机器人从 $P_0$ 走到 $P_1$，从 $P_1$ 走到 $P_2$，……，从 $P_{45}$ 走到 $P_{46}$，最后从 $P_{46}$ 走到 $P_0$。它遵循以下规则完成行走：

- 它应从 $P_0$ 出发，并面向 $P_1$
