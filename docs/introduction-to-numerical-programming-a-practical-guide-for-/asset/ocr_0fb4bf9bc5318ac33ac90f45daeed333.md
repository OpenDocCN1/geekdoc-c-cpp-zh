Pass 2:

| 30 | 20 | 50 | 10 | 40 | | 60 |
| 30 | 20 | 10 | 50 | 40 | | 60 |
| 30 | 20 | 10 | 40 | 50 | | 60 |

Pass 3:

| 20 | 30 | 10 | 40 | | 50 | 60 |
| 20 | 10 | 30 | 40 | | 50 | 60 |

Pass 4:

| 10 | 20 | 30 | | 40 | 50 | 60 |

The vertical double bar separates the unsorted lower values (on the left) from the sorted higher values (on the right). Swapped pairs of values are represented as boxed and bolded.

At the first pass, the algorithm sweeps through the whole list, comparing the adjacent values, swapping them if necessary, and placing finally the largest value (60) at the end of the list. The second pass operates along the same lines, but only with the first five elements, swapping the second-largest value (50) all the way to the end of the sublist. The last theoretically required sweep (“Pass 5”) would operate on the two left-most elements, but is no longer necessary since the array is already sorted. An optimized actual implementation should recognize that the elements are already in order and should drop this last pass.

Listing 4.1 presents three implementations of bubble sort. BubbleSort0 represents the basic implementation, without embedded detection of already-sorted arrays. The outer loop of passes is controlled by the counter ipass, and the length of the inner loop, over the pairs of adjacent elements, is gradually reduced from n − 1 down to 1. Irrespective of the particular array, BubbleSort0 performs all the n(n − 1)/2 theoretical comparisons before returning the sorted array.

An improved version, known as modified bubble sort, is implemented in the routine BubbleSort1. It uses a flag, named swap, which is initialized with 0 and is set to 1 if at least a swap is made during an entire pass. If by the end of a pass no swap has been performed (swap remains 0), it is implied that the array is already in order and the process is terminated. The best case, namely an already-sorted array, obviously requires just n − 1 compares during the first pass, but no swaps, reducing the total operation count to O(n).

The routine BubbleSort represents a yet improved variant of BubbleSort1, since it eliminates the redundancy caused by the double control of the outer loop, both by the counter ipass and the flag swap. The chosen coding solution is the replacement of the for-loop by a while-loop controlled by the flag swap solely.