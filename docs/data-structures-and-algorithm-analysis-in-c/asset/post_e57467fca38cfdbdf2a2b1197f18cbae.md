
some set of $M - j$ bins, and from previous considerations, the total number of such items is $2(M - j)$.¹

The proof is completed by noting that if $s_i > 1/3$, there is no way for $s_i$ to be placed in one of these $M$ bins. Clearly, it cannot go in one of the $j$ bins, since if it could, then first fit would have done so too. To place it in one of the remaining $M - j$ bins requires distributing $2(M - j) + 1$ items into the $M - j$ bins. Thus, some bin would have to have three items, each of which is larger than $1/3$, a clear impossibility. This contradicts the fact that all the sizes can be placed in $M$ bins, so the original assumption must be incorrect. Thus, $s_i \le 1/3$.

## Lemma 10.2

The number of objects placed in extra bins is at most $M - 1$.

### Proof

Assume that there are at least $M$ objects placed in extra bins. We know that $\sum_{i=1}^N s_i \le M$, since all the objects fit in $M$ bins. Suppose that $B_j$ is filled with $W_j$ total weight for $1 \le j \le M$. Suppose the first $M$ extra objects have sizes $x_1, x_2, \dots, x_M$. Then, since the items in the first $M$ bins plus the first $M$ extra items are a subset of all the items, it follows that

$$
\sum_{i=1}^N s_i \ge \sum_{j=1}^M W_j + \sum_{j=1}^M x_j \ge \sum_{j=1}^M (W_j + x_j)
$$

Now $W_j + x_j > 1$, since otherwise the item corresponding to $x_j$ would have been placed in $B_j$. Thus

$$
\sum_{i=1}^N s_i > \sum_{j=1}^M 1 > M
$$

But this is impossible if the $N$ items can be packed in $M$ bins. Thus, there can be at most $M - 1$ extra items.

## Theorem 10.4

Let $M$ be the optimal number of bins required to pack a list $I$ of items. Then first fit decreasing never uses more than $(4M + 1)/3$ bins.

### Proof

There are at most $M - 1$ extra items, of size at most $1/3$. Thus, there can be at most $\lfloor (M - 1)/3 \rfloor$ extra bins. The total number of bins used by first fit decreasing is thus at most $\lfloor (4M - 1)/3 \rfloor \le (4M + 1)/3$.

It is possible to prove a much tighter bound for both first fit decreasing and next fit decreasing.

¹ Recall that first fit packed these elements into $M - j$ bins and placed two items in each bin. Thus, there are $2(M - j)$ items.

![](img/e449061a0cac9cafaefd979fab665b33_485_0.png)

Figure 10.28 Example where first fit decreasing uses $11k + 8$ bins, but only $9k + 6$ bins are required

## Theorem 10.5

Let $M$ be the optimal number of bins required to pack a list $I$ of items. Then first fit decreasing never uses more than $\frac{11}{9}M + \frac{6}{9}$ bins. There exist sequences such that first fit decreasing uses $\frac{11}{9}M + \frac{6}{9}$ bins.

### Proof

The upper bound requires a very complicated analysis. The lower bound is exhibited by a sequence consisting of $6k + 4$ elements of size $1/3 + e$, followed by $6k + 4$ elements of size $1/4 + 2e$, followed by $6k + 4$ elements of size $1/4 + e$, followed by $12k + 8$ elements of size $1/2 - 2e$. Figure 10.28 shows that the optimal packing requires $9k + 6$ bins, but first fit decreasing uses $11k + 8$ bins. Set $M = 9k + 6$, and the result follows.

In practice, first fit decreasing performs extremely well. If sizes are chosen uniformly over the unit interval, then the expected number of extra bins is $\Theta(\sqrt{M})$. Bin packing is a fine example of how simple greedy heuristics can give good results.

## 10.2 Divide and Conquer

Another common technique used to design algorithms is divide and conquer. Divide-and-conquer algorithms consist of two parts:

- Divide: Smaller problems are solved recursively (except, of course, base cases).
- Conquer: The solution to the original problem is then formed from the solutions to the subproblems.

Traditionally, routines in which the text contains at least two recursive calls are called divide-and-conquer algorithms, while routines whose text contains only one recursive call are not. We generally insist that the subproblems be disjoint (that is, essentially nonoverlapping). Let us review some of the recursive algorithms that have been covered in this text.

We have already seen several divide-and-conquer algorithms. In Section 2.4.3, we saw an $O(N \log N)$ solution to the maximum subsequence sum problem. In Chapter 4, we saw linear-time tree traversal strategies. In Chapter 7, we saw the classic examples of divide and conquer, namely mergesort and quicksort, which have $O(N \log N)$ worst-case and average-case bounds, respectively.

We have also seen several examples of recursive algorithms that probably do not classify as divide-and-conquer, but merely reduce to a single simpler case. In Section 1.3, we saw a simple routine to print a number. In Chapter 2, we used recursion to perform efficient exponentiation. In Chapter 4, we examined simple search routines for binary search trees. In Section 6.6, we saw simple recursion used to merge leftist heaps. In Section 7.7, an algorithm was given for selection that takes linear average time. The disjoint set find operation was written recursively in Chapter 8. Chapter 9 showed routines to recover the shortest path in Dijkstra's algorithm and other procedures to perform depth-first search in graphs. None of these algorithms are really divide-and-conquer algorithms, because only one recursive call is performed.

We have also seen, in Section 2.4, a very bad recursive routine to compute the Fibonacci numbers. This could be called a divide-and-conquer algorithm, but it is terribly inefficient, because the problem really is not divided at all.

In this section, we will see more examples of the divide-and-conquer paradigm. Our first application is a problem in computational geometry: Given $N$ points in a plane, we will show that the closest pair of points can be found in $O(N \log N)$ time. The exercises describe some other problems in computational geometry which can be solved by divide and conquer. The remainder of the section shows some extremely interesting, but mostly theoretical, results. We provide an algorithm that solves the selection problem in $O(N)$ worst-case time. We also show that two $N$-bit numbers can be multiplied in $o(N^2)$ operations and that two $N \times N$ matrices can be multiplied in $o(N^3)$ operations. Unfortunately, even though these algorithms have better worst-case bounds than the conventional algorithms, none are practical except for very large inputs.

### 10.2.1 Running Time of Divide-and-Conquer Algorithms

All the efficient divide-and-conquer algorithms we will see divide the problems into subproblems, each of which is some fraction of the original problem, and then perform some additional work to compute the final answer. As an example, we have seen that mergesort operates on two problems, each of which is half the size of the original, and then uses $O(N)$ additional work. This yields the running time equation (with appropriate initial conditions)

$$
T(N) = 2T(N/2) + O(N)
$$

We saw in Chapter 7 that the solution to this equation is $O(N \log N)$. The following theorem can be used to determine the running time of most divide-and-conquer algorithms.

## Theorem 10.6

The solution to the equation $T(N) = aT(N/b) + \Theta(N^k)$, where $a \ge 1$ and $b > 1$, is

$$
T(N) = \begin{cases}
O(N^{\log_b a}) & \text{if } a > b^k \\
O(N^k \log N) & \text{if } a = b^k \\
O(N^k) & \text{if } a < b^k
\end{cases}
$$

### Proof

Following the analysis of mergesort in Chapter 7, we will assume that $N$ is a power of $b$; thus, let $N = b^m$. Then $N/b = b^{m-1}$ and $N^k = (b^m)^k = b^{mk} = (b^k)^m$. Let us assume $T(1) = 1$, and ignore the constant factor in $\Theta(N^k)$. Then we have

$$
T(b^m) = aT(b^{m-1}) + (b^k)^m
$$

If we divide through by $a^m$, we obtain the equation

$$
\frac{T(b^m)}{a^m} = \frac{T(b^{m-1})}{a^{m-1}} + \left\{ \frac{b^k}{a} \right\}^m \tag{10.3}
$$

We can apply this equation for other values of $m$, obtaining

$$
\frac{T(b^{m-1})}{a^{m-1}} = \frac{T(b^{m-2})}{a^{m-2}} + \left\{ \frac{b^k}{a} \right\}^{m-1} \tag{10.4}
$$

$$
\frac{T(b^{m-2})}{a^{m-2}} = \frac{T(b^{m-3})}{a^{m-3}} + \left\{ \frac{b^k}{a} \right\}^{m-2} \tag{10.5}
$$

$$
\frac{T(b^1)}{a^1} = \frac{T(b^0)}{a^0} + \left\{ \frac{b^k}{a} \right\}^1 \tag{10.6}
$$

We use our standard trick of adding up the telescoping equations (10.3) through (10.6). Virtually all the terms on the left cancel the leading terms on the right, yielding

$$
\frac{T(b^m)}{a^m} = 1 + \sum_{i=1}^m \left\{ \frac{b^k}{a} \right\}^i \tag{10.7}
$$

$$
= \sum_{i=0}^m \left\{ \frac{b^k}{a} \right\}^i \tag{10.8}
$$

Thus

$$
T(N) = T(b^m) = a^m \sum_{i=0}^m \left\{ \frac{b^k}{a} \right\}^i \tag{10.9}
$$
