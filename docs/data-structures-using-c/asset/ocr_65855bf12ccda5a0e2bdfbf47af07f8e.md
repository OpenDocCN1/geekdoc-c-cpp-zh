The implementation of a circular queue using an array is provided in Program Code 5.3. Let us see its working with an example. Consider max = 5 and initially, Front = Rear = 0. The iterations are shown in Table 5.1.

Table 5.1 Implementation of circular queue

| 0 | 1 | 2 | 3 | 4 | Front | Rear | Action |
|---|---|---|---|---|---|---|---|
| | | | | | 0 | 0 | Q_Empty |
| 11 | | | | | 0 | 1 | Insert 11 |
| 11 | 12 | | | | 0 | 2 | Insert 12 |
| 11 | 12 | 13 | | | 0 | 3 | Insert 13 |
| 11 | 12 | 13 | 14 | | 0 | 4 | Insert 14 |
| 11 | 12 | 13 | 14 | | 0 | | Insert 15 Can't insert 15 as Q_Full since Rear = (4 + 1)%5 = 0 which is equal to Front: |
| - | 12 | 13 | 14 | | 1 | 4 | Delete |
| - | - | 13 | 14 | | 2 | 4 | Delete |
| - | - | - | 14 | | 3 | 4 | Delete |
| - | - | - | - | 4 | 4 | 4 | Delete Can't delete as Front = Rear makes Q_Empty |

To check the Queue_Full and Queue_Empty conditions, we need to check whether the values of Front and Rear are equal. In the programming languages C/C++, the array index varies from 0 to n - 1, so that one location of the circular queue always remains unused. Such is not the case in languages such as Pascal. Hence, in a circular queue that uses arrays in C/C++, we can store n - 1 elements, where n is declared as the size of the array. Hence, for storing n elements, we should declare the array of size n + 1.

# 5.4.1 Advantages of Using Circular Queues

The following are the merits of using circular queues:

+   1. By using circular queues, data shifting is avoided as the front and rear are modified by using the mod() function. The mod() operation wraps the queue back to its beginning.
+   2. If the number of elements to be stored in the queue is fixed (i.e., if the queue size is specific), the circular queue is advantageous.
+   3. Many practical applications such as printer queue, priority queue, and simulations use the circular queue.

# 5.5 MULTI-QUEUES

If more number of queues is required to be implemented, then an efficient data structure to handle multiple queues is required. It is possible to utilize all the available spaces in a single array. When more than two queues, say n, are represented sequentially, we can