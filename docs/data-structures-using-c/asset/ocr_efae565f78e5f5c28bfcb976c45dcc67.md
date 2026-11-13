divide the available memory A[size] into n segments and allocate these segments to n queues, one to each queue i we shall use Front[i] and Rear[i]. We shall use the condition Front[i] = Rear[i] if and only if the i'th queue is empty, and the condition Rear[i] = Front[i] if and only if the i'th queue is full.

If we want five queues, then we can divide the array A[100] into equal parts of 20 and initialize front and rear for each queue, that is, Front[0] = Rear[0] = 0 and Front[1] = Rear[1] = 20, and so on for other queues (Fig. 5.3).

![](bbox=[0.26, 0.26, 0.84, 0.34])

Fig. 5.3 A multi-queue

After adding elements 5 and 8 in the second queue, the resultant queue will be as in Fig. 5.4.

![](bbox=[0.2, 0.48, 0.86, 0.55])

Fig. 5.4 Queue in Fig. 5.3 after addition of elements

# 5.6 DEQUE

The word deque is a short form of double-ended queue. It is pronounced as 'deck'. Deque defines a data structure where elements can be added or deleted at either the front end or the rear end, but no changes can be made elsewhere in the list. Thus, deque is a generalization of both a stack and a queue. It supports both stack-like and queue-like capabilities. It is a sequential container that is optimized for fast index-based access and efficient insertion at either of its ends. Deque can be implemented as either a continuous deque or as a linked deque. Figure 5.5 shows the representation of a deque.

![](bbox=[0.25, 0.81, 0.85, 0.89])

Fig. 5.5 Representation of a deque