![](bbox=[0.33, 0.15, 0.75, 0.4])

▲ Figure 4: Memory Representation of the Multidimensional Array

It can be observed in Figure 4 that the multidimensional array can be stored in two different ways in the memory. The allocation of elements can be done in a row-major form or a column-major form. In both the cases, the address of the elements would remain the same. The job of fetching the correct value for a given index will be done by the compiler. The general syntax to define a multidimensional array is as follows:

```
data type identifier[size 1]...[size n];
```

The preceding syntax can be modified as per the need of the program. In normal cases, we may not need arrays that have more than three dimensions. The array I_mark defined before is said to be a two-dimensional array as it has one row and one column.

The two-dimensional arrays, similar to one-dimensional array, can also be initialized at compile time. The syntax to initialize the two-dimensional array at compile time is as follows:

```
data type identifier[row size][column size] = { value 1, value 2, ..., value n };
```

For example, the array `int I_mark[3][4];` can be initialized at the compile time, as shown next:

```
int i_mark[2][3] = {75, 90, 40, 40, 50, 60, 70, 85, 80, 85, 55, 60}; or
int i_mark[2][3] = {{75, 90, 40, 40},{50, 60, 70, 85},{80, 85, 55, 60}};
```

Let us now see how to use the multidimensional arrays in C. Consider that the teacher wants to generate a result sheet of the students in her class. Program 6 illustrates how to calculate the result:

# ▲ Program 6

```
/* Program to illustrate the use of multidimensionalarray */
#include <stdio.h>
```