# 16.5 Tree Sort

one more than the other. In this case, you can arbitrarily choose to put the extra node in the left subtree. The following algorithm makes these compensations:

Building a minimum-height binary search tree

```
// Builds a minimum-height binary search tree from n sorted values in a file.
// Returns a pointer to the tree's root.
readTree(n: integer): BinaryNodePointer
if (n > 0) {
    // Get the root
    treePtr = pointer to new node with nullptr as its children pointer
    rootItem = next item from file
    treePtr->setItem(rootItem)
    // Construct the left subtree
    leftPtr = readTree(treePtr->getLeftChildPtr(), n / 2)
    treePtr->setLeftChild(leftPtr)
    // Construct the right subtree
    rightPtr = readTree(treePtr->getLeftChildPtr(), (n - 1) / 2)
    treePtr->setRightChild(rightPtr)
    return treePtr
} else
    return nullptr
```

You should trace this algorithm and convince yourself that it is correct for both even and odd values of n.

To summarize, you can easily restore a tree as a balanced binary search tree if the data is sorted—if it has been produced from the inorder traversal—and you know the n of nodes in the tree. You need so that you can determine the middle item and, in turn, the number of nodes in the left and right subtrees of the tree's root. Knowing this is a simple method of counting nodes as you traverse the tree and saving the value in a file that the restore operation can read.

Note readTree would be an appropriate protected method of BinarySearchTree, if you also had a public method to call it.

> Note: You can use the readTree algorithm to restore an out-of-balance binary search tree. Exercise 18 asks you to try it using an array instead of a file.

+   Question 9 Consider the pseudocode operation readTree.
a. What binary search tree results when you execute readTree with a file of the six integers, 2, 4, 6, 8, 10, 12?
b. Is the restoring tree's height a minimum? Is it complete?

You can use the ADT binary search tree to sort an array efficiently. To simplify the discussion, we will sort an array of integers in ascending order, as we did with the sorting algorithms in Chapter 11.