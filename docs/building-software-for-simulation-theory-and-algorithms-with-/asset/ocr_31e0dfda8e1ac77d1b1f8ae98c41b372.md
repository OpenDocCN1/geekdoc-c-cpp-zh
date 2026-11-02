# ### 4.3.1 The Event Schedule

The purpose of the event schedule is to keep the set of atomic models sorted in order of the times of their next autonomous actions. A large number of data structures are available for this purpose (see, e.g., Refs. 15, 41, 42, 54, and 121, but note that there is a vast literature on this subject), but the binary heap (hereafter, simply “the heap”) is particularly appropriate for two reasons:

+   1. The number of entries in the heap is at most the number of atomic models in the simulator, and in practice the size of the heap is often much smaller. An explicit heap, which is implemented inside an array, takes advantage of this property to fit itself into a small, contiguous region of memory.
+   2. The most common operation required by the simulator is rescheduling an atomic model. It is relatively inexpensive to move an object to a new position inside a heap, and this efficient rescheduling function can be implemented easily.

An explicit heap stores its N items in the first N + 1 elements of an array. The array can, therefore, be small to start and grow as needed; moreover, the contents of the array do not need to be reorganized when this is done. Adding more space incurs the cost of expanding the current block of memory allocated for the heap or, if this block is too small, of finding a new block and copying the heap’s elements to it. If the size of the heap is doubled at each instance, resizing will occur infrequently over the course of a long simulation run. The heap is guaranteed to stop growing when its size is greater than or equal to the number of atomic models in the simulation, and it may cease to grow long before that point is reached.

The heap organizes its atomic models into a binary tree. The position assigned to a model is chosen such that the time of its next event is less than or equal to the time of next event of its children (or child). This is illustrated in Figure 4.6.

The first node, the smallest element in the heap, has the first position in the array. Its two children occupy positions 2 and 3. The children of position 2 have positions 4 and 5; the children of position 3 have positions 6 and 7. The rule is that the model

![](bbox=[0.19, 0.57, 0.78, 0.8])