```
{
  if (curPtr != nullptr) {
    bagContents.push_back(curPtr->getItem());
    f1Vector(bagContents, curPtr->getNext());
  } // end if
} // end toVector
```

Even though f1Vector has a reference parameter, the method is safe because it is private. A similar situation occurs in Chapter 16 and is discussed further in a Note in Section 16.3.1.

**The private method** getPointerTo. The method getPointerTo calls a given entry within the linked chain. Unlike f1Vector’s traversal, this stops if it locates the node that contains the given entry. The iterative version of getPointerTo has one parameter, which is the given entry. We could define a private method to perform the recursion—as we did for traverse—that two parameters: the given entry and a head pointer. Then getPointerTo would call this new method. However, since getPointerTo is itself a private method, we can revise it to have the necessary parameters. This is the approach we take. Of course, we would have to revise the calls to the method that appears in the rest of the class.

By replacing the declaration of getPointerTo in the header file for class LinkedBag with the following:

```
// Locates a given entry within this bag
// Returns either a pointer to the node containing a given entry or
// the null pointer if the entry is not in the bag.
NodeType* getPointerTo(const ItemType& target,
NodeType* curPtr) const;
```

Before we go do so, we revise the calls to this method in the class that remove and contains items. The original calls are getPointerTo(aEntry), but now each needs to be getPointerTo(aEntry, headPtr).

The recursive definition of this method has two base cases. One case occurs when the chain is empty, causing the method to return nullptr. The other base case occurs when we locate the desired entry at curPtr->getItem(). In this case, the method returns curPtr. The recursive search continues the chain beginning at curPtr->getNext(). Thus, the method returns the following:

```
template class. getPointerTo(const ItemType& target,
NodeType* curPtr) const
{
  NodeType* result = nullptr;
  if (target== curPtr->getItem()) {
    result = curPtr;
  } else {
    result = getPointerTo(target, curPtr->getNext());
  } // end if
  return result;
} // end getPointerTo
```

Other methods can have a recursive definition left for you as for exercises.

> Question 14 Revise the method clear so that it calls a recursive method to deallocate the nodes in the chain.