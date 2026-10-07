# Chapter 3

# Algorithms 99

You wish to preprocess the tree so that queries of the form "is $u$ an ancestor of $v$?" can be answered in constant time. The preprocessing itself should take linear time. How can this be done?

3.19. As in the previous problem, you are given a binary tree $T = (V, E)$ with designated root node. In addition, there is a value for each node in $V$. Define a new array $z[\cdot]$ as follows: for each $u \in V$,

$z[u] = \text{the maximum of the x-values associated with } u$'s descendants.

Give a linear-time algorithm that calculates the $z$-array.

3.20. You are given a binary tree $T = (V, E)$ along with a designated root node $r \in V$. The parent of any node $v 
eq r$, denoted $p(v)$, is defined to be the node adjacent to $v$ in the path from $r$ to $v$. By convention, $p(r) = r$. For $k > 1$, $p^k(v) = p^{k-1}(p(v))$ and $p^1(v) = p(v)$ (so $p^k(v)$ is the $k$-th ancestor of $v$).

Each vertex $v$ of the tree has an associated non-negative integer $l(v)$. Give a linear-time algorithm to update the labels of all $v$ in $T$ according to the following rule: $l_{new}(v) = l(p^{l(v)}(v))$.

3.21. Give a linear-time algorithm to find an odd-cycle in a *directed* graph. (Hint: First solve this problem under the assumption that the graph is strongly connected.

3.22. Give an efficient algorithm that takes as input a directed graph $G = (V, E)$, and determines whether or not there is a vertex $s \in V$ from which all other vertices are reachable.

3.23. Give an efficient algorithm that takes as input a directed acyclic graph $G = (V

3.24. Give a linear-time algorithm for the following task:

Input: A directed acyclic graph $G$
Question: Does $G$ contain a directed path that touches every vertex exactly once

3.25. You are given a directed graph in which each node $u \in V$ has an associated price $p_u$ which is a positive integer. Define the array cost as follows: for each $u \in V$,

$cost[u] = \text{price of the cheapest node reachable from } u$ (including itself $u$), the cost

For instance, in the graph below (with prices shown for each vertex), the cost of the nodes $A, B, C, D, E, F$ are 2, 4, 1, 4, 1, 5 respectively.

![](bbox=[0.498, 0.77, 0.793, 0.903])