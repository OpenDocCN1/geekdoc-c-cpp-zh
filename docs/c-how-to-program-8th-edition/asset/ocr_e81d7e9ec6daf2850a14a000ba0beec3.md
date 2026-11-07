# ### Binary Search Trees

A **binary search tree** (with no duplicate node values) has the characteristic that the values in any left subtree are less than the value in its parent node, and the values in any right subtree are greater than the value in its parent node. Figure 20.19 illustrates a binary search tree with 9 values. Note that the shape of the binary search tree that corresponds to a set of data can vary, depending on the order in which the values are inserted into the tree.

![](bbox=[0.38, 0.251, 0.603, 0.354])

**Fig. 20.19**  |  A binary search tree.

# ### Implementing the Binary Search Tree Program

The program of Figs. 20.20–20.22 creates a binary search tree and traverses it (i.e., walks through all its nodes) three ways—using recursive **inorder**, **preorder** and **postorder traversals**. We explain these traversal algorithms shortly.

```
```cpp
// Fig. 20.20: TreeNode.h
// Template TreeNode class definition.
#ifndef TREENODE_H
#define TREENODE_H

// forward declaration of class Tree
template< typename NODETYPE > class Tree;

// TreeNode class-template definition
template< typename NODETYPE >
class TreeNode
{
   friend class Tree< NODETYPE >;
public:
   // constructor
   TreeNode( const NODETYPE & d )
      : leftPtr( 0 ), // pointer to left subtree
        data( d ), // tree node data
        rightPtr( 0 ) // pointer to right subtree
{
   // empty body
} // end TreeNode constructor

// return copy of node's data
NODETYPE getData() const
{
```

```

**Fig. 20.20**  |  TreeNode class-template definition. (Part 1 of 2.)