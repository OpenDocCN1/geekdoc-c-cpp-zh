

## 2.23 找出一个不能由数组子集和表示的数

### 问题描述

一个非递减整数数组 $a[1..n]$ 仅包含正数。找出最小的正整数，使得它不能表示为该数组若干元素的和（每个元素最多使用一次）。操作次数应为 $O(n)$。

### 解法

假设对于某个 $N$，所有可由 ${a[1],...,a[k]}$ 的子集和表示的数构成集合 ${1,2,...,N}$。如果 $a[k+1]$ 大于 $N+1$，则 $N+1$ 是不能表示为 ${a[1],...,a[k]}$ 的某些子集和的最小数。如果 $a[k+1] \leq N+1$，则所有可由 ${a[1],...,a[k+1]}$ 的子集和表示的数构成集合 ${1,2,...,N+a[k+1]}$。

```
Algorithm 60 Find a number not sum of subsets of array

1: $k \leftarrow 0$
2: $N \leftarrow 0$
3: Invariant: all the numbers that can be represented as sums of subsets of ${a[1],...,a[k]}$, form the set ${1,2,...,N}$
4: while $k+1 \leq n$ and $a[k+1] \leq N+1$ do
5:     $N \leftarrow N+a[k+1]$
6:     $k \leftarrow k+1$
7: end while ▷ $(k=n)$ or $(a[k+1]>N+1)$; the answer is $N+1$ in both cases
8: print(N+1)
```

## 2.24 两个有序数组中的第 $k$ 小元素

### 问题描述

给定两个有序数组 $a[1..n]$ 和 $b[1..m]$，找出这两个数组的并集中第 $k$ 小的元素。时间复杂度应为 $O(\log n + \log m)$。

### 解法

我们要在数组 $a[1,...,n]$ 和 $b[1,...,m]$ 的并集中寻找第 $k$ 小的元素 $x_k$。

由于我们要找的是第 $k$ 小的元素，我们可以将注意力限制在数组 $a[1,...,k]$ 和 $b[1,...,k]$ 上。如果 $k>m$ 或 $k>n$，我们可以将相应数组中索引大于 $k$ 的越界元素视为无穷大。

### 正确性证明

我们的算法首先比较 $a[\lfloor k/2\rfloor]$ 和 $b[\lceil k/2\rceil]$：

- 假设 $a[\lfloor k/2\rfloor] > b[\lceil k/2\rceil]$，则：
  - 在 $a$ 和 $b$ 的并集中，小于 $b[\lceil k/2\rceil]$ 的元素至多有 $k-2$ 个，即 $a[1,\ldots,\lfloor k/2\rfloor-1]$ 和 $b[1,\ldots,\lceil k/2\rceil-1]$，因此必有 $s_k > b[\lceil k/2\rceil]$。
  - 类似地，所有 $a[1,\ldots,\lfloor k/2\rfloor]$ 和 $b[1,\ldots,\lceil k/2\rceil]$ 中的元素都将小于 $a[\lfloor k/2\rfloor]$。但这些共有 $k$ 个元素，所以我们必有 $s_k < a[\lfloor k/2\rfloor+1]$。

这表明 $s_k$ 一定包含在子数组 $a[1,\ldots,\lfloor k/2\rfloor]$ 和 $b[\lceil k/2\rceil+1,\ldots,k]$ 的并集中。

特别地，由于我们丢弃了 $\lceil k/2\rceil$ 个小于 $s_k$ 的元素，$s_k$ 将是该并集中第 $\lfloor k/2\rfloor$ 小的元素。

然后我们可以通过在这个更小的问题上递归来找到 $s_k$。

- 当 $a[\lfloor k/2\rfloor] < b[\lceil k/2\rceil]$ 时，情况是对称的。
- 最后一种情况也是递归的基准情况，即 $a[\lfloor k/2\rfloor] = b[\lceil k/2\rceil]$，此时有 $s_k = a[\lfloor k/2\rfloor] = b[\lceil k/2\rceil]$。

## 2.25 对子序列组成的序列进行排序

### 问题描述

有一个由 $n$ 个元素组成的序列 $S$ 需要排序。输入序列由 $n/k$ 个子序列组成，每个子序列包含 $k$ 个元素。给定子序列中的元素都小于其后一个子序列中的元素，且大于其前一个子序列中的元素。时间复杂度应为 $\Omega(n\log k)$。

### 解法

要对长度为 $n$ 的整个序列进行排序，只需对 $n/k$ 个子序列中的每个子序列里的 $k$ 个元素进行排序。请注意，简单地将各个子序列的下界组合起来，并不能达到解决这个排序问题变体所需的比较次数下界。那只能证明不存在更快地独立排序这些子序列的算法。

现在，考虑对 $S$ 进行任意比较排序的决策树，其高度为 $h$。由于每个子序列中的元素可以按任意顺序排列，$k!$ 个排列中的任何一个都对应于某个子序列的最终排序。又因为有 $n/k$ 个子序列，每个子序列都可以按任意顺序排列，因此 $S$ 有 \((k!)^{n/k}\) 种排列可能对应于某个输入顺序的排序结果。

因此，任何用于排序 \(S\) 的决策树至少必须有 \((k!)^{n/k}\) 个叶节点。由于高度为 \(h\) 的二叉树至多有 \(2^h\) 个叶节点，我们必须有

$$2^h \ge (k!)^{n/k}$$

$$\Longrightarrow\quad h \ge \log\left((k!)^{n/k}\right) = \frac{n}{k}\log(k!)$$
$$\ge \frac{n}{k}\log\left(\left(\frac{k}{2}\right)^{k/2}\right)$$
$$= \frac{n}{2}\log\left(\frac{k}{2}\right)$$

由于对 \(S\) 排序的任何决策树中至少存在一条长度至少为 \(\frac{n}{2}\log(k/2)\) 的路径，因此任何基于比较的排序算法对 \(S\) 的最坏情况运行时间均为 \(\Omega(n\log k)\)。

## 2.26 找出缺失的整数

### 问题

数组 \(a[0..n-1]\) 包含 \([0..n]\) 中除一个之外的所有整数。在固定额外内存的限制下找出这个缺失的整数。操作次数应与 \(n\) 成正比。

### 解法

- 1. 计算所有数的总和：\(total = \frac{n(n+1)}{2}\)
- 2. 从总和中依次减去所有数，即可得到缺失的数。

程序 2.8：找出缺失的整数

```cpp
#include <vector>
#include <iostream>

int find_missing_number(std::vector<int> & v, int n)
{
    int total = n*(n + 1)/2;

    for(auto e : v)
        total -= e;
}

int main()
{
    std::vector<int> v {1, 2, 3, 5, 6};
    std::cout << find_missing_number(v, 6) << std::endl;
}
```

输出：

```text
4
```

## 2.27 原地反转

### 问题描述

给定数组 a[1..n]，在不使用其他数组的情况下，将其元素按相反顺序排列。

### 解法

对所有满足 $i<n+1-i$ 的 $i$ 执行 $swap(a[i], a[n+1-i])$，即 $2i<n+1\ \Longleftrightarrow\ 2i\le n\ \Longleftrightarrow\ i\le \frac{n}{2}$。

**算法 62** 原地反转数组

|  |  |
|---|---|
| 1: | 函数 REVERSE-INPLACE(a[1..n]) |
| 2: | 对于 i ← 1 到 $\frac{n}{2}$ 执行 |
| 3: | &nbsp;&nbsp;&nbsp;&nbsp;交换 a[i] 和 a[n + 1 − i] |
| 4: | 结束循环 |
| 5: | 结束函数 |

## 2.28 找出数组中出现一次的数

### 问题描述

数组 $a[0..n−1]$ 包含一些整数，每个元素都出现两次，只有一个元素只出现一次。在固定额外内存的限制下找出这个元素。操作次数应与 $n$ 成正比。

### 解法

利用异或（xor）运算，我们可以找出出现奇数次的数。

- 异或运算满足交换律和结合律（因此运算顺序无关紧要）。
- 一个数与其自身异或的结果总是零。
- 零与一个数异或的结果是该数。

因此，如果我们简单地将所有值异或在一起，所有出现两次的值将相互抵消（得到 0），而剩下的那个数（值）再与这个结果（0）异或，得到该值本身。

程序 2.9：找出数组中出现一次的数

```cpp
#include <vector>
#include <iostream>

size_t get_orphan(std::vector<int> & v)
{
    int value = 0;

    for (auto e : v)
        value ^= e;

    std::cout << "number: " << value << std::endl;
    // value now contains the number that occurred
    // odd number of times.
    // Retrieve its index in the array.

    size_t len = v.size();

    size_t index_orphan = -1;

    for (size_t index = 0; index < len; ++index)
    {
        if (v[index] == value)
        {
            index_orphan = index;
            std::cout << "index: " << index_orphan
                      << std::endl;
            return index_orphan;
        }
    }
    return index_orphan;
}

int main()
{
    std::vector<int> v {12, 8, 14, 13, 3, 12, 13,
        8, 14};
}
```

