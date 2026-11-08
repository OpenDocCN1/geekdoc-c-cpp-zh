b. Derive a class `extRomanType` from the class `romanType` to do the following: In the class `extRomanType`, overload the arithmetic operators `+`, `-`, `*`, and `/` so that arithmetic operations can be performed on Roman numbers. Also, overload the pre- and post-increment and decrement operators as member functions of the class `extRomanType`.

To add (subtract, multiply, or divide) Roman numbers, add (subtract, multiply, or divide, respectively) their decimal representations and then convert the result to the Roman numeral format. For subtraction, if the first number is smaller than the second number, output a message saying that, “Because the first number is smaller than the second, the numbers cannot be subtracted”. Similarly, for division, the numerator must be larger than the denominator. Use similar conventions for the increment and decrement operators.

+   c. Write the definitions of the functions to overload the operators described in part b.
+   
+   d. Write a program to test your class.

15. Consider the class template `listType` designed to implement a list in a program. For illustration purposes, that example included only the sorting operation. Extend the definition of the class template to include the remove and search operations. Write the definitions of the member functions to implement the class template `listType`. Also, write a test program to test various operations on a list.

16. Consider the class `dateType` given in Chapter 11. In this class, add the functions to overload the increment and decrement operators to increase the date by a day and decrease the date by a day, respectively; relational operators to compare two dates; and stream operators for easy input and output. (Assume that the date is input and output in the form MM-DD-YYYY.) Also write a program to test your class.

17. Programming Exercise 14, Chapter 10, describes how to design the class `lineType` to implement a line. Redo this programming exercise so that the class `lineType`:

+   a. Overloads the stream insertion operator, `<<`, for easy output.
+   
+   b. Overloads the stream extraction operator, `>>`, for easy input. (The line `ax + by = c` is input as `(a, b, c)`.)
+   
+   c. Overloads the assignment operator to copy a line into another line.
+   
+   d. Overloads the unary operator `+`, as a member function, so that it returns true if a line is vertical; false otherwise.
+   
+   e. Overloads the unary operator `-`, as a member function, so that it returns true if a line is horizontal; false otherwise.
+   
+   f. Overloads the operator `==`, as a member function, so that it returns true if two lines are equal; false otherwise.