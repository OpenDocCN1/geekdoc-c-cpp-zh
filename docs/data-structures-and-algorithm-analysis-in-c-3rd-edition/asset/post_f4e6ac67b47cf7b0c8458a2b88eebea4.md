
## 6.5 Sequential Tree Implementations

Next we consider a fundamentally different approach to implementing trees. The goal is to store a series of node values with the minimum information needed to reconstruct the tree structure. This approach, known as a sequential tree implementation, has the advantage of saving space because no pointers are stored. It has

Full and complete K-ary trees are analogous to full and complete binary trees, respectively. Figure 6.16 shows full and complete K-ary trees for K = 3. In practice, most applications of K-ary trees limit them to be either full or complete.

Many of the properties of binary trees extend to K-ary trees. Equivalent theorems to those in Section 5.1.1 regarding the number of NULL pointers in a K-ary tree and the relationship between the number of leaves and the number of internal nodes in a K-ary tree can be derived. We can also store a complete K-ary tree in an array, using simple formulas to compute a node’s relations in a manner similar to that used in Section 5.3.3.

**Figure 6.15** A general tree converted to the dynamic “left-child/right-sibling” representation. Compared to the representation of Figure 6.13, this representation requires less space.

**Figure 6.16** Full and complete 3-ary trees. (a) This tree is full (but not complete). (b) This tree is complete (but not full).

![](img/7ea3c39173f146f675b63b146d1535f3_237_0.png)

![](img/7ea3c39173f146f675b63b146d1535f3_237_1.png)

![](img/7ea3c39173f146f675b63b146d1535f3_237_2.png)

![](img/7ea3c39173f146f675b63b146d1535f3_237_3.png)

![](img/7ea3c39173f146f675b63b146d1535f3_239_0.png)

**Figure 6.17** Sample binary tree for sequential tree implementation examples.

To illustrate the difficulty involved in using the sequential tree representation for processing, consider searching for the right child of the root node. We must first move sequentially through the node list of the left subtree. Only at this point do we reach the value of the root’s right child. Clearly the sequential representation is space efficient, but not time efficient for descending through the tree along some arbitrary path.

Assume that each node value takes a constant amount of space. An example would be if the node value is a positive integer and NULL is indicated by the value zero. From the Full Binary Tree Theorem of Section 5.1.1, we know that the size of the node list will be about twice the number of nodes (i.e., the overhead fraction is 1/2). The extra space is required by the NULL pointers. We should be able to store the node list more compactly. However, any sequential implementation must recognize when a leaf node has been reached, that is, a leaf node indicates the end of a subtree. One way to do this is to explicitly list with each node whether it is an internal node or a leaf. If a node X is an internal node, then we know that its two children (which may be subtrees) immediately follow X in the node list. If X is a leaf node, then the next node in the list is the right child of some ancestor of X, not the right child of X. In particular, the next node will be the child of X’s most recent ancestor that has not yet seen its right child. However, this assumes that each internal node does in fact have two children, in other words, that the tree is full. Empty children must be indicated in the node list explicitly. Assume that internal nodes are marked with a prime (′) and that leaf nodes show no mark. Empty children of internal nodes are indicated by ‘/’, but the (empty) children of leaf nodes are not represented at all. Note that a full binary tree stores no NULL values with this implementation, and so requires less overhead.

**Example 6.6** We can represent the tree of Figure 6.17 as follows:

`A′B′/DC′E′G/F′HI` (6.2)

Note that slashes are needed for the empty children because this is not a full binary tree.

Storing n extra bits can be a considerable savings over storing n NULL values. In Example 6.6, each node is shown with a mark if it is internal, or no mark if it is a leaf. This requires that each node value has space to store the mark bit. This might be true if, for example, the node value were stored as a 4-byte integer but the range of the values stored was small enough so that not all bits are used. An example would be if all node values must be positive. Then the high-order (sign) bit of the integer value could be used as the mark bit.

Another approach is to store a separate bit vector to represent the status of each node. In this case, each node of the tree corresponds to one bit in the bit vector. A value of ‘1’ could indicate an internal node, and ‘0’ could indicate a leaf node.

**Example 6.7** The bit vector for the tree of Figure 6.17 (including positions for the null children of nodes B and E) would be

```
11001100100
```

(6.3)

Storing general trees by means of a sequential implementation requires that more explicit structural information be included with the node list. Not only must the general tree implementation indicate whether a node is leaf or internal, it must also indicate how many children the node has. Alternatively, the implementation can indicate when a node’s child list has come to an end. The next example dispenses with marks for internal or leaf nodes. Instead it includes a special mark (we will use the “)” symbol) to indicate the end of a child list. All leaf nodes are followed by a “)” symbol because they have no children. A leaf node that is also the last child for its parent would indicate this by two or more successive “)” symbols.

**Example 6.8** For the general tree of Figure 6.3, we get the sequential representation

```
RAC)D)E))BF)))
```

(6.4)

Note that F is followed by three “)” marks, because it is a leaf, the last node of B’s rightmost subtree, and the last node of R’s rightmost subtree.

Note that this representation for serializing general trees cannot be used for binary trees. This is because a binary tree is not merely a restricted form of general tree with at most two children. Every binary tree node has a left and a right child, though either or both might be empty. For example, the representation of Example 6.8 cannot let us distinguish whether node D in Figure 6.17 is the left or right child of node B.

## 6.6 Further Reading

The expression log* n cited in Section 6.2 is closely related to the inverse of Ackermann’s function. For more information about Ackermann’s function and the cost of path compression for UNION/FIND, see Robert E. Tarjan’s paper “On the efficiency of a good but not linear set merging algorithm” [Tar75]. The article “Data Structures and Algorithms for Disjoint Set Union Problems” by Galil and Italiano [GI91] covers many aspects of the equivalence class problem.

Foundations of Multidimensional and Metric Data Structures by Hanan Samet [Sam06] treats various implementations of tree structures in detail within the context of K-ary trees. Samet covers sequential implementations as well as the linked and array implementations such as those described in this chapter and Chapter 5. While these books are ostensibly concerned with spatial data structures, many of the concepts treated are relevant to anyone who must implement tree structures.

## 6.7 Exercises

- 6.1 Write an algorithm to determine if two general trees are identical. Make the algorithm as efficient as you can. Analyze your algorithm’s running time.

- 6.2 Write an algorithm to determine if two binary trees are identical when the ordering of the subtrees for a node is ignored. For example, if a tree has root node with value R, left child with value A and right child with value B, this would be considered identical to another tree with root node value R, left child value B, and right child value A. Make the algorithm as efficient as you can. Analyze your algorithm’s running time. How much harder would it be to make this algorithm work on a general tree?

- 6.3 Write a postorder traversal function for general trees, similar to the preorder traversal function named preorder given in Section 6.1.2.

- 6.4 Write a function that takes as input a general tree and returns the number of nodes in that tree. Write your function to use the GenTree and GTNode ADTs of Figure 6.2.

- 6.5 Describe how to implement the weighted union rule efficiently. In particular, describe what information must be stored with each node and how this information is updated when two trees are merged. Modify the implementation of Figure 6.4 to support the weighted union rule.

- 6.6 A potential alternative to the weighted union rule for combining two trees is the height union rule. The height union rule requires that the root of the tree with greater height become the root of the union. Explain why the height union rule can lead to worse average time behavior than the weighted union rule.

- 6.7 Using the weighted union rule and path compression, show the array for the parent pointer implementation that results from the following series of
