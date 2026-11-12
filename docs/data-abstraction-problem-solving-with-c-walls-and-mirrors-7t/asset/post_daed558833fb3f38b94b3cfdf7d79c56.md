
Processing a departure event at time: 30
Processing a departure event at time: 35
Processing a departure event at time: 40
Processing a departure event at time: 45
Processing a departure event at time: 50
Processing an arrival event at time: 88
Processing a departure event at time: 91
Simulation Ends

Final Statistics:
Total number of people processed: 10
Average amount of time spent waiting: 5.6

- 7. Modify and expand the event-driven simulation program that you wrote in Programming Problem 6.

  - a. Add an operation that displays the event list, and use it to check your hand trace in Exercise 11.

  - b. Add some statistics to the simulation. For example, compute the maximum wait in line, the average length of the line, and the maximum length of the line.

  - c. Modify the simulation so that it accounts for three tellers, each with a distinct line. You should keep in mind that there should be

    - Three queues, one for each teller
    - A rule that chooses a line when processing an arrival event (for example, enter the shortest line)
    - Three distinct departure events, one for each line
    - Rules for breaking ties in the event list

Run this simulation and the original simulation on several sets of input data. How do the statistics compare?

  - d. The bank is considering the following change: Instead of having three distinct lines (one for each teller), there will be a single line for the three tellers. The person at the front of the line will go to the first available teller. Modify the simulation of part c to account for this variation. Run both simulations on several sets of input data. How do the various statistics compare (averages and maximums)? What can you conclude about having a single line as opposed to having distinct lines?

- 8. The people who run the Motor Vehicle Department (MVD) have a problem. They are concerned that people do not spend enough time waiting in lines to appreciate the privilege of owning and driving an automobile. The current arrangement is as follows:

  - When people walk in the door, they must wait in a line to sign in.
  - Once they have signed in, they are told either to stand in line for registration renewal or to wait until they are called for license renewal.
  - Once they have completed their desired transaction, they must go and wait in line for the cashier.
  - When they finally get to the front of the cashier's line, if they expect to pay by check, they are told that all checks must get approved. To do this, it is necessary to go to the check-approver's table and then reenter the cashier's line at the end.

Write an event-driven simulation to help the MVD gather statistics. Each line of input will contain

  - A desired transaction code (L for license renewal, R for registration renewal)
  - A method-of-payment code ($ for cash, C for check)
  - An arrival time (integer)
  - A name

Write out the specifics of each event (when, who, what, and so on). Then display these final statistics:

  - The total number of license renewals and the average time spent in MVD (arrival until completion of payment) to renew a license
  - The total number of registration renewals and the average time spent in MVD (arrival until completion of payment) to renew a registration

Incorporate the following details into your program:

  - Define the following events: arrive, sign in, renew license, renew registration, and cope with the cashier (make a payment or find out about check approval).
  - In the case of a tie, let the order of events be determined by the list of events just given—that is, arrivals have the highest priority.
  - Assume that the various transactions take the following amounts of time:

| Transaction | Time |
|---|---|
| Sign in | 10 seconds |
| Renew license | 90 seconds |
| Register automobile | 60 seconds |
| See cashier (payment) | 30 seconds |
| See cashier (check not approved) | 10 seconds |

  - As ridiculous as it may seem, the people waiting for license renewal are called in alphabetical order. Note, however, that people are not pushed back once their transactions have started.
  - For the sake of this simulation, you can assume that checks are approved instantly. Therefore, the rule for arriving at the front of the cashier's line with a check that has not been approved is to go to the back of the cashier's line with a check that has been approved.

*This page intentionally left blank*

## Queue and Priority Queue Implementations

## Chapter 14

### Contents

- 14.1 Implementations of the ADT Queue. 397
- 14.1.1 An Implementation That Uses the ADT List 398
- 14.1.2 A Link-Based Implementation 400
- 14.1.3 An Array-Based Implementation 405
- 14.1.4 Comparing Implementations 410
- 14.2 An Implementation of the ADT Priority Queue 411
- Summary 412
- Exercises 412
- Programming Problems 413

### Prerequisites

Chapter 13 Queues and Priority Queues

The previous chapter discussed the ADT queue at length and introduced the ADT priority queue. This chapter will present several implementations of the queue and compare their advantages and disadvantages.

We will consider an implementation of the priority queue, but we can write a much more efficient implementation later, after we explore the ADT heap in Chapter 17.

### 14.1 Implementations of the ADT Queue

Like stacks, queues can have an array-based or a link-based implementation. However, we also can use an implementation of the ADT list to define a class of queues. Such a class is easy to write, as most of the work is done by the class of lists. If you needed a class of queues right away, you could use this approach. The result would not be as time efficient as possible, however.

We will begin by using an instance of the class LinkedList, as given in Listing 9-2 of Chapter 9, to store the queue's entries. We will then write a link-based implementation, as it is a bit more straightforward than the array-based one, which we will investigate last.

### 14.1.1 An Implementation That Uses the ADT List

You can use the ADT list to contain the items in a queue. This approach is especially useful if you need to define a class of queues quickly and already have a class of lists. Figure 14-1 illustrates such a queue. If the item in position 1 of a list represents the front of the queue, you can implement the method dequeue as the list operation remove(1) and the method peekFront as the list operation getEntry(1). Similarly, if you let the item at the end of the list represent the back of the queue, you can implement the operation enqueue(newEntry) as the list operation insert(getLength() + 1, newEntry).

![](img/288a0c22d14d2450c1e772f228f867b0_424_0.png)

The header file containing such a class definition for the ADT queue appears in Listing 14-1, and the implementation file is in Listing 14-2.

```
LISTING 14-1 The header file for the class ListQueue

/** ADT queue: ADT list implementation.
@file ListQueue.h */

#ifndef _LIST_QUEUE
#define _LIST_QUEUE

#include "QueueInterface.h"
#include "LinkedList.h"
#include "PrecondViolatedExcep.h"

template<class ItemType>
class ListQueue : public QueueInterface<ItemType>
{
private:
   LinkedList<ItemType>* listPtr; // Pointer to list of queue items
public:
   ListQueue();
   ListQueue(const ListQueue& aQueue);
   ~ListQueue();
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
