The array contains three rows and four columns, so it’s said to be a 3-by-4 array. In general, an array with *m* rows and *n* columns is called an *m*-by-*n* array.

Every element in array `a` is identified by a name of the form `a[i][j]`, where `a` is the array name, and `i` and `j` are the subscripts that uniquely identify each element. The element names in row 0 all have the first subscript 0. The element names in column 3 all have the second subscript 3. Referencing a two-dimensional array element as `a[x, y]` instead of `a[x][y]` is a logic error. C treats `a[x, y]` as `a[y]`, so this programming error is not a *syntax* error. The comma in this context is a comma operator which guarantees that a list of expressions evaluates from left to right. The value of a comma-separated list of expressions is the value of the rightmost expression in the list.

# 6.11.2 Initializing a Double-Subscripted Array

You can initialize a multidimensional array when you define it. For example, you can define and initialize the two-dimensional array `int b[2][2]` with:

```
int b[2][2] = {{1, 2}, {3, 4}};
```

The values in the initializer list are grouped by row in braces. The values in the first set of braces initialize row 0 and the values in the second set of braces initialize row 1. So, the values 1 and 2 initialize elements `b[0][0]` and `b[0][1]`, respectively, and the values 3 and 4 initialize elements `b[1][0]` and `b[1][1]`, respectively. If there are not enough initializers for a given row, that row’s remaining elements are initialized to 0. So the definition:

```
int b[2][2] = {{1}, {3, 4}};
```

would initialize `b[0][0]` to 1, `b[0][1]` to 0, `b[1][0]` to 3 and `b[1][1]` to 4. Figure 6.16 demonstrates defining and initializing two-dimensional arrays.

```
```c
// fig06_16.c
// Initializing multidimensional arrays.
#include <stdio.h>

void printArray(int a[][3]); // function prototype

// function main begins program execution
int main(void) {
    int array1[2][3] = {{1, 2, 3}, {4, 5, 6}};
    puts("Values in array1 by row are:");
    printArray(array1);

    int array2[2][3] = {{1, 2, 3}, {4, 5}};
    puts("Values in array2 by row are:");
    printArray(array2);

    int array3[2][3] = {{1, 2}, {4}};
    puts("Values in array3 by row are:");
    printArray(array3);
}
```
```

Fig. 6.16 | Initializing multidimensional arrays. (Part 1 of 2.)