# 15.2.1 Traversals of a Binary Tree

chain of linked nodes: Beginning with the chain's first node, you visit each node sequentially until you reach the end of the chain. Traversal of a binary tree, however, can visit the tree's nodes in one of several different orders. We examine the details of the traversal operations next.

A traversal algorithm for a binary tree visits each node in the tree. While visiting a node, you do something with or to the node, such as visiting or modifying the contents of the node. For the purpose of this discussion, assume that visiting a node means displaying the data portion of the node.

With the recursive definition of a binary tree in mind, you can construct a recursive traversal algorithm as follows. According to the definition, the binary tree T is either empty or of the form

![](bbox=[0.275, 0.335, 0.395, 0.375])

If T is empty, the traversal algorithm takes no action—an empty tree is the base case. If T is not empty, the traversal algorithm must perform three tasks: It must display the data in the root, and it must traverse the two subtrees T_L and T_R, each of which is a binary tree smaller than T. We can summarize this using the following pseudocode:

```
if (T is not empty)
  Display the data in T's root
  Traverse T's left subtree
  Traverse T's right subtree
```

Although we arbitrarily choose t's root before traversing its subtrees, the algorithm actually has three choices of when to visit r. It can visit r

+   * Before it traverses both of r's subtrees—as we just did
* After it has traversed r's left subtree T_L but before it traverses r's right subtree T_R
* After it has traversed both of r's subtrees

These choices result in preorder, inorder, and postorder traversal, respectively. Figure 15-11 shows the results of these traversals for a given binary tree.

Each traversal visits every node in a binary tree exactly once. Thus, n visits occur for a tree of n nodes. Each visit performs the same operations on each node, independent of n, so it must be O(1). Thus, each traversal is O(n).

Preorder traversal. The recursive preorder algorithm is as follows:

```
// Traverses the binary tree in preorder.
// Assumes that "visit a node" means to process the node's data item.
preorder(binTree): void

if (binTree is not empty)
  Visit the root of binTree
  preorder(Left subtree of binTree's root)
  preorder(Right subtree of binTree's root)
```