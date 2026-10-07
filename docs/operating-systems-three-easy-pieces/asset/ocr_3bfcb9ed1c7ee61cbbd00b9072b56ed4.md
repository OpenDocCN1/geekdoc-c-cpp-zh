# LOCK-BASED CONCURRENT DATA STRUCTURES

> TIP: BE WARY OF LOCKS AND CONTROL FLOW
A general design tip, which is useful in concurrent code as well as else-where, is to be wary of control flow changes that lead to function returns, exits, or other error conditions that halt the execution of a function. Because many functions will begin by acquiring a lock, allocating some memory, or doing similar operations, when errors arise, the code has to undo all of the state before returning, which is errorprone. Thus, it is best to structure code to minimize this.

Conceptually, a hand-over-hand linked list makes some sense; it enables high degree of concurrency in list operations. However, in practice, it is to make such a structure faster than the single lock approach, the overheads of acquiring and releasing locks for each node of a traversal is prohibitive. With very large lists, and a large number of threads, the concurrency enabled by allowing ongoing traversals, performing an operation, and releasing it. Perhaps some kind of hybrid (where you grab a new lock every so nodes) would be worth investigating.

# 29.3 Concurrent Queues

As you know by now, there is always a standard method to make a concurrent data structure: add a lock. For a queue, we will skip that approach, assuming you can figure it out.

Instead, we take a look at a slightly more concurrent queue designed by Michael and Scott [MS98]. The data structures and code used for this queue are found in Figure 29.9 on the following page.

If you study this queue carefully, you'll notice that there are two locks, one for the head of the queue, and one for the tail. The goal of these two locks is to enable concurrency of enqueue and dequeue operations. In the common case, the enqueue routine will only access the tail lock, and dequeue only the head lock.

One trick used by Michael and Scott is to add a dummy node (allocated in the queue initialization code); this dummy separates the head and tail operations. Study the code, or better yet, type it in, run it, and measure it, to understand how it works.

Queues are commonly used in multi-threaded applications. However, the type of queue used (with just locks) often does not meet the needs of such programs. A more fully developed bounded queue, that enables a thread to wait if the queue is empty or overly full, is the subject of intense study in the next chapter on condition variables. Watch for it!