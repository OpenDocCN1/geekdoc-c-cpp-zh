# # Chapter 20

# ## Case Study: Thread-Safe Queue

This first concurrent programming case study discusses several possible lock-based implementations of a thread-safe first-in-first-out queue. Of particular interest are the contrasts between public and private locks and between single and multiple locks.

# ### 20.1 Queues as Pairs of Lists

One classic design of a first-in-first-out queue uses two functional lists. The idea is to store the state of a queue into two lists: in and out. List out represents the front of the queue, in order, and list in is the back of the queue, in *reverse* order (Figure 20.1). Accordingly, the head of out is the oldest (first-inserted) element of the queue; the head of in is the youngest (last-inserted). Queue elements are removed from the front of list out and added to the front of list in. This way, both lists are used from the head, avoiding inefficient tail-end accesses. When out runs out of elements, you need to reverse in and make it the new out (the new in is then empty). This reversal is amortized over multiple queue operations, resulting in constant-time insertion and removal on average.

![](bbox=[0.333, 0.562, 0.69, 0.642])

**Figure 20.1** FIFO queue implemented as two LIFO lists.

In this chapter, the goal is to write a version of this queue that is safe for multi-threaded usage. The resulting queue will be non-blocking: Adding elements is always possible (unbounded capacity), and elements taken from the queue are returned as options so that taking from an empty queue can return `None`.

> ¹ The alternative is to block a thread on a full queue until elements are removed by other threads and on an empty queue until elements are added by other threads. This requires the use of synchronizers, which are discussed in Chapters 22 and 23. See possible blocking queue implementations in Listings 23.6 to 23.8.