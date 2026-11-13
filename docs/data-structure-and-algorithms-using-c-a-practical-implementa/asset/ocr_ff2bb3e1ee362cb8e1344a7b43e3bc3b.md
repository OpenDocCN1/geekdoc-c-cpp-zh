# INPUT RESTRICTED DEQUE

In this type of queue the insertion operation is restricted i.e/ it allows the insertion operation at one end but the deletion operation is at both the ends. One can perform the insertion operation at the rear end only but the insertion and deletion operation can be performed at front end.

# OUTPUT RESTRICTED DEQUE

In this type of queue the Deletion operation is restricted i.e/ it allows the deletion operation at one end but the insertion operation is at both the ends. One can perform the deletion operation at the front end only but the insertion and deletion operation can be performed at rear end.

# 6.6 Priority Queue

Priority queues are a kind of queue in which the elements are dequeued in priority order.

+   - They are a mutable data abstraction: enqueues and dequeues are destructive.
+   - Each element has a priority, an element of a totally ordered set (usually a number)
+   - More important things come out first, even if they were added later
+   - Our convention: smaller number = higher priority
+   - There is no (fast) operation to find out whether an arbitrary element is in the queue
+   - Useful for event-based simulators (with priority = simulated time), real-time games, searching, routing, compression via Huffman coding

Depending on the heaps the priority queue are also of two types such as Min Priority Queue Max Priority Queue

The Set of operations for Max Priority Queue are

+   - Insert(A,N) : Inserts an element N into A
+   - Maximum(A,X) : Finds the X from A where X is the Maximum