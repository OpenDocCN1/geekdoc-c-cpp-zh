# 9.2.3 Using Recursion in LinkedList Methods

Using recursion in the implementation of some of the methods in the class LinkedList can be an attractive alternative to an iterative approach. Section 4.3 of Chapter 4 developed the recursive methods fillVector and getPointerTo. Both methods considered a chain's first node and then recursively considered the rest of the chain. In general, we can state that you can process a linked chain by processing its first node and then the rest of the chain recursively. Thus, to add a new node to a chain of linked nodes at a given position, you use the following logic:

```
if (the insertion position is 1)
Add the new node to the beginning of the chain
else
Ignore the first node and add the new node to the rest of the chain
```

Adding to the beginning of a chain—or subchain—is the base case of this recursion. Happily, the beginning of a chain is the easiest place to make an addition.

If position is the desired position of the new node, newNodePtr points to the new node, and subChainPtr initially points to the chain and later points to the rest of the chain, we can add some detail to the previous logic, as follows:

```
if (position == 1)
{
    newNodePtr->setNext(subChainPtr)
    subChainPtr = newNodePtr
    Increment itemCount
}
else
    Using recursion, add the new node at position position - 1 of the subchain pointed
    to by subChainPtr->getNext()
```

The private method getPointerTo in Section 4.3 returned a pointer to a given entry in a chain. Since that operation traversed the chain but did not alter it, its recursive formulation was straightforward. However, the list's method insert does alter the chain. Getting the recursive method to make these changes is the challenge.

**The method insert.** Let's look at the recursive implementation of the insertion operation before we describe why it works. You learned in Section 4.3 that you write a private method to perform the recursion and you write a public method—typically the one that implements the ADT's operation—to invoke this private method. Thus, we have the following method definitions:

// The public method insert:

```
template<class ItemType>
bool LinkedList<ItemType>::insert(int newPosition, const ItemType& newEntry)
{
    bool ableToInsert = (newPosition >= 1) &&
                        (newPosition <= itemCount + 1);
    if (ableToInsert)
    {
        // Create a new node containing the new entry
        Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
        headPtr = insertNode(newPosition, newNodePtr, headPtr);
    } // end if

    return ableToInsert;
} // end insert
```