is optimal, as demonstrated by the existence of the third tree. From this we can see that neither of the obvious solutions works.

This is initially surprising, since the problem appears to be very similar to the construction of a Huffman encoding tree, which, as we have already seen, can be solved by a greedy algorithm. Construction of an optimal binary search tree is harder, because the data are not constrained to appear only at the leaves, and also because the tree must satisfy the binary search tree property.

A dynamic programming solution follows from two observations. Once again, suppose we are trying to place the (sorted) words \(W_{Left}, W_{Left+1}, \dots, W_{Right-1}, W_{Right}\) into a binary search tree. Suppose the optimal binary search tree has \(w_i\) as the root, where \(Left \le i \le Right\). Then the left subtree must contain \(w_{Left}, \dots, w_{i-1}\), and the right subtree must contain \(w_{i+1}, \dots, w_{Right}\) (by the binary search tree property). Further, both of these subtrees must also be optimal, since otherwise they could be replaced by optimal subtrees, which would give a better solution for \(w_{Left}, \dots, w_{Right}\). Thus, we can write a formula for the cost \(C_{Left, Right}\) of an optimal binary search tree. Figure 10.50 may be helpful.

If \(Left > Right\), then the cost of the tree is 0; this is the null tree case, which we always have for binary search trees. Otherwise, the root costs \(p_i\). The left subtree has a cost of \(C_{Left, i-1}\) relative to its root, and the right subtree has a cost of \(C_{i+1, Right}\) relative to its root. As Figure 10.50 shows, each node in these subtrees is one level deeper from \(w_i\) than from their respective roots, so we must add \(\sum_{j=Left}^{i-1} p_j\) and \(\sum_{j=i+1}^{Right} p_j\). This gives the formula

```
\(\begin{aligned} C_{Left, Right} &= \min_{Left \le i \le Right} \left\{ p_i + C_{Left, i-1} + C_{i+1, Right} + \sum_{j=Left}^{i-1} p_j + \sum_{j=i+1}^{Right} p_j \right\} \\ &= \min_{Left \le i \le Right} \left\{ C_{Left, i-1} + C_{i+1, Right} + \sum_{j=Left}^{Right} p_j \right\} \end{aligned}\)
```

From this equation, it is straightforward to write a program to compute the cost of the optimal binary search tree. As usual, the actual search tree can be maintained by saving the value of \(i\) that minimizes \(C_{Left, Right}\). The standard recursive routine can be used to print the actual tree.

![](bbox=[0.205, 0.692, 0.828, 0.902])

Figure 10.50 Structure of an optimal binary search tree