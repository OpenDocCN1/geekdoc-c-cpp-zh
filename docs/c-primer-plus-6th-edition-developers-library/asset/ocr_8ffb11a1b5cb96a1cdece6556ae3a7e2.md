# Programming Exercises

+   1. Modify the rain program in Listing 10.7 so that it does the calculations using pointers instead of subscripts. (You still have to declare and initialize the array.)
+   
+   2. Write a program that initializes an array-of-double and then copies the contents of the array into three other arrays. (All four arrays should be declared in the main program.) To make the first copy, use a function with array notation. To make the second copy, use a function with pointer notation and pointer incrementing. Have the first two functions take as arguments the name of the target array, the name of the source array, and the number of elements to be copied. Have the third function take as arguments the name of the target, the name of the source, and a pointer to the element following the last element of the source. That is, the function calls would look like this, given the following declarations:
+   
+   3. Write a function that returns the largest value stored in an array-of-int. Test the function in a simple program.
+   
+   4. Write a function that returns the index of the largest value stored in an array-of-double. Test the function in a simple program.
+   
+   5. Write a function that returns the difference between the largest and smallest elements of an array-of-double. Test the function in a simple program.
+   
+   6. Write a function that reverses the contents of an array of double and test it in a simple program.
+   
+   7. Write a program that initializes a two-dimensional array-of-double and uses one of the copy functions from exercise 2 to copy it to a second two-dimensional array. (Because a two-dimensional array is an array of arrays, a one-dimensional copy function can be used with each subarray.)
+   
+   8. Use a copy function from Programming Exercise 2 to copy the third through fifth elements of a seven-element array into a three-element array. The function itself need

```
double source[5] = {1.1, 2.2, 3.3, 4.4, 5.5};
double target1[5];
double target2[5];
double target3[5];
copy_arr(target1, source, 5);
copy_ptr(target2, source, 5);

copy_ptrs(target3, source, source + 5);
```