position. After that, it is compared with its descendants. Finally, when none of the descendants is greater than it then restores it to the position of the predecessor.

# Time complexity of Heap Sort

The build heap operation is run once and has O (n) time complexity. The shift-down version of heapify has O (log n) time complexity and is called n times. Therefore, the performance of this algorithm is O (n + nlog n) which evaluates to O (n log n)

| Heap Sort algorithm | Best Case | Average Case | Worst Case |
|---|---|---|---|
| | O (nlog n) | O (nlog n) | O (nlog n) |

# Radix Sort

The radix sort is a sorting algorithm that sort integers by processing individual digits. Radix sort is not limited to integers because integers can represent strings of characters (e.g., names or dates) and specially formatted floating-point numbers. As this string technique is based on the radix of the data items, hence it is named as radix sort. Radix sort is an example of non-comparison based sorting.

Two classifications of radix sorts are least significant digit (LSD) radix sorts and most significant digit (MSD) radix sorts. LSD radix sorts process the integer representations starting from the least significant digit and moves towards the most significant digit. MSD radix sort process from most significant digit to least significant digit.

LSD radix sort is suitable for sorting variable length integers and fixed length strings. MSD radix sort is suitable for sorting variable length strings and fixed-length integer representations. LSD radix sort illustrated in the following example.

# Example:

Input Data: 347, 142, 361, 423, 538, 126, 320, 549, 365

The numbers are sorted in the first pass according to the (least significant digits) unit digits.

| Input | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 347 | | | | | | | | 347 | | |
| 142 | | | 142 | | | | | | | |
| 361 | | 361 | | | | | | | | |
| 423 | | | | 423 | | | | | | |
| 538 | | | | | | | | | 538 | |
| 126 | | | | | | | 126 | | | |
| 320 | 320 | | | | | | | | | |
| 549 | | | | | | | | | | 549 |
| 365 | | | | | | 365 | | | | |