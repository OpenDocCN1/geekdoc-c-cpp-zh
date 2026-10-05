
Note slashes are needed for the empty children because this is not a full binary tree.

Storing n bits can be a considerable savings over storing n NULL values. In Example 6.6, each node is shown with a mark if it is internal, or no mark if it is a leaf. This requires that each node has space to store the mark bit. This might be true if, the node value was stored as a 4-byte integer but the range of values was small enough that not all bits are used. An example would be if all node values be positive. Then the high-order (sign) bit of the integer value could be used as the mark bit.

Another approach is to store a separate bit vector to represent the status of each node. In this case, each node corresponds to one bit in the bit vector. A value of '1' could indicate an internal node, and '0' could indicate a leaf node.

## Example 6.7
The bit vector for the tree if Figure 6.17 (including positions for the children of nodes B and E) would

```
1100110001 (6.3)
```

Storing general trees by means of sequential implementation requires that more explicit structural information be included with the node list. Not only must the general tree implementation include whether a node is leaf or internal, it must also indicate how many children the node has. Alternatively, the implementation can indicate when a node's child list has come to an end. The next example dispenses with marks for internal or leaf nodes. Instead it includes a special mark (we use "$" symbol) to indicate the end of a child list. All leaf nodes are followed by a ")" symbol because they have children. A leaf node that is also the last for its parent would indicate this by using two or more successive "$" symbols.

## Example 6.8
The general tree of Figure 6.3, we get the sequential representation

```
RAC(D(E))BF)) (6.4)
```

Note that F is followed by three "$" marks, because it is a leaf, the last node of B's rightmost subtree, and the last node of R's rightmost subtree.

Note that this representation for serializing general trees cannot be used for binary trees. A binary tree is not a restricted form of general tree with at most two children. Every binary tree has a left and a right child, though either or both might be empty. For example, the representation of Example 6.8 cannot let us distinguish whether node D in Figure 6.17 is the left or right child of node B.

## Further Reading

The expression $\alpha^*(n)$ cited in Section 6.2 is closely related to the inverse of Ackermann’s function. For more information about Ackermann’s function and the cost of path compression for UNION/FIND, see Robert E. Tarjan’s paper “On the efficiency of a bold but not linear merging algorithm” [Tar75]. The article “Data Structures and Algorithms for Disjoint Set Problems” by Galil and Italiano [GI91] covers many aspects of the equivalence class problem.

Foundations of Multidimensional and Metric Data Structures by Hanan Samet [Sam06] treats various implementations of tree structures in detail within the text of $K$-ary trees. Samet covers sequential implementations as well as the linked and array implementations such as those described in this chapter and Chapter 5. While these books are ostensibly concerned with spatial data structures, many of the concepts are relevant to anyone who implement tree structures.

## Exercises

- 6.1 Write an algorithm to determine if two general trees are identical. Make the algorithm as efficient as you can. Analyze your algorithm’s running time.
- 6.2 Write an algorithm to determine if two binary trees are identical when the ordering of the subtrees for a node is ignored. For example, if a tree has node value R, left child with value A and right child with value B, would be considered identical to another tree with root value R, left child value B, and right child value A. Make the algorithm as efficient as you can. Analyze your algorithm’s running time. How harder would it be to make this algorithm work on a general tree?
- 6.3 Write a preorder traversal for general trees, similar to the preorder traversal named preorder in Section 6.1.2.
- 6.4 Write a function that takes as input the number of nodes in that tree. Write your function to use the GenTree and GTNode APIs of 6.2.
- 6.5 Describe how to implement the weighted union rule efficiently. In particular, describe what information must be stored with each node and how information is updated when two trees are merged. Modify the implementation of Figure 6.4 to support the weighted union rule.
- 6.6 A potential alternative to the weighted union rule for combining two trees is the height union rule. The height union rule requires that the root of the tree with greater height become the root of the union. Explain why the height union rule can lead to worse average time behavior than the weighted union rule.
- 6.7 Using the weighted union rule and path compression, show the array for the parent pointer implementation that results from the following series of equivalences on a set of objects indexed by the values 0 through 15. Initially, each element in the set should be in a separate equivalence class. When two trees to be merged are the same size, make the root with greater index value be the child of the root with lesser index value.

(0, 2) (1, 2) (3, 4) (3, 1) (3, 5) (9, 11) (12, 14) (3, 1)

- 6.8 Using the weighted union rule and path compression, show the array for the parent pointer implementation that results from the following series of equivalences on a set of objects indexed by the values 0 through 15. Initially, each element in the set should be in a separate equivalence class. When two trees to be merged are the same size, make the root with greater index value be the child of the root with lesser index value.

(0, 2) (1, 2) (3, 4) (3, 1) (3, 5) (9, 11) (12, 14) (3, 1)

- 6.9 Devise a series of equivalence statements for a collection of items that yields a tree of height 5 when the weighted union rule and path compression is used.
- 6.10 One alternative to path compression that gives similar gains is called halving. In halving, when the path is traversed from the node to the root, we make the grandparent of every other node on the path i. Your operation should work as you move up the tree, rather than require the two passes needed by path compression.
- 6.11 Analyze the function of the "list of children" implementation, the "left-child/right-sibling" implementation, and the two implementations of Section 5.3.3.
- 6.12 Using the general tree representation of 6.2, write a function that takes as input the root of a general tree and returns a binary tree.
- 6.13 Use mathematical induction to prove that the number of leaves in a non-empty K-ary tree is $(K-1)n+1$, where n is the number of internal nodes.
- 6.14 Derive the overhead fraction for a full K-ary tree with space requirements as follows:
    (a) All nodes store data, K child pointers, and a parent pointer. The data field requires four bytes and each pointer requires four bytes.
    (b) All nodes store data and K child pointers. The data field requires sixteen bytes and each pointer requires four bytes.
    (c) All nodes store data and a parent pointer, and internal nodes store K child pointers. The data field requires eight bytes and each pointer requires four bytes.
    (d) Only leaf nodes store data; only internal nodes store K child pointers. The data field requires four bytes and each pointer requires two bytes.
- 6.16 (a) Write out the sequential representation for Figure 6.18 using the coding illustrated by Example 6.5.
    (b) Write out the sequential representation for Figure 6.18 using the coding illustrated by Example 6.6.
- 6.17 Draw the binary tree representing the following sequential representation for binary trees illustrated by Example 6.5:
ABD//E//C/F//
- 6.18 Draw the binary tree representing the following sequential representation for binary trees illustrated by Example 6.6:
A'/B'/C'D'/G/E
Show the bit vector for leaf and internal nodes (as illustrated by Example 6.7) for this tree.
- 6.19 Draw the general tree represented by the following sequential representation for general trees illustrated by Example 6.8:
XPC(Q)RV)M))))
- 6.20 (a) Write a function to decode the sequential representation for binary trees illustrated by Example 6.5. The input should be a pointer to the sequential representation and the output should be the root of the resulting binary tree.
