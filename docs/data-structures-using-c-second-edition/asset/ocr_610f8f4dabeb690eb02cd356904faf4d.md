Now, if you want to insert another value, it will not be possible because the queue is completely full. There is no empty space where the value can be inserted. Consider a scenario in which two successive deletions are made. The queue will then be given as shown in Fig. 8.14.

| 0 | 1 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

# Figure 8.14 Queue after two successive deletions

Here, FRONT = 2 and REAR = 9.

Suppose we want to insert a new element in the queue shown in Fig. 8.14. Even though there is space available, the overflow condition still exists because the condition REAR = MAX - 1 still holds true. This is a major drawback of a linear queue.

![](bbox=[0.103, 0.323, 0.403, 0.413])

# Figure 8.15 Circular queue

To resolve this problem, we have two solutions. First, shift the elements to the left so that the vacant space can be occupied and utilized efficiently. But this can be very time-consuming, especially when the queue is quite large. The second option is to use a circular queue. In the circular queue, the first index comes right after the last index. Conceptually, you can think of a circular queue as shown in Fig. 8.15.

The circular queue will be full only when FRONT = 0 and REAR = Max - 1. A circular queue is implemented in the same manner as a linear queue is implemented. The only difference will be in the code that performs insertion and deletion operations. For insertion, we now have to check for the following three conditions:

| 90 | 49 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| FRONT = 01 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | REAR = 9 |

# Figure 8.16 Full queue

Increment rear so that it points to location 9 and insert the value here

+   - If FRONT = 0 and REAR = MAX - 1, then the circular queue is full. Look at the queue given in Fig. 8.16 which illustrates this point.

| 90 | 49 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| FRONT = 01 | 2 | 3 | 4 | 5 | 6 | 7 | REAR = 8 | 9 |

# Figure 8.17 Queue with vacant locations

Set REAR = 0 and Insert the value here

+   - If REAR != MAX - 1, then REAR will be incremented and the value will be inserted as illustrated in Fig. 8.17.

| 7 | 18 | 14 | 36 | 45 | 21 | 80 | 81 |
|---|---|---|---|---|---|---|---|
| 0 | 1 FRONT = 2 | 3 | 4 | 5 | 6 | 7 | 8 REAR = 9 |

# Figure 8.18 Inserting an element in a circular queue

+   - If FRONT != 0 and REAR = MAX - 1, then it means that the queue is not full. So, set REAR = 0 and insert the new element there, as shown in Fig. 8.18.

Let us look at Fig. 8.19 which shows the algorithm to insert an element in a circular queue. In Step 1, we check for the overflow condition. In Step 2, we make two checks. First to see if the queue is empty, and second to see if the rear end has already reached the maximum capacity while there are certain free locations before the front end. In Step 3, the value is stored in the queue at the location pointed by REAR.

```
```
Step 1: IF FRONT = 0 and Rear = MAX - 1
    write "OVERFLOW"
    Goto step 4
Step 2: IF FRONT = -1
    FRONT = 0 and REAR = 0
ELSE IF REAR = MAX - 1 and FRONT != 0
    SET REAR = 0
ELSE
    SET REAR = REAR + 1
[END OF IF]
Step 3: SET QUEUE[REAR] = VAL
Step 4: EXIT
```
```

# Figure 8.19 Algorithm to insert an element in a circular queue

After seeing how a new element is added in a circular queue, let us now discuss how deletions are performed in this case. To delete an element, again we check for three conditions.