```
else
    value = DoSomething(tree->leftMostChild);
    value = value + DoSomething(tree->rightSibling);
}
return(value);
}
```

When the pointer to the root of a tree is passed as the argument to DoSomething, the value returned by the function corresponds to the

**Q31.** Which of the following is/are correct inorder traversal sequence(s) of binary search tree(s)?
1. 3, 5, 7, 8, 15, 19, 25
2. 5, 8, 9, 12, 10, 15, 25
3. 2, 7, 10, 8, 14, 16, 20
4. 4, 6, 7, 9, 18, 20, 25
(A) 1 and 4 only   (B) 2 and 3 only   (C) 2 and 4 only   (D) 2 only
**Ans:** A

**Q32.** What are the worst-case complexities of insertion and deletion of a key in a binary search tree?
(A) $\Theta(\log n)$ for both insertion and deletion
(B) $\Theta(n)$ for both insertion and deletion
(C) $\Theta(n)$ for insertion and $\Theta(\log n)$ for deletion
(D) $\Theta(\log n)$ for insertion and $\Theta(n)$ for deletion
**Ans:** (B)

**Q33.** The height of a tree is the length of the longest root-to-leaf path in it. The maximum and minimum number of nodes in a binary tree of height 5 are
(A) 63 and 6, respectively   (B) 64 and 5, respectively
(C) 32 and 6, respectively   (D) 31 and 5, respectively
**Ans:** (A)

**Q34.** A file is organized so that the ordering of data records is the same as or close to the ordering of data entries in some index. Then that index is called
(A) Dense   (B) Sparse   (C) Clustered   (D) Unclustered
**Ans:** (C)

**Q35.** Consider a max heap, represented by the array: 40, 30, 20, 10, 15, 16, 17, 8, 4. Now consider that a value 35 is inserted into this heap. After insertion, the new heap is
(A) 40, 30, 20, 10, 15, 16, 17, 8, 4, 35   (B) 40, 35, 20, 10, 30, 16, 17, 8, 4, 15
(C) 40, 30, 20, 10, 35, 16, 17, 8, 4, 15   (D) 40, 35, 20, 10, 15, 16, 17, 8, 4, 30
**Ans:** (B)

**Q36.** The graph shown below 8 edges with distinct integer edge weights. The minimum spanning tree (MST) is of weight 36 and contains the edges: {(A, C), (B, C), (B, E), (E, F), (D, F)}. The edge weights of only those edges which are in the MST are given in the figure shown below. The minimum possible sum of weights of all 8 edges of this graph is