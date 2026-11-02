![](bbox=[0.12, 0.1, 0.88, 0.35])

Fig. 6.20 | Two-dimensional array with three rows and four columns.

Every element in array a is identified in Fig. 6.20 by an element name of the form a[i][j]; a is the name of the array, and i and j are the indices that uniquely identify each element in a. The names of the elements in row 0 all have a first index of 0; the names of the elements in column 3 all have a second index of 3.

**Common Programming Error 6.7**
Referencing a two-dimensional array element as a(x, y) instead of a[x][y] is a logic error. C interprets a(x, y) as a[y] (because the comma in this context is treated as a comma operator), so this programmer error is not a syntax error.

# 6.11.2 Initializing a Double-Subscripted Array

A multidimensional array can be initialized when it's defined. For example, a two-dimensional array int b[2][2] could be defined and initialized with

```
int b[2][2] = {{1, 2}, {3, 4}};
```

The values are grouped by row in braces. The values in the first set of braces initialize row 0 and the values in the second set of braces initialize row 1. So, the values 1 and 2 initialize elements b[0][0] and b[0][1], respectively, and the values 3 and 4 initialize elements b[1][0] and b[1][1]. If there are not enough initializers for a given row, the remaining elements of that row are initialized to 0. Thus,

```
int b[2][2] = {{}, {3, 4}};
```

would initialize b[0][0] to 1, b[0][1] to 0, b[1][0] to 3 and b[1][1] to 4. Figure 6.21 demonstrates defining and initializing two-dimensional arrays.

```
1 // Fig. 6.21: fig06_21.c
2 // Initializing multidimensional arrays.
3 #include <stdio.h>
4
5 void printArray(int a[][3]); // function prototype
6
```

Fig. 6.21 | Initializing multidimensional arrays. (Part I of 2.)