Assuming the private method getNodeBefore that we specified in the header file, we can use the previous algorithm to define the insertSorted method, as follows:

```
```cpp
template<class ItemType>
void LinkedSortedList<ItemType>::insertSorted(const ItemType& newEntry)
{
   Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
   Node<ItemType>* prevPtr = getNodeBefore(newEntry);

   if (isEmpty() || (prevPtr == nullptr)) // Add at beginning
   {
      newNodePtr->setNext(headPtr);
      headPtr = newNodePtr;
   }
   else // Add after node before
   {
      Node<ItemType>* aftPtr = prevPtr->getNext();
      newNodePtr->setNext(aftPtr);
      prevPtr->setNext(newNodePtr);
   } // end if

   itemCount++;
} // end insertSorted
```
```

**The private method getNodeBefore.** We still need to implement the private method getNodeBefore to locate the node that is before the node that should or does contain the given entry. We will need two pointers as we traverse the list. Clearly, we need a pointer to the current node so we can compare its entry to the desired entry. But we also must retain a pointer to the previous node, because it is this pointer that the method returns. In the following implementation, these pointers are curPtr and prevPtr.

```
```cpp
template<class ItemType>
Node<ItemType>* LinkedSortedList<ItemType>::
   getNodeBefore(const ItemType& anEntry) const
{
   Node<ItemType>* curPtr = headPtr;
   Node<ItemType>* prevPtr = nullptr;
   while ((curPtr != nullptr) && (anEntry > curPtr->getItem()))
   {
      prevPtr = curPtr;
      curPtr = curPtr->getNext();
   } // end while

   return prevPtr;
} // end getNodeBefore
```
```

The programming problems at the end of this chapter ask you to complete this implementation of the sorted list.

![](bbox=[0.1, 0.75, 0.9, 0.82])

![](bbox=[0.1, 0.82, 0.9, 0.88])

![](bbox=[0.1, 0.88, 0.9, 0.95])