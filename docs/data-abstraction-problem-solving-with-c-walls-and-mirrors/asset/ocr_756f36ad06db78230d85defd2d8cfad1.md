# 410 CHAPTER 14 Queue and Priority Queue Implementations

FIGURE 14-11 A more time-efficient circular implementation: (a) a full queue; (b) an empty queue

![](bbox=[0.343, 0.153, 0.813, 0.368])

array location and let front be the index of location before the front of the queue. As Figure 14-11 illustrates, the queue is if

front equals (back + 1) % (MAX_QUEUE + 1)

but the queue is empty if

front equals back

This approach does not have the overhead of maintaining a counter or boolean variable, and so is more efficient of time. Programming Problems 3 and 4 discuss these two alternate implementations further.

# 14.1.4 Comparing Implementations

We have discussed implementations of the ADT queue that stores the queue's entries in an instance of the ADT list, a chain of linked nodes that has both a head pointer and a tail pointer, a circular array that has only one external pointer, an array, or a circular array. We have seen the details of three of these implementations. All of our implementations of the ADT queue are either array-based or linked based.

The reasons for making the choice between array-based and linked-based implementations are the same as those discussed in earlier chapters. This discussion is here in Section 4.5 of Chapter 4. We repeat the highlights in the context of queues.

An implementation on a statically allocated array prevents the enqueue operation from adding an item to the queue if the array is full. Such a queue is appropriate for many data structures, as buffers, within an operating system. If this restriction is not acceptable, you must use either a dynamically allocated array or a linked-based implementation.

Suppose you decide to use a linked-based implementation. Should you choose the implementation that uses a linear chain or the linked implementation of the ADT list? A linked chain actually represents the items in the ADT list, but using the ADT list to represent a queue is not as efficient as a linked chain. However, the ADT list is much simpler to write. If you decide to use a linked chain instead of the ADT list to represent the queue, you should use a linear chain or a circular chain? We leave this question for you to answer in Programming Problem 1.