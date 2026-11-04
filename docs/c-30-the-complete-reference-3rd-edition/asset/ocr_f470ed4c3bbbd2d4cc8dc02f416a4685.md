# Boundaries Are Enforced

Array boundaries are strictly enforced in C#; it is a runtime error to overrun or underrun the ends of an array. If you want to confirm this for yourself, try the following program that purposely overruns an array:

```
// Demonstrate an array overrun.
using System;

class ArrayErr {
    static void Main() {
        int[] sample = new int[10];
        int i;

        // Generate an array overrun.
        for(i = 0; i < 100; i = i+1)
            sample[i] = i;
    }
}
```

As soon as i reaches 10, an IndexOutOfRangeException is generated and the program is terminated. (See Chapter 13 for a discussion of exceptions and exception handling.)

# Multidimensional Arrays

Although the one-dimensional array is the most commonly used array in programming, multidimensional arrays are certainly not rare. A multidimensional array is an array that has two or more dimensions, and an individual element is accessed through the combination of two or more indices.

# Two-Dimensional Arrays

The simplest form of the multidimensional array is the two-dimensional array. In a two-dimensional array, the location of any specific element is specified by two indices. If you think of a two-dimensional array as a table of information, one index indicates the row, the other indicates the column.

To declare a two-dimensional integer array table of size 10, 20, you would write

```
int[,] table = new int[10, 20];
```

Pay careful attention to the declaration. Notice that the two dimensions are separated from each other by a comma. In the first part of the declaration, the syntax

```
[,]
```

indicates that a two-dimensional array reference variable is being created. When memory is actually allocated for the array using new, this syntax is used:

```
int[10, 20]
```

This creates a 10×20 array, and again, the comma separates the dimensions.