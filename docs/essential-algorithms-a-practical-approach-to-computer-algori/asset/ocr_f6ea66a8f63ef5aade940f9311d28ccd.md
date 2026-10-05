# 126 Chapter 5 ※ Stacks and Queues

![](bbox=[0.125, 0.09, 0.411, 0.301])

**Figure 5-10:** In a circular queue you treat the array's last item as if it comes right before the first item.

A circular array does present a new challenge, however. When the queue is empty, Next is the same as Last. If you add items to the queue, Next goes all the way around the array and catches to Last again, so there's no obvious way to tell whether the queue is empty or full.

You can handle this problem in a few ways. For example, you can keep track of the number of items in the queue, keep track of the unused spaces in the queue, or keep track of the number of items added and removed from the queue. The Circular sample program, which is available for download on the book's website, handles this problem by always keeping one of the array's spaces empty. If you added another value to the queue shown in Figure 5-10, the queue would be full when Next is just before Last, even though there was no empty array entry.

The following pseudocode shows the algorithm used by the example program for enqueueing an item:

```
// Variables to manage the queue.
Data: Queue[<queue size>
Integer: Next = 0
Integer: Last = 0
```

```
// Enqueue an item.
Enqueue[Data: value]
// Make sure there's room to add an item.
If ((Next + 1) Mod <queue size> == Last) Then <throw an exception>
```

```
Queue[Next] = value
Next = (Next + 1) Mod <queue size>
Enqueue
```

The following pseudocode shows the algorithm for dequeuing an item:

```
// Dequeue an item.
Data: Dequeue()
```