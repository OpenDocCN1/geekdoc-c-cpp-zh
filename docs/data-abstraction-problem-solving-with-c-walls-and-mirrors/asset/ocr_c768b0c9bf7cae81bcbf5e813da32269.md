# A Link-Based Implementation of the ADT Binary Search Tree 481

**Question 8** Given the binary search tree in Figure 15–18 of Chapter 15, trace the removal algorithms when removing any of the following values from the tree. Begin with the original tree each time.

+   * a. 70
* b. 20
* c. 60

Retrieving an entry. By refining the search algorithm, you can implement the operation getEntry. Recall from Section 15.3.2 of Chapter 15 that the search algorithm is

```
// Searches a binary tree for a given target value.
search(binTree: BinarySearchTree, target: ItemType)

if (binTree is empty)
    // The desired item is not found
else if (target == data item in the root of binTree)
    // The desired item is found
else if (target < data item in the root of binTree)
    search(Left subtree of binTree, target)
else
    search(Right subtree of binTree, target)
```

We can refine this algorithm as follows:

```
// Locates the node in the binary tree to which subTree points that
// the value target. Returns a pointer to the located node or nullptr if such
// node is not found.
findNode(subTree: BinaryNodePointer, target: ItemType): BinaryNodePointer
if (subTree == nullptr) // Not found
    return nullptr;
else if (subTree->getItem() == target) // Found
    return subTree;
else if (subTree->getItem() < target)
    // Search left subtree
    return findNode(subTree->getChildPtr(), target)
else
    // Search right subtree
    return findNode(subTree->getRightChildPtr(), target);
```

The operation getEntry must return the item with the desired value if it exists; otherwise it must throw an exception NotFoundException. The method, therefore, calls findNode and checks its return value. If the desired target is found, getEntry returns it. If findNode returns nullptr, getEntry throws an exception.

> Note: The traversals of a binary tree are the same as the traversals of a binary tree. Recall from Chapter 15 that an inorder traversal of a binary search tree will visit the tree’s nodes in sorted order according to their entries.

# 16.3.2 The Class BinarySearchTree

A C++ link-based definition of the BinarySearchTree is given in Listing 16-4. Notice the protected methods that implement the recursive algorithms. These methods are not public, because