$$(i == m) \lor (i \ne m \land j \ne n \land x = a[i,j])$$

Complement of this condition in conjunction with invariant $\Rightarrow$ the result assertion, which proves correctness of our program developed above.

# ## 6.3 Matching Nuts and Bolts Optimally

# ### Problem Description

There is a bag full of $n$ nuts and $n$ bolts, each of distinct sizes, such that there is one-to-one correspondence between the nuts and the bolts, i.e., for every nut, there is a bolt and vice versa. Nuts cannot be compared to nuts and bolts cannot be compared to bolts directly, but nuts can be compared to bolts by trying to fit one into the other. Design and implement an optimal algorithm for fitting all nuts to bolts. By optimal we mean to minimize the number of comparisons involved in the algorithm.

# ### Solution

The same problem can be posed to a computer scientist as follows:

Given two sets $B : \{b_1, \ldots, b_n\}$ and $N : \{n_1, \ldots, n_n\}$, where $B$ is a set of distinct real numbers (representing the sizes of the bolts) and $N$ is a permutation of $B$, we wish to find efficiently the unique permutation $\sigma \in S_n$ such that $b_i = n_{\sigma(i)}$, based on queries of the form *compare* $b_i$ and $n_j$. The answer to each such query is either:

+   1. $b_i > n_j$
+   2. $b_i = n_j$
+   3. $b_i < n_j$

Since there are $n!$ possibilities for $\sigma$, the obvious information theoretic lower bound shows that any bounded degree decision tree that solves the problem has depth at least $\log_3(n!)$.

Using Sterling’s approximation:

$$\log_3(n!) \approx \Theta(n \log_3 n)$$

Similar to comparison-based sorting, it can be analyzed using decision tree. Please note that we can model any algorithm for matching nuts and bolts as a decision tree.

The tree will be a *ternary tree*, since every comparison has three possible outcomes:

+   1. *less than,*