prevPtr points to the last node in the chain, the previous pair of assignment statements will indeed insert the new node at the end of the chain. Thus, insertion at the end of a chain is not a special case.

To summarize, the insertion process requires three high-level steps:

+   1. Create a new node and store the new data in it.
+   2. Determine the point of insertion.
+   3. Connect the new node to the linked chain by changing pointers.

These steps and the previous discussion are implemented in the following definition of insert:

```
template<class ItemType>
bool LinkedList<ItemType>::insert(int newPosition,
                                  const ItemType& newEntry)
{
   bool ableToInsert = (newPosition > 1) &&
                       (newPosition <= itemCount + 1);
   if (ableToInsert)
   {
      // Create a new node containing the new entry
      Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);

      // Attach new node to chain
      if (newPosition == 1)
      {
         // Insert new node at beginning of chain
         newNodePtr->setNext(headPtr);
         headPtr = newNodePtr;
      }
      else
      {
         // Find node that will be before new node
         Node<ItemType>* prevPtr = getNodeAt(newPosition - 1);

         // Insert new node after node to which prevPtr points
         newNodePtr->setNext(prevPtr->getNext());
         prevPtr->setNext(newNodePtr);
      } // end if

      itemCount++;  // Increase count of entries
   } // end if

   return ableToInsert;
} // end insert
```

If you have not already begun to test the methods in the core group, you should do so now.

+   Question 5 Given a nonempty list that is an instance of LinkedList, at what position does an insertion of a new entry require the fewest operations? Explain.
+   Question 6 In the previous method insert, the second statement tests the value of newPosition. Should the boolean expression it tests be isEmpty() || (newPosition == 1)? Explain.
+   Question 7 How does the insert method enforce the precondition of getNodeAt?

The method remove. To remove any entry from a list, you must be able to delete any node from a chain of linked nodes. You already know how to delete the first node in a chain, because the