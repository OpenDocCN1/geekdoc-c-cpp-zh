# 6.1 Arrays 201

| M[0][0] | M[0][1] | M[0][2] | M[1][0] | M[1][1] | M[1][2] |

| First row | Second row |

**Fig. 6.2:** Storage structure of a two-dimensional array.

However in C++, the subscript of each dimension of an array element starts from 0. So in the program, the array is represented as

```
M = [M[0][0] M[0][1] M[0][2]
     [M[1][0] M[1][1] M[1][2]]
```

Element M[1][0], with 1 as its row subscript and 0 as its column subscript, denotes the first element of the second row of the matrix. A two-dimensional array is stored by rows in memory. That is, the first row is stored first, and then the second, and so on. The elements of each row are stored according to their column subscripts. This storage method is also called row-major storage. The storage order of the two-dimensional array M in memory is demonstrated in Figure 6.2.

For an n-dimensional array, we use a similar method to order the array elements. We view the subscripts of the n dimensions as a counter, where the later subscript is the lower order, and every digit ranges between the lower bound and the upper bound of the corresponding dimension. When the count of digit exceeds the upper bound, a carry is made to the previous digit, and the current and lower digits recount from their respective lower bounds. We can discover that the subscript of the first dimension varies slowest, and the subscript of the last dimension varies quickest. It is noticeable that for each dimension, the lower bound is 0 and the upper bound is the value of the subscript expression in the array declaration minus 1. For example, the following array declaration

```
int M[2][3][4];
```

declares a three-dimensional array, and the storage order of elements is indicated in Figure 6.3.

In general, arrays with three or more dimensions are rarely used, and the most frequently used is a one-dimensional array.

| M[0][0][0] | M[0][0][1] | M[0][0][2] | M[0][0][3] | M[0][1][0] | M[0][1][1] |
| M[0][1][2] | M[0][1][3] | M[0][2][0] | M[0][2][1] | M[0][2][2] | M[0][2][3] |
| M[1][0][0] | M[1][0][1] | M[1][0][2] | M[1][0][3] | M[1][1][0] | M[1][1][1] |
| M[1][1][2] | M[1][1][3] | M[1][2][0] | M[1][2][1] | M[1][2][2] | M[1][2][3] |

**Fig. 6.3:** Storage structure of a three-dimensional array.