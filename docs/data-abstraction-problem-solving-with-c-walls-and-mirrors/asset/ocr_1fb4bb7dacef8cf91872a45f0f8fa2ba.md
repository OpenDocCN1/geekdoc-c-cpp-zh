# The ADT Binary Tree 437

# FIGURE 15-11 Three traversals of a binary tree

![](bbox=[0.068, 0.126, 0.825, 0.303])

(a) Preorder: 60, 20, 10, 40, 30, 50, 70
(b) Inorder: 10, 20, 30, 40, 50, 60, 70, 20
(c) Postorder: 10, 30, 50, 40, 20, 70, 60, 20

(Nodes indicate traversal order.)

The preorder traversal of the tree in Figure 15-11a visits the nodes in this order: 60, 20, 10, 40, 30, 50, 70, such as if you apply traversal to a binary tree that represents an algebraic expression, such as any tree in Figure 15-3, and display the nodes as you visit them, you will obtain the prefix form of the expression.

Inorder traversal. The recursive inorder traversal algorithm is as follows:

```
// Traverses the given binary tree in inorder.
// Assumes that "visit a node" means to process the node data item.
inorder(binTree: BinaryTree): void
if (binTree is not empty)
{
    inorder(Left subtree of binTree's root)
    visit(root of binTree)
    inorder(Right subtree of binTree's root)
}
```

Inorder traversal

The result of the inorder traversal of the tree in Figure 15-11b is 10, 20, 30, 40, 50, 60, 70. If you apply inorder traversal to a binary tree search, you will visit the nodes in order according to their data values. This is the case for the tree in Figure 15-11b.

Postorder traversal. Finally, the recursive postorder traversal algorithm is as follows:

```
// Traverses the given binary tree in postorder.
// Assumes that "visit a node" means to process the node data item.
postorder(binTree: BinaryTree): void
if (binTree is not empty)
{
    postorder(Left subtree of binTree's root)
    postorder(Right subtree of binTree's root)
    visit(root of binTree)
}
```

Postorder traversal

The prefix expressions are (a)-ab; (b)-a/bc; (c)-×-abc.