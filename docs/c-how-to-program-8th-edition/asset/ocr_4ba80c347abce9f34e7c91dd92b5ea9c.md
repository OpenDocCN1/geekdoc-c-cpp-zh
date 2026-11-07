```
Values in array1 by row are:
1 2 3
4 5 6

Values in array2 by row are:
1 2 3
4 5 0

Values in array3 by row are:
1 2 0
4 0 0
```

*Fig. 7.21* | Initializing multidimensional arrays. (Part 2 of 2.)

the values 4, 5 and 6. If the braces around each sublist are removed from the array1 initializer list, the compiler initializes the elements of row 0 followed by the elements of row 1, yielding the same result.

The declaration of array2 (line 13) provides only five initializers. The initializers are assigned to row 0, then row 1. Any elements that do not have an explicit initializer are initialized to zero, so array2[1][2] is initialized to zero.

The declaration of array3 (line 14) provides three initializers in two sublists. The sublist for row 0 explicitly initializes the first two elements of row 0 to 1 and 2; the third element is implicitly initialized to zero. The sublist for row 1 explicitly initializes the first element to 4 and implicitly initializes the last two elements to zero.

The program calls function printArray to output each array’s elements. Notice that the function prototype (line 6) and definition (lines 27–38) specify the parameter const int a[][columns]. When a function receives a one-dimensional array as an argument, the array brackets are empty in the function’s parameter list. The size of a two-dimensional array’s first dimension (i.e., the number of rows) is not required either, but all subsequent dimension sizes are required. The compiler uses these sizes to determine the locations in memory of elements in multidimensional arrays. All array elements are stored consecutively in memory, regardless of the number of dimensions. In a two-dimensional array, row 0 is stored in memory followed by row 1. Each row is a one-dimensional array. To locate an element in a particular row, the function must know exactly how many elements are in each row so it can skip the proper number of memory locations when accessing the array. Thus, when accessing a[1][2], the function knows to skip row 0’s three elements in memory to get to row 1. Then, the function accesses element 2 of that row.

Many common array manipulations use for statements. For example, the following for statement sets all the elements in row 2 of array a in Fig. 7.20 to zero:

```
for ( int column = 0; column < 4; ++column )
    a[ 2 ][ column ] = 0;
```

The for statement varies only the second subscript (i.e., the column subscript). The preceding for statement is equivalent to the following assignment statements:

```
a[ 2 ][ 0 ] = 0;
a[ 2 ][ 1 ] = 0;
a[ 2 ][ 2 ] = 0;
a[ 2 ][ 3 ] = 0;
```