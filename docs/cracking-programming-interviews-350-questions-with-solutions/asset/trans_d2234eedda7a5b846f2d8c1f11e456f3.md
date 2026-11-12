
如何使用二分查找来做到这一点！），因此总运行时间为 $O(n\log n)$。

## 另一个问题

教授现在希望将他的算法扩展到竖笛四重奏，该四重奏由高音、中音、次中音和低音竖笛组成。他升级其启发式方法，对每个区间 $T_i \in T$ 给出一个度量 $m_{ik}$，表示音符 $i$ 由第 $k$ 支竖笛演奏的可能性，其中 $k=1,2,3,4$。给出一个高效算法，确定四个不相交集合 $(S_1,S_2,S_3,S_4 \subseteq T)$，其中每个 $S_k$ 包含互不重叠的区间（表面上对应于四支相应竖笛演奏的音符），使得下式最大化：

$$\sum_{k=1}^{4}\sum_{T_i\in S_k}m_{ik}.$$

## 解法

观察到，如果允许两支或更多乐器在同一个区间 $T_j$ 内演奏，则最优解可以通过对每支乐器分别求解来获得，使用前一个问题的算法。

当两支乐器不能在同一个时间区间内演奏时，问题会更加复杂。然而，请注意，它允许两支乐器在同一个时间瞬间演奏，例如，当两支乐器在两个重叠的时间区间内演奏时。我们将通过推广前一个问题的动态规划来解决这个问题。

设 $\phi_{j_1,j_2,j_3,j_4}$ 为子问题 $(T_j,T_{j+1},\ldots,T_n)$ 在如下限制下的目标函数最大值：乐器 $k$ 可以演奏的最早区间为 $j_k$，其中 $1\le k\le4$。注意，对于每个 $1\le k\le4$，$j_k$ 至少为 $j$，且从不超过 $n$。原问题的解为 $\phi_{1,1,1,1}$。我们将根据 $j_k$ 对于 $1\le k\le4$ 是等于 $j$ 还是严格大于 $j$，将表项分为 $2^4=16$ 类。我们给出 $j_1=j_2=j$ 且 $j_3,j_4>j$ 情形下的动态规划方程。鼓励你推导其他情形的方程。

在 $j_1=j_2=j$ 且 $j_3,j_4>j$ 的情形下，时间区间 $T_j$ 有三种可能情况。容易观察到这三种情况各自的最优子结构。

- 在区间 $T_j$ 内没有演奏任何乐器。那么，此情形下目标函数的值等于 $\phi_{j+1,j+1,j_3,j_4}$。
- 在区间 $T_j$ 内演奏乐器 1。那么，它下一次可以演奏的最早区间是 $T_{j_1'}$。在此情形下，目标函数的值等于 $m_{j,1}+\phi_{j_1',j+1,j_3,j_4}$。
- 在区间 $T_j$ 内演奏乐器 2。那么，它下一次可以演奏的最早区间是 $T_{j_2'}$。在此情形下，目标函数的值等于 $m_{j,2}+\phi_{j+1,j_2',j_3,j_4}$。

如前所述，$\phi_{j_1,j_2,j_3,j_4}$ 将是上述各情形中目标函数值的最大值。边界条件由下式给出

$$\phi_{n_1,n_2,n_3,n_4}=\max_{1\leq k\leq 4} m_{n_k}.$$

注意，每个表项最多有 $4+1=5$ 种情况（情况数最多出现在 $j_1=j_2=j_3=j_4=j$ 时）。因此，计算每个表项需要 $O(1)$ 时间。表项数量至多为 $n^5$，因此填表时间为 $O(n^5)$（试着弄清楚在自底向上方法中填表所需的顺序！）。注意，这主导了对区间排序以及对 $n_j$ 进行预处理的 $O(n\log n)$ 时间。因此，总运行时间为 $O(n^5)$。

请注意，上述动态规划中的坐标 $j$ 可以去掉，而不会改变动态规划方程的本质结构。于是，运行时间变为 $O(n^4)$。

## 4.3. 最大子数组问题

### 问题

设计并实现一个高效程序，在一维整数数组中查找具有最大和的连续子数组。请注意，输入数组中至少有一个正整数。

### Kadane 算法

有一种称为 Kadane 算法的扫描算法，它从最左侧元素开始并扫描到最右侧元素，以跟踪最大和子数组。它适用于动态规划框架，因为它具有最优子结构，即利用截至第 $(i-1)$ 个元素的最大和子数组来求截至第 $i$ 个元素的最大和子数组。

该算法在 `max_ending_here` 中累加部分和，并适当地更新当前最大值 `max_so_far`。只要部分和保持为正，就用第 $i$ 个索引中的值来增加它；否则将其重置为零。

如果数组的所有元素都是非负的，那么这个问题是平凡的，因为整个数组就是解。类似地，如果所有元素都是非正的，则解为空，值为 0。因此，我们考虑同时包含正值和负值的数据集。

#### 算法 63. Kadane 一维算法

```text
1: function KADANE1D(start, end)
2:     max_so_far ← 0
3:     max_ending_here ← 0
4:     while start ≠ end do
5:         max_ending_here ← max(max_ending_here + *start, 0)
6:         max_so_far ← max(max_so_far, max_ending_here)
7:         start ← start + 1
8:     end while
9:     return max_so_far
10: end function
```

#### C++11 实现

程序 4.4：实现 Kadane 算法

```cpp
#include <algorithm>

template <typename ForwardIterator>
typename std::iterator_traits<
    ForwardIterator>::value_type
kadane1d(ForwardIterator start,
         ForwardIterator end)
{
    typedef typename std::iterator_traits<
        ForwardIterator
    >::value_type value_type;

    value_type max_so_far = 0,
               max_ending_here = 0;

    while (start != end)
    {
        max_ending_here =
            std::max(max_ending_here + *start++,
                     0);
        max_so_far =
            std::max(max_so_far, max_ending_here);
    }
    return max_so_far;
}
```

#### 用法

程序 4.5：实现 Kadane 算法

```cpp
#include <iostream>
#include <array>
#include <vector>
#include <forward_list>
#include "kadane1d.hpp"

int main()
{
    std::array<int, 8> a
        {-2, -3, 4, -1, -2, 1, 5, -3};

    std::cout << kadane1d(a.cbegin(), a.cend())
              << std::endl;

    std::vector<int> v
        {-1, 4, -2, 5, -5, 2, -20, 6};

    std::cout << kadane1d(v.cbegin(), v.cend())
              << std::endl;

    std::forward_list<int> l
        {-2, 1, -3, 4, -1, 2, 1, -5, 4};

    std::cout << kadane1d(l.cbegin(), l.cend())
              << std::endl;
}
```

它输出

```text
7
7
6
```

### 查找最大子数组的索引

#### 问题

设计并实现一个高效程序，在一维整数数组中查找具有最大和的连续子数组。结果应包含子数组的和以及 (start, end)。

容易看出

- 最大子数组以正元素开始并以正元素结束
- 如果我们从第一个正元素（即 a[l]）开始，并对后续元素求和，直到在 a[r] 处和变为负，那么最优子数组要么
  - 在 a[l..r] 中且从 a[l] 开始，要么
  - 在 a[r + 1..n] 中。

#### 算法 64. Kadane 一维算法：查找索引

```text
 1: function KADANE1D(start, end)
 2:     max_so_far ← 0
 3:     max_ending_here ← 0
 4:     l ← 0
 5:     r ← 0
 6:     l_i ← 0
 7:     while start ≠ end do
 8:         max_ending_here ← (max_ending_here + *start)
 9:         if max_ending_here < 0 then
10:             max_ending_here ← 0
11:             l_i ← start + 1
12:         end if
13:         if max_so_far < max_ending_here then
14:             max_so_far ← max_ending_here
15:             l ← l_i
16:             r ← start
17:         end if
18:         start ← start + 1
19:     end while
20:     return <max_so_far, l, r>
21: end function
```

#### C++11 实现

程序 4.6：实现 Kadane 算法：查找索引

```cpp
#include <algorithm>
#include <tuple>

template <typename ForwardIterator>
std::tuple<typename std::iterator_traits<
                         ForwardIterator
                         >::value_type,
           ForwardIterator, ForwardIterator>
kadane1d(ForwardIterator start,
         ForwardIterator end)
{
    typedef typename std::iterator_traits<
                         ForwardIterator
                         >::value_type value_type;

    value_type max_so_far = 0, max_ending_here = 0;

    ForwardIterator l, r, l_i = start;

    while (start != end)
    {
        max_ending_here += *start;
```
