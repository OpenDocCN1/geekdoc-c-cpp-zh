root to a leaf is A–B–D–G–I. The number of nodes on this path is 5. Hence, the height of the binary tree is 5.

Suppose that a pointer, p, to the root node of a binary tree is given. We next describe a C++ function, height, to find the height of the binary tree. The pointer to the root node is passed as a parameter to the function height.

If the binary tree is empty, then the height is 0. Suppose that the binary tree is nonempty. To find the height of the binary tree, we first find the height of the left subtree and the height of the right subtree. We then take the maximum of these two heights and add 1 to find the height of the binary tree. To find the height of the left (right) subtree, we apply the same procedure because the left (right) subtree is a binary tree. Therefore, the general algorithm to find the height of a binary tree is as follows. Suppose height(p) denotes the height of the binary tree with root p.

```
if (p is nullptr)
    height(p) = 0
else
    height(p) = 1 + max(height(p->lLink), height(p->rLink))
```

Clearly, this is a recursive algorithm. The following function implements this algorithm:

```
template <class elemType>
int height(nodeType<elemType> *p)
{
    if (p == nullptr)
        return 0;
    else
        return 1 + max(height(p->lLink), height(p->rLink));
}
```

The definition of the function height uses the function max to determine the larger of two integers. The function max can be easily implemented as follows.

Similarly, we can implement algorithms to find the number of nodes and number of leaves in a binary tree.

# Copy Tree

One useful operation on binary trees is to make an identical copy of a binary tree. A binary tree is a dynamic data structure; that is, memory for the nodes of a binary tree is allocated and deallocated during program execution. Therefore, if we use just the value of the pointer of the root node to make a copy of a binary tree, we get a shallow copy of the data. To make an identical copy of a binary tree, we need to create as many nodes as there are in the binary tree to be copied. Moreover, in the copied tree, these nodes must appear in the same order as they are in the original binary tree.

Given a pointer to the root node of a binary tree, we next describe a function that makes a copy of a given binary tree. This function is also quite useful in implementing the copy constructor and overloading the assignment operator, as described later in this chapter (see “Implementing Binary Trees”).