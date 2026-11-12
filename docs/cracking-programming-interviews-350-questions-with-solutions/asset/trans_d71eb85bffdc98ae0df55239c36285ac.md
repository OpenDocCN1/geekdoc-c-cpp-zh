

```cpp
const std::string &s1,
const std::string &s2)
{
    const size_t len1 = s1.size(),
               len2 = s2.size();

    std::vector<size_t> col(len2 + 1),
                        prevCol(len2 + 1);

    for(size_t i = 0; i < prevCol.size(); i++)
        prevCol[i] = i;

    for (size_t i = 0; i < len1; i++)
    {
        col[0] = i+1;

        for (size_t j = 0; j < len2; j++)
        {
            col[j+1] =
                std::min(
                    std::min(
                        1 + col[j],
                        1 + prevCol[1 + j]
                    ),
                    prevCol[j] + (s1[i]==s2[j]
                        ? 0 : 1)
                );
        }
        col.swap(prevCol);
    }
    return prevCol[len2];
}

int main()
{
    assert(levenshtein_distance(
        "cat", "act") == 2);

    assert(levenshtein_distance(
        "COIN", "CON") == 1);
}
```

程序 4.3：Boost 实现：Levenshtein 编辑距离

```cpp
#include <boost/numeric/ublas/matrix.hpp>

int levenshtein_distance(
    const std::string & s1,
    const std::string & s2)
{
    const size_t len1 = s1.length(),
               len2 = s2.length();

    boost::numeric::ublas::matrix<size_t> m(
        len1 + 1, len2 + 1);

    for(size_t i = 0; i < len1 + 1; ++i)
    {
        m(i, 0) = i;
    }

    for(size_t j = 0; j < len2 + 1; ++j)
    {
        m(0, j) = j;
    }

    size_t cost, cell_cost, min_cost = 0;

    for(size_t i = 0; i < len1; ++i)
    {
        cost = 0;

        for(size_t j = 0; j < len2; ++j)
        {
            cell_cost = 1;

            if(s1[i] == s2[j])
            {
                cell_cost = 0;
            }

            min_cost = m(i, j);

            if(min_cost > m(i, j + 1))
                min_cost = m(i, j + 1);

            if(min_cost > m(i + 1, j))
                min_cost = m(i + 1, j);

            cell_cost += min_cost;
            m(i + 1, j + 1) = cell_cost;

            if(i == 0)
                cost = cell_cost;
            else
            {
                if(cell_cost < cost)
                    cost = cell_cost;
            }
        }
    }

    return m(len1, len2);
}

int main()
{
    assert(levenshtein_distance(
        "cat", "act") == 2);

    assert(levenshtein_distance(
        "combo", "coin") == 3);
}
```

### 时间复杂度

对于 $D(i,j)$ 的计算，我们只考察单元格 $D(i-1,j-1)$、$D(i,j-1)$ 和 $D(i-1,j)$，以及 2 个字符 $S_1[i]$ 和 $S_2[j]$。因此，填充一个单元格需要常数次单元格检查、算术运算和比较。由于上面计算的表中有 $m \times n$ 个单元格，所以 $D(m,n)$ 的总时间复杂度为 $O(mn)$。

### 递推关系：计算 Damerau 编辑距离

- $D(i,0)=i$
- $D(0,j)=j$

那么 $D(i,j)$ 是以下三种可能之一：

1. $D(i-1,j-1)$，若 $S_1[i] == S_2[j]$
2. $1 + \min(D(i-2,j-2),D(i-1,j),D(i,j-1))$，若 $S_1[i-1..i] == \operatorname{reverse}(S_2[j-1..j])$
3. $1 + \min(D(i-1,j-1),D(i-1,j),D(i,j-1))$，否则。

我们将此算法的实现留作读者的练习。

### 空间优化

这些基本动态规划算法显然具有 $O(mn)$ 的运行时间和空间消耗，因为它们要填充 $O(mn)$ 个单元格，而填充单个单元格需要常数次操作和空间。当使用按列填充 $D$ 的顺序时，可以简单地将所需空间降至 $O(m)$。当填充第 $j$ 列时，只需要前一列或前两列中的单元格值，具体取决于使用的是 Levenshtein 距离还是 Damerau 距离。这意味着在计算第 $j$ 列时，内存中只需要保留第 $(j-1)$ 列，或者还保留第 $(j-2)$ 列，因此所需空间为 $O(m)$。

### 性质

容易验证，以下性质对于 *Levenshtein* 和 *Damerau* 编辑距离下的 D 的编辑距离计算版本和近似字符串匹配版本都成立：

- **对角性质**：$D(i,j)-D(i-1,j-1)=0$ 或 $1$
- **邻接性质**：
  - $D(i,j)-D(i,j-1)=-1$、$0$ 或 $1$，且
  - $D(i,j)-D(i-1,j)=-1$、$0$ 或 $1$

### 归约为单源最短路径问题

动态规划方法给出的解法涉及构造一个大小为 $m \times n$ 的表，其中每个表项对应一个 *部分编辑*，目标是计算该表的 *最右下方的表项*，即 $D(m,n)$。

看待该问题的另一种方式是将表中的每个表项视为有向图的一个顶点。因此，一个顶点对应一个 *部分编辑*。如果与 $j$ 对应的部分编辑比与 $i$ 对应的部分编辑多涉及一次编辑操作，则存在一条边 $(i, j)$。一个简化的有向图可以把插入描绘为水平边，把删除描绘为垂直边，把替换（或替代）描绘为对角边。

因此，字符串编辑距离问题被归约为单源最短路径问题，即寻找从顶点 $(0,0)$ 到顶点 $(m,n)$ 的一条最短路径。我们将实现细节留作读者的练习。

## 4.2 音乐识别

竖笛是一种简单的吹奏乐器，听起来很像长笛。Lin Quan 教授最近编写程序让他的计算机聆听来自竖笛的一段音乐流，并将其转换为一个时间区间集合 $T = \{T_1, T_2, \ldots, T_n\}$（这些区间可能重叠），其中每个区间对应该系统转写出的一个音符的持续时间。此外，教授还开发了一种启发式方法，对于每个区间 $T_i \in T$，给出一个度量 $m_i$，表示音符 $i$ 由竖笛演奏的可能性。$m_i$ 越大，音符 $i$ 由竖笛演奏的置信度越高。

### 问题描述

教授希望确定哪些音符是由竖笛演奏的。由于（正确演奏时）竖笛一次只能发出一个音符，因此如果两个区间有公共交集，则其中一个音符必定是虚假的（由背景噪声产生）。请给出一个高效算法，确定一个互不重叠的区间集合 $S' \subseteq T$（表面上对应竖笛演奏的音符），使得下式最大化

$$\sum_{T_i \in S'} m_i$$

### 解法

我们将使用动态规划来解决这个问题。令 $start(T_j)$ 和 $end(T_j)$ 分别表示区间 $T_j$ 的开始时间和结束时间。首先，按开始时间递增的顺序对区间排序。这需要 $O(n \log n)$ 时间。当然，如果区间已经按此顺序排好，我们可以跳过这一步。这似乎是合理的，因为记录器是按开始时间递增的顺序遇到这些时间区间的。

我们的子问题具有以下形式：寻找一个互不重叠的区间集合 $S = \{T_j, T_{j+1}, \ldots, T_n\}$，使得量（以下称为目标函数）

$$\sum_{T_i \in S} m_i$$

最大化。因此，共有 $n$ 个子问题，每个 $1 \leq j \leq n$ 对应一个子问题。令 $n_j$ 为满足 $start(T_{j'}) > end(T_j)$ 的最小 $j'$ 值。也就是说，如果在区间 $T_j$ 内演奏该乐器，那么之后最早可以演奏该乐器的区间是 $T_{n_j}$。令 $\phi_j$ 为子问题 $\{T_j,T_{j+1},\ldots,T_n\}$ 的目标函数最大值。原问题的答案是 $\phi_1$。

在子问题 $\{T_j,T_{j+1},\ldots,T_n\}$ 的任意一个最优互不重叠区间子集中，对于时间区间 $T_j$ 有两种可能的情况。容易看出这两种情况下的目标函数。

**情况 1：** 在区间 $T_j$ 内没有演奏该乐器。那么，最优子集的目标函数值等于 $\phi_{j+1}$。

**情况 2：** 在区间 $T_j$ 内演奏了该乐器。那么，之后最早可以演奏该乐器的区间是 $T_{n_j}$。在这种情况下，最优子集的目标函数值为 $m_j + \phi_{n_j}$。

结合上述两种情况，我们有

$$\phi_j = \max(\phi_{j+1}, m_j + \phi_{n_j})$$

该动态规划的边界条件由 $\phi_n = m_n$ 给出。可以按 $j$ 值递减的顺序自底向上填充该表。如果预先计算了所有 $n_j$，则计算每个表项需要 $O(1)$ 时间。因此，填充该表的时间为 $O(n)$。预先计算所有 $n_j$ 需要 $O(n \log n)$ 时间（试着弄清楚

