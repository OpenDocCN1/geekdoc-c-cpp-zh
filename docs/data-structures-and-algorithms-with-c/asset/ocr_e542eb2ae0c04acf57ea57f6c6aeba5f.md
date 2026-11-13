This drawback can be overcome in two different ways. The first solution is by left shifting all elements after every deletion. However, this is not suitable since after every deletion, the entire elements required shifting left and front and rear should be readjusted according to that.

The second solution is by implementing a circular queue and it is a suitable method to overcome the above drawback.

# CIRCULAR QUEUE

A circular queue (also known as a circular buffer) is a linear data structure that uses a single, fixed-size buffer as if it were connected end-to-end. A circular queue is just one of the efficient ways to implement a queue. It also follows First-in-First-out (FIFO) principle.

# Circular Queue Representation with Array

In array representation, the queue is considered as circular queue when the positions 0 and MAX-1 are adjacent. It means when rear (or front) reaches MAX-1 position then increment in rear (or front) causes rear (or front) to reach the first position that is 0.

One solution of the problem is if not all the elements of the array can be used to accommodate queue elements; in particular, an array of size n can accommodate a maximum of n – 1 elements and one of the slot always remains unused.

![](bbox=[0.1, 0.44, 0.9, 0.88])

Figure 6.5: Different operations on Circular Queue