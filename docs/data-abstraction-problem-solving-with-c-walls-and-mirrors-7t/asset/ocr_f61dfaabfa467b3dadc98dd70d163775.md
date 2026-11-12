```
bool isEmpty() const;
bool enqueue(const ItemType& newEntry);
bool dequeue();
//** throw PrecondViolatedExcep if queue is empty. */
ItemType peekFront() const throw(PrecondViolatedExcep);
}; // end ListQueue
#include "ListQueue.cpp"
#endif
```

```
LISTING 14-2 The implementation file for the class ListQueue

/** ADT queue: ADT list implementation.
 @file ListQueue.cpp */

 #include "ListQueue.h" // Header file

 template<class ItemType>
 ListQueue<ItemType>::ListQueue()
 {
    listPtr = new LinkedList<ItemType>();
 } // end default constructor

 template<class ItemType>
 ListQueue<ItemType>::ListQueue(const ListQueue& aQueue) :
    listPtr(aQueue.listPtr)
 {
 } // end copy constructor

 template<class ItemType>
 ListQueue<ItemType>::~ListQueue()
 {
 } // end destructor

 template<class ItemType>
 bool ListQueue<ItemType>::isEmpty() const
 {
    return listPtr->isEmpty();
 } // end isEmpty

 template<class ItemType>
 bool ListQueue<ItemType>::enqueue(const ItemType& newEntry)
 {
    return listPtr->insert(listPtr->getLength() + 1, newEntry);
 } // end enqueue

 template<class ItemType>
 bool ListQueue<ItemType>::dequeue()
 {
    return listPtr->remove(1);
 } // end dequeue

 template<class ItemType>
 ItemType ListQueue<ItemType>::peekFront() const
 throw(PrecondViolatedExcep)
```