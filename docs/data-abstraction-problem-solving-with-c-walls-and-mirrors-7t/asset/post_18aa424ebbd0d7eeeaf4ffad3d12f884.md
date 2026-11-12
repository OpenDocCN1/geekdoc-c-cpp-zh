

| Method | Description |
| :--- | :--- |
| clear() | Task: Removes all nodes from this binary tree. Input: None. Output: None. (The binary tree is empty.) |
| getEntry(anEntry) | Task: Gets a specific entry in this binary tree. Input: anEntry is the desired data item. Output: The entry in the binary tree that matches anEntry. Throws an exception if the entry is not found. |
| contains(data) | Task: Tests whether the given data item occurs in this binary tree. Input: data is the data item. Output: True if the binary tree contains the given data item, or false if not. |
| preorderTraverse(visit) | Task: Traverses this binary tree in preorder and calls the function visit once for each node. Input: visit is a client-defined function that performs an operation on or with the data in each visited node. Output: None. |
| inorderTraverse(visit) | Task: Traverses this binary tree in inorder and calls the function visit once for each node. Input: visit is a client-defined function that performs an operation on or with the data in each visited node. Output: None. |
| postorderTraverse(visit) | Task: Traverses this binary tree in postorder and calls the function visit once for each node. Input: visit is a client-defined function that performs an operation on or with the data in each visited node. Output: None. |

### FIGURE 15-12 UML diagram for the class BinaryTree

| BinaryTree |
| :--- |
| +isEmpty(): boolean |
| +getHeight(): integer |
| +getNumberOfNodes(): integer |
| +getRootData(): ItemType |
| +setRootData(newData: ItemType): void |
| +add(newData: ItemType): boolean |
| +remove(data: ItemType): boolean |
| +clear(): void |
| +getEntry(anEntry: ItemType): ItemType |
| +contains(data: ItemType): boolean |
| +preorderTraverse(visit: (item: ItemType): void): void |
| +inorderTraverse(visit: (item: ItemType): void): void |
| +postorderTraverse(visit: (item: ItemType): void): void |

Example. You can use the add operation to build the binary tree in Figure 15-5a, where the node labels represent character data:

Using ADT binary tree operations to build a binary tree

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

Given the specification of the add method, you have no reason to expect that the previous statements, in fact, produce the binary tree in the figure. Assuming that the operations are successful, we will know only that the binary tree has seven nodes containing the given data. Our specification of add is intentionally vague and gives the programmer who implements the class BinaryTree flexibility. It also makes BinaryTree more useful as a base class, as you will see in the next chapter.

## 15.2.3 An Interface Template for the ADT Binary Tree

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
    @pre  The binary tree is not empty.
    @post The root's data has been returned, and the binary tree is unchanged.
    @return The data in the root of the binary tree. */
   virtual ItemType getRootData() const = 0;

   /** Replaces the data item in the root of this binary tree
    with the given data, if the tree is not empty. However, if
    the tree is empty, inserts a new root node containing the
    given data into the tree.
    @pre None.
    @post The data in the root of the binary tree is as given.
    @param newData The data for the root. */
   virtual void setRootData(const ItemType& newData) = 0;

   /** Adds a new node containing the given data to this binary tree.
    @param newData The data for the new node. */
   @post The binary tree contains a new node.
   @return True if the addition is successful, or false not. */
   virtual bool add(const ItemType& newData) = 0;

   /** Removes the node containing the given data item from this binary tree.
    @param data The data value to remove from the binary tree. */
   @return True if the removal is successful, or false not. */
   virtual bool remove(const ItemType& data) = 0;

   /** Removes all nodes from this binary tree. */
   virtual void clear() = 0;

   /** Gets a specific entry in this binary tree.
    @post The desired entry has been returned, and the binary tree
    is unchanged. If no such entry was found, an exception is thrown.
    @param anEntry The entry to locate.
    @return The entry in the binary tree that matches the given entry.
    @throw NotFoundException if the given entry is not in the tree. */
   virtual ItemType getEntry(const ItemType& anEntry) const
   throw(NotFoundException) = 0;

   /** Tests whether a given entry occurs in this binary tree.
    @post The binary search tree is unchanged.
    @param anEntry The entry to find.
    @return True if the entry occurs in the tree, or false if not. */
   virtual bool contains(const ItemType& anEntry) const = 0;

   /** Traverses this binary tree in preorder (inorder, postorder) and
    calls the function visit once for each node.
    @param visit A client-defined function that performs an operation on
    or with the data in each visited node. */
   virtual void preorderTraverse(void visit(ItemType&)) const = 0;
   virtual void inorderTraverse(void visit(ItemType&)) const = 0;
   virtual void postorderTraverse(void visit(ItemType&)) const = 0;
}; // end BinaryTreeInterface

#endif
```

![](img/288a0c22d14d2450c1e772f228f867b0_468_0.png)

## 15.3 The ADT Binary Search Tree

Searching for a particular item is one operation for which the ADT binary tree is ill suited. The binary search tree is a binary tree that corrects this deficiency by organizing its data by value. Recall that each node n in a binary search tree satisfies the following three properties:

- n's value is greater than all values in its left subtree TL
- n's value is less than all values in its right subtree TR
- Both TL and TR are binary search trees.

This organization of data enables you to search a binary search tree for a particular data item, given its value instead of its position.

**Example.** Let's consider a binary search tree whose nodes contain people's names. Suppose that these objects are Alan, Bob, Elisa, Jane, Nancy, Tom, and Wendy. Figure 15-13 illustrates one binary search tree that we can form with these names.

### FIGURE 15-13 A binary search tree of names

![](img/288a0c22d14d2450c1e772f228f867b0_469_0.png)

Many different binary search trees can contain the same data, however. For example, in addition to the tree in Figure 15-13, each tree in Figure 15-14 is a valid binary search tree for the names Alan, Bob, Elisa, Jane, Nancy, Tom, and Wendy. Although these trees have different shapes, each one satisfies the requirements of a binary search tree.

> Several different binary search trees are possible for the same data

### FIGURE 15-14 Binary search trees with the same data as in Figure 15-13

![](img/288a0c22d14d2450c1e772f228f867b0_469_1.png)

### 15.3.1 Binary Search Tree Operations

As an ADT, the binary search tree has operations that are like the operations for the ADTs you studied in previous chapters, in that they involve inserting, removing, and retrieving data. Unlike the position-oriented ADTs stack, list, and queue, but like the ADT sorted list, the insertion, removal, and retrieval operations are by value, not by position. On the other hand, the other operations—including

