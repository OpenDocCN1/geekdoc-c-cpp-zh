

## 1.13 搜索二维有序数组

列索引。因此，让我们利用在查找第一次出现位置并进而查找所有出现位置的解法中获得的洞见，对鞍背搜索进行必要的修改。

### 算法 27 鞍背计数——正确算法

```text
function SADDLEBACK-COUNT(a[0..m-1, 0..n-1], x)
i ← 0
j ← n − 1
current_col_index ← j
count ← 0
while j ≤ n − 1 do
    if a[i, j] < x then
        i ← i + 1
    else if a[i, j] > x then
        j ← j − 1
    else if a[i, j] == x then
        current_col_index ← j
        while current_col_index ≥ 0 and
              a[i][current_col_index] == x do
            count ← count + 1
            current_col_index ← current_col_index − 1
        end while
        i ← i + 1
    end if
end while
return count
end function
```

### 程序 1.26：实现鞍背计数

```cpp
#include <algorithm>
#include <array>

template <int m, int n>
using TwoDimArray
    = std::array<std::array<int, n>, m>;

template <int m, int n>
size_t saddleback_count(
    TwoDimArray<m, n> & a, int x)
{
    size_t i = 0, j = n - 1, count = 0;
    int current_col_index = j;

    while (j <= n - 1)
    {
        if (a[i][j] < x) i += 1;
        else if (a[i][j] > x) j -= 1;
        else // a[i][j] == x
        {
            current_col_index = j;
            while (current_col_index >= 0 &&
                   a[i][current_col_index] == x)
            {
                ++count;
                current_col_index--;
            }
            ++i;
        }
    }

    return count;
}
```

### 程序 1.27：使用鞍背计数

```cpp
1 #include "saddleback_count_correct.hpp"
2 #include <iostream>
3
4 int main()
5 {
6     TwoDimArray<4, 4> a = { 2, 2, 3, 5,
7                            3, 4, 6, 6,
8                            3, 5, 6, 6,
9                            3, 6, 6, 9
10                        };
11
12     size_t count
13         = saddleback_count<4, 4>(a, 6);
14
15     std::cout << "Count of 6 is: "
16               << count << std::endl;
17 }
```

输出结果为：

```text
Count of 6 is: 6
```

### 程序 1.28：鞍背计数的另一种用法

```cpp
#include "saddleback_count_correct.hpp"
#include <iostream>

int main()
{
    TwoDimArray<4, 4> a = {
        6, 6, 6, 6,
        6, 6, 6, 6,
        6, 6, 6, 6,
        6, 6, 6, 6
    };

    size_t count
        = saddleback_count<4, 4>(a, 6);

    std::cout << "Count of 6 is: "
              << count << std::endl;
}
```

输出结果为：

```text
Count of 6 is: 16
```

时间复杂度与查找所有出现位置的算法相同，即 $O(mn)$。

### 备注

该算法被称为*鞍背搜索*，因为搜索空间被限制在一个区域内，该区域左上角为最小元素，右下角为最大元素，两个环使其看起来像一个马鞍。

## 1.14 汉明问题

### 问题描述

考虑序列 $Seq: q = 1, 2, 3, 4, 5, 6, 8, 9, 10, 12, \ldots$，该序列由所有除 2、3 和 5 之外没有其他质因数的数组成。描述 $Seq$ 的另一种方式是给出其中数值的出现顺序：

- 1. **公理 1：** 1 在 $Seq$ 中。
- 2. **公理 2：** 如果 $x$ 在 $Seq$ 中，那么 $2 \times x$、$3 \times x$ 和 $5 \times x$ 也在 $Seq$ 中。
- 3. **公理 3：** $Seq$ 中唯一的数值由公理 1 和公理 2 给出。

编写一个程序，按顺序将 $Seq$ 的前 1000 个值存储在数组 $q[0..999]$ 中，即建立……

$R: q[0..999]$ 按顺序包含 $Seq$ 的前 1000 个值。

### 解法

由于公理 2 规定，如果一个较小的值在 $Seq$ 中，那么某个值也在 $Seq$ 中，因此按顺序生成这些值可能是有意义的。那么，一种可能性是将 $R$ 中的常量 1000 替换为变量 $i$，从而得到不变量

$P = 1 \leq i \leq 1000 \land q[0..i-1]$ 包含 $Seq$ 的前 $i$ 个值。

有了这个不变量，明显的程序结构是：

```text
1: i ← 1
2: q[0] ← 1                                          ▷ P
3: while i ≠ 1000 do                 ▷ 不变量：P；界：1000 − i
4:     计算 xnext，即 Seq 中的第 i 个值
5:     i ← i + 1
6:     q[i] ← xnext
7: end while
```

剩下的问题是确定如何计算 xnext，即要生成的下一个 Seq 值。由于 Seq 的值是按顺序生成的，xnext 必须 ≥ q[i − 1]。其次，由于 1 已经在 q[0..i − 1] 中，xnext 必须满足上述公理 2。这意味着 xnext 必须具有 2 × x、3 × x 或 5 × x 的形式，其中 x 是 q[0..i − 1] 中已有的某个值。因此

xnext 是形式为 2 × x、3 × x 或 5 × x（x 在 q[0..i − 1] 中）的大于 q[i − 1] 的最小值。

因此，我们引入三个变量 x2、x3 和 x5，其含义如以下断言 P1 所述：

  - x2 是形式为 2 × x（x 在 q[0..i − 1] 中）的大于 q[i − 1] 的最小值
  - x3 是形式为 3 × x（x 在 q[0..i − 1] 中）的大于 q[i − 1] 的最小值
  - x5 是形式为 5 × x（x 在 q[0..i − 1] 中）的大于 q[i − 1] 的最小值

值 xnext 是 x2、x3 和 x5 中的最小值。因此，我们看到变量 xnext 实际上并不需要，我们将程序结构修改为：

```text
1: i ← 1
2: q[0] ← 1
3: while i ≠ 1000 do                 ▷ 不变量：P；界：1000 − i
4:     计算 x2, x3, x5 以满足 P1
5:     i ← i + 1
6:     q[i] ← min(x2, x3, x5)
7: end while
```

现在我们演示如何将断言从循环中取出。在每次迭代中计算 x2、x3 和 x5 以建立 P1 可能很耗时。然而，随着 i 的增加并且 P1 保持为不变量，它们的变化相当缓慢，因此有可能通过将 P1 从循环中取出并使其成为循环不变量的一部分来加速算法。q[0..i − 1] 有序这一事实也带来了额外的希望。因此，我们研究以下程序结构：

### 算法 28 汉明问题

```text
 1: i ← 1
 2: q[0] ← 1                                      ▷ P
 3: 建立 P₁
 4: x₂ ← 2
 5: x₃ ← 3
 6: x₅ ← 5
 7: j₂ ← 0
 8: j₃ ← 0
 9: j₅ ← 0
10: while i ≠ 1000 do                             ▷ 不变量：P ∧ P₁；界：1000 − i
11:     i ← i + 1
12:     q[i] ← min(x₂, x₃, x₅)                     ▷ 重新建立 P₁
13:     while x₂ ≤ q[i − 1] do
14:         j₂ ← j₂ + 1
15:         x₂ ← 2 × q[j₂]
16:     end while
17:     while x₃ ≤ q[i − 1] do
18:         j₃ ← j₃ + 1
19:         x₃ ← 3 × q[j₃]
20:     end while
21:     while x₅ ≤ q[i − 1] do
22:         j₅ ← j₅ + 1
23:         x₅ ← 5 × q[j₅]
24:     end while
25: end while
```

## 1.15 常数时间范围查询

### 问题

描述一种算法，给定 0 到 k 范围内的 n 个整数，该算法处理其输入，然后以 O(1) 时间回答关于这 n 个整数中有多少个落在范围 [a..b] 内的任何查询。该算法应使用 Θ(n + k) 的预处理时间。

### 解法

按照下面描述的计数排序方式计算 C 数组。

计数排序假设 n 个输入元素中的每一个都是 0 到 k 范围内的整数，其中 k 为某个整数。当 k = O(n) 时，排序运行时间为 Θ(n)。

计数排序的基本思想是：对于每个输入元素 x，确定小于 x 的元素个数。此信息可用于将元素 x 直接放置到输出数组中的相应位置。

在计数排序的代码中，我们假设输入是数组 A[1..n]，因此 length[A] = n。我们还需要另外两个数组：

- 1. 数组 B[1..n] 保存排序后的输出，
- 2. 数组 C[0..k] 提供临时工作存储。

```text
算法 29 计数排序算法
1: function COUNTING-SORT(A, B, k)
2:     for i ← 0 to k do
3:         C[i] ← 0
4:     end for
5:     for j ← 1 to length[A] do
6:         C[A[j]] ← C[A[j]] + 1    ▷ C[i] 现在包含等于 i 的元素个数。
7:     end for
8:     for i ← 1 to k do
9:         C[i] ← C[i] + C[i - 1]   ▷ C[i] 现在包含小于或等于 i 的元素个数。
10:    end for
11:    for j ← length[A] downto 1 do
12:        B[C[A[j]]] ← A[j]
13:        C[A[j]] ← C[A[j]] - 1
14:    end for
15: end function
```

### 时间复杂度

- 1. 第 2-4 行的 for 循环耗时 Θ(k)，
- 2. 第 5-7 行的 for 循环耗时 Θ(n)，
- 3. 第 8-10 行的 for 循环耗时 Θ(k)，
- 4. 第 11-14 行的 for 循环耗时 Θ(n)。

因此，总时间为 Θ(k + n)。

在实践中，我们通常在使用计数排序时令 k = O(n)，这种情况下运行时间为 Θ(n)。

计数排序击败了 Ω(n log n) 的下界，因为它不是比较排序。实际上，程序中任何地方都不会对输入元素进行比较。相反，计数排序使用元素的实际值来索引数组。当我们偏离比较排序模型时，排序的 Θ(n log n) 下界不适用。

计数排序的一个重要性质是它是稳定的：具有相同

