
## 4.3. 最大子数组问题

它打印出

```text
Printing Prefix Array with Value and Original Index
8:0 5:1 7:2 8:3 4:4 14:5 9:6
Printing Value Sorted Prefix Array
4:4 5:1 7:2 8:0 8:3 9:6 14:5
Printing Pairwise Value Differences with
original indices
(1:4:1) (2:1:2) (1:2:0) (0:0:3) (1:3:6) (5:6:5)
Subarray with sum closest to zero is
-3 2 1

Printing Prefix Array with Value and Original Index
-3:0 -1:1 3:2 -3:3 -11:4 -1:5 10:6
Printing Value Sorted Prefix Array
-11:4 -3:0 -3:3 -1:1 -1:5 3:2 10:6
Printing Pairwise Value Differences with
original indices
(8:4:0) (0:0:3) (2:3:1) (0:1:5) (4:5:2) (7:2:6)
Subarray with sum closest to zero is
2 4 -6

Printing Prefix Array with Value and Original Index
10:0 8:1 1:2
Printing Value Sorted Prefix Array
1:2 8:1 10:0
Printing Pairwise Value Differences with
original indices
(7:2:1) (2:1:0)
Subarray with sum closest to zero is
10 -2 -7
```

### 查找和最接近 k 的子数组

### 问题

找到一个和值最接近整数 s 的子数组。

从前一个问题可以看出，a[l..k] 的和 =
prefixa[k] - prefixa[l - 1] = s

因此，为了找到和最接近零的子数组，我们只需在前缀数组中定位两个在 k 距离意义上最接近的元素。

练习的其余部分留给读者完成。

### 最大二维子数组问题

### 问题

设计并实现一个高效程序，在二维整数数组中寻找一个具有最大和的连续二维子数组。

Bentley 给出了一种基于 Kadane 一维算法的巧妙算法，用于在二维数组中解决此问题，从而使其看起来像 Kadane 的二维算法。

它将 Kadane 算法应用于每一个可能的行区间，对每个区间内的行求和，生成一维数组，供 Kadane 算法寻找最优列和。Bentley 算法的核心思想之一是*前缀和*，其目的是在处理后续行区间时避免重复求和。

一维 Kadane 算法先运行在数组每一行的元素（*row₁, row₂ … rowₘ*）上，将这些行视为一维流，然后运行在每一对行的和（*row₁ + row₂, row₁ + row₃ … row₁ + rowₘ*）上。解由一维 Kadane 算法在这些情况下产生的最大和给出。如果 *x₁* 和 *x₂* 是指向最大子流的起点和终点的指针，且 *Rowᵢ* 和 *Rowⱼ* 是求和最大的两行相加行，则解由左上角 (*Rowᵢ, x₁*) 和右下角 (*Rowⱼ, x₂*) 给出的矩形界定。该算法可总结如下：

- 1. 在长度为 m 的维度上计算*前缀数组*。这需要 *O(mn)* 次计算。
- 2. 如果最大子数组位于 *Rowᵢ* 和 *Rowⱼ*（包含端点）之间，则有 \(\frac{m(m+1)}{2}\) 个这样的对。
- 3. 对于给定列，*Rowᵢ* 和 *Rowⱼ* 之间数组元素的和已经作为前缀和的一部分计算出来。因此每个列和看起来就像跨所有列的一维数组中的单个元素，即它看起来像一个一行 *n* 列的一维数组。
- 4. 对这些对应用 Kadane 一维算法，以得到如上所述的最大子数组。因此总时间复杂度为 *O(m²n²)*。

让我们将该算法形式化如下：

- 1. 令输入数组为 *a[0..m, 0..n]*，即它有 m 行和 n 列。令 *aᵢ* 表示该数组的第 *i* 行。
- 2. 令前缀数组的第 $i^{th}$ 行表示为 $prefixa_i$，它表示 $a_1 + a_2 ... a_i$。
- 3. 请注意 $prefixa_i = prefixa_{i-1} + a_i$，其中 $i \in 1..m$。如前所述，前缀数组的计算需要 $mn$ 次加法。因此
  $a_i = prefixa_i - prefixa_{i-1}$
- 4. 容易看出，对行 $l$ 到 $k$ 求和，即 $a[l..k]$，可以计算为
  $a_l + a_{l+1} + \cdots + a_{k-1} + a_k =$
  $prefixa_l - prefixa_{l-1} +$
  $prefixa_{l+1} - prefixa_l +$
  $\vdots$
  $prefixa_{k-1} - prefixa_{k-2} +$
  $prefixa_k - prefixa_{k-1} =$
  $prefixa_k - prefixa_{l-1}$
  这些包含 $m(m+1)/2$ 对。
- 5. 对每个区间 $[l,k]$，将 Kadane 一维算法应用于 $prefixa_k - prefixa_{l-1}$，以找到最大和。因此总体时间复杂度为 $O(m^2 n)$。

我们将 C++ 编码练习留给读者。

### K-最大子数组问题

### 问题

设计并实现一个高效程序，找出和最大的 $K$ 个子数组。请注意，一维或二维数组的最大子数组问题，是寻找数组中使其元素之和最大的数组部分。

让我们回顾前缀数组概念：$a[l..k] = prefixa[k] - prefixa[l - 1]$。为了找到最大子数组 $a[l..k]$，我们必须找到使项 $a[l..k]$ 之和最大的索引 $l$ 和 $k$。令 $minprefixa[i]$ 表示子数组 $a[0..i - 1]$ 的最小前缀数组。$max(a[l..k]) = max(prefixa[k] - prefixa[l - 1]) = max(prefixa[k] - minprefixa[k])$。因此，为了计算最大子数组，我们只需累加前缀和，同时维护先前前缀和的最小值，该最小值可以从累加的前缀和中减去，以得到目前为止的最大和。

### 算法65 使用前缀数组的最大子数组和

```text
1: function MAXSUBARRAY(a[0..n − 1])
2:     minprefixsum ← 0
3:     currmaxsum ← 0
4:     prefix[0] ← 0
5:     for i ← 0, n − 1 do
6:         prefix[i] ← prefix[i − 1] + a[i]
7:         cand ← prefix[i] − minprefixsum
8:         currmaxsum ← max(currmaxsum, cand)
9:         minprefixsum ← min(minprefixsum, prefix[i])
10:    end for
11:    return max_so_far
12: end function
```

基于上述算法，我们可以很容易地将其扩展为一维情形下的 K-最大子数组。我们不再使用单个变量来保存最小前缀和，而是维护一个包含 K 个最小前缀和的列表，并按非递减顺序排序。两个已排序序列 x 和 y 的合并列表记为 merge(x, y)。

### 算法66 使用前缀数组的 K-最大子数组和

```text
1: function KMAXSUBARRAY(a[0..n − 1])
2:     for k ← 1, K do
3:         min[k] ← −∞
4:         M[k] ← −∞
5:     end for
6:     sum[0] ← 0
7:     min[1] ← 0
8:     M[1] ← 0
9:     for i ← 1, n do
10:        sum[i] ← sum[i − 1] + a[i]
11:        for k ← 1, K do
12:            cand[k] ← sum[i] − min[k]
13:        end for
14:        M ← K largest elements of merge(M, cand)
15:        insert sum[i] into min
16:    end for
17: end function
```

由于需要执行 n 次迭代，总时间复杂度为 O(Kn)。当 K = 1 时，结果与 Kadane 算法和前缀数组的 O(n) 时间复杂度相当。

## 第5章：图

### 5.1 可靠分发

### 问题

一个通信网络由节点集合 $V$ 和有向边（通信链路）集合 $E \subset V \times V$ 组成。每条边 $e \in E$ 都有一个权重 $w(e) \geq 0$，表示使用 $e$ 的成本。从给定源 $s \in V$ 出发的分发，是一组由 $|V|-1$ 条有向路径组成的集合，这些路径从 $s$ 到 $V-\{s\}$ 中其他每个顶点。分发的成本是其组成路径的权重之和。（因此，某些边可能在分发成本中被多次计算。）

- 1. 给出一个高效算法，以确定从给定源 $s \in V$ 出发的最低成本分发。你可以假设所有节点 $V$ 都从 $s$ 可达。
- 2. 通信网络中的某条边可能失效，但我们不知道是哪一条。给出一个高效算法，以确定如果对手从 $E$ 中删除一条边，从 $s$ 出发的最低成本分发的成本最多可能增加多少。（如果对手能使某个顶点从 $s$ 不可达，则成本为无限大。）

### 解答

- 1. 该问题可以建模为单源最短路径问题。分发是一棵从 $s$ 到图中其他每个顶点的路径树。由于分发的成本是其路径长度之和，最小成本分发是一组最短路径。由于边权重非负，我们可以使用 Dijkstra 算法。使用二叉堆，Dijkstra 算法的运行时间可以从 $O(|V|^2)$ 改进到 $O((|V|+|E|)\log |V|)$。

