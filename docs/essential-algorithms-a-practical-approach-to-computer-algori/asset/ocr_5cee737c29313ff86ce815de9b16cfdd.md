# Appendix A ■ Summary of Algorithmic Concepts 479

# Chapter 4: Arrays

Array is a contiguous piece of memory that holds items.
Array packing—You can pack items into a piece of memory by mapping array indices to memory locations. For example, to save space you may need a triangular array by mapping indices in the triangular array into a one-dimensional array. Similarly, you can make arrays with nonzero lower bounds by mapping the bounds to a regular zero-based array.

Sparse arrays—You can use linked structures to build space-efficient sparse arrays or matrices.

# Chapter 5: Stacks and Queues

A stack is a data structure that provides last-in-first-out(LIFO) access to items. You can implement a stack in a linked list or array, although you may need to resize the array if it becomes full.
– queue is a data structure that provides first-in-first-out (FIFO) access to items. You can implement a stack in a linked list or circular array, although you may need to resize the array if it becomes full.
– priority queue, items are retrieved in priority order.
Pronounced “deck,” a deque is a queue that allows you to add or remove items from either end.
– Uses—Other algorithms use stacks and queues to hold items while they are being processed.

# Chapter 6: Sorting

Insertion—As in insertionsort, the algorithm takes an item and inserts it into the correct position in some data structure.
– Selection—As in selectsort, the algorithm examines the items that have not yet been processed, finds the best one at that moment, and adds it to some data structure.
– Decreasing range—As in bubblesort, the algorithm keeps track of the range of interest and restricts that range over time to reduce the number of items it must consider.
– A heap is a tree in which every node has value at least as large as its children's values. A heap can be used as a priority queue.
– Storing a complete tree—An algorithm can store a complete tree in an array.
Divide and conquer—An algorithm breaks the problem into smaller pieces and solves the pieces, usually recursively.
– Randomization—Quicksort can use randomization to reduce worstcase behavior because of items initially in a particular order. (This doesn't protect it if there are many duplicate items.)