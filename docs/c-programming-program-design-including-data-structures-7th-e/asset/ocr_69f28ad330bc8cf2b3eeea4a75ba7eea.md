> NOTE
> 
> In addition to the inorder, preorder, and postorder traversals, a binary tree can also be traversed **level-by-level**, also known as **breadth-first traversal**. In Chapter 20, we discuss graphs. A binary tree is also a graph. We discuss how to implement breadth-first traversal algorithms for graphs. You can modify that algorithm to do a breadth-first traversal of binary trees.

# Implementing Binary Trees

The preceding sections described various operations that can be performed on a binary tree, as well as the functions to implement these operations. This section describes binary trees as an abstract data type (ADT). Before designing the class to implement a binary tree as an ADT, let us list the various operations that are typically performed on a binary tree.

+   1. Determine whether the binary tree is empty.
+   2. Search the binary tree for a particular item.
+   3. Insert an item in the binary tree.
+   4. Delete an item from the binary tree.
+   5. Find the height of the binary tree.
+   6. Find the number of nodes in the binary tree.
+   7. Find the number of leaves in the binary tree.
+   8. Traverse the binary tree.
+   9. Copy the binary tree.

The item search, insertion, and deletion operations all require the binary tree to be traversed. However, because the nodes of a binary tree are in no particular order, these algorithms are not very efficient on arbitrary binary trees. That is, no criteria exist to guide the search on these binary trees, as we will see in the next section. Therefore, we will discuss these algorithms when we discuss special binary trees.

The following class defines binary trees as an ADT. The definition of the node is the same as before. However, for the sake of completeness and easy reference, we give the definition of the node followed by the definition of the class:

```
```cpp
//Definition of the Node
template <class elemType>
struct nodeType
{
    elemType info;
    nodeType<elemType> *lLink;
    nodeType<elemType> *rLink;
};
```
```