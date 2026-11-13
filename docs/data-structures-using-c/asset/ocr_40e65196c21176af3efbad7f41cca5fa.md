Let us consider an example. Let the list of numbers to be sorted be {13, 11, 14, 11, 15, 19, 12, 16, 15, 18, 19}. Now, the first element 13 becomes pivot. We need to place 13 at a proper location so that all elements to its left are smaller and the right are greater.

| A | 13 | 11 | 14 | 11 | 15 | 19 | 12 | 16 | 15 | 13 | 15 | 18 | 19 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

Initially, the array is pivoted about its first element A[pivot] = 13.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 13 | 11 | 14 | 11 | 15 | 19 | 12 | 16 | 15 | 13 | 15 | 18 | 19 |

Let us first find the elements larger than the pivot, that is, 13. In addition, let us find the last element not larger than the pivot. These elements are in positions 2 and 9. Let us swap those.

| 13 | 11 | 14 | 11 | 15 | 19 | 12 | 16 | 15 | 13 | 15 | 18 | 19 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 13 | 11 | 13 | 11 | 15 | 19 | 12 | 16 | 15 | 14 | 15 | 18 | 19 |

Let us again start scanning from both directions.

| 13 | 11 | 13 | 11 | 15 | 19 | 12 | 16 | 15 | 14 | 15 | 18 | 19 |

The elements 12 and 15 are to be swapped to get the following sequence:

| 13 | 11 | 13 | 11 | 12 | 19 | 15 | 16 | 15 | 14 | 15 | 18 | 19 |

Let us repeat the steps to get the following sequence:

| 13 | 11 | 13 | 11 | 12 | 19 | 15 | 16 | 15 | 14 | 15 | 18 | 19 |