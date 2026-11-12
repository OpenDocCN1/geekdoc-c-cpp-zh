
Here tree1 is an empty binary tree; tree2Ptr and tree3Ptr each point to binary trees that have only a root node. These two roots contain the strings "A" and "B", respectively; and tree4Ptr points to a binary tree whose root contains "C" and has subtrees pointed to by tree2Ptr and tree3Ptr.

Programming Tip: In the previous example, if you were to use BinaryTreeInterface instead of BinaryNodeTree in the data type of either tree2Ptr or tree3Ptr, you would have to cast the variable to BinaryNodeTree before you could call the third constructor. For example, suppose you defined tree2Ptr as follows:
`BinaryTreeInterface<string>* tree2Ptr = new BinaryNodeTree<string>("A");`
You would then define tree4Ptr as follows:
`BinaryNodeTree<string>* tree4Ptr = new BinaryNodeTree<string>("C", static_cast<BinaryNodeTree<string>*>(tree2Ptr), tree3Ptr);`

BinaryNodeTree also declares an overloaded assignment operator. You could also, of course, overload other operators.

```
LISTING 16-3 A header file for the link-based implementation of the class BinaryNodeTree
/* ADT binary tree: Link-based implementation.
   File BinaryNodeTree.h. */

#ifndef _BINARY_NODE_TREE
#define _BINARY_NODE_TREE

#include "BinaryTreeInterface.h"
#include "BinaryNode.h"
#include "PrecondViolatedExcep.h"
#include "NotFoundException.h"

template<class ItemType>
class BinaryNodeTree<ItemType> : public BinaryTreeInterface<ItemType>
{
private:
   BinaryNode<ItemType>* rootPtr;

protected:
   ////////////////////////////////////////////////////////
   //      Protected Utility Methods Section:
   //      Recursive helper methods for the public methods.
   ////////////////////////////////////////////////////////
   int getHeightHelper(BinaryNode<ItemType>* subTreePtr) const;
   int getNumberOfNodesHelper(BinaryNode<ItemType>* subTreePtr) const;
   // Recursively deletes all nodes from the tree.
   void destroyTree(BinaryNode<ItemType>* subTreePtr);
   // Recursively adds a new node to the tree in a left/right fashion to
   // keep the tree balanced.
```

```
BinaryNode<ItemType>* balancedAdd(BinaryNode<ItemType>* subTreePtr,
BinaryNode<ItemType>* newNodePtr);
// Removes the target value from the tree by calling moveValuesUpTree
// to overwrite value with value from child.
BinaryNode<ItemType>* removeValue(BinaryNode<ItemType>* subTreePtr,
const ItemType target, bool& success);
```

```
// Copies values up the tree to overwrite value in current node until
// a leaf is reached; the leaf is then removed, since its value is
// stored in the parent.
BinaryNode<ItemType>* moveValuesUpTree(BinaryNode<ItemType>* subTreePtr);
```

```
// Recursively searches for target value in the tree by using a
// preorder traversal.
BinaryNode<ItemType>* findNode(BinaryNode<ItemType>* treePtr,
const ItemType& target,
bool& success) const;
```

```
// Copies the tree rooted at treePtr and returns a pointer to
// the copy.
BinaryNode<ItemType>* copyTree(const BinaryNode<ItemType>* treePtr) const;
```

```
// Recursive traversal helper methods:
void preorder(void visit(ItemType&),
BinaryNode<ItemType>* treePtr) const;
void inorder(void visit(ItemType&),
BinaryNode<ItemType>* treePtr) const;
void postorder(void visit(ItemType&),
BinaryNode<ItemType>* treePtr) const;
```

```
public:

// Constructor and Destructor Section.

BinaryNodeTree();
BinaryNodeTree(const ItemType& rootItem);
BinaryNodeTree(const ItemType& rootItem,
const BinaryNodeTree<ItemType>* leftTreePtr,
const BinaryNodeTree<ItemType>* rightTreePtr);
BinaryNodeTree(const BinaryNodeTree<ItemType>& tree);
virtual ~BinaryNodeTree();
```

```
// Public BinaryTreeInterface Methods Section.

bool isEmpty() const;
int getHeight() const;
int getNumberOfNodes() const;
ItemType getRootData() const throw(PrecondViolatedExcep);
void setRootData(const ItemType& newData);
bool add(const ItemType& newData); // Adds a node
bool remove(const ItemType& data); // Removes a node
void clear();
```

```
ItemType getEntry(const ItemType& anEntry) const
    throw(NotFoundException);
bool contains(const ItemType& anEntry) const;

////////////////////////////////////////
// Public Traversals Section.
////////////////////////////////////////
// void preorderTraverse(void visit(ItemType&)) const;
void inorderTraverse(void visit(ItemType&)) const;
void postorderTraverse(void visit(ItemType&)) const;

////////////////////////////////////////
// Overloaded Operator Section.
////////////////////////////////////////
// BinaryNodeTree& operator=(const BinaryNodeTree& rightHandSide);
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
{ } // end default constructor

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

Thus, copyTree has the following definition:

```
template<class ItemType>
BinaryNode<ItemType>* BinaryNodeTree<ItemType>::copyTree(const BinaryNode<ItemType>* treePtr) const
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

To copy a tree, traverse it in preorder and insert each item visited into a new node

The copy constructor then looks like this:

```
template<class ItemType>
BinaryNodeTree<ItemType>::BinaryNodeTree(const BinaryNodeTree<ItemType>& treePtr)
{
   rootPtr = copyTree(treePtr.rootPtr);
} // end copy constructor
```

Similarly, the protected method destroyTree, which the destructor calls, uses a recursive postorder traversal to delete each node in the tree. A postorder traversal is appropriate here because you can delete a node only after you have first traversed and deleted both of its subtrees. Thus, destroyTree has the following definition:

```
template<class ItemType>
void BinaryNodeTree<ItemType>::destroyTree(BinaryNode<ItemType>* subTreePtr)
{
   if (subTreePtr != nullptr)
   {
      destroyTree(subTreePtr->getLeftChildPtr());
      destroyTree(subTreePtr->getRightChildPtr());
      delete subTreePtr;
   } // end if
} // end destroyTree
```

The destructor then only needs to make the call destroyTree(rootPtr).
