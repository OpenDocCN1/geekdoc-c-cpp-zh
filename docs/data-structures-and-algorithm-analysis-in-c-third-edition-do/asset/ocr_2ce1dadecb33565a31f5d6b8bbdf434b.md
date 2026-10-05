Sec. 5.5 Heaps and Priority Queues

183

![](bbox=[0.233, 0.185, 0.766, 0.463])

Figure 5.20 Two series of exchanges to build a max-heap. (a) This heap is built by a series of nine exchanges in the order (4-2), (4-1), (2-1), (5-4), (6-3), (5-6), (7-5), (7-6). (b) This heap is built by a series of four exchanges in the order (5-2), (7-3), (7-1), (6-1).

Figure 5.21 Final stage in the heap-building algorithm. Both subtrees of node R are heaps. All that remains is to push R down to its proper level in the heap.

level where it is greater than its children, or is a leaf node. This process is implemented by the private method siftdown. The siftdown operation is illustrated by Figure 5.22.

This approach assumes that the subtrees are already heaps, suggesting that a complete algorithm can be obtained by visiting the nodes in some order such that the children of a node are visited before the node itself. One simple way to do this is simply to work from the high index of the array to the low index. Actually, the build process need not visit the leaf nodes (they can never move down because they are already at the bottom), so the building algorithm can start in the middle of the array, the exchanges shown in Figure 5.20(b) result from this process. Method buildHeap implements the building algorithm.