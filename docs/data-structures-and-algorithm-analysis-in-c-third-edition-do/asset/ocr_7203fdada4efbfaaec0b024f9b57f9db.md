# Chap. 7 Internal Sorting

Initial Input: Array A

| 27 | 91 | 1 | 97 | 17 | 23 | 84 | 28 | 72 | 5 | 67 | 25 |

First pass values for Count.
rtoi = 1.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 0 | 2 | 1 | 1 | 2 | 0 | 4 | 1 | 0 | |

Count array:
Index positions for Array B.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 0 | 2 | 3 | 4 | 5 | 7 | 7 | 11 | 12 | 12 | |

End of Pass 1: Array A.

| 91 | 1 | 72 | 23 | 84 | 5 | 25 | 27 | 97 | 17 | 67 | 28 |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |

Second pass values for Count.
rtoi = 10.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 2 | 1 | 4 | 0 | 0 | 0 | 1 | 1 | 2 | |

Count array:
Index positions for Array B.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 2 | 3 | 7 | 7 | 7 | 7 | 8 | 9 | 10 | 12 | |

End of Pass 2: Array A.

| 1 | 5 | 17 | 23 | 25 | 27 | 28 | 67 | 72 | 84 | 91 | 97 |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |

> Figure 7.19 An example showing function radix applied to the input of Figure7.17. Row 1 shows the initial values within the input array. Row 2 shows the values for cnt after counting the number of records for each bin. Row 3 shows the index values stored in array cnt. for cnt [0] is 0, indicating no input values are in bin 0. Cnt [1] is 2, indicating that array B positions 0 and 1 hold the values for bin 1. Cnt [2] is 3, indicating that array B position 2 will hold the (single) value for bin 2. Cnt [7] is 11, indicating that array B positions 7 through 10 hold the four values for bin 7. Row 4 shows the results of the first pass of the Radix Sort.