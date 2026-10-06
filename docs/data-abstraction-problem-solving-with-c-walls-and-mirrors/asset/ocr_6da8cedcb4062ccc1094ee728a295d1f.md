```
// Copy data from first node to located node
entryNodePtr->setItem(headPtr->getItem());

// Delete first node
Node<ItemType>* nodeDeletePtr = headPtr;
headPtr = headPtr->getNext();

// Return the node to the system
nodeDeletePtr->setNext(nullptr);
delete nodeDeletePtr;
nodeDeletePtr = nullptr;

itemCount--;
} // end if

return canRemove;
// remove
```

After the method remove deletes, a system can use this returned memory and possibly even reallocate it your program as a result of the new operator. Suppose that this reallocation occurs when you ask for a node for your linked chain. Be sure that your new node does not point to your chain, because you executed the statement nodeDeletePtr->setNext(nullptr) before you deleted the node. Doing this and setting the variable nodeDeletePtr to nullptr are examples of defensive programming that can avoid devastating, subtle errors later in the program. We take these steps, even though nodeDeletePtr is a local variable that we do not use, to clarify to future programmers who revise our method.

> Tip: Remember that any time you allocate memory using new, you must eventually delete it using delete.

> Note: For a pointer p, delete p deallocates the node to which p points; it does not delete p. The pointer still exists, but it contains an undefined value. You should not reference p or any other pointer variable that points to the allocated node. To help you avoid this kind of error, you can assign nullptr to p after deleting p. However, if variables other than p point to the deleted node, the possibility of error exists.

+   Question 11 Given the previous definition of the method remove, which entry in a bag can be deleted in the least time? Why?

+   Question 12 Given the previous definition of the method remove, which entry in a bag takes the most time to delete? Why?

The method clear. The method clear cannot simply set itemCount to zero, ignoring all of the entries in the linked chain. Because the nodes in the chain were allocated dynamically, clear must deallocate them. Thus, we have the following for this method:

```
template<class ItemType>
void LinkedBag<ItemType>::clear()
```