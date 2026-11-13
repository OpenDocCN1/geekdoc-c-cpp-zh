# # Heap Sort

The Heapsort is more efficient and improved version of Selection sort. It also works by determining the largest element of the list, placing that at the end of the list, then continuing with the rest of the list. Heapsort is an in-place sorting algorithm, but it is not a stable sort. Heap-sort was invented by J. W. J. Williams in 1964.

The heapsort is based on a data structure called heap, a special kind of binary tree. Recall that, in heap, the left child of A[K] is stored at A[2*K] and right child is stored at A[2*K+1]. As this sorting technique uses heap data structure, hence it is named as heap sort.

Once the data list has been made into a max-heap, the root node is guaranteed to be the largest element. When it is removed and placed at the end of the list, the heap is rearranged so the largest element remaining moves to the root.

The operation for creating a heap is also referred as heapify helps to build a heap from a list of data items. Now, heapify operation has two variations: shift-up and shift-down.

The shift-up process begins with an empty heap, then successive inserts elements in the tree and build a heap by the shift-up operation. Here, the building of heap is done using top-down approach. In shift-up operation, if the newly inserted element is greater (max-heap) or smaller (min-heap) than its parent then it needs to be interchanged with parent.

# **Example:**

Build the heap using shift-up process: 60, 50, 30, 10, 80, 70, 20 and 40

Insert 60:

![](bbox=[0.468, 0.484, 0.531, 0.522])

Insert 50:

![](bbox=[0.414, 0.552, 0.585, 0.632])

Insert 30:

![](bbox=[0.414, 0.652, 0.585, 0.732])

Insert 10:

![](bbox=[0.367, 0.772, 0.632, 0.882])