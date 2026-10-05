192

Chap. 5 Binary Trees

![](bbox=[0.355, 0.196, 0.642, 0.313])

**Figure 5.30** An impossible Huffman tree, showing the situation where the two nodes with least weight, $l_1$ and $l_2$, are not the deepest nodes in the tree. Triangles represent subtrees.

**Theorem 5.3** Function *buildHuff* builds the Huffman tree with the minimum external path weight for the given set of letters.

**Proof:** The proof is by induction on $n$, the number of letters.

+   * **Base Case:** For $n=2$, the Huffman tree must have the minimum external path weight because there are only two possible trees, each with identical weighted lengths for the two leaves.
* **Induction Hypothesis:** Assume that any tree created by *buildHuff* that contains $n-1$ leaves has minimum external path weight.
* **Induction Step:** From a given tree $T$ built by *buildHuff* with $n$ leaves, $n \geq 2$, suppose that $w_1 \leq w_2 \leq \dots \leq w_n$ where $w_1$ to $w_n$ are the weights of the letters. Call $V$ the parent of the leaves with frequencies $w_1$ and $w_2$. From the lemma, we know that the leaf nodes containing the letters with frequencies $w_1$ and $w_2$ are as deep as any nodes in $T$. If any other leaf were deeper, we reduce their weighted path length by swapping them with $w_1$ or $w_2$. But the lemma tells us that no deeper nodes exist. Call $T'$ the Huffman tree that is identical to $T$ except that node $V$ is replaced with a leaf $V'$ whose weight is $w_1+w2$. By the induction hypothesis, $T'$ has minimum external path length. Returning the children to $V$ restores $T$, which must also have minimum external path length.

By that mathematical induction, function *buildHuff* creates the Huffman tree with minimum external path length.

# 5.6.2 Assigning using Huffman Codes

Once the Huffman tree has been constructed, it is an easy matter to assign codes to individual letters. Beginning at the root, we assign either a '0' or a '1' to edge in the tree. '0' is assigned to edges connecting a node with its left child, and '1' to edges connecting a node with its right child. This process is illustrated by