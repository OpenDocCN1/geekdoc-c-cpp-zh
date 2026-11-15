# SHORT ANSWER PROBLEMS

# True-False Problems

Indicate whether the following statements are true (T) or false (F):

+   1. If the initializing sequence is shorter than an array, then the rest of the values are initialized to zero.

+   2. If an array is defined without a size, but with an initialization sequence, then the array size is arbitrary.

+   3. When the value of a subscript or index is greater than the largest valid subscript of an array, it will always cause an execution error.

+   4. All values of an array are printed if we specify the identifier of the array without subscripts.

# Multiple Choice

+   5. An array is
+   (a) a group of values that all have a common variable name and all have the same data type.
+   (b) a collection of elements of different data types that are stored in adjacent memory locations.
+   (c) a variable that contains multiple values of the same data type.
+   (d) a location in memory that holds multiple values of the same data type.

+   6. An individual element in the array is addressed by specifying
+   (a) the name of the array and the number of the element.
+   (b) the name of the array.
+   (c) the number of the element within the array followed by the name of the array.
+   (d) the number of the element in the array.

+   7. The subscript identifies the ____ of a particular element in the array.
+   (a) location
+   (b) value
+   (c) range
+   (d) name

+   8. The following code will ____:
+   sum = 0;
+   for (row=0; row<N_ROW; row++)
+       sum += table[row][2];
+   (a) sum the values of row 2.
+   (b) sum the values of column 2.
+   (c) sum the values of row N_ROW.
+   (d) none of the above.

# Memory Snapshot Problems

Give the corresponding snapshots of memory after each of the following sets of statements is executed (use a question mark to indicate an array element that is not initialized):

+   9. int k, t[5];
+   ...
+   t[0] = 5;
+   for (k=0; k<=3; k++)
+       t[k+1] = t[k] + 3;