# FIGURE 14-3 A circular chain of linked nodes with one external pointer

![](bbox=[0.2, 0.15, 0.65, 0.28])

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
}
```