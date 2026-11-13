
increase, the potential change is at most O(log N). Adding the actual time and potential change gives the O(log N) amortized bound for deleteMin.

Finally, for the decreaseKey operation, let C be the number of cascading cuts. The actual cost of a decreaseKey is C + 1, which is the total number of cuts performed. The first (noncascading) cut creates a new tree and thus increases the potential by 1. Each cascading cut creates a new tree but converts a marked node to an unmarked (root) node, for a net loss of one unit per cascading cut. The last cut also can convert an unmarked node (in Fig. 11.20 it is node 5) into a marked node, thus increasing the potential by 2. The total change in potential is thus at most 3 - C. Adding the actual time and the potential change gives a total of 4, which is O(1).

## 11.5 Splay Trees

As a final example, we analyze the running time of splay trees. Recall, from Chapter 4, that after an access of some item X is performed, a splaying step moves X to the root by a series of three operations: zig, zig-zag, and zig-zig. These tree rotations are shown in Figure 11.21. We adopt the convention that if a tree rotation is being performed at node X, then prior to the rotation, P is its parent and (if X is not the child of the root) G is its grandparent.

Recall that the time required for any tree operation on node X is proportional to the number of nodes on the path from the root to X. If we count each zig operation as one rotation and each zig-zig or zig-zag as two rotations, then the cost of any access is equal to 1 plus the number of rotations.

![](img/e449061a0cac9cafaefd979fab665b33_569_0.png)

Figure 11.21 zig, zig-zag, and zig-zig operations; each has a symmetric case (not shown)

In order to show an O(log N) amortized bound for the splaying step, we need a potential function that can increase by at most O(log N) over the entire splaying step but that will also cancel out the number of rotations performed during the step. It is not at all easy to find a potential function that satisfies these criteria. A simple first guess at a potential function might be the sum of the depths of all the nodes in the tree. This does not work, because the potential can increase by $\Theta(N)$ during an access. A canonical example of this occurs when elements are inserted in sequential order.

$$\Phi(T) = \sum_{i \in T} \log S(i)$$

where $S(i)$ represents the number of descendants of $i$ (including $i$ itself). The potential function is the sum, over all nodes $i$ of the tree $T$, of the logarithm of $S(i)$.

To simplify the notation, we will define

$$R(i) = \log S(i)$$

This makes

$$\Phi(T) = \sum_{i \in T} R(i)$$

$R(i)$ represents the $rank$ of node $i$. The terminology is similar to what we used in the analysis of the disjoint set algorithm, binomial queues, and Fibonacci heaps. In all these data structures, the meaning of $rank$ is somewhat different, but the rank is generally meant to be on the order (magnitude) of the logarithm of the size of the tree. For a tree $T$ with $N$ nodes, the rank of the root is simply $R(T) = \log N$. Using the sum of ranks as a potential function is similar to using the sum of heights as a potential function. The important difference is that while a rotation can change the heights of many nodes in the tree, only $X$, $P$, and $G$ can have their ranks changed.

Before proving the main theorem, we need the following lemma.

### Lemma 11.4

If $a + b \le c$, and $a$ and $b$ are both positive integers, then

$$\log a + \log b \le 2 \log c - 2$$

### Proof

By the arithmetic-geometric mean inequality,

$$\sqrt{ab} \le (a + b)/2$$

Thus,

$$\sqrt{ab} \le c/2$$

Squaring both sides gives

$ab \le c^2 / 4$

Taking logarithms of both sides proves the lemma.

With the preliminaries taken care of, we are ready to prove the main theorem.

### Theorem 11.5

The amortized time to splay a tree with root T at node X is at most 3(R(T) - R(X)) + 1 = O(log N).

### Proof

The potential function is the sum of the ranks of the nodes in T.

If X is the root of T, then there are no rotations, so there is no potential change.

The actual time is 1 to access the node; thus, the amortized time is 1 and the theorem is true. Thus, we may assume that there is at least one rotation.

For any splaying step, let R(X) and S(X) be the rank and size of X before the step, and let R'(X) and S'(X) be the rank and size of X immediately after the splaying step.

We will show that the amortized time required for a zig is at most 3(R'(X) - R(X)) + 1 and that the amortized time for either a zig-zag or zig-zig is at most 3(R'(X) - R(X)).

We will show that when we add over all steps, the sum telescopes to the desired time bound.

Zig step: For the zig step, the actual time is 1 (for the single rotation), and the potential change is R'(X) + R'(P) - R(X) - R(P). Notice that the potential change is easy to compute, because only Xs and Ps trees change rank. Thus, using AT to represent amortized time,

$AT_{zig} = 1 + R'(X) + R'(P) - R(X) - R(P)$

From Figure 11.21 we see that $S'(X) \ge S'(P)$, thus, it follows that $R'(X) \ge R'(P)$. Thus,

$AT_{zig} \le 1 + R'(X) - R(X)$

Since $S'(X) \ge S(X)$, it follows that $R'(X) - R(X) \ge 0$, so we may increase the right side, obtaining

$AT_{zig} \le 1 + 3(R'(X) - R(X))$

Zig-zag step: For the zig-zag case, the actual cost is 2, and the potential change is $R'(X) + R'(P) + R'(G) - R(X) - R(P) - R(G)$. This gives an amortized time bound of

$AT_{zig-zag} = 2 + R'(X) + R'(P) + R'(G) - R(X) - R(P) - R(G)$

From Figure 11.21 we see that $S'(X) = S'(G)$, so their ranks must be equal. Thus, we obtain

$AT_{zig-zag} = 2 + R'(P) + R'(G) - R(X) - R(P)$

We also see that $S(P) \ge S(X)$. Consequently, $R(X) \le R(P)$. Making this substitution gives

$AT_{zig-zag} \le 2 + R(P) + R(G) - 2R(X)$

From Figure 11.21 we see that $S(P) + S(G) \le S(X)$. If we apply Lemma 11.4, we obtain

$\log S(P) + \log S(G) \le 2 \log S(X) - 2$

By the definition of $rank$, this becomes

$R(P) + R(G) \le 2R(X) - 2$

Substituting this, we obtain

$AT_{zig-zag} \le 2R(X) - 2R(X)$
$\le 2(R(X) - R(X))$

Since $R(X) \ge R(X)$, we obtain

$AT_{zig-zag} \le 3(R(X) - R(X))$

Zig-zig step. The third case is the zig-zig. The proof of this case is very similar to the zig-zag case. The important inequalities are $R(X) = R(G)$, $R(X) \ge R(P)$, $R(X) \le R(P)$, and $S(X) + S(G) \le S(X)$. We leave the details as Exercise 11.8.

The amortized cost of an entire splay is the sum of the amortized costs of each splay step. Figure 11.22 shows the steps that are performed in a splay at node 2. Let $R_1(2)$, $R_2(2)$, $R_3(2)$, and $R_4(2)$ be the rank of node 2 in each of the four trees. The cost of the first step, which is a zig-zag, is at most $3(R_1(2) - R_1(2))$. The cost of the second step, which is a zig-zig, is $3(R_2(2) - R_2(2))$. The last step is a zig and has cost no larger than $3(R_4(2) - R_3(2)) + 1$. The total cost thus telescopes to $3(R_4(2) - R_1(2)) + 1$.

![](img/e449061a0cac9cafaefd979fab665b33_572_0.png)

Figure 11.22 The splaying steps involved in splaying at node 2

In general, by adding up the amortized costs of all the rotations, of which at most one can be a zig, we see that the total amortized cost to splay at node X is at most 3(R(X) - R(X)) + 1, where R(X) is the rank of X before the first splaying step and R(X) is the rank of X after the last splaying step. Since the last splaying step leaves X at the root, we obtain an amortized bound of 3(R(T) - R(X)) + 1, which is O(log N).

Because every operation on a splay tree requires a splay, the amortized cost of any operation is within a constant factor of the amortized cost of a splay. Thus, all splay tree access operations take O(log N) amortized time. To show that insertions and deletions take O(log N), amortized time, potential changes that occur either prior to or after the splaying step should be accounted for.

In the case of insertion, assume we are inserting into an N-1 node tree. Thus, after the insertion, we have an N-node tree, and the splaying bound applies. However, the insertion at the leaf node adds potential prior to the splay to each node on the path from the leaf node to the root. Let n1, n2, ..., nk be the nodes on the path prior to the insertion of the leaf (nk is the root), and assume they have size s1, s2, ..., sk. After the insertions, the sizes are s1 + 1, s2 + 1, ..., sk + 1. (The leaf will contribute 0 to the potential so we can ignore it.) Note that (excluding the root node) $s_j + 1 \le s_{j+1}$, so the new rank of nj is no more than the old rank of nj+1. Thus, the increase of ranks, which is the maximum increase in potential that results from adding a new leaf, is limited by the new rank of the root, which is O(log N).

A deletion consists of a nonsplaying step that attaches one tree to another. This does increase the rank of one node, but that is limited by log N (and is compensated by the removal of a node, which at the time was a root). Thus the splaying costs accurately bound the cost of a deletion.

By using a more general potential function, it is possible to show that splay trees have several remarkable properties. This is discussed in more detail in the exercises.

## Summary

In this chapter, we have seen how an amortized analysis can be used to apportion charges among operations. To perform the analysis, we invent a fictitious potential function. The potential function measures the state of the system. A high-potential data structure is volatile, having been built on relatively cheap operations. When the expensive bill comes for an operation, it is paid for by the savings of previous operations. One can view potential as standing for potential disaster, in that very expensive operations can occur only when the data structure has a high potential and has used considerably less time than has been allocated.

Low potential in a data structure means that the cost of each operation has been roughly equal to the amount allocated for it. Negative potential means debt; more time has been spent than has been allocated, so the allocated (or amortized) time is not a meaningful bound.

As expressed by Equation (11.2), the amortized time for an operation is equal to the sum of the actual time and potential change. Taken over an entire sequence of operations, the amortized time for the sequence is equal to the total sequence time plus the net change in potential. As long as this net change is positive, then the amortized bound provides an upper bound for the actual time spent and is meaningful.
