
```
{
   if (isEmpty())
      throw PrecondViolatedExcep("peekFront() called with empty queue.");
   // Queue is not empty; return front
   return listPtr->getEntry(1);
} // end peekFront
// End of implementation file
```

Of particular note in the implementation file are the definitions of the constructor, copy constructor, and destructor. The constructor creates a new instance of a list. Omitting this step is an easy oversight to make, leading to incorrect execution instead of a syntax error. The copy constructor uses an initializer, `listPtr(new ListPtr)`, to invoke the list's copy constructor. Finally, even though the destructor has an empty body, the list's destructor will be invoked. Exercise 8 at the end of this chapter asks you to consider the efficiency of this implementation.

## 14.1.2 A Link-Based Implementation

A link-based implementation of a queue uses a chain of linked nodes, much like the other link-based implementations that you have seen. However, the queue presents a challenge, since we must be able to not only remove entries from its front but also add them to its back. Removing a node from the beginning of a linked chain is easy, but to add a new node to the chain's end, we need a pointer to the chain's last node. One way to accomplish this is to begin at the first node and traverse the chain until we reach the last one. A much more efficient approach uses a **tail pointer** to reference the end of the chain—just as the head pointer references the beginning of the chain. Figure 14-2 illustrates a chain of linked nodes that has both head and tail pointers. Like the head pointer `frontPtr`, `backPtr` is external to the chain.

FIGURE 14-2 A chain of linked nodes with head and tail pointers

![](img/288a0c22d14d2450c1e772f228f867b0_426_0.png)

A linear linked chain or a circular linked chain can represent a queue

Figure 14-3 shows that you can actually get by with one external pointer—to the back—if you make the last node point to the first one. This data structure is a **circular chain** of linked nodes. Notice that the nodes in a circular chain have next pointers that never contain `nullptr`. We will refer to a chain like the one in Figure 14-2 as a **linear chain**, regardless of how many external pointers it has. Such a chain does have a node whose next pointer is `nullptr`.

Programming Problem 1 at the end of the chapter asks you to consider the details of the circular chain implementation. Here we will develop an implementation of the ADT queue using a chain that has both head and tail pointers, as illustrated in Figure 14-2.

FIGURE 14-3 A circular chain of linked nodes with one external pointer

![](img/288a0c22d14d2450c1e772f228f867b0_427_0.png)

> Note: If you use a linear chain with only a head pointer to implement a queue, the enqueue operation will be inefficient. Each addition to the queue requires a traversal to the end of the chain. As the queue increases in length, the traversal time—and hence enqueue's time requirement—will increase.

Listing 14-3 shows the header file for our class definition.

```
LISTING 14-4 The header file for the class LinkedQueue

/* ADT queue: Link-based implementation.
   @file LinkedQueue.h */

#ifndef _LINKED_QUEUE
#define _LINKED_QUEUE

#include "QueueInterface.h"
#include "Node.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class LinkedQueue : public QueueInterface<ItemType>
{
private:
   // The queue is implemented as a chain of linked nodes that has
   // two external pointers, a head pointer for the front of the queue
   // and a tail pointer for the back of the queue.
   Node<ItemType>* backPtr;
   Node<ItemType>* frontPtr;

public:
   LinkedQueue();
   LinkedQueue(const LinkedQueue& aQueue);
   ~LinkedQueue();

   bool isEmpty() const;
   bool enqueue(const ItemType& newEntry);
   bool dequeue();

   /** @throw PrecondViolatedExcep if the queue is empty */
   ItemType peekFront() const throw(PrecondViolatedExcep);
}; // end LinkedQueue

#include "LinkedQueue.cpp"
#endif
```

The method enqueue. Inserting a new node, to which newNodePtr points, at the back of the chain that represents the queue requires three pointer changes: the next pointer in the new node, the next pointer in the current back node, and the outer pointer backPtr. Figure 14-4 illustrates these changes during the addition of an item to a nonempty queue and indicates the order in which they can occur. The statements to perform this addition are

```
newNodePtr->setNext(nullptr);
backPtr->setNext(newNodePtr);
backPtr = newNodePtr;
```

![](img/288a0c22d14d2450c1e772f228f867b0_428_0.png)

The addition of an item to an empty queue is a special case, as Figure 14-5 illustrates. If newNodePtr points to the new node, the following statements add the node to the empty chain:

```
frontPtr = newNodePtr;
backPtr = newNodePtr;
```

These statements easily follow from the realization that the chain has only one node, which is both the first and last node in the chain.

FIGURE 14-5 Adding an item to an empty queue: (a) before enqueue; (b) after enqueue

![](img/288a0c22d14d2450c1e772f228f867b0_429_0.png)

Thus, we have the following definition for the method enqueue:

```
template<class ItemType>
bool LinkedQueue<ItemType>::enqueue(const ItemType& newEntry)
{
   Node<ItemType>* newNodePtr = new Node<ItemType>(newEntry);
   // Insert the new node
   if (isEmpty())
   {
      frontPtr = newNodePtr;        // The queue was empty
   }
   else
   {
      backPtr->setNext(newNodePtr); // The queue was not empty
   }
   backPtr = newNodePtr;           // New node is at back
   return true;
} // end enqueue
```

The method dequeue. Removing the front of the queue involves deleting the first node of the chain. This is an easier operation than removing the last node, which, fortunately, we do not have to do. Figure 14-6 illustrates the removal of the front item from a queue that contains more than one item. Notice that you need to change only the external pointer frontPtr. Removal from a queue of one item is a special case that sets the external pointers backPtr and frontPtr to nullptr.

The following definition of the method dequeue shows how to implement these two cases:

```
template<class ItemType>
bool LinkedQueue<ItemType>::dequeue()
{
   bool result = false;
   if (!isEmpty())
   {
      // Queue is not empty; remove front
      // Node<ItemType>* nodeToDeletePtr = frontPtr;
      if (frontPtr == backPtr)
      {
         // Special case: one node in queue
         frontPtr = nullptr;
         backPtr = nullptr;
      }
      else
      {
         frontPtr = frontPtr->getNext();
         // Return deleted node to system
         nodeToDeletePtr->setNext(nullptr);
         delete nodeToDeletePtr;
         nodeToDeletePtr = nullptr;
      }
      result = true;
   } // end if
   return result;
} // end dequeue
```

FIGURE 14-6 Removing an item from a queue of more than one item

![](img/288a0c22d14d2450c1e772f228f867b0_430_0.png)

**Retrieval.** The method peekFront simply returns the value frontPtr->getItem() after checking that the queue is not empty. We leave the rest of this implementation to you as an exercise. (See Exercises 1 through 3 at the end of this chapter.)

- **Question 1** Why is a tail pointer desirable when you use a chain of linked nodes to implement a queue?
- **Question 2** If you use a circular chain that has only a tail pointer, as Figure 14-3 illustrates, how do you access the data in the first node?
- **Question 3** If the ADT queue had a method clear that removed all entries from a queue, what would its definition be in the previous link-based implementation?

## 14.1.3 An Array-Based Implementation

For applications in which a fixed-sized queue does not present a problem, you can use an array to represent a queue. A naive array-based implementation of a queue might include the following definitions, as Figure 14-7a illustrates:

```
const int MAX_QUEUE = maximum size of queue;
...
ItemType items[MAX_QUEUE]; // Array of queue items
int front; // Index to front of queue
int back; // Index to back of queue
```

![](img/288a0c22d14d2450c1e772f228f867b0_431_0.png)

Here front and back are the indices of the front and back entries, respectively, in the queue. Initially, front is 0 and back is -1. To add a new item to the queue, you increment back and place the item in items[back]. To remove an item, you simply increment front. The queue is empty whenever back is less than front. The queue is full when back equals MAX_QUEUE - 1.

The problem with this strategy is rightward drift—that is, after a sequence of additions and removals, the items in the queue will drift toward the end of the array, making it appear full. In other words, back could equal MAX_QUEUE - 1 even when the queue contains only a few items. Figure 14-7b illustrates this situation.

One possible solution to this problem is to shift array entries to the left, either after each removal from the queue or whenever back equals MAX_QUEUE - 1. This solution guarantees that the queue can always contain up to MAX_QUEUE items. Shifting is not really satisfactory, however, as it would dominate the cost of the implementation.

> **Question 4** Suppose that we change the naive array-based implementation of a queue pictured in Figure 14-7 so that the back of the queue is in items[0]. Although repeated removals from the front would no longer cause rightward drift, what other problem would this implementation cause?

A much more elegant solution is possible by viewing the array as circular, as Figure 14-8 illustrates. To remove an item, you increment the queue index front, and to insert an item, you increment
