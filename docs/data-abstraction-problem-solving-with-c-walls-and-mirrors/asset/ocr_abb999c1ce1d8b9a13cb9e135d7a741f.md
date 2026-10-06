# 472 CHAPTER 16 Tree Implementations

for Kody. The search algorithm would terminate at Nancy's empty subtree, as Figure 16-7 illustrates. You would then insert Kody as Nancy's left child, as Figure 16-7c shows.

Because Nancy has no left child, the insertion is simple, requiring only Nancy's left child pointer to Kody. Searching for an entry that is not in the binary search tree ends at an empty subtree, you insert a new item as a new leaf. Because adding a leaf requires only a change of the appropriate pointer in the parent, the work required for insertion is virtually the same as for the corresponding search.

We define the public method as follows:

```
template<class ItemType>
bool BinarySearchTree<ItemType>::add(const ItemType& newData)
{
    BinaryNodeItemType* newNodePtr = new BinaryNode<ItemType>(newData);
    rootPtr = insertInOrder(rootPtr, newNodePtr);

    return true;
} // end add
```

The method creates a new node and passes pointers to the tree and the new node to a recursive method that actually performs the insertion. The following high-level pseudocode describes this insertion process:

First draft of the insertion algorithm

```
// Inserts a new node into a binary search tree.
insertInOrder(subtreePtr, BinaryNodePointer,
    newNodePtr, BinaryNodePointer): BinaryNodePointer

    Search the pointed to by subtreePtr for the item in the node pointed
    if (the search terminates at parent's left subtree)
        SetLeftChildPtr of parentNode to newNodePtr
    else
        SetRightChildPtr of parentNode to newNodePtr
```

The appropriate pointer—leftChildPtr or rightChildPtr—of node parentNode must be set to the new node. The recursive nature of the search algorithm provides an elegant means of setting the pointer, provided that you return this possibly changed pointer. The situation is quite similar to the insertion method for the AD list we saw in Chapter 9. If the tree was empty before insertion, the external pointer to the root of the tree would be nullptr and would not make a recursive call. Thus, you would return a pointer to the new node. Our pseudocode is refined as:

Refinement of the insertion algorithm

```
// Inserts a new item into the binary search tree to which subtreePtr points.
insertInOrder(subtreePtr, BinaryNodePointer,
    newNodePtr, BinaryNodePointer): BinaryNodePointer

    if (subtreePtr is nullptr)
        return newNodePtr
    else if (subtreePtr->getItem() > newNodePtr->getItem())
        tempPtr = insertInOrder(subtreePtr->getLeftChildPtr(), newNodePtr)
        subtreePtr->setLeftChildPtr(tempPtr)
    else
```