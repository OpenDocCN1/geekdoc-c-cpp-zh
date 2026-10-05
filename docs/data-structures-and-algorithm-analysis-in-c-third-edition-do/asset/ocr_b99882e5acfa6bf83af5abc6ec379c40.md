on the stack a description of the initial problem for n rings. The rest of the function is simply a while loop that pops the stack and executes the appropriate operation. In the case of a TOH operation (for n > 0), we store on the stack representations for the three operations executed by the recursive function. However, these operations must be placed on the stack in reverse order, so that they will be popped off in the correct order.

Recursive algorithms lend themselves to efficient implementation with a stack when the amount of information needed to describe a sub-problem is small. For example, Section 7.5 discusses a stack-based implementation for Quicksort.

# 4.3 Queues

Like the stack, the queue is a list-like structure that provides restricted access to its elements. Queue elements may only be inserted at the back (called an enqueue operation) and removed from the front (called a dequeue operation). Queues operate like standing in a movie theater ticket counter. If nobody cheats, then newcomers go to the back of the line. The person at the front of the line is the next to be served. Thus, queues release their elements in order of arrival. Accountants have used queues long before the existence of computers. They call a queue “FIFO” list, which stands for “First-In, First-Out.” Figure 4.23 shows a sample queue AD. Array-based queue and linked queue.

# 4.3.1 Array-Based Queues

The array-based queue is somewhat tricky to implement effectively. A simple version of the array-based list implementation is not efficient.

Assume that there are n elements in the queue. By analogy to the array-based list implementation, we would require that all elements of the queue be stored in the first n positions of the array. If the rear element of the queue to be in position 0, then dequeue operations require only Θ(1) time because the front of the queue (the one being removed) is the last element in the array. However, enqueue operations will require Θ(n) time, because the n elements currently in the queue must be shifted one position in the array. If instead we chose the rear element of the queue to be in position n - 1, then an enqueue operation is equivalent to an append operation on a list. This requires only Θ(1) time. But now, a dequeue operation requires Θ(n) time, because all of the elements must be shifted down by one position to retain the property that the remaining n - 1 elements reside in the first n - 1 positions of the array.

> In Britain, a line of people is called a “queue,” and getting into line to wait for service is called “queuing up.”