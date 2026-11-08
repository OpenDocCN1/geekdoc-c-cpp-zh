
From the definition of the node, it is clear that for each node:

- 1. The data is stored in `info`.
- 2. A pointer to the left child is stored in `lLink`.
- 3. A pointer to the right child is stored in `rLink`.

Furthermore, a pointer to the root node of the binary tree is stored outside of the binary tree in a pointer variable, usually called the `root`, of type `nodeType`. Thus, in general, a binary tree looks like the diagram in Figure 19–4.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1352_0.png)

For simplicity, we will continue to draw binary trees as before. That is, we will use circles to represent nodes and left and right arrows to represent links. As before, three lines at the end of an arrow mean that the subtree is empty.

Before we leave this section, let us define a few terms.

A node in a binary tree is called a **leaf** if it has no left and right children. Let U and V be two nodes in the binary tree T. U is called the **parent** of V if there is a branch from U to V. A **path** from a node X to a node Y in a binary tree is a sequence of nodes X₀, X₁, …, Xₙ such that:

- i. X = X₀, Xₙ = Y
- ii. Xᵢ₋₁ is the parent of Xᵢ for all i = 1, 2, …, n. That is, there is a branch from X₀ to X₁, X₁ to X₂, …, Xᵢ₋₁ to Xᵢ, …, Xₙ₋₁ to Xₙ.

If X₀, X₁, …, Xₙ is a path from node X to node Y, sometimes we denote it by X = X₀ → X₁ → … → Xₙ₋₁ → Xₙ = Y. Or simply X → X₁ → … → Xₙ₋₁ → Xₙ = Y.

Because the branches only go from a parent to its children, from the previous discussion it is clear that in a binary tree, there is a unique path from the root to every node in the binary tree.

**Definition:** The length of a path is the number of branches on that path.

**Definition:** The level of a node in a binary tree is the number of branches on the path from the root to the node.

Clearly, the level of the root node of a binary tree is 0, and the level of the children of the root node is 1.

**Definition:** The height of a binary tree is the number of nodes on the longest path from the root to a leaf.

### EXAMPLE 19-2

Consider the binary tree of Figure 19-5. In this example, the terms such as node A and (node with info A) mean the same thing.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1353_0.png)

**FIGURE 19-5**  Binary tree

In this binary tree, the nodes I, E, and H have no left and right children. So, the nodes I, E, and H are leaves.

There is a branch from node A to node B. So, node A is the parent of node B. Similarly, node A is the parent of node C, node B is the parent of nodes D and E, node C is the parent of node F, node D is the parent of node G, and so on.

A→B→D→G is a path from node A to node G. Because there are three branches on this path, the length of this path is 3. Similarly, B→D→G→I is a path from node B to node I.

There are three leaves in this binary tree, which are I, E, and H. Also, the paths from root to these leaves are: A→B→D→G→I, A→B→E, and A→C→F→H. Clearly, the longest path from root to a leaf is A→B→D→G→I. The number of nodes on this path is 5. Hence, the height of the binary tree is 5.

Suppose that a pointer, p, to the root node of a binary tree is given. We next describe a C++ function, height, to find the height of the binary tree. The pointer to the root node is passed as a parameter to the function height.

If the binary tree is empty, then the height is 0. Suppose that the binary tree is nonempty. To find the height of the binary tree, we first find the height of the left subtree and the height of the right subtree. We then take the maximum of these two heights and add 1 to find the height of the binary tree. To find the height of the left (right) subtree, we apply the same procedure because the left (right) subtree is a binary tree. Therefore, the general algorithm to find the height of a binary tree is as follows. Suppose height(p) denotes the height of the binary tree with root p.

```
if (p is NULL)
    height(p) = 0
else
    height(p) = 1 + max(height(p->lLink), height(p->rLink))
```

Clearly, this is a recursive algorithm. The following function implements this algorithm:

```cpp
template <class elemType>
int height(nodeType<elemType> *p)
{
    if (p == NULL)
        return 0;
    else
        return 1 + max(height(p->lLink), height(p->rLink));
}
```

The definition of the function height uses the function max to determine the larger of two integers. The function max can be easily implemented.

Similarly, we can implement algorithms to find the number of nodes and number of leaves in a binary tree.

## Copy Tree

One useful operation on binary trees is to make an identical copy of a binary tree. A binary tree is a dynamic data structure; that is, memory for the nodes of a binary tree is allocated and deallocated during program execution. Therefore, if we use just the value of the pointer of the root node to make a copy of a binary tree, we get a shallow copy of the data. To make an identical copy of a binary tree, we need to create as many nodes as there are in the binary tree to be copied. Moreover, in the copied tree, these nodes must appear in the same order as they are in the original tree.

Given a pointer to the root node of a binary tree, we next describe a function that makes a copy of a given binary tree. This function is also quite useful in implementing the copy constructor and overloading the assignment operator, as described later in this chapter (see “Implementing Binary Trees”).

```cpp
template <class elemType>
void copyTree(nodeType<elemType>* copiedTreeRoot,
              nodeType<elemType>* otherTreeRoot)
{
    if (otherTreeRoot == NULL)
        copiedTreeRoot = NULL;
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

The item insertion, deletion, and lookup operations require that the binary tree be traversed. Thus, the most common operation performed on a binary tree is to traverse the binary tree, or visit each node of the binary tree. As you can see from the diagram of a binary tree, the actual traversal must start at the root node because there is a pointer to the root of the binary tree. For each node, we have two choices:

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

Consider the binary tree in Figure 19-6. Let $T$ be a binary tree. Suppose that $T$ is nonempty and the root node of $T$ is $A$. Then inorder($T$) or inorder($A$) denotes the listing of nodes of $T$ in the inorder sequence and root($T$) denotes the root node of $T$. For simplicity, we assume that visiting a node means to output the data stored in the node. In the section “Binary Tree Traversal and Functions as Parameters,” we will explain how to modify the binary tree traversal algorithms so that by using a function, the user can specify the action to be performed on a node when the node is visited.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1356_0.png)

**FIGURE 19-6**  Binary tree for an inorder traversal

Let $T$ denote the binary tree in Figure 19-6. Then, root($T$) = $A$. Therefore, we start the traversal at $A$. That is, inorder($A$). Because the binary tree is nonempty, to determine inorder($A$), we do the following:
