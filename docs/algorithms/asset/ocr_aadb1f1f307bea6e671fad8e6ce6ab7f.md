Chapter 6

Algorithms 157

# Figure 6.1 A dag and its linearization (topological ordering).

![](bbox=[0.298, 0.114, 0.952, 0.225])

to be 0. We proceed with progressively “larger” subproblems—distances to vertices that are further and further along the linearization—where we are thinking of a subproblem as large if we need to solve a lot of other subproblems before we get to it.

This is a very general technique. At each node, we compute some function of the values of the node’s predecessors. So it happens that our particular function is a minimum of sums, but we could just well make it maximum, in which case we would get longest paths in the dag. Or we could use a product instead of sum inside the brackets, in which case we would end computing the path with the smallest product of edges.

Dynamic programming is a very powerful algorithmic paradigm in which a problem is solved by identifying a collection of subproblems and tackling them one by one, smallest first, using the answers to small problems to figure out larger ones, until the whole of them is solved. In dynamic programming we are not given a dag; the dag is implicit. Its nodes are the subproblems we define, and its edges are the dependencies between the subproblems: to solve subproblem B we need the answer to A, then there is a (conceptual) edge from A to B. In this case, A is thought of as a smaller subproblem than B—and it will always be smaller, in an obvious sense.

It’s time we saw an example.

# 6.2 Longest increasing subsequences

In the increasing subsequence problem, the input is a sequence of numbers $a_1, \dots, a_n$. A subsequence is any subset of these numbers taken in order, of the form $a_{i_1}, a_{i_2}, \dots, a_{i_k}$, where $1 \le i_1 < i_2 < \dots < i_k \le n$, and an increasing subsequence is one in which the numbers are getting strictly larger. The task is to find the subsequence of greatest length. For instance, the longest increasing subsequence of 5, 2, 8, 6, 3, 9, 7 is 2, 3, 6, 9:

5 2 8 6 3 9 7