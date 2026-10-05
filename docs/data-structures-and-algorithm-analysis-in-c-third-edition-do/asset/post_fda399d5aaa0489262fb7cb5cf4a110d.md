
## Sec. 16.1 Dynamic Programming

subproblems are solved repeatedly, and (2) we can find a suitable way of doing the necessary bookkeeping. Dynamic programming algorithms are usually not implemented by using a table to store recursive calls (i.e., going backwards as is done by Fibonacci). Instead, algorithms are typically implemented by building the table of subproblems from the bottom up. Fibonacci represents the most common form of dynamic programming than does Fibonacci, even though it doesn't use the complete table.

### 16.1.1 The Knapsack Problem

We will next consider a problem that appears with many variations in a variety of commercial settings. Many businesses need to pack items with the greatest efficiency. One way to describe this basic idea is in terms of packing items into a knapsack, so we will refer to it as the Knapsack Problem. We will first define a particular formulation of the knapsack problem, and then we will discuss other versions of the knapsack problem in the exercises and in Chapter 17.

Assume that we have a knapsack with a certain amount of space that we define using integer value $K$. We also have $n$ items each with a certain size such that $i$ has integer size $k_i$. The problem is to find a subset of the $n$ items whose sizes sum exactly to $K$, if one exists. For example, if our knapsack has capacity $K=5$ and the two items are of size $k_1=2$ and $k_2=4$, then no such subset exists. But if we add a third item of size $k_3=1$, then we can fill the knapsack exactly with the first and third items. We can define the problem more formally as: Find $S \subseteq \{1, 2, \dots, n\}$ that

> $$\sum_{i \in S} k_i = K$$

**Example 16.1** Assume that we are given a knapsack of size $K=163$ and 10 items of size $4, 9, 15, 19, 27, 44, 54, 68, 73, 101$. Can we find a subset of the items that exactly fills the knapsack? You should take a few minutes and try to before reading and looking at the answer.

One solution to the problem is: $19, 27, 44, 73$.

**Example 16.2** Having solved the previous example for knapsack of size 163, how hard is it to solve for a knapsack of size 164?

Unfortunately, knowing the answer for 163 is of no use at all when solving for 164. One solution is: $9, 54, 101$.

If you tried these examples, you probably found yourself doing a lot of trial-and-error and a lot of backtracking. To come up with an algorithm, we want an organized way to go through the possible subsets. Is there a smaller problem, so that we can divide and conquer? We essentially have two parts to the input: The knapsack size $K$ and the $n$ items. It probably will not do us much good to try and break the knapsack into pieces and solve the sub-pieces (since we already saw that knowing the answer for a knapsack of size 163 did not help us solve the problem for a knapsack of size 164).

So, what can we say about solving the problem with or without the $nth$ item? This seems to lead to a way to break down the problem. If the $nth$ item is needed for a solution (that is, if we solve the problem with the first $n-1$ items) then we can also solve the problem when the $nth$ item is available (we just ignore it). On the other hand, if we do include the $nth$ item as a member of the subset, then we would need to solve the problem with the first $n-1$ items and a knapsack of size $K-k_n$ (since the $n$th item is taking up $k_n$ space in the knapsack).

To organize this process, we define the problem in two parameters: the knapsack size $K$ and the number of items $n$. Denote an instance of the problem as $P(n, K)$. Now we can say $P(n, K)$ has a solution if and only there exists a solution for either $P(n-1, K)$ or $P(n-1, K-k_n)$. That is, we can solve $P(n)$ only if we solve one of the subproblems we use or do not use the $nth$ item. Of course, the order of items is arbitrary. We just need to give them some order to keep things simple.

Continuing this, to solve any subproblem of size $n-1$, we only need to solve two subproblems of size $n-2$. And so on, until we are down to only one item that either fills the knapsack or not. This naturally leads to a cost expressed by the recurrence $T(n) = 2T(n-1) + c = \Theta(2^n)$. That can be pretty expensive!

But... we realize that there are $n(K+1)$ subproblems to solve! Clearly, there is the possibility that many subproblems are solved repeatedly. This is a natural opportunity to use dynamic programming. We simply build an array of $n \times (K+1)$ that contains the solutions for all subproblems $P(i, k)$, $1 \le i \le n, 0 \le k \le K$.

There are two approaches to solving the problem. One is to start with our problem of $P(n, K)$ and make recursive calls to solve the subproblems, each time checking the array to see if a subproblem has been solved, and filling the corresponding cell in the array whenever we get a new subproblem solution. The other is to start filling the array for row 1 (which indicates a successful solution only for a knapsack of size $k_1$). We then fill in the succeeding rows from $i=2$ to $n$, left to right, as follows.

$P(n-1, K)$, has a solution,

```
then P(n, K) has a solution
else if P(n - 1, K - k_n) has a solution
    then P(n, K) has a solution
    else P(n, K) has no solution.
```

In other words, a new slot in the array gets its solution by looking at two slots in preceding row. Filling each slot in the array takes constant time, the cost of the algorithm is $\Theta(nK)$.

**Example 16.3** Solve the Knapsack Problem for $K = 10$ and five items with sizes 9, 2, 7, 4, 1. We do this by filling the following array.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| $k_1$ | O | | | | | | | | I | | |
| $k_2$ | | O | | | | | | | | O | |
| $k_3$ | | | O | | | | | I | | 1/O | |
| $k_4$ | | | | O | | I | | O | | O | |
| $k_5$ | | | | | O | I | O | I/O | O | I |

Key:

- - : Not solution for $P(i, k)$.
- O: Solution(s) for $P(i, k)$ with omitted.
- I: Solution(s) for $P(i, k)$ with included.
- I/O: Solution(s) for $P(i, k)$ with both.

In other words, a new slot in the array gets its solution by looking at two slots in preceding row. Filling each slot in the array takes constant time, the cost of the algorithm is $\Theta(nK)$.

### 16.1.2 All-Pairs Shortest Paths

We consider the problem of finding the shortest distance between all pairs of vertices in $G$. To solve this, we could run Dijkstra's algorithm for each vertex $v \in V$. If $G$ is sparse, the cost will be $\Theta(VE + V^2 \log V)$.

We will do this organization through the use of $k$-path. Define a $k$-path from vertex $v$ to vertex $u$ to be any path whose intermediate vertices (aside from $v$ and $u$) all have indices less than $k$. A 0-path is defined as a direct edge from $v$ to $u$.

$D_k(v, u)$ is the length of the shortest $k$-path from vertex $v$ to vertex $u$. Assume that we already know the shortest $k$-path from $v$ to $u$. The shortest $(k+1)$-path either goes through $k$ or it does not. If it goes through $k$, then the best path is the best $k$-path from $v$ to $k$ followed by the best $k$-path from $k$ to $u$. Otherwise, we keep the best k-path seen before.

![](img/0ae21f56d2533acf0527c86ba21e6_540.png)
**Figure 16.2** An example of $k$-paths in Floyd's algorithm.
