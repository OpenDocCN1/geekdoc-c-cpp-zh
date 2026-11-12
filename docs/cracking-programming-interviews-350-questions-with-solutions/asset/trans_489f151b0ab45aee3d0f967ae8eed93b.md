
## 6.5 加权中位数

使得和 \(\sum_{i=1}^{n} w_i d(p,p_i)\) 最小化，其中 \(d(a,b)\) 是点 \(a\) 和 \(b\) 之间的距离。

论证加权中位数是一维邮局选址问题的最优解，其中点就是实数，并且点 \(a\) 和 \(b\) 之间的距离为 \(d(a,b)=|a-b|\)。

- 5. 求二维邮局选址问题的最优解，其中点是 \((x,y)\) 坐标对，并且点 \(a=(x_1,y_1)\) 和 \(b=(x_2,y_2)\) 之间的距离是由 \(d(a,b)=|x_1-x_2|+|y_1-y_2|\) 给出的曼哈顿距离。

### 解答

- **1.** 令 \(x_k\) 为 \(x_1,x_2,\ldots,x_n\) 的中位数。根据中位数的定义，\(x_k\) 恰好大于 \(\left\lceil\frac{n+1}{2}\right\rceil-1\) 个其他元素 \(x_i\)。那么小于 \(x_k\) 的元素的权重之和为

  \[
  \sum_{x_i<x_k} w_i
  = \frac{1}{n}\times\left(\left\lceil\frac{n+1}{2}\right\rceil-1\right)
  \leq \frac{1}{n}\left\lceil\frac{n-1}{2}\right\rceil
  < \frac{1}{2}.
  \]

  由于所有元素互不相同，\(x_k\) 也恰好小于 \(n-\left\lceil\frac{n+1}{2}\right\rceil\) 个其他元素。因此，

  \[
  \sum_{x_i>x_k} w_i
  = \frac{1}{n}\times\left(n-\left\lceil\frac{n+1}{2}\right\rceil\right)
  = 1-\frac{1}{n}\left\lceil\frac{n+1}{2}\right\rceil
  < 1-\frac{1}{n}\left(\frac{n}{2}\right)
  \leq \frac{1}{2}.
  \]

  因此，根据加权中位数的定义，\(x_k\) 也是加权中位数。

- **2.** 为了计算 \(n\) 个元素的加权中位数，我们先对元素排序，然后累加元素的权重，直到找到中位数。

```
**Algorithm 79** Weighted Median
1: function WEIGHTED-MEDIAN(A)
2:   k ← 1
3:   s ← 0
4:   while s + w_k < 1/2 do
5:     s ← s + w_k
6:     k ← k + 1
7:   end while
8:   return x_k
9: end function
```

该算法的循环不变量是：\(s\) 为所有小于 \(x_k\) 的元素的权重之和：

\[
s = \sum_{x_i < x_k} w_i
\]

我们用归纳法证明这一点。基本情况成立，因为在第一次迭代中 \(s = 0\)。由于列表已排序，对于所有 \(i < k\)，都有 \(x_i < x_k\)。由归纳法，\(s\) 是正确的，因为在循环的每次迭代中，\(s\) 都会增加下一个元素的权重。

该循环保证会终止，因为所有元素的权重之和为 1。我们利用加权中位数的定义证明，当循环终止时 \(x_k\) 是加权中位数。

令 \(s'\) 为循环倒数第二次迭代开始时 \(s\) 的值：\(s = s' + w_{k-1}\)。由于倒数第二次迭代未满足终止条件，我们知道

\[
s' + w_{k-1} < \frac{1}{2}
\]

\[
\sum_{x_i < x_k} w_i = s < \frac{1}{2}
\]

注意，如果循环迭代零次，这仍然成立，因为 \(s = 0 < \frac{1}{2}\)。这证明了成为加权中位数的第一个条件。接下来我们证明第二个条件。大于 \(x_k\) 的元素的权重之和为

\[
\sum_{x_i > x_k} w_i = 1 - \left( \sum_{x_i < x_k} w_i \right) - w_k = 1 - s - w_k
\]

由循环终止条件，

\[
\begin{aligned}
\sum_{x_i < x_k} w_i &= s \le \frac{1}{2} - w_k \\
-s &\ge -\frac{1}{2} + w_k \\
1 - s - w_k &\le \frac{1}{2} \\
\sum_{x_i > x_k} w_i &\le \frac{1}{2}
\end{aligned}
\]

因此，\(x_k\) 也满足成为加权中位数的第二个条件。因此 \(x_k\) 是中位数，并且该算法是正确的。

该算法的运行时间是排序数组所需的时间加上寻找中位数所需的时间。我们可以在 \(O(n \log n)\) 时间内对数组排序。WEIGHTED-MEDIAN 中的循环有 \(O(n)\) 次迭代，每次迭代需要 \(O(1)\) 时间，因此总运行时间为 \(O(n \log n)\)。

- **3.** 给定一个 \(\Theta(n)\) 时间的中位数算法，加权中位数可以在 \(\Theta(n)\) 最坏情况下时间内计算出来。基本策略类似于二分查找：算法计算中位数，并在包含加权中位数的输入的一半上递归。

```
Algorithm 80 Linear-Time Weighted Median

1: function LINEAR-TIME-WEIGHTED-MEDIAN(A, l)
2:     n ← length[A]
3:     m ← MEDIAN(A)
4:     B ← ∅                                      ▷ B = {A[i] < m}
5:     C ← ∅                                      ▷ C = {A[i] ≥ m}
6:     w_B ← 0                                    ▷ w_B = total weight of B
7:     if length[A] == 1 then
8:         return A[1]
9:     end if
10:    for i ← 1 to n do
11:        if A[i] < m then
12:            w_B ← w_B + w_i
13:            Append A[i] to array B
14:        else
15:            Append A[i] to array C
16:        end if
17:    end for
18:    if l + w_B > 1/2 then                         ▷ Weighted median ∈ B
19:        LINEAR-TIME-WEIGHTED-MEDIAN(B, l)
20:    else
21:        LINEAR-TIME-WEIGHTED-MEDIAN(C, l + w_B)
22:    end if
23: end function
```

该算法的初始调用是 LINEAR-TIME-WEIGHTED-MEDIAN(A, 0)。在该算法中，A 是一个数组，包含初始输入的加权中位数，而 \(l\) 是初始输入数组中所有小于 \(A\) 中所有元素的元素的权重之和。B 包含所有小于中位数的元素，C 包含所有大于或等于中位数的元素，\(w_B\) 是 \(B\) 中元素的权重之和。

为了证明该算法是正确的，我们证明以下前置条件对每次递归调用都成立：初始 \(A\) 的加权中位数 \(y\) 始终存在于对 \(A\) 的递归调用中，并且 \(l\) 是所有小于 \(A\) 中所有元素的元素 \(x_i\) 的权重之和。该前置条件对初始调用显然成立。我们用归纳法证明该前置条件在每次递归调用中也成立。假设前置条件成立。首先考虑 \(l + w_B > \frac{1}{2}\) 的情况。由于 \(y\) 必定在 \(A\) 中，在第 18 行，\(y\) 必定在 \(B\) 或 \(C\) 中。由于所有小于 \(B\) 中任一元素的元素的权重之和大于 \(\frac{1}{2}\)，根据定义，加权中位数不可能在 \(C\) 中，因此它必定在 \(B\) 中。此外，我们没有丢弃 \(B\) 中的任何元素，因此 \(l\) 是正确的，并且前置条件得到满足。

如果在第 18 行有 \(l + w_B \le \frac{1}{2}\)，那么 \(y\) 必定在 \(C\) 中。\(C\) 的所有元素都大于 \(B\) 的所有元素，因此小于 \(y\) 的元素的权重之和为 \(l + w_B\)，并且递归调用的前置条件也得到满足。因此，由归纳法，前置条件始终成立。

该算法总是会终止，因为每次递归调用时 \(A\) 的大小都会减小。当算法终止时，结果是正确的。由于加权中位数始终在 \(A\) 中，因此当只剩下一个元素时，它必定是加权中位数。该算法运行时间为 \(\Theta(n)\)。计算中位数并将 \(A\) 拆分为 \(B\) 和 \(C\) 需要 \(\Theta(n)\) 时间。每次递归调用都将数组的大小从 \(n\) 减小到 \(\left\lceil \frac{n}{2} \right\rceil\)。因此递推式为 \(T(n)=T\left(\frac{n}{2}\right)+\Theta(n)=\Theta(n)\)。

- **4.** 我们论证一维邮局选址问题的解是这些点的加权中位数。邮局选址问题的目标是选择 \(p\) 以最小化成本。

\[
c(p)=\sum_{i=1}^{n} w_i d(p,p_i)
\]

我们可以将 \(c(p)\) 重写为小于 \(p\) 的点与大于 \(p\) 的点所贡献的成本之和：

\[
c(p)=\left(\sum_{p_i<p} w_i(p-p_i)\right)+\left(\sum_{p_i>p} w_i(p_i-p)\right)
\]

注意，如果对某个 \(k\) 有 \(p=p_k\)，那么该点不会对成本产生贡献。当 \(p\) 变化时，该成本函数是连续的：对所有 \(i\)，\(\lim_{p\to p_i^+} c(p)=c(p_i)\)。

为了找到该函数的极小值，我们对 \(p\) 求导：

\[
\frac{dc}{dp}=\left(\sum_{p_i<p}w_i\right)-\left(\sum_{p_i>p}w_i\right)
\]

注意，在某个 \(i\) 使得 \(p=p_i\) 的地方，该导数未定义，因为 \(c(p)\) 的左极限和右极限不同。还要注意，\(\frac{dc}{dp}\) 是一个非递减函数，因为随着 \(p\) 增大，满足 \(p_i<p\) 的点的数量不会减少。注意，对于 \(p<\min(p_1,p_2,\ldots,p_n)\)，有 \(\frac{dc}{dp}<0\)；对于 \(p>\max(p_1,p_2,\ldots,p_n)\)，有 \(\frac{dc}{dp}>0\)。因此存在一个点 \(p^*\)，使得对于 \(p<p^*\) 的点有 \(\frac{dc}{dp}\leq 0\)，对于 \(p>p^*\) 的点有 \(\frac{dc}{dp}\geq 0\)，并且该点是全局最小值。我们证明加权中位数 \(y\) 就是这样的点。

对于所有 \(p<y\)，其中 \(y\) 不是加权中位数，且对某个 \(i\) 有 \(p\ne p_i\)，

\[
\sum_{p_i<p}w_i>\sum_{p_i>p}w_i
\]

这意味着 \(\frac{dc}{dp}>0\)。对于某个 \(i\) 有 \(p=p_i\) 且 \(p\ne y\) 的情况，\(\frac{dc}{dp}\) 的左极限和右极限始终具有相同的符号，因此同样的论证适用。因此，对于所有不是加权中位数的 \(p\)，都有 \(c(p)>c(y)\)，所以加权中位数 \(y\) 是全局最小值。

- **5.** 使用曼哈顿距离求解二维邮局选址问题，等价于对每个维度分别求解一维邮局选址问题。令解为 \(p=(p_x,p_y)\)。注意，使用曼哈顿距离时，我们可以将成本函数写成两个一维邮局选址成本函数之和，如下所示：

\[
g(p)=\left(\sum_{i=1}^{n}w_i\lvert x_i-p_x\rvert\right)+\left(\sum_{i=1}^{n}w_i\lvert y_i-p_y\rvert\right)
\]

还要注意，\(\frac{\partial g}{\partial p_x}\) 不依赖于输入点的 \(y\) 坐标，并且仅使用 \(x\) 坐标作为输入时，其形式与上一部分中的 \(\frac{dc}{dp}\) 完全相同。类似地，\(\frac{\partial g}{\partial p_y}\) 仅依赖于 \(y\) 坐标。因此，为了最小化 \(g(p)\)，我们可以独立地最小化两个维度的成本。二维问题的最优解是：令 \(p_x\) 为输入 \(x_1,x_2,\ldots,x_n\) 的一维邮局选址问题的解，令 \(p_y\) 为输入 \(y_1,y_2,\ldots,y_n\) 的一维邮局选址问题的解。

