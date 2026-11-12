

```
ItemType getEntry(const ItemType& anEntry) const
throw(NotFoundException);
bool contains(const ItemType& anEntry) const;
//
// Public Traversals Section.
//
void preorderTraverse(void visit(ItemType&)) const;
void inorderTraverse(void visit(ItemType&)) const;
void postorderTraverse(void visit(ItemType&)) const;
//
// Overloaded Operator Section.
//
BinaryNodeTree& operator=(const BinaryNodeTree& rightHandSide);
} // end BinaryNodeTree
#include "BinaryNodeTree.cpp"
#endif
```

## 16.2.2 The Implementation

Although we will not provide a complete implementation file here, we will examine its most significant portions.

The constructors. The public constructors have the following definitions in the implementation file:

```
template<class ItemType>
BinaryNodeTree<ItemType>::BinaryNodeTree() : rootPtr(nullptr)
{
} // end default constructor
template<class ItemType>
BinaryNodeTree<ItemType>::BinaryNodeTree(const ItemType& rootItem)
{
rootPtr = new BinaryNode<ItemType>(rootItem, nullptr, nullptr);
} // end constructor
template<class ItemType>
BinaryNodeTree<ItemType>::BinaryNodeTree(const ItemType& rootItem,
const BinaryNodeTree<ItemType>* leftTreePtr,
const BinaryNodeTree<ItemType>* rightTreePtr)
{
rootPtr = new BinaryNode<ItemType>(rootItem,
copyTree(leftTreePtr->getRootPtr()),
copyTree(rightTreePtr->getRootPtr()));
} // end constructor
```

The default constructor uses an initializer to set the value of rootPtr to nullptr. The second constructor sets rootPtr to a new node containing the given data item. The third constructor also makes rootPtr point to a new node, but the node contains the given data item and pointers to copies of the given subtrees. We talk about the method copyTree next during our discussion of the copy constructor.

The copy constructor and destructor. The copy constructor and the destructor implicitly use traversal. Since traversal is a recursive operation, the copy constructor and destructor each call a recursive method. As we have mentioned before, public ADT methods usually are not themselves recursive, but rather call a recursive method that is either private or protected. We do this to hide the underlying data structure from the client.

The protected method copyTree, which the copy constructor calls, uses a recursive preorder traversal to copy each node in the tree. By copying each node as soon as the traversal visits it, copyTree can make an exact copy of the original tree. To make the copy distinct from the original tree, the new nodes must be linked together by using new pointers. That is, you cannot simply copy the pointers in the nodes of the original tree. The result is a deep copy of the tree.

To copy a tree, traverse it in preorder and insert each item visited into a new node

```cpp
template<class ItemType>
BinaryNodeTree<ItemType>::copyTree(const BinaryNode<ItemType>* treePtr) const
{
   BinaryNode<ItemType>* newTreePtr = nullptr;

   // Copy tree nodes during a preorder traversal
   if (treePtr != nullptr)
   {
      // Copy node
      newTreePtr = new BinaryNode<ItemType>(treePtr->getItem(),
                                            nullptr, nullptr);
      newTreePtr->setLeftChildPtr(copyTree(treePtr->getLeftChildPtr()));
      newTreePtr->setRightChildPtr(copyTree(treePtr->getRightChildPtr()));
   } // end if

   // Else tree is empty (newTreePtr is nullptr)

   return newTreePtr;
} // end copyTree
```

The copy constructor then looks like this:

```cpp
template<class ItemType>
BinaryNodeTree<ItemType>::BinaryNodeTree(const BinaryNodeTree<ItemType>& treePtr)
{
   rootPtr = copyTree(treePtr.rootPtr);
} // end copy constructor
```

Similarly, the protected method destroyTree, which the destructor calls, uses a recursive postorder traversal to delete each node in the tree. A postorder traversal is appropriate here because you can delete a node only after you have first traversed and deleted both of its subtrees. Thus, destroyTree has the following definition:

```cpp
template<class ItemType>
void BinaryNodeTree<ItemType>::destroyTree(BinaryNode<ItemType>* subTreePtr)
{
   if (subTreePtr != nullptr)
   {
      destroyTree(subTreePtr->getLeftChildPtr());
      destroyTree(subTreePtr->getRightChildPtr());
      delete subTreePtr;
      subTreePtr = nullptr;
   } // end if
} // end destroyTree
```

The destructor then only needs to make the call destroyTree(rootPtr).

The method getHeight. The public method getHeight calls the protected, recursive method getHeightHelper. The height of a subtree rooted at a particular node is 1—for the node itself—plus the height of the node's tallest subtree. Thus, we define the protected method getHeightHelper as follows:

```
template<class ItemType>
int BinaryNodeTree<ItemType>::
getHeightHelper(BinaryNode<ItemType>* subTreePtr) const
{
    if (subTreePtr == nullptr)
        return 0;
    else
        return 1 + max(getHeightHelper(subTreePtr->getLeftChildPtr()),
                       getHeightHelper(subTreePtr->getRightChildPtr()));
} // end getHeightHelper
```

The public method getHeight contains just the statement

```
return getHeightHelper(rootPtr);
```

The method getNumberOfNodes has a similar definition.

- Question 2 What are the definitions of the public method getNumberOfNodes and the protected helper method getNumberOfNodesHelper?
- Question 3 What is the definition of the public method setRootData?
- Question 4 What is the definition of the public method getRootData? Recall that this method has a precondition.

The method add. The specification of the public method add says to add a new node containing given data to a binary tree. It does not indicate where that new node should be in the tree. Thus, we have flexibility in how we define the method. Moreover, derived classes of BinaryNodeTree can both override add to change its behavior and adhere to its specification.

Let's add the new node so that the resulting tree is balanced. Once again, we can use recursion to achieve our goal. The public method add can create a new node containing the data passed to it as an argument. Then the method can pass this node to a protected, recursive method that adds it in an appropriate place in the tree. The protected method must then return a pointer to the tree's root. If we name the protected method balancedAdd, the public add method has the following definition:

```
template<class ItemType>
bool BinaryNodeTree<ItemType>::add(const ItemType& newData)
{
    BinaryNode<ItemType>* newNodePtr = new BinaryNode<ItemType>(newData);
    rootPtr = balancedAdd(rootPtr, newNodePtr);
    return true;
} // end add
```

Now we need to define the protected method balancedAdd. Notice that the add method passes two arguments to balancedAdd: a pointer to the root of the tree—or subtree—to which we will add a node and a pointer to the new node. To add a node to the tree, we add the node to the root's shorter subtree. This is the recursive step, since the subtree is a binary tree. The base case occurs when a subtree is empty.

Here is the definition of balancedAdd:

```cpp
template<class ItemType>
BinaryNode<ItemType>* BinaryNodeTree<ItemType>::
    balancedAdd(BinaryNode<ItemType>* subTreePtr,
                BinaryNode<ItemType>* newNodePtr)
{
   if (subTreePtr == nullptr)
      return newNodePtr;
   else
   {
      BinaryNode<ItemType>* leftPtr = subTreePtr->getLeftChildPtr();
      BinaryNode<ItemType>* rightPtr = subTreePtr->getRightChildPtr();

      if (getHeightHelper(leftPtr) > getHeightHelper(rightPtr))
      {
         rightPtr = balancedAdd(rightPtr, newNodePtr);
         subTreePtr->setRightChildPtr(rightPtr);
      }
      else
      {
         leftPtr = balancedAdd(leftPtr, newNodePtr);
         subTreePtr->setLeftChildPtr(leftPtr);
      }  // end if

      return subTreePtr;
   }  // end if
} // end balancedAdd
```

For example, the following statements in balancedAdd add a new node to a right subtree:

```cpp
rightPtr = balancedAdd(rightPtr, newNodePtr);
subTreePtr->setRightChildPtr(rightPtr);
```

The recursive call to balancedAdd adds the new node and returns a pointer to the revised subtree. However, we need to link this subtree to the rest of the tree. The call to setRightChildPtr accomplishes this. The addition of a new node to a left subtree is performed in a similar manner. Note that such insertions are analogous to the recursive addition of a new node to a linear chain of linked nodes, as discussed in Section 9.2.3 of Chapter 9. Reviewing that section will give you insight into the process here.

Figure 16-3 shows the effect of a sequence of add operations on an initially empty binary tree.

- Question 5 Where would a new node be placed next in the binary tree shown in Figure 16-3?

The traversals. Since the traversals are recursive, the public traversal methods each call a protected method that performs the actual recursion. For example, the public method inorderTraverse calls the protected method inorder. Like inorderTraverse, inorder has the function visit as a parameter. This function specifies the tree item as a reference parameter, which enables the client not only to examine the item but also to modify it. The second parameter of inorder is

