# ABSTRACT DATA TYPE: QUEUE

# DATA

• A finite number of objects, not necessarily distinct, having the same data type and ordered by when they were added.

# OPERATIONS

| PSEUDOCODE | DESCRIPTION |
|---|---|
| isEmpty() | Task: Sees whether this queue is empty.
Input: None.
Output: True if the queue is empty; otherwise false. |
| enqueue(newEntry) | Task: Adds newEntry at the back of this queue.
Input: newEntry.
Output: True if the operation is successful; otherwise false. |
| dequeue() | Task: Removes the front of this queue. That is, removes the item that was added earliest.
Input: None.
Output: True if the operation is successful; otherwise false. |
| peekFront() | Task: Returns the front of this queue. That is, gets the item that was added earliest. The operation does not change the queue.
Input: None.
Output: The front of the queue. |

Figure 13-2 illustrates the effect of these operations on a queue of integers. Notice that enqueue adds an item at the back of the queue and that peekFront looks at the item at the front of the queue, whereas dequeue removes the item at the front of the queue.

# FIGURE 13-2 Some queue operations

| Operation | Queue after operation |
|---|---|
| aQueue = an empty queue | |
| aQueue.enqueue(5) | 5 |
| aQueue.enqueue(2) | 5 2 |
| aQueue.enqueue(7) | 5 2 7 |
| aQueue.peekFront() | 5 2 7 (Returns 5) |
| aQueue.dequeue() | 2 7 |
| aQueue.dequeue() | 7 |
| aQueue.dequeue() | |

**Question 1** If you add the letters A, B, C, and D in sequence to a queue of characters and then remove them, in what order will they leave the queue?