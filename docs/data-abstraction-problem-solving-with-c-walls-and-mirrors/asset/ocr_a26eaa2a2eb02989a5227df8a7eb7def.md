# CHAPTER 16 Tree Implementations

The previous chapter discussed various kinds of trees, but it focused on the ADTs binary tree and search tree. This chapter will show you how to implement these two ADTs by using constructs of C++. In each case, the data structures will be private members of a class of trees.

# 16.1 The Nodes in a Binary Tree

The first step in implementing a tree is to choose a data structure to represent its nodes. Since each node must contain both data and "pointers" to the nodes' children—which are other nodes in the tree—it is natural to make each node object. Thus, we will use a C++ class to define the nodes in the tree. If we place these nodes in an array, the "pointers" are in array indices. However, if the nodes are part of a linked chain, we use C++ pointers to link them together.

# 16.1.1 An Array-Based Representation

Let's name our class TreeNode. An array-based implementation of a tree uses an array of nodes, so a class of such trees could have the following data members:

```
TreeNode<ItemType> tree[MAX_NODES]; // Array of tree nodes
int root; // Index of root
int free; // Index of free list
```

The variable root is an index to the tree's root node within the array. If the tree is empty, root is -1.
As the tree grows by insertions and deletions, its nodes may not be in contiguous elements of the array, this implementation requires us to establish a collection of available nodes, called a free list. To insert a new node into the tree, you first obtain an available node from the free list. If you remove a node from the tree, you place it into the free list so that you can reuse the node at a later time. The data member free is the index to the first node in the free list. We will talk about the free list in a moment.
Although these data members are appropriate for any tree, we want to restrict our conversation to binary trees and consider a class of its nodes. The class TreeNode, as given in Listing 16-1, is such a class.

> LISTING 16-1 template<class ItemType> class TreeNode for an array-based implementation of the ADT binary tree

```
template<class ItemType>
class TreeNode
{
private:
    ItemType item; // Data portion
    int leftChild; // Index to left child
    int rightChild; // Index to right child

public:
    TreeNode();
    TreeNode(const ItemType& nodeItem, int left, int right);

// Declarations of the methods setItem, getItem, setLeft, getLeft,
    // setRight, and getRight are here.

};\ // end TreeNode
```