# 14.2 An Implementation of the ADT Priority Queue

While we could place the entries of a priority queue into either an array or a chain of linked nodes, doing so would be like implementing the ADT sorted list, which we did in Chapter 12. Rather than repeating those implementations, we can use a sorted list to contain the entries of a priority queue. The header file in Listing 14-6 defines a class of priority queues that has as a private data member an instance of the class LinkedSortedList, as given in Listing 12-2 of Chapter 12.

```
LISTING 14-6 A header file for the class SL_PriorityQueue.

/* ADT priority queue: ADT sorted list implementation.
@file SL_PriorityQueue.h */
#ifndef SL_PRIORITY_QUEUE_
#define SL_PRIORITY_QUEUE_

#include "PriorityQueueInterface.h"
#include "LinkedSortedList.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class SL_PriorityQueue : public PriorityQueueInterface<ItemType>
{
private:
   LinkedSortedList<ItemType>* slistPtr; // Pointer to sorted list of
                                      // items in the priority queue
public:
   SL_PriorityQueue();
   SL_PriorityQueue(const SL_PriorityQueue& pq);
   ~SL_PriorityQueue();
   bool isEmpty() const;
   bool add(const ItemType& newEntry);
   bool remove();
   //@throw PrecondViolatedExcep if priority queue is empty.
   ItemType peek() const throw(PrecondViolatedExcep);
}; // end SL_PriorityQueue

#include "SL_PriorityQueue.cpp"
#endif
```

Before we can implement the class SL_PriorityQueue, we need to consider how the sorted list behaves. LinkedSortedList maintains the entries in a sorted list in sorted order. It does so by comparing the entries with each other. For a priority queue, we want these comparisons to be based on the priorities of the entries. Let's assume that each entry is an object that has its priority as a data member. You will learn in C++ Interlude 5 how to make a comparison operator, such as >, base its comparison on specific aspects of its two operands. For now, let's assume that the comparisons are made according to priority. Note that the highest-priority value can be either the largest value or the smallest value, according to the application at hand.

To give you an idea of how to implement this class, let's look at the definitions of the add and remove operations:

```
template<class ItemType>
bool SL_PriorityQueue<ItemType>::add(const ItemType& newEntry)
```