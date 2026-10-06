# 282 CHAPTER 9 List Implementations

```
// The private method insertNode:
// Adds a node to the subchain pointed to by subChainPtr
// at a given position. Returns a pointer to the augmented subchain.
template<class ItemType>
Node<ItemType>* LinkedList<ItemType>::insertNode(int position,
Node<ItemType>* newNodePtr, Node<ItemType>* subChainPtr)
{
    if (position == 1)n        // Insert new node at beginning of subchain
        newNodePtr->setNext(subChainPtr);
        subChainPtr = newNodePtr;
        itemCount++; // Increase count of entries
    }
    else {
        Node<ItemType>* afterPtr =
            insertNode(position - 1, newNodePtr, subChainPtr->getNext());
        subChainPtr->setNext(afterPtr);
    }
    return subChainPtr;
}
end insertNode;
```

The recursive method insertNode adds the node to the subchain to which subChain points at the given position. We will trace and explain its logic next.

**Tracing an addition to the list's.** Consider the list in Figure 9-9 represents. Let's add a new entry at the beginning of the chain using an invocation such as

```
myList->insert(1, newEntry);
```

The public insert will create a new node containing newEntry (Figure 9-b) and then call the private method insertNode with the invocation

```
insertNode(1, newNodePtr, headPtr);
```

The pointer in the argument headPtr is copied to the parameter subChainPtr, and so it also points to the first node in the chain, as Figure 9-9c illustrates.
The new node is linked to the beginning of the original chain, as Figure 9-9d shows. Notice that subChainPtr is unchanged, even though it is the argument that corresponds to the parameter subChainPtr. The private method insert returns the value of subChainPtr, and the public method insert assigns that value to headPtr. The chain with the completed addition appears as in Figure 9-e.

**Tracing an addition to the list's interior.** What happens when the addition is not at the beginning of the original chain? Let's trace what happens when we add a third node to the chain given in Figure 9-a. The public method insert creates a new node and calls the private method insertNode with the invocation

```
insertNode(3, newNodePtr, headPtr);
```

As in the previous example, the pointer in the argument headPtr is copied to the parameter subChainPtr, and so it also points to the first node in the chain, as Figure 9-10 illustrates. Since the insertion is not at position 1, another recursive call occurs:

```
insertNode(2, newNodePtr, subChainPtr->getNext());
```