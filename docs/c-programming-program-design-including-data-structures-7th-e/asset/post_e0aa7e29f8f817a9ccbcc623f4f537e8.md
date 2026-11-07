
```cpp
template <class elemType>
void copyTree(nodeType<elemType>*& copiedTreeRoot,
              nodeType<elemType>* otherTreeRoot)
{
    if (otherTreeRoot == nullptr)
        copiedTreeRoot = nullptr;
    else
    {
        copiedTreeRoot = new nodeType<elemType>;
        copiedTreeRoot->info = otherTreeRoot->info;
        copyTree(copiedTreeRoot->lLink, otherTreeRoot->lLink);
        copyTree(copiedTreeRoot->rLink, otherTreeRoot->rLink);
    }
} //end copyTree
```

We will use the function copyTree when we overload the assignment operator and implement the copy constructor.

## Binary Tree Traversal

The item insertion, deletion, and lookup operations require that the binary tree be traversed. Thus, the most common operation performed on a binary tree is to traverse the binary tree, or visit each node of the binary tree. As you can see from the diagram of a binary tree, the traversal must start at the root node because there is a pointer to the root node of the binary tree. For each node, we have two choices:

- Visit the node first.
- Visit the subtrees first.

These choices lead to three commonly used traversals of a binary tree:

- Inorder traversal
- Preorder traversal
- Postorder traversal

### INORDER TRAVERSAL

In an inorder traversal, the binary tree is traversed as follows:

- 1. Traverse the left subtree.
- 2. Visit the node.
- 3. Traverse the right subtree.

### PREORDER TRAVERSAL

In a preorder traversal, the binary tree is traversed as follows:

- 1. Visit the node.
- 2. Traverse the left subtree.
- 3. Traverse the right subtree.

### POSTORDER TRAVERSAL

In a postorder traversal, the binary tree is traversed as follows:

- 1. Traverse the left subtree.
- 2. Traverse the right subtree.
- 3. Visit the node.

Clearly, each of these traversal algorithms is recursive.

The listing of the nodes produced by the inorder traversal of a binary tree is called the **inorder sequence**. The listing of the nodes produced by the preorder traversal is called the **preorder sequence**, and the listing of the nodes produced by the postorder traversal is called the **postorder sequence**.

### EXAMPLE 19-4

Consider the binary tree in Figure 19–6. Let *T* be a binary tree. Suppose that *T* is nonempty and the root node of *T* is A. Then inorder(*T*) or inorder(A) denotes the listing of nodes of *T* in the inorder sequence and root(*T*) denotes the root node of *T*. For simplicity, we assume that visiting a node means to output the data stored in the node. In the section “Binary Tree Traversal and Functions as Parameters,” we will explain how to modify the binary tree traversal algorithms so that by using a function, the user can specify the action to be performed on a node when the node is visited.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1405_0.png)

**FIGURE 19-6** Binary tree for an inorder traversal

Let *T* denote the binary tree in Figure 19–6. Then, root(*T*) = A. Therefore, we start the traversal at A. That is, determine inorder(A). Because the binary tree is nonempty, to determine inorder(A), we do the following:

- 1. Determine inorder($L_A$), where $L_A$ is the left subtree of $A$. Note that $L_A = \{B, D, F\}$.
- 2. Visit $A$.
- 3. Determine inorder($R_A$), where $R_A$ is the right subtree of $A$. Note that $R_A = \{C, E, G\}$.

Now we cannot do Step 2 until we have finished Step 1.

- 1. **inorder($L_A$):** Now $L_A$ is a binary tree, and root($L_A$) = $B$. So to determine inorder($L_A$), we do the following:
  - 1.1. Determine inorder($L_B$), where $L_B = \{D, F\}$.
  - 1.2. Visit $B$.
  - 1.3. Determine inorder($R_B$), where $R_B = \emptyset$.

As before, first we complete Step 1.1 before proceeding to Step 1.2.

- 1.1. **inorder($L_B$):** Now $L_B$ is a binary tree, and root($L_B$) = $D$. So to determine inorder($L_B$), we do the following:
  - 1.1.1. Determine inorder($L_D$), where $L_D = \emptyset$.
  - 1.1.2. Visit $D$.
  - 1.1.3. Determine inorder($R_D$), where $R_D = \{F\}$.

Because $L_D = \emptyset$, Step 1.1.1 is completed, so we proceed to Step 1.1.2, which outputs $D$. Because Step 1.1.2 is also completed, we proceed to Step 1.1.3.

- 1.1.3. Determine inorder($R_D$), where $R_D = \{F\}$. Now $R_D$ is a binary tree, and root($R_D$) = $F$. So to determine inorder($R_D$), we do the following:
  - 1.1.3.1. Determine inorder($L_F$), where $L_F = \emptyset$.
  - 1.1.3.2. Visit $F$.
  - 1.1.3.3. Determine inorder($R_F$), where $R_F = \emptyset$.

Because $L_F = \emptyset$, Step 1.1.3.1 is completed, so we proceed to Step 1.1.3.2, which outputs $F$. Because Step 1.1.3.2 is also completed, we proceed to Step 1.1.3.3. Because $R_F = \emptyset$, this step is also completed. Thus, Step 1.1.3 is completed, which in turn completes Step 1.1.1.

Next, we proceed to Step 1.2, which outputs $B$. After completing Step 1.2, we proceed to Step 1.3. Now Step 1.3 requires us to determine inorder($R_B$). However, $R_B = \emptyset$, so Step 1.3 is completed, which in turn completes Step 1.

- 2. Next, we proceed to Step 2, which outputs $A$. At this point we have completed inorder($L_A$) and visited $A$.

- 3. Now, we proceed to Step 3, that is, determine inorder($R_A$), where $R_A = \{C, E, G\}$. Now $R_A$ is a nonempty binary tree and root($R_A$) = $C$, so to determine inorder($R_A$), we need to do the following:
  - 3.1. Determine inorder($L_C$), where $L_C = \emptyset$.
  - 3.2. Visit $C$.

Now $L_C = \emptyset$, so Step 3.1 is completed. Next, in Step 3.2, we output $C$, which completes this step. After completing Step 3.2, we proceed to Step 3.3.

- 3.3. Determine inorder($R_C$), where $R_C = \{E, G\}$. Now $R_C$ is a nonempty binary tree with root($R_C$) = $E$. Thus, inorder($R_C$) requires us to complete the following steps:
  - 3.3.1. Determine inorder($L_E$), where $L_E = \{G\}$.
  - 3.3.2. Visit $E$.
  - 3.3.3. Determine inorder($R_E$), where $R_E = \emptyset$.

To complete Step 3.3.1, we must determine inorder($L_E$), where $L_E = \{G\}$. Now $L_E$ is a binary tree with root($L_E$) = $G$. Therefore, to determine inorder($L_E$), we must complete the following steps:

    - 3.3.1.1. Determine inorder($L_G$), where $L_G = \emptyset$.
    - 3.3.1.2. Visit $G$.
    - 3.3.1.3. Determine inorder($R_G$), where $R_G = \emptyset$.

Now $L_G = \emptyset$, so Step 3.3.1.1 is completed. Next Step 3.3.1.2 outputs $G$, which completes this step. Because $R_G = \emptyset$, Step 3.3.1.3 is also completed. This in turn completes Step 3.3.1.

After completing Step 3.3.1, to complete Step 3.3.2, we output $E$. Next because $R_E = \emptyset$, Step 3.3.3 is also completed, which in turn completes Step 3.3.

Because Step 3.3 is completed, Step 3 is also completed, that is we have determined inorder($R_A$). It now follows that:

inorder($A$) = $DFBACGE$

In a similar manner, the preorder and postorder traversals output the nodes in the following order:

preorder($A$) = $ABDFCEG$

postorder($A$) = $FDBGECA$

As you can see from the walk-through of the inorder traversal, after visiting the left subtree of a node, we must come back to the node itself. The links are only in one direction; that is, the parent node points to the left and right children, but there is no pointer from each child to the parent. Therefore, before going to a child, we must somehow save a pointer to the parent node. A convenient way to do this is to write a recursive inorder function because in a recursive call, after completing a particular call, the control goes back to the caller. (Later, we will discuss how to write nonrecursive traversal functions.) The recursive definition of the function to implement the inorder traversal algorithms is:

```cpp
template <class elemType>
void inorder(nodeType<elemType> *p) const
{
    if (p != nullptr)
    {
        inorder(p->lLink);
        cout << p->info << " ";
        inorder(p->rLink);
    }
}
```

To do the inorder traversal of a binary tree, the root node of the binary tree is passed as a parameter to the function inorder. For example, if root points to the root node of the binary tree, a call to the function inorder is:

```cpp
inorder(root);
```

Similarly, we can write the functions to implement the preorder and postorder traversals. The definitions of these functions are given next:

```cpp
template <class elemType>
void preorder(nodeType<elemType> *p) const
{
    if (p != nullptr)
    {
        cout << p->info << " ";
        preorder(p->lLink);
        preorder(p->rLink);
    }
}
```

```cpp
template <class elemType>
void postorder(nodeType<elemType> *p) const
{
    if (p != nullptr)
    {
        postorder(p->lLink);
        postorder(p->rLink);
        cout << p->info << " ";
    }
}
```

> **NOTE**  
> This section described the binary tree traversal algorithms inorder, preorder, and postorder. If you want to make a copy of a binary tree while preserving the structure of the binary tree, you can use preorder traversal. To delete all of the nodes of a binary tree, you can use the postorder traversal. Later in this chapter, we will discuss binary search trees. The inorder traversal of a binary search tree visits the nodes in sorted order.
