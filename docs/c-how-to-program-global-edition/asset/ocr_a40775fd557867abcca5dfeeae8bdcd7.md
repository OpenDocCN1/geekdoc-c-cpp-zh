+   6.5
+   
+   a) Error: Semicolon at the end of the `#define` preprocessor directive.  
+      Correction: Eliminate semicolon.
+   
+   b) Error: Assigning a value to a symbolic constant using an assignment statement.  
+      Correction: Assign a value to the symbolic constant in a `#define` preprocessor directive without using the assignment operator as in `#define SIZE 10`.
+   
+   c) Error: Referencing an array element outside the bounds of the array (b[10]).  
+      Correction: Change the final value of the control variable to 9.
+   
+   d) Error: Semicolon at the end of the `#include` preprocessor directive.  
+      Correction: Eliminate semicolon.
+   
+   e) Error: Array indexing done incorrectly.  
+      Correction: Change the statement to `a[1][1] = 5;`
+   
+   f) Error: Assigning a value to a symbolic constant using an assignment statement.  
+      Correction: Assign a value to the symbolic constant in a `#define` preprocessor directive without using the assignment operator as in `#define VALUE 120`.

# Exercises

6.6 Fill in the blanks in each of the following:

+   a) Arrays are ______ entities as they remain the same size during program execution.
+   
+   b) An array is a ______ group of memory locations that share the same ______.
+   
+   c) The first element in every array is the ______ element, for example, the first element of an array is referred to as ______.
+   
+   d) Array elements are referred by ______ followed by the ______ of the element.
+   
+   e) Arrays are passed to functions by ______.
+   
+   f) C has no array ______, which means a program can accidentally store data passing the bound of the array.
+   
+   g) The ______ operator cannot be used directly with arrays for copying data from one array to another.
+   
+   h) Every string contains a special string-termination character called the ______ character, represented by the character constant ______.
+   
+   i) A 5-by-7 array contains ______ rows, ______ columns and ______ elements
+   
+   j) The name of the element in the second row and third column of an array would be ______.

6.7 State which of the following are true and which are false. If false, explain why.

+   a) If there are fewer initializers in an initializer list than the number of elements in the array, the remaining elements will contain garbage values.
+   
+   b) A static local variable in a function definition exists for the duration of the program.
+   
+   c) The type `size_t` represents an unsigned integral type
+   
+   d) If the array size is omitted from a definition with an initializer list, the number of elements in the array will not be defined.
+   
+   e) To calculate the amount of memory used by an array, multiply the number of elements by the size in bytes each element occupies.
+   
+   f) When individual array elements are passed to a function, they are passed by reference and their modified value is retained in the calling function.

6.8 Write statements to accomplish each of the following:

+   a) Multiply the value of element 4 of an integer array `n` with 3 and display it.
+   
+   b) Write a loop that adds all the elements of the array `n[10]` and stores the result in `total`.
+   
+   c) Initialize each of the 9 elements of a two-dimensional integer array `n[3][3]` to 3, using loops.
+   
+   d) Find the largest and smallest element of a two dimensional array `sales[4][5]`.