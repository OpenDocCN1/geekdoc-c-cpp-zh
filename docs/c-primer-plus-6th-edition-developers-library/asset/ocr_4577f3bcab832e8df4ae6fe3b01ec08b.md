not be altered; just choose the right actual arguments. (The actual arguments need not be an array name and array size. They only have to be the address of an array element and a number of elements to be processed.)

+   9. Write a program that initializes a two-dimensional 3×5 array-of-double and uses a VLA-based function to copy it to a second two-dimensional array. Also provide a VLA-based function to display the contents of the two arrays. The two functions should be capable, in general, of processing arbitrary N×M arrays. (If you don’t have access to a VLA-capable compiler, use the traditional C approach of functions that can process an N×5 array.)

+   10. Write a function that sets each element in an array to the sum of the corresponding elements in two other arrays. That is, if array 1 has the values 2, 4, 5, and 8 and array 2 has the values 1, 0, 4, and 6, the function assigns array 3 the values 3, 4, 9, and 14. The function should take three array names and an array size as arguments. Test the function in a simple program.

+   11. Write a program that declares a 3×5 array of int and initializes it to some values of your choice. Have the program print the values, double all the values, and then display the new values. Write a function to do the displaying and a second function to do the doubling. Have the functions take the array name and the number of rows as arguments.

+   12. Rewrite the rain program in Listing 10.7 so that the main tasks are performed by functions instead of in main().

+   13. Write a program that prompts the user to enter three sets of five double numbers each. (You may assume the user responds correctly and doesn’t enter non-numeric data.) The program should accomplish all of the following:
+   
+      a. Store the information in a 3×5 array.
+      b. Compute the average of each set of five values.
+      c. Compute the average of all the values.
+      d. Determine the largest value of the 15 values.
+      e. Report the results.
+   
+   Each major task should be handled by a separate function using the traditional C approach to handling arrays. Accomplish task “b” by using a function that computes and returns the average of a one-dimensional array; use a loop to call this function three times. The other tasks should take the entire array as an argument, and the functions performing tasks “c” and “d” should return the answer to the calling program.

+   14. Do Programming Exercise 13, but use variable-length array function parameters.