Consider the tree given in Fig. 9.15. The pre-order traversal of the tree is given as A, B, C. Root node first, the left sub-tree next, and then the right sub-tree. Pre-order traversal is also called as depth-first traversal. In this algorithm, the left sub-tree is always traversed before the right sub-tree.

```
Step 1: Repeat Steps 2 to 4 while TREE != NULL
Step 2: Write TREE -> DATA
Step 3: PREORDER(TREE -> LEFT)
Step 4: PREORDER(TREE -> RIGHT)
[END OF LOOP]
Step 5: END
```

# Figure 9.16 Algorithm for pre-order traversal

The word 'pre' in the pre-order specifies that the root node is accessed prior to any other nodes in the left and right sub-trees. Pre-order algorithm is also known as the NLR traversal algorithm (Node-Left-Right). The algorithm for pre-order traversal is shown in Fig. 9.16.

Pre-order traversal algorithms are used to extract a prefix notation from an expression tree. For example, consider the expressions given below. When we traverse the elements of a tree using the pre-order traversal algorithm, the expression that we get is a prefix expression.

```
+ - a b * c / d (from Fig. 9.13)
% + + a b * c d / ^ e f - g h (from Fig of Example 9.2)
^ + / a b * c d % f g - h i (from Fig of Example 9.3)
```

Example 9.6 In Figs (a) and (b), find the sequence of nodes that will be visited using pre-order traversal algorithm.
Solution
TRAVERSAL ORDER: A, B, D, G, H, L, E, C, F, I, J, and K
TRAVERSAL ORDER: A, B, D, C, D, E, F, G, H, and I

![](bbox=[0.1, 0.45, 0.5, 0.62])

# 9.4.2 In-order Traversal

+   1. Traversing the left sub-tree,
+   2. Visiting the root node, and finally
+   3. Traversing the right sub-tree.

Consider the tree given in Fig. 9.15. The in-order traversal of the tree is given as B, A, and c. Left sub-tree first, the root node next, and then the right sub-tree. In-order traversal is also called as symmetric traversal. In this algorithm, the left sub-tree is always traversed before the root node and the right sub-tree. The word 'in' in the in-order specifies that the root node is accessed in between the left and the right sub-trees. In-order algorithm is also known as the LNR traversal algorithm (Left-Node-Right). The algorithm for in-order traversal is shown in Fig. 9.17.

```
Step 1: Repeat Steps 2 to 4 while TREE != NULL
Step 2: INORDER(TREE -> LEFT)
Step 3: Write TREE -> DATA
Step 4: INORDER(TREE -> RIGHT)
[END OF LOOP]
Step 5: END
```

# Figure 9.17 Algorithm for in-order traversal

In-order traversal algorithm is usually used to display the elements of a binary search tree. Here, all the elements with a value lower than a given value are accessed before the elements with a higher value. We will discuss binary search trees in detail in the next chapter.