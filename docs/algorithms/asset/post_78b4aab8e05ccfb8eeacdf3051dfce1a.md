
# Chapter 9

# Algorithms 27

Start with some problem $P_0$
$S = \{P_0\}$, the set of active subproblems
Repeat while $S \neq \emptyset$:
  choose a subproblem $P \in S$ and remove it from $S$
  expand it into smaller subproblems $P_1, P_2, \dots, P_k$
  For each $P_i$:
    If $Test(P_i)$ succeeds: halt and announce the solution
    If $Test(P_i)$ fails: discard $P_i$
    Otherwise: add $P_i$ to $S$
Announce that there is no solution

For $SAT$, the choose procedure picks a clause, and expand picks a variable within that clause. We have already discussed reasonable ways of making such choices.

With the right test, expand, and choose routines, backtracking is remarkably effective in practice. The backtracking algorithm we solved for $SAT$ is the basis of many successful satisfiability programs. Another sign of quality is this: if presented with a $2^{SAT}$ instance, it will always find a satisfying assignment, if one exists, in polynomial time (Exercise 9.1)!

## 9.1.2 Branch-and-bound

The same principle can be generalized from search problems like $SAT$ to optimization problems. For concretely, let's say we have a minimization problem; maximization will follow the same pattern.

As before, we deal with partial solutions, each of which represents a subproblem, namely, what is the (cost of) best way to complete this solution? And before, we need a bound for eliminating partial solutions, since there is no source of efficiency in our method. To reject a subproblem, we must be certain that its cost exceeds that of other solution we have already encountered. Its exact cost is unknown to us is generally not efficiently computable. So we use a quicker lower bound on this.

```
Start with some problem $P_0$
$S = \{P_0\}$, the set of active subproblems
bestsoft = $\infty$
Repeat while $S$ is nonempty:
  choose a subproblem $P \in S$ and remove
  it from $S$
  expand it into smaller subproblems $P_1, P_2, \dots, P_k$
  For each $P_i$:
    If $P_i$ is a complete solution: update bestsoft
    else if lowerbound($P_i$) < bestsoft: add $P_i$ to $S$
return bestsoft
```

Let's see how this works for the traveling salesman problem on a graph $G=(V, E)$ with edge lengths $d_e > 0$. A partial solution is a simple path $a \sim b$ passing through some vertices $S \subseteq V$, $S$ includes the endpoints $a$ and $b$. We can denote such a partial solution by the tuple $[a, S, b]$—in fact, $a$ will be fixed throughout the algorithm. The corresponding subproblem is to find the best completion of the tour, that is, the cheapest path $b \rightsquigarrow a$ with intermediate nodes $V-S$. Notice that the initial problem is of the form $[a, a]$ for any $a \in V$ of our choosing.

At each step of the branch-and-bound algorithm, we extend a particular partial solution $[a, S, b]$ by a single edge $(b, x)$, where $x \in V-S$. We can be up to $|V-S|$ ways to do this, and each of these branches leads to a subproblem of the form $[a, S \cup \{x\}, b]$.

How can we lower-bound the cost of completing a particular $[a, S, b]$? Many sophisticated methods have been developed for this, but let's look at a simpler one. The remainder of the tour consists of a path through $V-S$, plus edges from $a$ and $b$ to $V-S$. Therefore, its cost is at least that of the following:

1. The lightest edge from $a$ to $V-S$.
2. The lightest edge from $b$ to $V-S$.
3. The minimum spanning tree of $V-S$.

(Do you see why?) And this lower bound can be computed quickly by a minimum spanning tree. Figure 9.2 runs through an example: each node of the tree represents a partial tour (the path from the root to that node) at some stage is considered by the branch-and-bound procedure. Notice how just 28 partial solutions are considered, instead of the $7! = 5,040$ that would arise in brute-force search.

## 9.2 Approximation algorithms

In an optimization problem we are given an instance $I$ and are asked to find the optimum solution—the one with the maximum if we have a maximization problem like INDSET, or the minimum if we are dealing with a minimization problem such as TSP. For every instance $I$, let us denote by $opt(I)$ the value (or cost) of the optimum. It makes little simpler to assume that $opt(I)$ is always a positive integer.

We have already seen an example of a (famous) approximation algorithm in Section 5.4: the greedy scheme for COVER. For any instance of size $n$, we showed that this algorithm is guaranteed to find a set cover of cardinality at most $opt(I) \log n$. This $\log n$ factor is known as the approximation guarantee of the algorithm.

More generally, consider any minimization problem. Suppose now that we have an algorithm $A$ for our problem which, given an $I$, returns a solution with value $A(I)$. The approximation ratio of $A$ is defined to be
$$\alpha_A = \max \frac{A(I)}{opt(I)}.$$

Figure 9.2 (a) A graph and its optimal traveling salesman tree. (b) The branch-and-bound search, explored left to right. Boxed numbers indicate lower bounds on cost.
(a) img/3dd1f1364df87b068fc32a15b999_287_0.png
(b) img/3dd1f1364df87b068fc32a15b999_287_1.png

In other words, $\alpha_A$ measures the factor by which the output of algorithm $A$ exceeds the optimal solution. The approximation ratio can also be defined for maximization problems in the same way—except to get a number larger than 1 we take the reciprocal.

So, when faced with an NP-complete optimization problem, a reasonable goal is to look for an approximation algorithm $A$ whose $\alpha_A$ is as small as possible. this kind of guarantee might seem a little puzzling: How can we come close to the optimum if we cannot determine the optimum? Let’s look at a simple example.

Figure 9.3 A graph whose optimal vertex cover, shown shaded, is of size 8.
img/3dd1f1364df87b068fc32a15b999_288_0.png

### 9.2.1 Vertex cover

We already know the VERTEX COVER problem is NP-hard.

### Vertex Cover

Input: An undirected graph $G = (V, E)$.
Output: A subset of the vertices $S \subseteq V$ that touches every edge.
Goal: Minimize $|S|$.

See Figure 9.3 for an example.

Since VERTEX COVER is a special case of SET COVER, we know from Chapter 5 that it can be approximated within a factor of $O(\log n)$ by the greedy algorithm: repeatedly delete the vertex of highest degree and include it in the vertex cover. There are graphs on which the greedy algorithm returns a vertex cover that is indeed $\log n$ the optimum.

A better approximation algorithm for VERTEX COVER is based on the notion of matching, a subset of edges that have no vertices in common (Figure 9.4). A matching is maximal if no more edges can be added to it. Maximal matchings will help find good vertex covers, moreover, they are easy to generate: repeatedly pick edges that are disjoint from the ones already chosen, until this is longer possible.

What is the relationship between matchings and vertex covers? Here is the crucial fact: any vertex cover of a graph $G$ must be at least the number of edges in any matching in $G$; that is, any matching provides a lower bound on OPT. Finding such a lower bound is a key step in designing an approximation algorithm, because we must compare the quality of the solution found by our algorithm to OPT, which is NP-complete to compute.

**Figure 9.4** (a) A matching, (b) its completion to a maximal matching, and (c) the resulting vertex cover.
img/3dd1f1364df87b068fc32a15b999_289_0.png

One more observation completes the design of our approximation algorithm: let $S$ be a set that contains both endpoints of each edge in a maximal matching $M$. $S$ must be a vertex cover—if it isn't, that is, if it doesn't touch some edge $e \in E, M$ could not possibly be maximal if we could still add $e$ to it. But our cover has $2|M|$ vertices. From the previous paragraph we know that *any vertex cover* must have at least $|M|$. So we're done.

Here's the algorithm for VERTEX COVER:

```
Find a maximal matching $M \subseteq E$
Return $S = [all \ endpoints \ edges \ in \ M]$
```

This simple procedure always returns a vertex cover whose size is at most twice optimal!

In summary, even though we have no way of finding the best vertex cover, we can easily find another structure, a maximal matching, with two key properties:

1. Its size gives us a lower bound on the optimal vertex cover.
2. It can be used to build a vertex cover, whose size is related to that of the optimal cover using property 1.

Thus, this simple algorithm has an approximation ratio of $\alpha_A \le 2$. In fact, it is not hard to find examples on which it makes a 100% error; however, $\alpha_A = 2$.

### 9.2.2 Clustering

We turn to a *clustering* problem, in which we have some data (text documents, say, or images, speech samples) that we want divide into groups. It is often useful to define "distances" between these data points, numbers that capture how close or far they are from one another. Assume that we have such distances and that they satisfy the usual *metric properties*:

- $d(x, y) \ge 0$ for all $x, y$.
