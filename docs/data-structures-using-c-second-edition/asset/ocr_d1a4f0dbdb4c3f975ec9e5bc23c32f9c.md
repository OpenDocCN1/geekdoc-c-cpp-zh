sequentially in an array. It follows the same rules as that of a complete binary tree. That is, if an element is at position i in the array, then its left child is stored at position 2i and its right child at position 2i + 1. Conversely, an element at position 1 has its parent stored at position 1/2.
• Being a complete binary tree, all the levels of the tree except the last level are completely filled.
• The height of a binary tree is given as log2 n, where n is the number of elements.
• Heaps (also known as partially ordered trees) are a very popular data structure for implementing priority queues.

A binary heap is a useful data structure in which elements can be added randomly but only the element with the highest value is removed in case of max heap and lowest value in case of min heap. A binary tree is an efficient data structure, but a binary heap is more space efficient and simpler.

# 12.1.1 Inserting a New Element in a Binary Heap

Consider a max heap H with n elements. Inserting a new value into the heap is done in the following two steps:

+   1. Add the new value at the bottom of H in such a way that H is still a complete binary tree but not necessarily a heap.
+   2. Let the new value rise to its appropriate place in H so that H now becomes a heap as well.

To do this, compare the new value with its parent to check if they are in the correct order. If they are, then the procedure halts, else the new value and its parent's value are swapped and Step 2 is repeated.

# Example 12.1 Consider the max heap given in Fig. 12.2 and insert 99 in it.

# Solution

![](bbox=[0.2, 0.51, 0.8, 0.65])

The first step says that insert the element in the heap so that the heap is a complete binary tree. So, insert the new value as the right child of node 27 in the heap. This is illustrated in Fig. 12.3. Now, as per the second step, let the new value rise to its appropriate place in H so that H becomes a heap as well. Compare 99 with its parent node value. If it is less than its parent's value, then the new node is in its appropriate place and H is a heap. If the new value is greater than that of its parent's node, then swap the two values. Repeat the whole process until H becomes a heap. This is illustrated in Fig. 12.4.

![](bbox=[0.15, 0.8, 0.85, 0.93])