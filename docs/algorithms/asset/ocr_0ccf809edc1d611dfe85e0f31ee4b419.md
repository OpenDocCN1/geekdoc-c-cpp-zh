# Chapter 5

# Algorithms 17

of the nodes involved—one dollar per unit of time. Thus the overall time for $m$ find's is $O(m \log n)$ plus at most $O(n \log n)$.

In more detail, a node receives its allowance as soon as it ceases to be a root, at which point its rank is fixed. If this rank lies in the interval $[k+1,\dots, 2^k]$, the node receives $2^k$ dollars. By Property 3, the number of nodes with rank > $k$ is bounded by

```
$$\frac{n}{2^{k+1}} + \frac{n}{2^{k+2}} + \dots \leq \frac{n}{2^k}$
```

Therefore the total money given to nodes in this particular interval is at most $n$ dollars, and since there are $\log n$ intervals, the total money distributed to all nodes is $\leq n \log n$.

Now, the time to pick a specific find is simply the number of pointers followed. Consider the ascending rank values along this chain of nodes $x$ on the fall into two categories: either the rank of $\pi(x)$ is in a higher interval than the rank of $x$, or it lies in the same interval. There are at most $n$ nodes of the first type (do you see why?), the work they do takes $O(\log n)$ time. The remaining nodes—whose parents' ranks are in the same interval as theirs—have to pay a dollar out of their pocket money for their processing time.

This works if the initial allowance of each node $x$ is enough to cover all of its payments in the sequence of $f$ operations. Here's the crucial observation: each time $x$ pays a dollar, its parent changes to one of higher rank. Therefore, if $x$'s rank lies in the interval $[k+1,\dots, 2^k]$, it has to pay most $2^k$ dollars before its parent's rank is in a higher interval;whereupon it never has to pay again.

# 5.1.5 Prim's algorithm

Let's return our discussion of minimum spanning tree algorithms. What the cut tells us in general terms is that any algorithm conforming to the following greedy schema is guaranteed to work.

```
$X=\text{(edges picked so far)}$$\nrepeat until $|X|=|V|-1$:$\npick a set $S \subset V$ for which $X$ has no edges between $S$ and $V$\nlet $e \in E$ be the minimum-weight edge between $S$ and $V-S$\nX=X \cup \{e\}$
```

A popular alternative to Kruskal's algorithm is Prim's, in which the intermediate set of edges $X$ always forms a subtree, and $S$ is chosen to be the set of this tree's vertices.

On each iteration, the subtree defined by $X$ grows by one edge, latest vertex outside $S$ (Figure 5.8). We can equivalently think of $S$ as growing to include the vertex $v \notin S$ of smallest cost:

```
$cost(v) = \min_{u \in S} w(u, v)$.
```