
## FIGURE 14-11 A more time-efficient circular implementation: (a) a full queue; (b) an empty queue

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_436_0.png)

array location and let front be the index of the location before the front of the queue. As Figure 14-11 illustrates, the queue is full if front equals (back + 1) % (MAX_QUEUE + 1) but the queue is empty if front equals back

Using an extra array location is more time efficient

This approach does not have the overhead of maintaining a counter or boolean variable, and so is more efficient of time. Programming Problems 3 and 4 discuss these two alternate implementations further.

## 14.1.4 Comparing Implementations

We have suggested implementations of the ADT queue that store the queue's entries in either an instance of the ADT list, a chain of linked nodes that has both a head pointer and a tail pointer, a circular chain that has only one external pointer, an array, or a circular array. You have seen the details of three of these implementations. All of our implementations of the ADT queue are ultimately either array based or link based.

The reasons for making the choice between array-based and link-based implementations are the same as those discussed in earlier chapters. The discussion here is similar to the one in Section 4.5 of Chapter 4. We repeat the highlights here in the context of queues.

### Fixed size

An implementation based on a statically allocated array prevents the enqueue operation from adding an item to the queue if the array is full. Such a queue is appropriate for many data structures, such as buffers, within an operating system.

### Dynamic size

If this restriction is not acceptable, you must use either a dynamically allocated array or a link-based implementation.

### Reuse of an already implemented class saves you time

Suppose that you decide to use a link-based implementation. Should you choose the implementation that uses a linked chain or the one that uses a link-based implementation of the ADT list? Because a linked chain actually represents the items in the ADT list, using the ADT list to represent a queue is not as efficient as using a linked chain directly. However, the ADT list approach is much simpler to write. If you decide to use a linked chain instead of the ADT list to represent the queue, should you use a linear chain or a circular chain? We leave this question for you to answer in Programming Problem 1.

## 14.2 An Implementation of the ADT Priority Queue

While we could place the entries of a priority queue into either an array or a chain of linked nodes, doing so would be like implementing the ADT sorted list, which we did in Chapter 12. Rather than repeating those implementations, we can use a sorted list to contain the entries of a priority queue. The header file in Listing 14-6 defines a class of priority queues that has as a private data member an instance of the class LinkedSortedList, as given in Listing 12-2 of Chapter 12.

```
LISTING 14-6 A header file for the class SL_PriorityQueue.
/* ADT priority queue: ADT sorted list implementation.
@file SL_PriorityQueue.h */
#ifndef _PRIORITY_QUEUE
#define _PRIORITY_QUEUE
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
   /* @throw PrecondViolatedExcep if priority queue is empty. */
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
{
    slistPtr->insertSorted(newEntry);
    return true;
} // end add
template<class ItemType>
bool SL_PriorityQueue<ItemType>::remove()
{
    // The highest-priority item is at the end of the sorted list
    return slistPtr->remove(slistPtr->getLength());
} // end remove
```

We will leave the remainder of this implementation to you as an exercise. Note, however, that we will discuss a more time-efficient implementation in Chapter 17, when we introduce the ADT heap.

Question 6 Define the method peek for the sorted list implementation of the ADT priority queue.

## SUMMARY

- 1. The enqueue and dequeue operations for a queue require efficient access to both ends of the queue. Therefore, a link-based implementation of a queue uses a linear linked chain that has both a head pointer and a tail pointer. Alternatively, you can use a circular linked chain.

- 2. An array-based implementation of a queue is prone to rightward drift. This phenomenon can make a queue look full when it really is not. Shifting the items in the array is one way to compensate for rightward drift. A more efficient solution uses a circular array.

- 3. If you use a circular array to implement a queue, you must be able to distinguish between the queue-full and queue-empty conditions. You can make this distinction by counting the number of items in the queue, using a boolean variable isFull, or leaving one array location empty.

- 4. You can use an array, a chain of linked nodes, or a sorted list to contain the entries in a priority queue. A more time-efficient implementation is possible by using the ADT heap, which we will consider later in this book.

## EXERCISES

- 1. Implement the copy constructor for the class LinkedQueue that is declared in Listing 14-3. Hint: Look at the copy constructor for the ADT stack in Listing 7-4 of Chapter 7.

- 2. Repeat the previous exercise, but implement a memory-safe copy constructor instead. If a memory allocation fails, this constructor should release all memory that was allocated prior to the failure and then throw an exception.

- 3. The destructor for the class LinkedQueue that is declared in Listing 14-3 could repeatedly call dequeue. Although easy to write, this destructor can be inefficient due to repeated method calls. Write another implementation for the destructor that deallocates the linked chain directly without calling dequeue.

- 4. An operation that displays the contents of a queue can be useful during program debugging. Add a display operation to the ADT queue such that display assumes and uses the link-based implementation of the ADT queue.

- 5. Consider a method called getNumberOfElements that returns the number of elements in a queue without changing the queue. The return type is int, and it does not accept any parameters.

  - a. Add getNumberOfElements to the array-based ADT queue given in this chapter.
  - b. Add getNumberOfElements to the link-based ADT queue given in this chapter.

- 6. Show that the implementation of a queue that uses an extra array element as described in Section 14.1.3 is more efficient than the counter variation, even though it appears to perform two extra additions in the test:

front equals (back + 1) % (MAX_QUEUE + 1)

- 7. Consider the class ListQueue that implements the ADT queue by using the ADT list to represent the items in the queue. Discuss the efficiency of the queue's enqueue and dequeue operations when the ADT list's implementation is

  - a. Array based
  - b. Link based

- 8. The class ListQueue, as given in Listing 14-1, maintains the queue's front at the end of a list of the queue's entries and has the back of the queue at the beginning of that list. Note that the list is an object of the class LinkedList. What is the impact on the efficiency of the operations enqueue and dequeue if we were to maintain the queue's front at the beginning of the list and the queue's back at the list's end?

- 9. Complete the implementation of the class SL_PriorityQueue, as described in Section 14.2.

- 10. Implement the class SL_PriorityQueue, assuming that low values indicate a higher priority. Such a priority queue is useful within operating systems and other similar applications. When the underlying sorted list has a link-based implementation, using the lowest value for the highest priority makes the priority queue operations more efficient. Describe why this benefit is true.

## PROGRAMMING PROBLEMS

- 1. Write a link-based implementation of a queue that uses a circular linked chain to represent the items in the queue. You will need a single tail pointer. When you are done, compare your implementation to the one given in this chapter that uses a linear linked chain with two external pointers. Which implementation is easier to write? Which is easier to understand? Which is more efficient?

- 2. Write an array-based implementation of a queue that uses a resizable, circular array to represent the items in the queue.

- 3. Revise the array-based implementation of a queue given in this chapter. Instead of counting the number of items in the queue, use a boolean variable isFull to distinguish between the full and empty conditions.

- 4. This chapter described another array-based implementation of a queue that uses no special data member—such as count or isFull (see the previous programming problem)—to distinguish between the full and empty conditions. In this implementation, you declare MAX_QUEUE + 1 locations for the array items, but use only MAX_QUEUE of them for queue items. You sacrifice one array location by making front the index of the location before the front of the queue. The queue is full if front equals (back + 1) % (MAX_QUEUE + 1), but the queue is empty if front equals back. Implement this array-based approach.

- 5. Exercise 9 in the previous chapter defined the double-ended queue, or deque. Implement the ADT deque by using a circular array to contain the items in the deque.

- 6. Repeat the previous programming problem, but maintain the deque's entries in a linked chain.

- 7. Implement the ADT deque, as described in Exercise 9 of the previous chapter, as a derived class of ArrayQueue, as given in Listings 14-4 and 14-5.
