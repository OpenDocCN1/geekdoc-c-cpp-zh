The only argument that should be needed for a function to empty the queue is the queue’s address, suggesting this prototype:

```
void EmptyTheQueue(Queue * pq);
```

# Implementing the Interface Data Representation

The first step is deciding what C data form to use for a queue. One possibility is an array. The advantages to arrays are that they’re easy to use and that adding an item to the end of an array’s filled portion is easy. The problem comes with removing an item from the front of the queue. In the analogy of people in a ticket line, removing an item from the front of the queue consists of copying the value of the first element of the array (simple) and then moving each item left in the array one element toward the front. Although this is easy to program, it wastes a lot of computer time (see Figure 17.6).

Four folks in a queue

![](bbox=[0.26, 0.5, 0.795, 0.565])

Ken joins the queue, then Sue leaves the queue

![](bbox=[0.26, 0.62, 0.795, 0.73])

Figure 17.6 Using an array as a queue.

A second way to handle the removal problem in an array implementation is to leave the remaining elements where they are and, instead, change which element you call the front (see Figure 17.7). This method’s problem is that the vacated elements become dead space, so the available space in the queue keeps decreasing.