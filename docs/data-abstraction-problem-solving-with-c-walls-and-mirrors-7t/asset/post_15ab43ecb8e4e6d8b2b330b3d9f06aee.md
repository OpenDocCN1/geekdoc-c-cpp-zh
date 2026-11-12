
### FIGURE 14-8 A circular array as an implementation of a queue

![](img/288a0c22d14d2450c1e772f228f867b0_432_0.png)

back. Figure 14-9 illustrates the effect of a sequence of three queue operations on front, back, and the array. Notice that front and back “advance” clockwise around the array.

When either front or back advances past MAX_QUEUE - 1, it should wrap around to 0. This wraparound eliminates the problem of rightward drift, which occurred in the previous naive implementation, because here the circular array has no end. You obtain the wraparound effect of a circular queue by using modulo arithmetic (that is, the C++ % operator) when incrementing front and back. For example, you can add newEntry to the queue by using the statements

```
Adding to a queue
back = (back + 1) % MAX_QUEUE;
items[back] = newEntry;
```

Notice that if back equaled MAX_QUEUE - 1 before the addition of newEntry, the first statement, back = (back + 1) % MAX_QUEUE, would have the effect of wrapping back around to index 0. Similarly, you can remove the entry at the front of the queue by using the statement

```
Deleting from a queue
front = (front + 1) % MAX_QUEUE;
```

To initialize the queue, you set front to 0 and back to MAX_QUEUE - 1.

### FIGURE 14-9 The effect of three consecutive operations on the queue in Figure 14-8

![](img/288a0c22d14d2450c1e772f228f867b0_432_1.png)

### FIGURE 14-10 (a) front passes back when the queue becomes empty; (b) back catches up to front when the queue becomes full

![](img/288a0c22d14d2450c1e772f228f867b0_433_0.png)

The only difficulty with this scheme is detecting when the queue is empty or full. It seems reasonable to select as the queue-empty condition

**front is one slot ahead of back**

front and back cannot be used to distinguish between queue-full and queue-empty conditions

By counting queue items, you can detect queue-full and queue-empty conditions

as this appears to indicate that front “passes” back when the queue becomes empty, as Figure 14-10a depicts. However, it is also possible that this condition signals a full queue: Because the queue is circular, back might in fact “catch up” with front as the queue becomes full. Figure 14-10b illustrates this situation.

Obviously, you need a way to distinguish between the two situations. One way is to keep a count of the number of items in the queue. Before adding an item to the queue, you check whether the count is equal to MAX_QUEUE; if it is, the queue is full. Before removing an item from the queue, you check whether the count is equal to zero; if it is, the queue is empty.

**The header file.** Listing 14-4 contains the header file for an array-based implementation of the ADT queue that uses a circular array as just described. Because the data is stored in statically allocated memory, the compiler-generated destructor and copy constructor are sufficient.1

1 If you use a dynamically allocated array, you must provide a destructor and copy constructor.

```
LISTING 14-4 The header file for the class ArrayQueue

/** ADT queue: Circular array-based implementation.
#file ArrayQueue.h */
#ifndef _ARRAY_QUEUE
#define _ARRAY_QUEUE
#include "QueueInterface.h"
#include "PrecondViolatedExcep.h"

const int MAX_QUEUE = 50;

template<class ItemType>
class ArrayQueue : public QueueInterface<ItemType>
{
private:
   ItemType items[MAX_QUEUE]; // Array of queue items
   int front;                 // Index to front of queue
   int back;                  // Index to back of queue
   int count;                 // Number of items currently in the queue

public:
   ArrayQueue();
   // Copy constructor and destructor supplied by compiler
   bool isEmpty() const;
   bool enqueue(const ItemType& newEntry);
   bool dequeue();
   /** @throw PrecondViolatedExcep if queue is empty. */
   ItemType peekFront() const throw(PrecondViolatedExcep);
}; // end ArrayQueue
#include "ArrayQueue.cpp"
#endif
```

The implementation file. Listing 14-5 contains the definitions of ArrayQueue's methods as they appear in the implementation file.

```
LISTING 14-5 The implementation file for the class ArrayQueue

/** ADT queue: Circular array-based implementation.
#file ArrayQueue.cpp */
#include "ArrayQueue.h"   // Header file

template<class ItemType>
ArrayQueue<ItemType>::ArrayQueue() : front(0), back(MAX_QUEUE - 1), count(0)
{  } // end default constructor

template<class ItemType>
bool ArrayQueue<ItemType>::isEmpty() const
{
   return count == 0;
} // end isEmpty
```

```
template<class ItemType>
bool ArrayQueue<ItemType>::enqueue(const ItemType& newEntry)
{
   bool result = false;
   if (count < MAX_QUEUE)
   // Queue has room for another item
   back = (back + 1) % MAX_QUEUE;
   items[back] = newEntry;
   count++;
   result = true;
   } // end if

   return result;
} // end enqueue

template<class ItemType>
bool ArrayQueue<ItemType>::dequeue()
{
   bool result = false;
   if (!isEmpty())
   {
   front = (front + 1) % MAX_QUEUE;
   count--;
   result = true;
   } // end if

   return result;
} // end dequeue

template<class ItemType>
ItemType ArrayQueue<ItemType>::peekFront() const
throw(PrecondViolatedExcep)
{
   // Enforce precondition
   if (isEmpty())
   throw PrecondViolatedExcep("peekFront() called with empty queue");

   // Queue is not empty; return front
   return items[front];
   // end peekFront
}
```

Question 5 If the ADT queue had a method clear that removed all entries from a queue, what would its definition be in the previous array-based implementation?

Variations. Several commonly used variations of the previous circular-array approach do not require a count of the number of entries in the queue. One approach uses a boolean variable isFull to distinguish between the full and empty conditions. The expense of maintaining this variable is about the same as that of maintaining a counter, however. An isFull flag can replace the counter. A faster implementation declares MAX_QUEUE + 1 locations for the array items, but uses only MAX_QUEUE of them for queue items. You sacrifice one

### FIGURE 14-11 A more time-efficient circular implementation: (a) a full queue; (b) an empty queue

![](img/288a0c22d14d2450c1e772f228f867b0_436_0.png)

array location and let front be the index of the location before the front of the queue. As Figure 14-11 illustrates, the queue is full if

```
front equals (back + 1) % (MAX_QUEUE + 1)
```

but the queue is empty if

```
front equals back
```

Using an extra array location is more time efficient

This approach does not have the overhead of maintaining a counter or boolean variable, and so is more efficient of time. Programming Problems 3 and 4 discuss these two alternate implementations further.

## 14.1.4 Comparing Implementations

We have suggested implementations of the ADT queue that store the queue's entries in either an instance of the ADT list, a chain of linked nodes that has both a head pointer and a tail pointer, a circular chain that has only one external pointer, an array, or a circular array. You have seen the details of three of these implementations. All of our implementations of the ADT queue are ultimately either array based or link based.

The reasons for making the choice between array-based and link-based implementations are the same as those discussed in earlier chapters. The discussion here is similar to the one in Section 4.5 of Chapter 4. We repeat the highlights here in the context of queues.

Fixed size dynamic size

An implementation based on a statically allocated array prevents the enqueue operation from adding an item to the queue if the array is full. Such a queue is appropriate for many data structures, such as buffers, within an operating system. If this restriction is not acceptable, you must use either a dynamically allocated array or a link-based implementation.

**Reuse of an already implemented class saves you time**

Suppose that you decide to use a link-based implementation. Should you choose the implementation that uses a linked chain or the one that uses a link-based implementation of the ADT list? Because a linked chain actually represents the items in the ADT list, using the ADT list to represent a queue is not as efficient as using a linked chain directly. However, the ADT list approach is much simpler to write.

If you decide to use a linked chain instead of the ADT list to represent the queue, should you use a linear chain or a circular chain? We leave this question for you to answer in Programming Problem 1.
