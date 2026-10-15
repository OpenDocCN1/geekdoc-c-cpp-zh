```
```cpp
cout << "\nValues in array3 by row are:" << endl;
printArray( array3 );
return 0; // indicates successful termination
} // end main

// output array with two rows and three columns
void printArray( const int a[][ 3 ] )
{
   // loop through array's rows
   for ( int i = 0; i < 2; i++ )
   {
      // loop through columns of current row
      for ( int j = 0; j < 3; j++ )
         cout << a[ i ][ j ] << ' ';

      cout << endl; // start new line of output
   } // end outer for
} // end function printArray
```
```

```
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
```

The declaration of array1 (line 11) provides six initializers in two sublists. The first sublist initializes row 0 of the array to the values 1, 2 and 3; and the second sublist initializes row 1 of the array to the values 4, 5 and 6. If the braces around each sublist are removed from the array1 initializer list, the compiler initializes the elements of row 0 followed by the elements of row 1, yielding the same result.

The declaration of array2 (line 12) provides only five initializers. The initializers are assigned to row 0, then row 1. Any elements that do not have an explicit initializer are initialized to zero, so array2[ 1 ][ 2 ] is initialized to zero.

The declaration of array3 (line 13) provides three initializers in two sublists. The sublist for row 0 explicitly initializes the first two elements of row 0 to 1 and 2; the third element is implicitly initialized to zero. The sublist for row 1 explicitly initializes the first element to 4 and implicitly initializes the last two elements to zero.

The program calls function printArray to output each array’s elements. Notice that the function definition (lines 27–38) specifies the parameter const int a[][ 3 ]. When a function receives a one-dimensional array as an argument, the array brackets are empty in the function’s parameter list. The size of the first dimension (i.e., the number of rows) of a two-dimensional array is not required either, but all subsequent dimension sizes are

![](bbox=[0.141, 0.106, 0.857, 0.596])