# Binary Search Example

Assume we have the array given below, notice it is sorted and will remain sorted throughout the entire algorithm. A searching algorithm should never alter the data it searches! Target = 25.

| 3 | 5 | 1 | 0 |
| 5 | 1 | 2 | 6 |
| 6 | 2 | 3 | 10 |
| 10 | 3 | 4 | 12 |
| 12 | 4 | 5 | 15 |
| 15 | 5 | 6 | 17 |
| 17 | 6 | 7 | 18 |
| 18 | 7 | 8 | 21 |
| 21 | 8 | 9 | 22 |
| 22 | 9 | 10 | 25 |
| 25 | 10 | 11 | 27 |
| 27 | 11 | 12 | 30 |
| 30 | 12 | 13 | 31 |
| 31 | 13 | 14 | 33 |
| 33 | 14 | | |

# What is the goodness of the binary search as applied to the example above?

+   - Only four comparisons were needed to find target (in the above example). A sequential search would have required 11.
+   - Bigger Point: With each comparison made between the target and the element at the midpoint we eliminate approximately half (hence the name binary) of the remaining index values as a possible location where the target could be found.