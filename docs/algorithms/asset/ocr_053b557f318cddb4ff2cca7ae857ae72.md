# 9.2 Approximation algorithms

some vertices $S \subseteq V$, $S$ includes the endpoints $a$ and $b$. We can denote such a partial solution by the tuple $[a, S, b]$—in fact, a will be fixed throughout the algorithm. The corresponding subproblem is to find the best completion of the tour, that is, the cheapest path $b \rightsquigarrow a$ with intermediate nodes $V-S$. Notice that the initial problem is of the form $[a, a]$ for any $a \in V$ of our choosing.

At each step of the branch-and-bound algorithm, we extend a particular partial solution $[a, S, b]$ by a single edge $(b, x)$, where $x \in V-S$. We can be up to $|V-S|$ ways to do this, and each of these branches leads to a subproblem of the form $[a, S \cup \{x\}, b]$.

How can we lower-bound the cost of completing a particular $[a, S, b]$? Many sophisticated methods have been developed for this, but let's look at a simpler one. The remainder of the tour consists of a path through $V-S$, plus edges from $a$ and $b$ to $V-S$. Therefore, its cost is at least that of the following:

+   1. The lightest edge from $a$ to $V-S$.
2. The lightest edge from $b$ to $V-S$.
3. The minimum spanning tree of $V-S$.

(Do you see why?) And this lower bound can be computed quickly by a minimum spanning tree. Figure 9.2 runs through an example: each node of the tree represents a partial tour (the path from the root to that node) that at some stage is considered by the branch-and-bound procedure. Notice how just 28 partial solutions are considered, instead of the $7! = 5,040$ that would arise in a brute-force search.

# 9.2 Approximation algorithms

In an optimization problem we are given an instance $I$ and are asked to find the optimum solution—the one with the maximum gain if we have a maximization problem like INDSET, or the minimum if we are dealing with a minimization problem such as the TSP. For every instance $I$, let us denote by $opt(I)$ the value (or cost) of the optimum. It makes a little simpler to assume that $opt(I)$ is always a positive integer.

We have already seen an example of a (famous) approximation algorithm in Section 5.4: the greedy scheme for COVER. For any instance of size $n$, we showed that this greedy algorithm is guaranteed to quickly find a set cover of cardinality at most $opt(I) \log n$. This $\log n$ factor is known as the approximation guarantee of the algorithm.

More generally, consider any minimization problem. Suppose now that we have an algorithm $A$ for our problem which, given an instance $I$, returns a solution with value $A(I)$. The approximation ratio of $\mathcal{A}$ is defined to be

> $$\alpha_A = \max \frac{A(I)}{opt(I)}.$