

## 7.3 并行前缀问题

设 $\bullet$ 为任意结合二元运算；即它满足
$$x \bullet (y \bullet z) = (x \bullet y) \bullet z.$$
我们简单地将此运算称为乘积。例如，$\bullet$ 可以表示加法、乘法或两个数的最大值。

### 问题描述

给定一个数字序列 $x_1, x_2, \ldots, x_n$，对所有满足 $1 \leq k \leq n$ 的 $k$，计算乘积 $x_1 \bullet x_2 \bullet \cdots \bullet x_k$。

### 解决方案

我们用 $PR(i,j)$ 表示乘积 $x_i \bullet x_{i+1} \bullet \cdots \bullet x_j$。我们的目标是计算 $PR(1,k)\,\forall k,\,1 \leq k \leq n$。前缀问题的顺序版本是平凡的；我们只需按顺序计算前缀。并行前缀问题则不那么容易解决。我们采用的方法是分治法。和通常一样，我们假设 $n$ 是 2 的幂。

### 归纳假设

*我们知道如何解决 $\frac{n}{2}$ 个元素的并行前缀问题。*

一个元素的情况是平凡的。算法将输入对半划分，并通过归纳分别求解每一半。由此，我们得到 $PR(1,k)$ 和 $PR(\frac{n}{2}+1,\frac{n}{2}+k)\,\forall k,\,1 \leq k \leq \frac{n}{2}$ 的值。前半部分的值可以直接使用。对于 $\frac{n}{2} < m \leq n$ 的 $PR(1,m)$ 可以通过计算 $PR(1,\frac{n}{2}) \bullet PR(\frac{n}{2}+1,m)$ 得到。这两个项都可以通过归纳得知。请注意，我们使用了运算的结合律。完整算法如下。

### 算法107 并行前缀算法

```text
1: function PARALLEL_PREFIX(x, n)
2:     Input: x: an array in the range 1 to n ▷ we assume that n is a power of 2
3:     Output: x: the i-th element contains the i-th prefix.
4:     PP(1, n)
5: end function
6: function PP(Left, Right)
7:     if Right − Left = 1 then
8:         x[Right] ← x[Left] • x[Right] ▷ • is an associative binary operation
9:     else
10:        Middle ← ⌊(Left + Right − 1) / 2⌋
11:        Execute in parallel
12:            PP(Left, Middle) ▷ assigned to P₁ to Pₙ⁄₂
13:            PP(Middle + 1, Right) ▷ assigned to Pₙ⁄₂₊₁ to Pₙ
14:        for i ← Middle + 1 to Right do
15:            Execute in parallel
16:                x[i] ← x[Middle] • x[i]
17:        end for
18:    end if
19: end function
```

### 复杂度

在算法的每次递归调用中，输入被分成两个不相交的集合。因此两个子问题可以并行求解。如果我们有 $n$ 个处理器来处理规模为 $n$ 的问题，那么可以将其中一半分配给每个子问题。合并步骤需要 $n/2$ 步，这些步骤也可以并行执行，因为所有步骤都使用 x[Middle]。尽管多个处理器必须同时读取 x[Middle]，但它们都写入不同的位置。总体而言，$T(n, n/2) = O(\log n)$，且 $E(n, n) = O(1/\log n)$，因为顺序算法显然在 $O(n)$ 步内运行。

### 提高并行前缀的效率

技巧是使用相同的归纳假设，但以不同的方式划分输入。再次假设 $n$ 是 2 的幂，并且有 $n$ 个处理器。设 $E$ 表示所有下标 $i$ 为偶数的 xᵢ 的集合。如果我们求出 $E$ 中所有元素的并行前缀，那么求出其余具有奇数下标的前缀就很容易：如果 $PR(1, 2i)$ 对所有满足 $1 \leq i \leq n/2$ 的 $i$ 已知，那么对于每个奇数前缀 $PR(1, 2i + 1)$，我们需要再计算一个乘积（$PR(1, 2i) \bullet x_{2i+1}$）。我们可以分两个阶段求出 $E$ 中元素的前缀。首先，我们并行计算 $x_{2i-1} \triangleleft x_{2i}$ 对所有 $i \leq n/2$ 的值，并将结果存储在 $x_{2i}$ 中。换句话说，我们收集 $E$ 中所有元素与其左邻元素的乘积。然后，我们通过归纳求解 $E$ 的规模为 $n/2$ 的前缀问题。每个 $x_{2i}$ 的结果就是正确的前缀，因为每个 $x_{2i}$ 已经包含了与 $x_{2i-1}$ 的乘积。如果我们知道了所有偶数下标的前缀，那么我们已经知道如何用一步并行计算来求出奇数下标的前缀。完整程序如下。

### 算法108 并行前缀：高效算法

```text
1: function PARALLEL_PREFIX(x, n)
2:   Input: x: an array in the range 1 to n ▷ we assume that n is a power of 2
3:   Output: x: the i-th element contains the i-th prefix.
4:     PP(1)
5: end function
6: function PP(Inc)
7:   if Inc = n then
8:     x[n] ← x[⌈n/2⌉] ◁ x[n]   ▷ ◁ is an associative binary operation
9:   else
10:    for i ← 1 to n/(2 × Inc) do
11:      Execute in parallel
12:        x[2 × i × Inc] ← x[2 × i × Inc] ◁ x[2 × i × Inc − Inc]
13:    end for
14:    PP(2 × Inc)
15:    for i ← 1 to n/(2 × Inc) − 1 do
16:      Execute in parallel
17:        x[2 × i × Inc + Inc] ← x[2 × i × Inc] ◁ x[2 × i × Inc + Inc]
18:    end for
19:   end if
20: end function
```

### 复杂度

算法 PARALLEL_PREFIX 中的两个循环都可以用 $n/2$ 个处理器在 $O(1)$ 时间内并行执行。递归调用应用于规模减半的问题，因此算法的运行时间为 $O(\log n)$。总步数 $S(n)$ 满足递推关系

$$S(n) = S(n/2) + n - 1$$
$$S(2) = 1$$

这意味着 $S(n) = O(n)$。但这意味着我们可以修改算法，使其在仅有 $O(n/\log n)$ 个处理器的情况下在 $O(\log n)$ 时间内运行，从而达到 $O(1)$ 的效率。这一改进的关键在于只使用一次递归调用而不是两次，同时仍然能够并行执行合并步骤。

## 7.4 在链表中查找排名

通常，在并行环境中处理链式表示比处理数组要困难得多。例如，链表本质上是顺序的。如果访问链表的唯一途径是通过链表的头节点，那么我们必须一个元素一个元素地遍历链表，不可能实现并行。然而，在许多情况下，链表中的元素（或指向它们的指针）实际上存储在一个连续的数组中。在这种情况下，可以对链表进行并行访问，因此有望设计出快速的并行算法。

这里将链表中一个元素的排名定义为该元素到链表末尾的距离；因此，头节点的排名为 \(n\)，第二个元素的排名为 \(n-1\)，依此类推。

### 问题描述

给定一个包含 \(n\) 个元素的链表，所有元素都存储在一个数组 \(A[1..n]\) 中，计算每个元素在链表中的排名。

### 解决方案

我们可以通过简单遍历链表来解决顺序问题。我们为这个问题设计并行算法所采用的方法称为倍增法。我们为每个元素分配一个处理器。最初，每个处理器只知道其元素在链表中的右邻居。在第一步中，每个处理器找到其邻居的邻居。第一步之后，每个处理器知道距其元素距离为 2 的元素。如果在第 \(i\) 步，每个处理器知道距其元素距离为 \(k\) 的元素，那么在一个步骤内每个处理器可以找到距离为 \(2k\) 的元素。此过程持续进行，直到到达链表末尾。

设 \(N[i]\) 为在某一时刻 \(P_i\) 所知的链表中 \(i\) 右侧最远的元素。最初，\(N[i]\) 是右邻居，除了最后一个元素，其右邻居为 nil。基本上，在每一步中，\(P_i\) 将 \(N[i]\) 更新为 \(N[N[i]]\)，直到到达链表末尾。设 \(R[i]\) 为 \(i\) 的排名。最初 \(R[i]\) 设置为 0，除了链表中的最后一个元素，其设置为 1。该元素通过其 nil 指针被检测到。当处理器遇到一个排名 \(R\) 非零的邻居时，该处理器可以确定自己的排名。

最初，只有排名为 1 的元素知道自己的排名。第一步之后，排名为 2 的元素发现其右邻居的排名为 1，因此它知道自己的排名为 2。第二步之后，排名为 3 和 4 被确定，依此类推。如果 \(P_i\) 发现 \(N[i]\) 指向一个已排名的

