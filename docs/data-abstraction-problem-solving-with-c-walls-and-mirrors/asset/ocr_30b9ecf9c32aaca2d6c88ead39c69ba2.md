# 14.2 An Implementation of the ADT Priority Queue

While we could the entries of a priority queue into either an array or a chain of linked nodes, doing so would be like implementing the ADT sorted list, which we did in Chapter 12. Rather than repeating operations, we use a sorted list to contain the entries of a priority queue. The header file in Listing 14-6 defines a class of priority queues that has a private data member an instance of the class LinkedSortedList, as given in Listing 12-2 of Chapter 12.

LISTING 14-6 A header file for the class SL_PriorityQueue.
```cpp
/** ADT priority queue: ADT sorted list implementation.
 * @file SL_PriorityQueue.h */
#ifndef PRIORITY_QUEUE
#define PRIORITY_QUEUE

#include "PriorityQueueInterface.h"
#include "LinkedSortedList.h"
#include "PreViolatedException.h"

template<class ItemType>
class SL_PriorityQueue : public PriorityQueueInterface<ItemType>
{
private:
    LinkedSortedList<ItemType>* listPtr; // Pointer to sorted list of
// items in the priority queue

public:
    SL_PriorityQueue();
    SL_PriorityQueue(const SL_PriorityQueue& pq);
    ~SL_PriorityQueue();
    bool isEmpty() const;
    bool add(const ItemType& newEntry);
    bool remove();

    /** @throws PreViolatedException if priority queue is empty. */
    ItemType peek() const (PreViolatedException);
}; // end SL_PriorityQueue
#include "SL_PriorityQueue.cpp"
#endif
```

Before we implement the class SL_PriorityQueue, we need to consider how the sorted list behaves. LinkedSortedList maintains the entries in a sorted order. It does so by comparing the entries with each other. For a priority queue, we want these comparisons to be based on the priorities of the entries. Let's assume that each entry is an object that has its priority as a data member. You will learn in C++15 how to make a comparison operator, such as >, base its comparison on specific aspects of its operands. For now, let's assume that the comparisons are made according to priority. Note that the highest-priority can be the largest or the smallest value, according to the application at hand.

To give you an idea of how to implement this class, let's look at the definitions of the add and remove operations:

```
template<class ItemType>
bool SL_PriorityQueue<ItemType>::add(const ItemType& newEntry)
```