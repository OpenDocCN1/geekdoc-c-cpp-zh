# CHAPTER 16 Tree Implementations

FIGURE 16-15 An initially empty binary search tree after the insertion of 60, 20, 10, 40, 30, 50, and 70

![](bbox=[0.487, 0.153, 0.673, 0.335])

Use a preorder traversal to save a binary search tree in a file; restore to its original shape by using add

If the program uses a binary search tree to represent the database, it must save the tree's data in a file so that it can later restore the tree. Two different algorithms for saving and restoring a binary search tree will be considered here. The first algorithm restores a binary search tree to its original shape. The second restores a binary search tree to a shape that is balanced.

Saving a binary search tree and restoring it to its original shape. The first algorithm restores a binary search tree to exactly the same shape it had before was saved. For example, consider the binary tree in Figure 16-15. If you use the preorder, you get the sequence 60, 20, 10, 40, 30, 50, 70. If you use the add method to insert values into a binary search tree that is initially empty, you will get the original tree.

A balanced binary search tree increases the efficiency of the ADT operations

Saving a binary search tree and restoring it to a balanced shape. After you save a binary search tree in a file, do you necessarily restore the restored tree to its original shape? Recall that you can use any set of data items to create several binary search trees with different shapes. Although the shape of a binary search tree has no effect whatsoever on the correctness of the ADT operations, it will affect the efficiency of those operations. Efficient operations are ensured if your binary tree is balanced.

The algorithm that restores a binary search tree to a balanced tree is surprisingly simple. To gain some insight into the solution, consider a full tree of minimum height—a condition stronger than balanced. If you save a tree in a file using an inorder traversal, the file will be in sorted order, as in Figure 16-16 illustrations.

A full tree with $2^h-1$ nodes for height $h$ has the exact match of the data items in its root. The left and right subtrees of the root are full trees of $2^{h-1}-1$ nodes (that is, half of $n-1$, where $n$ is odd or, equivalently, $n/2$). Thus, you can use the recursive algorithm to build a full binary search tree from $n$ nodes, provided you know or determine $n$ before.

Building a full binary search tree

```
// Builds a full binary search tree from n sorted values in a file.
fullTree(int n): BinaryNodePointer
if (n == 0) {
    // Get the root
    treePtr = new node with nullptr as its child pointers
    rootItem = next item from file
    treePtr->setItem(rootItem)
}
```