aList provided < is defined for type T objects. In this exercise, you must overload operator<() to define what it means for one user record to be less than another.

+   11. Design and implement a class `BigInt` whose values are large integers with perhaps hundreds of digits. Overload the addition operator to add two large integers. Treat each number as a list, each of whose elements is a block of digits of the number. Add the integers (lists) element by element, carrying from one element to the next when necessary.
+   
+   12. Proceed as in Problem 11, but add a subtraction operator. Write a two-function `BigInt` calculator program to test your class.
+   
+   13. Extend class `BigInt` from Problem 11 by overloading the multiplication operator.
+   
+   14. Extend class `BigInt` from Problem 11 by overloading the division operator (more challenging).

# Section 15.5

+   1. Write a program `binary` so that the command
+   
+      `binary DecimalValue`
+   
+      will calculate and display the binary representation of `DecimalValue`.
+   
+   2. The *median* of a list of *n* numbers is a value such that *n/2* of the values are greater than that value, and *n/2* of the values are less than that value. The usual procedure to find the median is to sort the list and then pick the middle number as the median if the list has an odd number of elements, or the average of the two middle numbers if the number of elements is even. Write a program to find the median of a list, so that the command
+   
+      `median FileName`
+   
+      will calculate and display the median of the values in file `FileName`, but the command
+   
+      `median`
+   
+      will calculate and display the median of a list of numbers entered from the keyboard.
+   
+   3. Write a program so that the following command will make a copy of `File1` with the name `File2`:
+   
+      `copy File1 File2`
+   
+   4. Write a program so that the following command will display the specified file on the screen, one page (23 lines) at a time, waiting between pages until the user presses some key:
+   
+      `page File`