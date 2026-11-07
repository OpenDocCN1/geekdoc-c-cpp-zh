![](bbox=[0.183, 0.097, 0.911, 0.265])

**FIGURE 19-27** Queue after two more addQueue operations

Now consider the deleteQueue operation:

```
deleteQueue();
```

After this operation, the array containing the queue is as shown in Figure 19-28.

![](bbox=[0.183, 0.406, 0.911, 0.548])

**FIGURE 19-28** Queue after the deleteQueue operation

Will this queue design work? Suppose A stands for adding (that is, addQueue) an element to the queue, and D stands for deleting (that is, deleteQueue) an element from the queue. Consider the following sequence of operations:

```
AAADADADADADADADA...
```

This sequence of operations would eventually set the index queueRear to point to the last array position, giving the impression that the queue is full. However, the queue has only two or three elements, and the front of the array is empty (see Figure 19-29).

![](bbox=[0.183, 0.806, 0.911, 0.947])

**FIGURE 19-29** Queue after the sequence of operations AAADADADADADADADA...