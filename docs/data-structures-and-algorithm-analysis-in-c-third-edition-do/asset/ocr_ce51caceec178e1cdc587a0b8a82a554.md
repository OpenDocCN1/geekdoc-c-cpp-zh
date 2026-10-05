214

Chap. 6 Non-Binary Trees

![](bbox=[0.209, 0.185, 0.792, 0.403])

**Figure 6.9** The "list of children" implementation for general trees. The columns to the left of the node array labels the array indices. The column labeled "Val" stores node values. The column labeled "Par" stores indices (or pointers) to the parents. The last column stores pointers to the linked list of children for each internal node. Each element of the linked list stores a pointer to one of the node's children (shown as the array index of the target node).

children may have change. In some applications, once a node is created the number of children never changes. In such cases, a fixed amount of space can be allocated for the node where it is created, based on the number of children for the node. Matters become more complicated if children can be added to or deleted from a node, requiring that the node's space allocation be adjusted accordingly.

# 6.3.1 List of Children

Our first attempt to create a general tree implementation is called the "list of children" implementation for general trees. It simply stores with each internal node a linked list of children. This is illustrated by Figure 6.9.

The "list of children" implementation stores the tree nodes in an array. Each node contains a value, a pointer (or index) to its parent, and a pointer to a linked list of node's children, stored in order from left to right. Each linked list element contains a pointer to one. Thus, the leftmost child of a node can be found directly because it is the first element in the linked list. However, to find the right sibling for a node is more difficult. Consider the case of a node $M$ and its parent $P$. To find $M$'s right sibling, we must move down the list of $P$ until the linked list element storing the pointer to $M$ has been found. Going one step further us to the linked list element that stores a pointer to $M$'s right sibling. Thus, in the worst case, to find $M$'s right sibling requires that all children of $M$'s parent be searched.