After the rearrangement of the array elements, the corresponding complete binary tree is a heap, and to aid your visualization, we have drawn the corresponding tree beside the array. But keep in mind that the only place that the numbers are stored is in the array. The tree is just our visualization of how those elements are structured. In a moment, we’ll provide the details of how the rearrangement into a heap occurs, but first let’s look at the rest of the heapsort algorithm.

Recall that the largest value in a heap is stored in the root, and that in our array representation of a complete binary tree, the root node is stored in the first array position. Thus, since the array represents a heap, we know that the largest array element is in the first array position. To get the largest value into the correct array position, we simply interchange the first and the final array elements. After interchanging these two array elements, we know that the largest array element is in the final array position, as shown here:

find the largest element, and move it to the end of the array

| 5 | 27 | 42 | 21 | 23 | 22 | 35 | 19 | 4 | 45 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

The dark vertical line in the array separates the “unsorted side” of the array (on the left) from the “sorted side.” Moreover, the unsorted side (on the left) still represents a complete binary tree, which is almost a heap, as shown at the top of the next page.

| 5 | 27 | 42 | 21 | 23 | 22 | 35 | 19 | 4 | 45 |
|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |

![](bbox=[0.552, 0.533, 0.746, 0.675])

When we consider the unsorted side as a complete binary tree, it is only the root that violates the heap storage rule. This root is smaller than its children. So, the next step of the heapsort is to reposition this one out-of-place value in order to restore the heap. In Section 11.1 we discussed this process of restoring the heap by repositioning the out-of-place root. The process, called reheapification downward, begins by comparing the value in the root with the value of each of its children. If one or both children are larger than the root, then the root node’s value is exchanged with the larger of the two children. This moves the troublesome value down one level in the tree. For our example, the out-of-place value (5) is exchanged with its larger child (42), as shown on the next page.

fix the heap