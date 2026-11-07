```
```cpp
template <class elemType>
void preorder(nodeType<elemType> *p) const
{
    if (p != NULL)
    {
        cout << p->info << " ";
        preorder(p->lLink);
        preorder(p->rLink);
    }
}
```
```

```
```cpp
template <class elemType>
void postorder(nodeType<elemType> *p) const
{
    if (p != NULL)
    {
        postorder(p->lLink);
        postorder(p->rLink);
        cout << p->info << " ";
    }
}
```
```

> > **NOTE**  
> > This section described the binary tree traversal algorithms inorder, preorder, and postorder. If you want to make a copy of a binary tree while preserving the structure of the binary tree, you can use preorder traversal. To delete all of the nodes of a binary tree, you can use the postorder traversal. Later in this chapter, we discuss binary search trees. The inorder traversal of a binary search tree visits the nodes in sorted order.

> > **NOTE**  
> > In addition to the inorder, preorder, and postorder traversals, a binary tree can also be traversed **level-by-level**, also known as **breadth-first traversal**. In Chapter 21, we discuss graphs. A binary tree is also a graph. We discuss how to implement breadth-first traversal algorithms for graphs. You can modify that algorithm to do a breadth-first traversal of binary trees.

# Implementing Binary Trees

The preceding sections described various operations that can be performed on a binary tree, as well as the functions to implement these operations. This section describes binary trees as an abstract data type (ADT). Before designing the class to implement a binary tree as an ADT, let us list the various operations that are typically performed on a binary tree.

+   1. Determine whether the binary tree is empty.
+   2. Search the binary tree for a particular item.
+   3. Insert an item in the binary tree.
+   4. Delete an item from the binary tree.