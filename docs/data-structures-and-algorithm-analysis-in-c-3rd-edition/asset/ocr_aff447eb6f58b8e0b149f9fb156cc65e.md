![](bbox=[0.15, 0.07, 0.85, 0.42])

(a)

| Position | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| Parent | - | 0 | 0 | 1 | 1 | 2 | 2 | 3 | 3 | 4 | 4 | 5 |
| Left Child | 1 | 3 | 5 | 7 | 9 | 11 | - | - | - | - | - | - |
| Right Child | 2 | 4 | 6 | 8 | 10 | - | - | - | - | - | - | - |
| Left Sibling | - | - | 1 | - | 3 | - | 5 | - | 7 | - | 9 | - |
| Right Sibling | - | 2 | - | 4 | - | 6 | - | 8 | - | 10 | - | - |

(b)

# Figure 5.12 A complete binary tree and its array implementation. (a) The complete binary tree with twelve nodes. Each node has been labeled with its position in the tree. (b) The positions for the relatives of each node. A dash indicates that the relative does not exist.

result from storing the records in sorted order. On the other hand, if we use a sorted array-based list to implement the dictionary, then binary search can be used to find a record in only Θ(log n) time. However, insertion will now require Θ(n) time on average because, once the proper location for the new record in the sorted list has been found, many records might be shifted to make room for the new record.

Is there some way to organize a collection of records so that inserting records and searching for records can both be done quickly? This section presents the binary search tree (BST), which allows an improved solution to this problem.

A BST is a binary tree that conforms to the following condition, known as the Binary Search Tree Property: All nodes stored in the left subtree of a node whose key value is K have key values less than K. All nodes stored in the right subtree of a node whose key value is K have key values greater than or equal to K. Figure 5.13 shows two BSTs for a collection of values. One consequence of the Binary Search Tree Property is that if the BST nodes are printed using an inorder traversal (see Section 5.2), the resulting enumeration will be in sorted order from lowest to highest.

Figure 5.14 shows a class declaration for the BST that implements the dictionary ADT. The public member functions include those required by the dictionary