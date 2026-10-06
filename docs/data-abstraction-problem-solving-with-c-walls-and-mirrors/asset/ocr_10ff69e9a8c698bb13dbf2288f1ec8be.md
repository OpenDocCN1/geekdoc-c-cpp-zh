# A Link-Based Implementation of the ADT Bag 147

FIGURE 4-8 (a) A linked chain and its shallow copy; (b) a linked chain and its deep copy

![](bbox=[0.105, 0.137, 0.735, 0.413])

For our new link-based implementation, a compiler-generated copy constructor would copy only the members itemCount and headPtr. For example, Figure 4-8a pictures a linked chain and the result of this shallow copy. Both the original pointer headPtr and its copy point to the same linked chain. In other words, the chains are not copied. If you need to create a copy of the linked chain, you must write your own copy constructor. That is, a deep copy is needed, as Figure 4-8b illustrates.

Thus, the copy constructor appears as follows.

```
template<class ItemType>
LinkedBag<ItemType>::LinkedBag(const LinkedBag<ItemType>& aBag){
    int itemCount = aBag->itemCount;
    Node<ItemType>* origChainPtr = aBag->headPtr;
    if (origChainPtr == nullptr)
        headPtr = nullptr; // Original bag is empty, so we copy
    else {
        // Copy first node
        headPtr = new Node<ItemType>();
        headPtr->setItem(origChainPtr->getItem());
        // Copy remaining nodes
        Node<ItemType>* newChainPtr = headPtr;
        while (origChainPtr != nullptr) // Last pointer
            origChainPtr = origChainPtr->getNext(); // Advance pointer
            // Get next item from original chain
            ItemType nextItem = origChainPtr->getItem();
            // Create a new node containing the next item
            Node<ItemType>* newNodePtr = new Node<ItemType>(nextItem);
        }
}
```