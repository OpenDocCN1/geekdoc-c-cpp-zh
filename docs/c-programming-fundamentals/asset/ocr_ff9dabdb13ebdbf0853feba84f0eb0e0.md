# Exercises

# Theory Questions

+   1. What are exceptions? What are the differences between synchronous and asynchronous exceptions?
+   2. Explain the exception handling model of C++ with various constructs supported by it.
+   3. What is the syntax for indicating a list of exceptions that a function can raise? What happens if an unspecified exception is raised?
+   4. What happens when an exception is raised in a try block having a few constructed objects?
+   5. What happens when a raised exception is not caught by a catch block?
+   6. List the ten rules for handling exceptions successfully.

# Practical Questions

+   1. Write a program to demonstrate the catching of all exceptions.
+   2. Write a program in C++ to compute the square root of a number. The input value must be tested for validity. If it is negative, should the user-defined function my_sqrt() raise an exception?
+   3. Write a program in C++ that transfers the control to a user-defined terminate function when a raised exception is uncaught.
+   4. Write a program in C++ that installs the user-defined unexpected function to handle exceptions.
+   5. Write a program in C++ that divides two complex numbers. Overload the divide (/) operator. Can this program handle cases such as division-by-zero using exceptions?
+   6. Write a program in C++ for matrix multiplication. The matrix multiplication function should notify the user if the order of the matrix is invalid using exceptions.
+   7. Write a program in C++ to add two vectors. Each vector object, an instance of the class Vector, has the dynamic allocation of their data members. Can this program catch exceptions raised by new operators and take corrective actions?