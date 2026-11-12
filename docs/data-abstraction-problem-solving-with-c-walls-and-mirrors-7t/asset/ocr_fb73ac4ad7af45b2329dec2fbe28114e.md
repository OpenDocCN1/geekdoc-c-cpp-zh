We again must use the different template type when we implement the method:

```
template<class friendItemType>
ostream& operator<<(ostream& outStream,
    const LinkedList<friendItemType>& outputList)
{
    int position = 1;
    Node<friendItemType>* curPtr = outputList.headPtr;
    while (curPtr != nullptr)
    {
        outStream << position << ": " << curPtr->getItem() << endl;
        curPtr = curPtr->getNext();
        position++;
    } // end while

    return outStream;
} // end operator<<
```

A friend method

Because the operator<< method is already part of the ostream class, we don't need to include it in our namespace by writing LinkedList<ItemType>:: before the method name.

Note that the method accesses the private data member headPtr of the class LinkedList. Although this access violates the principle of information hiding, it is done in a controlled fashion: The class LinkedList explicitly grants this access by declaring the method as a friend.

We can extend the concept of friend methods by creating friend classes. Granting a class access as a friend of another class allows all of the methods contained in the friend class to have access to the private and protected parts of the granting class. This feature is particularly useful when one class is used in the implementation of another class. For example, we have seen link-based implementations of ADTs that have a node declared as a separate class. For example, the LinkedList classes uses the class Node. An alternative is to implement the node as a class whose data members and methods are private and to declare the LinkedList class as a friend class. For example, you could define a node for the ADT list as follows:

Friend classes

```
template<class ItemType>
class ListNode        // A node on the list
{
private:
    ItemType item;          // A data item on the list
    Node<ItemType>* next;   // Pointer to next node

    Node();
    Node(const ItemType& nodeItem, Node<ItemType>* nextNode);

    // Friend class - can access private parts
    friend class LinkedList<ItemType>;
}; // end ListNode
```

The class LinkedList is a friend of ListNode

The class LinkedList has the same access privileges to the node's data members item and next as ListNode does. Friends of a base class do not have access to the private and protected parts added by a derived class—only to the private and protected members that appear in the base class.

A friend of a base class is not a friend of a derived class