# Self-Review Exercises

# 6.1 Answer each of the following:

+   a) Lists and tables of values are stored in ______.
+   b) The number used to refer to a particular element of an array is called its ______.
+   c) A(n) ______ should be used to specify the size of an array because it makes the program more modifiable.
+   d) The process of placing the elements of an array in order is called ______ the array.
+   e) Determining whether an array contains a certain key value is called ______ the array.
+   f) An array that uses two indices is referred to as a(n) ______ array.

# 6.2 State whether the following are true or false. If the answer is false, explain why.

+   a) An array can store many different types of values.
+   b) An array index can be of data type double.
+   c) If there are fewer initializers in an initializer list than the number of elements in the array, C automatically initializes the remaining elements to the last value in the list of initializers.
+   d) It’s an error if an initializer list contains more initializers than there are array elements.
+   e) An individual array element that’s passed to a function as an argument of the form a[i] and modified in the called function will contain the modified value in the calling function.

# 6.3 Follow the instructions below regarding an array called fractions.

+   a) Define a symbolic constant SIZE to be replaced with the replacement text 10.
+   b) Define an array with SIZE elements of type double and initialize the elements to 0.
+   c) Refer to array element 4.
+   d) Assign the value 1.667 to array element nine.
+   e) Assign the value 3.333 to the seventh element of the array.
+   f) Print array elements 6 and 9 with two digits of precision to the right of the decimal point, and show the output that’s displayed on the screen.
+   g) Print all the elements of the array, using a for iteration statement. Assume the integer variable x has been defined as a control variable for the loop. Show the output.

# 6.4 Write statements to accomplish the following:

+   a) Define table to be an integer array and to have 3 rows and 3 columns. Assume the symbolic constant SIZE has been defined to be 3.
+   b) How many elements does the array table contain? Print the total number of elements.
+   c) Use a for iteration statement to initialize each element of table to the sum of its indices. Assume the integer variables x and y are defined as control variables.
+   d) Print the values of each element of array table. Assume the array was initialized with the definition:
+   int table[SIZE][SIZE] = {
+   { 1, 8 }, { 2, 4, 6 }, { 5 }
+   };

# 6.5 Find the error in each of the following program segments and correct the error.

+   a) #define SIZE 100;
+   b) SIZE = 10;
+   c) Assume int b[10] = { 0 };
+   for (i = 0; i <= 10; ++i) {
+   b[i] = 1;
+   }
+   d) #include <stdio.h>;
+   e) Assume int a[2][2] = { { 1, 2 }, { 3, 4 } };
+   a[1, 1] = 5;
+   f) #define VALUE = 120