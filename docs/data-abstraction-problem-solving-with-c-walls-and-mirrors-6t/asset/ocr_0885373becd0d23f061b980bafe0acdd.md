![](bbox=[0.015, 0.095, 0.045, 0.135])

Example. You can use the add operation to build the binary tree in Figure 15-5a, where the node labels represent character data:

```
tree = new empty binary tree
tree.add('A')
tree.add('B')
tree.add('C')
tree.add('D')
tree.add('E')
tree.add('F')
tree.add('G')
```

Given the specification of the add method, you have no reason to expect that the previous statements, in fact, produce the binary tree in the figure. Assuming that the operations are successful, you will know only that the binary tree has seven nodes containing the given data. Our specification of add is intentionally vague and gives the programmer who implements the class BinaryTree flexibility. It also makes BinaryTree more useful as a base class, as you will see in the next chapter.

# 15.2.3 An Interface Template for the ADT Binary Tree

We formalize our specifications for the ADT binary tree by writing the interface template given in Listing 15-1.

```
LISTING 15-1 An interface template for the ADT binary tree

/** Interface for the ADT binary tree.
 @file BinaryTreeInterface.h */
#ifndef BINARY_TREE_INTERFACE
#define BINARY_TREE_INTERFACE

template<class ItemType>
class BinaryTreeInterface
{
   public:
      /** Tests whether this binary tree is empty.
       @return True if the binary tree is empty, or false if not. */
      virtual bool isEmpty() const = 0;

      /** Gets the height of this binary tree.
       @return The height of the binary tree. */
      virtual int getHeight() const = 0;

      /** Gets the number of nodes in this binary tree.
       @return The number of nodes in the binary tree. */
      virtual int getNumberOfNodes() const = 0;

      /** Gets the data that is in the root of this binary tree.
      @pre The binary tree is not empty.
      @post The root's data has been returned, and the binary tree is unchanged.
      @return The data in the root of the binary tree. */
      virtual ItemType getRootData() const = 0;

      /** Replaces the data item in the root of this binary tree
       with the given data, if the tree is not empty. However, if
```