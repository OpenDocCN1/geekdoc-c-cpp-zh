# 7.2 REPRESENTATION OF A QUEUE

Queues can be represented in two ways:

+   - Static representation using arrays
+   - Dynamic representation using linked list

# 7.2.1 Array Representation

A one-dimensional array is used to represent a queue. Consider a queue QUE [1:N], two pointers FRONT and REAR represent two ends of the QUE. To insert an element, the REAR pointer is used and to delete an element, the FRONT pointer is used (Figure 7.1).

![](bbox=[0.254, 0.301, 0.75, 0.383])

Figure 7.1 Array representation of queue QUE [1:N]

A queue QUE [1:N] cannot hold more than N elements, and every insertion of an element must check the condition whether the QUE is full, and deletion of an element must ensure that QUE is not empty.

# 7.2.2 LINKED REPRESENTATION

Using linked list, queue is created dynamically by which the size of the queue can be increased as per the necessity in the application or program, whereas using arrays the size of the queue is fixed.

Figure 7.2 shows the single linked list representation of a queue. The pointer FRONT points to the first node, and REAR to the last node in the list.

![](bbox=[0.156, 0.65, 0.844, 0.75])

Figure 7.2 Linked representation of a queue

When FRONT=REAR the queue is said to be empty.

# 7.3 OPERATIONS ON A QUEUE

The two basic operations on queues are:

+   1. Insertion (Enqueue)—adds an element into the queue
+   2. Deletion (Deque)—removes an element from the queue