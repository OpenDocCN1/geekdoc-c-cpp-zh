
## Figure 6.9 The optimal traveling salesman tour has length 10.

![](img/3dd1f1364df8f87b80683fc32a15b999_184_0.png)

A piece of bad news about the TSP, which we will better understand in Chapter 8, is that it is highly unlikely to be solvable in polynomial time.

How long does it take, then? Well, the brute-force approach is to evaluate every possible tour and return the best one. Since there are $(n-1)!$ possibilities, this strategy takes $O(n!)$ time. We will see that dynamic programming yields a much faster solution, though not a polynomial one.

What is the appropriate subproblem for the TSP? Subproblems refer to partial tours, and the most obvious partial tour is the initial portion of a tour. Suppose we have started at $i$ as required, have visited a few cities, and are now in $j$. What information do we need in order to extend this particular tour? We certainly know $j$, since this will determine which cities are most convenient to visit next. And we need to know all the cities visited so far, so that we do not repeat any of them. Here, then, is an appropriate subproblem.

For a subset of cities $S \subseteq \{1, 2, \dots, n\}$ that includes $1$, and $j \in S$, let $C(S, j)$ be the length of the shortest path visiting each node in $S$ exactly, starting at 1 and ending at $j$. When $|S| > 1$, we define $C(S, 1) = \infty$ since the path cannot start and end at 1. Now, let's express $C(S, j)$ in terms of smaller subproblems. We need to start at 1 and end at $j$; what should we pick as the second-to-last city? It has to be some $i \in S \setminus \{j\}$, so the overall path length is the distance from 1 to $i$, $C(S \setminus \{j\}, i)$, plus the length of the final edge $d_{ij}$. We must pick the best $i$:

```
C(S, j) = \min_{i \in S \setminus \{j\}} C(S \setminus \{j\}, i) + d_{ij}.
```

## On time and memory

The amount of time it takes to run a dynamic programming algorithm is easy to discern from the dag of subproblems; in many cases it is just the total number of edges! All we are really doing is visiting the nodes in linearized order, examining each node's edges, doing a constant amount of work per edge. By the end, each edge has been examined. But how much memory is required? There is no simple method of characterizing this. It is certainly possible to do the job with an amount of memory proportional to the number of subproblems, but we can get away with much less. The reason is that the value of a particular problem only needs to be remembered until the larger subproblems depending on it have been solved. For example, the Floyd-Warshall algorithm value of $dist(i, j, k)$ is not needed once $dist(i, j, k+1)$ values have been computed. Therefore, we only need $|V|$ arrays to store $dist$ values, one for odd values of $k$ and one for even: when computing $dist(i, j, k)$, we overwrite $dist(i, j, k-2)$. And let us not forget, as always in dynamic programming, we also need one more $prev(i, j)$, storing the last vertex in the shortest path from $i$ to $j$, a value that must be updated with this bookkeeping step. Can you see how the edit distance in Figure 6.5 only needs memory proportional to the length of the string? The subproblems are ordered by $|S|$. Here's the code:

```
C([1, 1]) = 0
for s = 2 to n:
  for subsets S ⊆ {1, ..., n} of size s and containing 1:
    C(S, 1) = ∞
    for j ∈ S, j ≠ 1:
      C(S, j) = ... (see above)
```

There are at most $2^n$ subproblems, and each takes linear time to solve. The total running time is $O(2^n)$.

## 6.7 Independent sets in trees

A subset of nodes $S \subseteq V$ is an independent set of graph $G=(V, E)$ if there are no edges between them. For instance, in Figure 6.10 the nodes $\{1, 4, 5\}$ form an independent set, but do not because of the edge between 4 and 5. The largest independent set is $\{2, 3, 6\}$.

## Figure 6.10 The largest independent set in this graph has size 3.

![](img/3dd1f1364df8f87b80683fc32a15b999_186_0.png)

Like several problems we have seen in this chapter (knapsack, traveling salesman), finding the largest independent set in a graph is believed to be intractable. However, when the graph happens to be a tree, the problem can be solved in linear time using dynamic programming. And what are the appropriate subproblems? In the chain multiplication problem we noticed that the layered structure of a tree provides a natural definition of a subproblem—as long as one node of the tree has been identified as a root. So here's the algorithm: Start by rooting the tree at any node $r$. Now, each node defines a subtree—the one hanging from it. This immediately suggests subproblems:

$I(u)$ = size of largest independent set of subtree hanging from $u$.

Our final goal is $I(r)$. Dynamic programming proceeds as always from smaller subproblems to larger ones, that is to say, bottom-up to the root. Suppose we know the independent sets for all subsets below a node $u$; in other words, suppose we know $I(u)$ for all descendants of $u$. How can we compute $I(u)$? Let's split the computation into two cases: any independent set includes $u$ or it doesn't (Figure 6.11).

```
I(u) = \max \left(1 + \sum_{grandchildren\ of\ u} I(w), \sum_{children\ of\ u} I(w)\right)
```

If the independent set includes $u$, then we get one point for it, but we aren't allowed to include the children of $u$—therefore we move on to the grandchildren. This is the first case in the formula. On the other hand, if we don't include $u$, then we don't get a point for it, but we can move on to its children.

The number of subproblems is exactly the number of vertices. With a little care, the running time can be made linear, $O(|V| + |E|)$.

## Figure 6.11 $I(u)$ is the size of the largest independent set of the subtree rooted at $u$. Two cases: either $u$ is in this independent set, or it isn't.

![](img/3dd1f1364df8f87b80683fc32a15b999_187_0.png)

## Exercises

6.1. A contiguous subsequence of a list $S$ is a subsequence made up of consecutive elements of $S$. For instance, if $S$ is $5, 15, -30, 10, -5, 40, 10, 15, -30$, give a linear-time algorithm for the following:
- *Input:* A list of integers $S$;
- *Output:* The maximum sum of a contiguous subsequence.

6.2. You are going on a trip, starting at mile 0. Along the way there are $n$ hotels, at miles $a_1 < a_2 < \dots < a_n$, and for each hotel $i$ there is a penalty $w_i$ if you stop there. If you stop at hotel $i$ and then later at hotel $j$, the penalty is $(a_j - a_i)^2$. You want to choose a sequence of hotels to stop at to minimize the total penalty. Give a linear-time algorithm for this.

6.3. McDonald's is considering opening a series of restaurants along a line. The locations are, in increasing order, $m_1, m_2, \dots, m_n$, and the expected profit from opening a restaurant at $i$ is $p_i$. The constraints are:
- At each location, McDonald's may open one restaurant.
- Any two restaurants should be at least $k$ miles apart.

Give an efficient algorithm to compute the maximum profit subject to the given constraints.

6.4. You are given a string $s[1..n]$, which you believe to be a corrupted document in which all punctuation has vanished. You wish to reconstruct the document using a dictionary, which is available in the form of a Boolean function $dict()$: for any string $w$,

```
$\begin{aligned} dict(w) &= \begin{cases} \text{true} & w \text{ is a valid word} \\ \text{false} & \text{otherwise.}\end{cases} \end{aligned}$
```

(a) Give a dynamic programming algorithm that determines whether the string $s$ can be reconstituted as a sequence of words. The running time should be at most $O(n^2)$, assuming calls to $dict$ take unit time.
(b) In the event that the string is valid, make your algorithm output the corresponding sequence of words.

6.5. Pebbling a checkerboard. We are given a checkerboard with 4 rows and $n$ columns, and we are given a set of $2n$ pebbles, and we want to place some or all of these on the checkerboard (each pebble can be placed on exactly one square) to maximize the sum of the integers in the squares that are covered by pebbles. There is one constraint: for a placement of pebbles to be legal, no two of them can be on horizontally or vertically adjacent squares (diagonal adjacency is forbidden).

+- Determine the number of legal patterns that can occur in any column (in isolation, ignoring the pebbles in adjacent columns) and describe these patterns.
- Call two patterns compatible if they can be placed on adjacent columns.

Give an efficient algorithm to compute the maximum sum.
