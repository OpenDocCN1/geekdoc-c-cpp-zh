![](bbox=[0.414, 0.193, 0.735, 0.293])

bound will occur when each internal node has two non-empty children, that is, the tree is full. However, this observation does not tell what shape of tree will yield the highest percentage of non-empty leaves. It turns out not to matter, because all full binary trees with $n$ internal nodes have the same number of leaves. This fact allows us to compute the space requirements for a full binary tree implementation whose leaves require a different amount of space from its internal nodes.

# Theorem 5.1 Full Binary Tree Theorem: The number of leaves in a non-empty binary tree is one more than the number of internal nodes.

**Proof:** The proof is by mathematical induction on $n$, the number of internal nodes. This is an example of an induction proof where we reduce from an arbitrary instance of size $n-1$ that meets the induction hypothesis.

+   - **Base Cases:** The non-empty tree with zero internal nodes has one leaf. A full binary tree with one internal node has two leaf nodes. Thus, the base cases for $n=0$ and $n=1$ conform to the theorem.
- **Induction Hypothesis:** Assume that any binary tree $\mathbf{T}$ containing $n-1$ internal nodes has $n$ leaves.
- **Induction Step:** Given tree $\mathbf{T}$ with $n$ internal nodes, select one internal node $I$ whose children are both leaves. Remove both of $I$'s children, making $I$ a leaf node. Call the new tree $\mathbf{T}'$. $\mathbf{T}'$ has $n-1$ internal nodes. From the induction hypothesis, $\mathbf{T}'$ has $n$ leaves. Now, restore $I$'s children. We now again have $\mathbf{T}$ with $n$ internal nodes. How many leaves does $T$ have? Because $T'$$ has $n$ leaves, adding the two children yields $n+2$. However, $I$ counted as one of the leaves in $\mathbf{T}'$ and has now become an internal node. Thus, $\mathbf{T}$ has $n+1$ leaves and $n$ internal nodes.

By mathematical induction the theorem holds for all values of $n \ge 0$.

When analyzing the space requirements for a binary tree implementation, it is useful to know how many empty subsets a tree contains. A simple extension of the Full Binary Tree Tells us exactly how many empty subsets there are in any binary tree, whether full or not. Here are two approaches to proving the following theorem, and each suggests a useful way of thinking about binary trees.