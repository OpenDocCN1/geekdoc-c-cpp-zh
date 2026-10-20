sponds to a set of data can vary, depending on the order in which the values are inserted into the tree.

Figures 22.17 and 22.18 create a generic binary search tree class and use it to manipulate a tree of integers. The application in Fig. 22.18 traverses the tree (i.e., walks through all its nodes) three ways—using recursive inorder, preorder and postorder traversals. The program generates 10 random numbers and inserts each into the tree. Class Tree<T> is declared in package com.deitel.ch22 for reuse.

![](bbox=[0.3, 0.27, 0.7, 0.42])

# Fig. 22.16 | Binary search tree containing 12 values.

```
// Fig. 22.17: Tree.java
// TreeNode and Tree class declarations for a binary search tree.
package com.deitel.ch22;

// class TreeNode definition
class TreeNode< T extends Comparable< T > >
{
    // package access members
    TreeNode< T > leftNode; // left node
    T data; // node value
    TreeNode< T > rightNode; // right node

    // constructor initializes data and makes this a leaf node
    public TreeNode( T nodeData )
    {
        data = nodeData;
        leftNode = rightNode = null; // node has no children
    } // end TreeNode constructor

    // locate insertion point and insert new node; ignore duplicate values
    public void insert( T insertValue )
    {
        // insert in left subtree
        if ( insertValue.compareTo( data ) < 0 )
        {
            // insert new TreeNode
            if ( leftNode == null )
                leftNode = new TreeNode< T >( insertValue );
            else // continue traversing left subtree recursively
                leftNode.insert( insertValue );
        } // end if
```

# Fig. 22.17 | TreeNode and Tree class declarations for a binary search tree. (Part 1 of 3.)