wraparound from end to start is called a circular queue. Virtually, we want the insertion process and the rear to wraparound the queue.

Hence, a more efficient queue representation is obtained by implementing the array Q as circular. Here, as we go on adding elements to the queue and reach the end of the array, the next element is stored in the first slot of the array if it is empty. Suppose the queue Q is of size n. Now, if we go on adding elements in the queue, we may reach the location n - 1. If it is not circular, no more elements can be added even though there are empty locations at the front of the array. Instead, if there are empty locations at the front, using a circular queue we can add elements at that location rather than signalling an error as the queue is full or is shifting the data.

The empty slots will be filled with new incoming elements even though Rear = n - 1. Hence, the circular queue allows us to continue adding elements even though we have reached the end of the array. The queue is said to be full only when there are n elements in the queue. The pictorial representation of a circular queue is shown in Figs 5.2(a) and 5.2(b).

![](bbox=[0.255, 0.405, 0.855, 0.905])

Fig. 5.2 Circular queue (a) Conceptual view (b) Physical view