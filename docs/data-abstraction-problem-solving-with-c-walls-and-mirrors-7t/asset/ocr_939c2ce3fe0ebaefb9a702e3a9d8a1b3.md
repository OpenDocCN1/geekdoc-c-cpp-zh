# FIGURE 14-8 A circular array as an implementation of a queue

![](bbox=[0.45, 0.15, 0.75, 0.3])

back. Figure 14-9 illustrates the effect of a sequence of three queue operations on front, back, and the array. Notice that front and back “advance” clockwise around the array.

When either front or back advances past MAX_QUEUE – 1, it should wrap around to 0. This wraparound eliminates the problem of rightward drift, which occurred in the previous naive implementation, because here the circular array has no end. You obtain the wraparound effect of a circular queue by using modulo arithmetic (that is, the C++ % operator) when incrementing front and back. For example, you can add newEntry to the queue by using the statements

```
Adding to a queue
back = (back + 1) % MAX_QUEUE;
items[back] = newEntry;
```

Notice that if back equaled MAX_QUEUE – 1 before the addition of newItem, the first statement, back = (back + 1) % MAX_QUEUE, would have the effect of wrapping back around to index 0. Similarly, you can remove the entry at the front of the queue by using the statement

```
Deleting from a queue
front = (front + 1) % MAX_QUEUE;
```

To initialize the queue, you set front to 0 and back to MAX_QUEUE – 1.

# FIGURE 14-9 The effect of three consecutive operations on the queue in Figure 14-8

![](bbox=[0.15, 0.72, 0.85, 0.9])