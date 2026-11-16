allow indexing via array subscripting.

# EFFICIENCY: LINKED LIST OR VECTOR?

In cases where each individual element in the collection is small (less than 64 bytes), a vector almost always outperforms a linked list. This is because of the way a CPU accesses memory.

Reading values from memory is very slow for the CPU, so when it needs to read a value from memory, it also loads neighboring values into a high-speed cache. Because elements in a vector are contiguous in memory, accessing an element at a specific index also loads its neighboring indices into the cache.

However, because elements in a linked list are not contiguous, loading one element also loads unrelated memory into the cache. Thus, operations such as looping over an entire collection are much more efficient with a vector than with a linked list, even though both operations have a time complexity of O(n).

# Queues

A queue exhibits **first-in, first-out (FIFO)** behavior, much like waiting in a line at a store. With a queue, you cannot remove elements in any arbitrary order. With a queue, you must remove elements in the same order in which they were added. Although many books use **enqueue** to reference insertion into a queue and **dequeue** to reference removal from a queue, the implementation of `std::queue` uses `push` (or `emplace`) for insertion and `pop` for removal. To access the element at the front of the queue, use `front`.

The following code inserts three elements into a queue and then removes each element from the queue, outputting the values:

Click here to view code image