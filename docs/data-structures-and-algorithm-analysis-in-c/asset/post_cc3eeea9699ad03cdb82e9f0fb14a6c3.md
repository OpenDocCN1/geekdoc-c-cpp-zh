
![](img/e449061a0cac9cafaefd979fab665b33_381_0.png)

Figure 8.18 A large disjoint set tree (numbers below nodes are ranks)

We begin by establishing two lemmas concerning the properties of the ranks. Figure 8.18 gives a visual picture of both lemmas.

### Lemma 8.1

When executing a sequence of union instructions, a node of rank r > 0 must have at least one child of rank 0, 1, ..., r - 1.

### Proof

By induction. The basis r = 1 is clearly true. When a node grows from rank r - 1 to rank r, it obtains a child of rank r - 1. By the inductive hypothesis, it already has children of ranks 0, 1, ..., r - 2, thus establishing the lemma.

The next lemma seems somewhat obvious but is used implicitly in the analysis.

### Lemma 8.2

At any point in the union/find algorithm, the ranks of the nodes on a path from the leaf to a root increase monotonically.

### Proof

The lemma is obvious if there is no path compression. If, after path compression, some node v is a descendant of w, then clearly v must have been a descendant of w when only unions were considered. Hence the rank of v is less than the rank of w.

Suppose we have two algorithms, A and B. Algorithm A works and computes all the answers correctly, but algorithm B does not compute correctly, or even produce useful answers. Suppose, however, that every step in algorithm A can be mapped to an equivalent step in algorithm B. Then it is easy to see that the running time for algorithm B describes the running time for algorithm A exactly.

We can use this idea to analyze the running time of the disjoint sets data structure. We will describe an algorithm B, whose running time is exactly the same as the disjoint sets structure, and then algorithm C, whose running time is exactly the same as algorithm B. Thus any bound for algorithm C will be a bound for the disjoint sets data structure.

## Partial Path Compression

Algorithm A is our standard sequence of union-by-rank and find with path compression operations. We design an algorithm B that will perform the exact same sequence of path compression operations as algorithm A. In algorithm B, we perform all unions prior to any find. Then each find operation in algorithm A is replaced by a partial find operation in algorithm B. A partial find operation specifies the search item and the node up to which the path compression is performed. The node that will be used is the node that would have been the root at the time the matching find was performed in algorithm A.

Figure 8.19 shows that algorithm A and algorithm B will get equivalent trees (forests) at the end, and it is easy to see that the exact same amount of parent changes are performed by algorithm A's finds, compared to algorithm B's partial finds. But algorithm B should be simpler to analyze, since we have removed the mixing of unions and finds from the equation. The basic quantity to analyze is the number of parent changes that can occur in any sequence of partial finds, since all but the top two nodes in any find with path compression will obtain new parents.

## A Recursive Decomposition

What we would like to do now is to divide each tree into two halves: a top half and a bottom half. We would then like to ensure that the number of partial find operations in the top half plus the number of partial find operations in the bottom half is exactly the same as the total number of partial find operations. We would then like to write a formula for the total path compression cost in the tree in terms of the path compression cost in the top half plus the path compression cost in the bottom half. Without specifying how we decide which nodes are in the top half, and which nodes are in the bottom half, we can look at Figures 8.20, 8.21, and 8.22, to see how most of what we want to do can work immediately.

![](img/e449061a0cac9cafaefd979fab665b33_382_0.png)

**Figure 8.19** Sequences of union and find operations replaced with equivalent cost of union and partial find operations

TOP

BOTTOM

![](img/e449061a0cac9cafaefd979fab665b33_383_0.png)

**Figure 8.20** Recursive decomposition, case 1: Partial find is entirely in bottom

TOP

BOTTOM

![](img/e449061a0cac9cafaefd979fab665b33_383_1.png)

**Figure 8.21** Recursive decomposition, case 2: Partial find is entirely in top

TOP

BOTTOM

![](img/e449061a0cac9cafaefd979fab665b33_383_2.png)

**Figure 8.22** Recursive decomposition, case 3: Partial find goes from bottom to top

In Figure 8.21, the partial find resides entirely in the top half. Thus one partial find in the top half corresponds to one original partial find, and the charges can be recursively assigned to the top half.

However, we run into lots of trouble when we reach Figure 8.22. Here x is in the bottom half, and y is in the top half. The path compression would require that all nodes from x to y's child acquire y as its parent. For nodes in the top half, that is no problem, but for nodes in the bottom half this is a dealbreaker: Any recursive charges to the bottom have to keep everything in the bottom. So as Figure 8.23 shows, we can perform the path compression on the top, but while some nodes in the bottom will need new parents, it is not clear what to do, because the new parents for those bottom nodes cannot be top nodes, and the new parents cannot be other bottom nodes.

The only option is to make a loop where these nodes' parents are themselves and make sure these parent changes are correctly charged in our accounting. Although this is a new algorithm because it can no longer be used to generate an identical tree, we don't need identical trees; we only need to be sure that each original partial find can be mapped into a new partial find operation and that the charges are identical. Figure 8.24 shows what the new tree will look like, and so the big remaining issue is accounting.

Looking at Figure 8.24, we see that the path compression charges from x to y can be split into three parts. First, there is the path compression from z (the first top node on the upward path) to y. Clearly those charges are already accounted for recursively. Then there is the charge from the topmost-bottom node w to z. But that is only one unit, and there can be at most one of those per partial find operation. In fact, we can do a little better. There can be at most one of those per partial find operation on the top half. But how do we account for the parent charges on the path from x to w? One idea would be to argue that those changes would be exactly the same cost as if there were a partial find from x to w. But there is a big problem with that argument: It converts an original partial find into a partial find on the top plus a partial find on the bottom, which means the number of operations M would no longer be the same.

![](img/e449061a0cac9cafaefd979fab665b33_384_0.png)

**Figure 8.23** Recursive decomposition, case 3: Path compression can be performed on the top nodes, but the bottom nodes must get new parents; the parents cannot be top parents, and they cannot be other bottom nodes

![](img/e449061a0cac9cafaefd979fab665b33_385_0.png)

**Figure 8.24** Recursive decomposition, case 3: The bottom node new parents are the nodes themselves

Fortunately, there is a simpler argument: Since each node on the bottom can have its parent set to itself only once, the number of charges are limited by the number of nodes on the bottom whose parents are also in the bottom (i.e., w is excluded).

There is one important detail that we must verify: Can we get in trouble on a subsequent partial find given that our reformulation detaches the nodes between x and w from the path to y? The answer is no. In the original partial find, suppose any of the nodes between x and w are involved in a subsequent original partial find. In that case, it will be with one of y's ancestors, and when that happens, any of those nodes will be the topmost "bottom node" in our reformulation. Thus on the subsequent partial find, the original partial find's parent change will have a corresponding one unit charge in our reformulation.

We can now proceed with the analysis. Let M be the total number of original partial find operations. Let Mt be the total number of partial find operations performed exclusively on the top half, and let Mb be the total number of partial find operations performed exclusively on the bottom half. Let N be the total number of nodes. Let Nt be the total number of top-half nodes, let Nb be the total number of bottom-half nodes, and let Nnb be the total number of non-root bottom nodes (i.e., the number of bottom nodes whose parents are also bottom nodes prior to any partial finds).

### Lemma 8.3
M = Mt + Mb.

### Proof

In cases 1 and 3, each original partial find operation is replaced by a partial find on the top half, and in case 2, it is replaced by a partial find on the bottom half. Thus each partial find is replaced by exactly one partial find operation on one of the halves.

Our basic idea is that we are going to partition the nodes so that all nodes with rank s or lower are in the bottom, and the remaining nodes are in the top. The choice of s will be made later in the proof. The next lemma shows that we can provide a recursive formula
