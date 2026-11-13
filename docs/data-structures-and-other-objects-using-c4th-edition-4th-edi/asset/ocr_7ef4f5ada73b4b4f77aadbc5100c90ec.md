A queue is a First-In/First-Out data structure similar to a line of people at a ticket window. It can be used whenever you need a data structure that allows entries to “wait their turn.” In this chapter we discuss applications of the queue data structure, give two implementations of a queue class, and discuss the differences between queues and stacks. We also discuss a double-ended queue (or dequeue) and (in the projects) show a more flexible kind of queue called a priority queue.

# 8.1 THE STL QUEUE

The word queue is pronounced as if you were saying the letter Q; the word queue means the same thing as the word line when used in phrases like “waiting in a line.” Every time you get in line at a supermarket or in a bank or at a ticket window, you are adding yourself to a queue. If everybody is polite, then people add themselves to the rear of the queue (the rear of the line), and the person at the front of the queue is always the person who is served first. The queue data structure works in exactly the same way, and the abstract definition of a queue reflects this intuition.

> **Queue Definition**
> 
> A queue is a data structure of ordered entries such that entries can only be inserted at one end (called the rear) and removed at the other end (called the front). The entry at the front end of the queue is called the first entry.

stacks versus queues

When we say that the entries in a queue are ordered, all we mean is that there is a first one (the front one), a second one, a third one, and so forth. We do not require that the entries be compared using the < operator. The entries may be of any type. In this regard, the situation is the same as it was for a stack.

Because entries must be removed in exactly the same order that they were added to the queue, a queue is called a First-In/First-Out data structure (abbreviated FIFO). This differs from a stack, which is a Last-In/First-Out data structure, but apart from this difference, a stack and a queue are very similar data structures. They differ only in the rule that determines which entry is removed from the list first. The contrast between stacks and queues is illustrated in Figure 8.1. In either structure the entries depicted are entered in the order A, B, C, and D. With a queue, they are removed in the same order: A, B, C, D. With a stack, they are removed in the reverse order: D, C, B, A.