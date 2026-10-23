# Data Structure simplified

This process continues till all the elements are not inserted in the heap. Complete heap is illustrated in the figure 10.8.

Next task is to select the items from the heap so that they can be stored in an array in sorted order. During the selection of the elements root is selected first, since it is the maximum element. It is placed at the last index of the array, as illustrated in the figure 10.10.

![](bbox=[0.201, 0.206, 0.918, 0.669])

This is followed by determining the right most node of the lowest level of the tree. If the rightmost is not available than the left node of the same parent is considered for replacement with the root as illustrated in the 10.9(b). In the considered figure the rightmost node at the lowest level does not exist. However, the left node (20) of the same parent i.e. 70 is to be placed in the root.

Replacement of item may lead to the violation of heap definition. Consequently, again all the elements are checked for their values. If element is more, shift up operation results. S ince, in the resultant tree of 10.9 (b) heaps definition violates due to the availability of items in the tree which are more than the root node. Consequently, shift up operation is to be applied. Resultant tree is illustrated in the figure 10.11.