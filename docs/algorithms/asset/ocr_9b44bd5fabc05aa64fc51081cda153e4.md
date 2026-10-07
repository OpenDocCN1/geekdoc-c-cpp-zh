# 152

# Exercises

(a) Prove this property carefully.

(B) Here is the MST algorithm. The input is some undirected graph
G = (V, E) (in adjacency list format) with edge weights $w_e$.
sort the edges according to their weights
for each edge $e \in E$, in decreasing order of $w_e$:
if $e$ is part of a cycle of $G$:
G = G - e$ (that is, remove $e$ from $G$)
return G

Prove that algorithm is correct.

(c) On each iteration, the algorithm must check whether there is a cycle containing a specific edge $e$. Give a linear-time algorithm for this,
and justify its correctness.

(d) What is the overall time taken by this algorithm, in terms of $|E|$?

+   5.23. You are given a graph $G = (V, E)$ with positive edge weights, and a minimum spanning tree $T = (V, E')$ with respect to these weights; you may assume $G$ and $T$ are given as adjacency lists. Now suppose the weight of a particular edge $e \in E$ is modified from $w(e)$ to a new value $\hat{w}(e)$. You wish to update the minimum spanning tree $T$ to reflect this change, without recomputing the entire tree from scratch. There are four cases. In each case give a linear-time algorithm for updating the tree.

+   (a) $e 
otin E'$
(b) $e \in E'$ and $\hat{w}(e) < w(e)$.
(c) $e \in E'$ and $\hat{w}(e) > w(e)$.
(d) $e 
otin E'$ and $\hat{w}(e) > w(e)$.

+   5.24. We sometimes light spanning trees with certain special properties. Here's an example.

Input: Undirected graph $G = (V, E)$; edge weights $w_e$; subset of vertices
U $\cup V$

Output: The lightest spanning tree in which the nodes of $U$ are leaves\(there might be other leaves in this tree).

(The answer isn't necessarily a minimum spanning tree.)
Give an algorithm for this problem which runs in $O(|E|\log|V|)$ time. *Hint*: When you remove nodes $U$ from the optimal solution, what is left?

+   5.25. A binary counter of unsigned length supports two operations: *increment* (which increases its value by one) and *reset* (which sets its value back to zero). Show that, starting from an initial zero, any sequence of $n$ increment and reset operations takes time $O(n)$; that is, the amortized time per operation is $O(1).

+   5.26. Here's a problem that occurs in automatic program analysis. For a set of variables $x_1, \dots, x_n$, you are given some *equality* constraints, of the form