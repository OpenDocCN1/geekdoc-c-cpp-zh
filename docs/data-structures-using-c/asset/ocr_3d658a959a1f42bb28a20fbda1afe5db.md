A queue implemented using an array has many disadvantages, as arrays provide static declaration and hence are less flexible with respect to run-time changes in the size of the queue. We shall discuss the implementation of queues using a linked list, which overcomes these drawbacks, in Chapter 6.

# RECAPITULATION

+   * A queue is an ordered list where all insertions are done at one end called the rear and deletions at another end called the front. These limits guarantee that the data is processed in the sequence in which it is entered. In short, a queue is a first in first out (FIFO) or last in last out (LILO) structure.
+   * A queue is a linear data structure as it can be implemented using the help of arrays (using static memory allocation) or linked lists (using dynamic memory allocation). An array insertion and deletion of data elements. In addition, it uses static memory allocation so that it can store a fixed number of elements. Hence, array implementation is not suitable for frequent insertions and deletions.
+   * These drawbacks can be avoided by implementing the queue using a circular array. In a circular queue, as we go on adding elements to the queue and reach the end of the array, the next element is stored in the first slot of the array if it is free.
+   * There are variations of queues such as circular queue, multi-queues, and deque. Deque defines a data structure where elements can be added or deleted at either the front end or the rear end but no changes can be made elsewhere in the list.
+   * Queues are used in many applications such as simulation, priority queue, job queue, and so on. Priority queues are those in which we can insert or delete elements from any position based on some fundamental ordering with respect to the priorities of the elements.

# KEY TERMS

+   * **Add** This operation adds an element at the rear of the queue if the queue is not full. This operation is also named as *enqueue* and *insert*.
+   * **Circular queue** The technique that essentially allows the queues to wrap around upon reaching the end of the array is called a circular queue.
+   * **Delete** This operation deletes an element from the front of the queue and returns the same. This operation is also named as *dequeue*.
+   * **Deque** The word *deque* is a short form of double-ended queue. It is pronounced as "deck". Deque defines a data structure where elements can be added or deleted at either the front end or the rear end, but no changes can be made elsewhere in the list. Thus, a deque is a generalization of both a stack and a queue.
+   * **FIFO** A queue is a first in first out (FIFO) or last in last out (LILO) structure to guarantee that the data are processed in the sequence in which they are entered.
+   * **Multi-queue** If more number of queues is required to be implemented, then an efficient data structure to handle multiple queues is required. It is possible to utilize all the available space in a single array. When more than two queues, say n, are represented sequentially, we can divide the available memory into n segments and allocate these segments to n queues, one each.