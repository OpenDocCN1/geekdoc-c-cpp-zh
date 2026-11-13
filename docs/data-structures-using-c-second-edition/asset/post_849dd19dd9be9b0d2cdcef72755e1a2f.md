
12. Consider the binary search tree given below. Now do the following operations:
- Find the result of in-order, pre-order, and post-order traversals.
- Show the deletion of the root node
- Insert 11, 22, 33, 44, 55, 66, and 77 in the tree

![](img/be6359df08208122bec6fad1103de211_355_0.png)

13. Consider the AVL tree given below and insert 18, 81, 29, 15, 19, 26, 25, and 1 in it. Delete nodes 39, 63, 15, and 1 from the AVL tree formed after solving the above question.

![](img/be6359df08208122bec6fad1103de211_355_1.png)

14. Discuss the properties of a red-black tree. Explain the insertion cases.

15. Explain splay trees in detail with relevant examples.

16. Provide the memory representation of the binary tree given below:
- Find the result of one-way in-order, one-way pre-order, and two-way in-order threading of the tree
- In each case, draw the tree and also give its memory representation

![](img/be6359df08208122bec6fad1103de211_355_2.png)

17. Balance the AVL trees given below.

![](img/be6359df08208122bec6fad1103de211_355_3.png)

18. Create an AVL tree using the following sequence of data: 16, 27, 9, 11, 36, 54, 81, 63, 72.

19. Draw all possible binary search trees of 7, 9, and 11.

## Programming Exercises

- 1. Write a program to insert and delete values from a binary search tree.
- 2. Write a program to count the number of nodes in a binary search tree.

## Multiple-choice Questions

- 1. In the worst case, a binary search tree will take how much time to search an element? (a) O(n) (b) O(log n) (c) O(n^2) (d) O(n log n)

- 2. How much time does an AVL tree take to perform search, insert, and delete operations in the average case as well as the worst case? (a) O(n) (b) O(log n) (c) O(n^2) (d) O(n log n)

- 3. When the left sub-tree of the tree is one level higher than that of the right sub-tree, then the balance factor is (a) 0 (b) 1 (c) -1 (d) 2

- 4. Which rotation is done when the new node is inserted in the right sub-tree of the right sub-tree of the critical node? (a) LL (b) LR (c) RL (d) RR

- 5. When a node N is accessed it is splayed to make it the (a) Root node (b) Parent node (c) Child node (d) Sibling node

## True or False

- 1. In a binary search tree, all the nodes in the left sub-tree have a value less than that of the root node.
- 2. If we take two empty binary search trees and insert the same elements but in a different order, then the resultant trees will be the same.
- 3. When we insert a new node in a binary search tree, it will be added as an internal node.
- 4. Mirror image of a binary search tree is obtained by interchanging the left sub-tree with the right sub-tree at every node of the tree.
- 5. If the thread appears in the right field, then it will point to the in-order successor of the node.
- 6. If the node to be deleted is present in the left sub-tree of A, then B rotation is applied.
- 7. Height of an AVL tree is limited to \(\Omega(\log n)\).
- 8. Critical node is the nearest ancestor node on the path from the root to the inserted node whose balance factor is -1, 0, or 1.
- 9. RL rotation is done when the new node is inserted in the right sub-tree of the right sub-tree of the critical node.
- 10. In a red-black tree, some leaf nodes can be red.

## Fill in the Blanks

- 1. _____ is also called a fully threaded binary tree.
- 2. To find the node with the largest value, we will find the value of the rightmost node of the _____.
- 3. If the thread appears in the right field, then it will point to the _____ of the node.
- 4. The balance factor of a node is calculated by _____.
- 5. Balance factor -1 means _____.
- 6. Searching an AVL tree takes _____ time.
- 7. _____ rotation is done when the new node is inserted in the left sub-tree of the left sub-tree of the critical node.
- 8. In a red-black tree, the colour of the root node is _____ and the colour of leaf node is _____.
- 9. The zig rotation is done when _____.
- 10. In splay trees, rotation is analogous to _____ operation.

## CHAPTER 11
## Multi-way Search Trees

> **LEARNING OBJECTIVE**
> In this chapter we will study about multi-way search trees which are quite different from other binary search trees. Though the concept is similar to normal binary search trees, but M-way search trees can store more than one key values in a single node. The chapter starts with a general description of M-way search trees, and then discusses in detail M-way search trees such as B trees, B+ trees, and 2-3 trees.

### 11.1 INTRODUCTION

We have discussed that every node in a binary search tree contains one value and two pointers, left and right, which point to the node's left and right sub-trees, respectively. The structure of a binary search tree node is shown in Fig. 11.1.
The same concept is used in an M-way search tree which has M – 1 values per node and M sub-trees. In such a tree, M is called the degree of the tree. Note that in a binary search tree M = 2, so it has one value and two sub-trees. In other words, every internal node of an M-way search tree consists of pointers to M sub-trees and contains M – 1 keys, where M ≥ 2.

| Pointer to left sub-tree | Value or Key of the node | Pointer to right sub-tree |
|---|---|---|

**Figure 11.1** Structure of a binary search tree node

The structure of an M-way search tree node is shown in Fig. 11.2.

| P0 | K0 | P1 | K1 | P2 | K2 | ...... | Pn-1 | Kn-1 | Pn |
|---|---|---|---|---|---|---|---|---|---|

**Figure 11.2** Structure of an M-way search tree node

In the structure shown, P0, P1, P2, ..., Pn are pointers to the node's sub-trees and K0, K1, K2, ..., Kn-1 are the key values of the node. All the key values are stored in ascending order. That is, Ki < Ki+1, for 0 ≤ i ≤ n-2.

![](img/be6359df08208122bec6fad1103de211_358_0.png)

Figure 11.3 M-way search tree of order 3

In an M-way search tree, it is not compulsory that every node has exactly m-1 values and m sub-trees. Rather, the node can have anywhere from 1 to m-1 values, and the number of sub-trees can vary from 0 (for a leaf node) to 1 + i, where i is the number of key values in the node. m is thus a fixed upper limit that defines how many key values can be stored in the node.

Consider the M-way search tree shown in Fig. 11.3. Here m = 3. So a node can store a maximum of two key values and can contain pointers to three sub-trees.

In our example, we have taken a very small value of m so that the concept becomes easier for the reader, but in practice, m is usually very large. Using a 3-way search tree, let us lay down some of the basic properties of an M-way search tree.

- Note that the key values in the sub-tree pointed by p_i are less than the key value k_i. Similarly, all the key values in the sub-tree pointed by p_i are less than k_i, so on and so forth. Thus, the generalized rule is that all the key values in the sub-tree pointed by p_i are less than k_i, where 0 <= i <= n-1.
- Note that the key values in the sub-tree pointed by p_i are greater than the key value k_i. Similarly, all the key values in the sub-tree pointed by p_i are greater than k_i, so on and so forth. Thus, the generalized rule is that all the key values in the sub-tree pointed by p_i are greater than k_i, where 0 <= i <= n-1.

In an M-way search tree, every sub-tree is also an M-way search tree and follows the same rules.

### 11.2 B TREES

A B tree is a specialized M-way tree developed by Rudolf Bayer and Ed McCreight in 1970 that is widely used for disk access. A B tree of order m can have a maximum of m-1 keys and m pointers to its sub-trees. A B tree may contain a large number of key values and pointers to sub-trees. Storing a large number of keys in a single node keeps the height of the tree relatively small.

A B tree is designed to store sorted data and allows search, insertion, and deletion operations to be performed in logarithmic amortized time. A B tree of order m (the maximum number of children that each node can have) is a tree with all the properties of an M-way search tree. In addition it has the following properties:

- 1. Every node in the B tree has at most (maximum) m children.
- 2. Every node in the B tree except the root node and leaf nodes has at least (minimum) m/2 children. This condition helps to keep the tree bushy so that the path from the root node to the leaf is very short, even in a tree that stores a lot of data.
- 3. The root node has at least two children if it is not a terminal (leaf) node.
- 4. All leaf nodes are at the same level.

An internal node in the B tree can have n number of children, where 0 <= n <= m. It is not necessary that every node has the same number of children, but the only restriction is that the node should have at least m/2 children. As B tree of order 4 is given in Fig. 11.4.

![](img/be6359df08208122bec6fad1103de211_358_1.png)

Figure 11.4 B tree of order 4
