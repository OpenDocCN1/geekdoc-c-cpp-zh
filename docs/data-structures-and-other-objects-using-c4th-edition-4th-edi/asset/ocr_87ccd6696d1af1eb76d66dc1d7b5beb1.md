![](bbox=[0.386, 0.186, 0.706, 0.326])

Of course, this “exchange” of values actually occurs within the array that represents the heap, so that the array now looks like this:

| 42 | 27 | 5 | 21 | 23 | 22 | 35 | 19 | 4 || 45 |
|---|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] || [9] |

In this example, the 5 is still out of place, so we will once again exchange it with its largest child, resulting in the array (and heap) shown here:

| 42 | 27 | 35 | 21 | 23 | 22 | 5 | 19 | 4 || 45 |
|---|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] || [9] |

![](bbox=[0.606, 0.512, 0.846, 0.662])

Keep in mind that only the unsorted side of the array must be maintained as a heap. In general, the reheapification continues until the troublesome value reaches a leaf or it reaches a spot where it is no longer than its children.

When the unsorted side of the array is once again a heap, the heapsort continues by exchanging the largest element in the unsorted side with the rightmost element of the unsorted side. For our example, the 42 is exchanged with the 4, as shown here:

| 4 | 27 | 35 | 21 | 23 | 22 | 5 | 19 | 42 || 45 |
|---|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] || [9] |