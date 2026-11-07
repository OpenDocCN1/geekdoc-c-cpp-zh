+   f) Use a for statement to print the elements of array values using pointer/offset notation with the array name as the pointer.
+   
+   g) Use a for statement to print the elements of array values by subscripting the pointer to the array.
+   
+   h) Refer to the fifth element of values using array subscript notation, pointer/offset notation with the array name as the pointer, pointer subscript notation and pointer/offset notation.
+   
+   i) What address is referenced by `vPtr + 3`? What value is stored at that location?
+   
+   j) Assuming that `vPtr` points to `values[4]`, what address is referenced by `vPtr -= 4`? What value is stored at that location?

# ### 8.9  *(Write C++ Statements)*

For each of the following, write a single statement that performs the specified task. Assume that long integer array values1 and value2 have been declared and value1 has been initialized to 200000.

+   a) Declare the variable `longPtr` to be a pointer to an object of type long.
+   
+   b) Assign the address of variable `value1` to pointer variable `longPtr`.
+   
+   c) Print the value of the object pointed to by `longPtr`.
+   
+   d) Assign the value of the object pointed to by `longPtr` to variable `value2`.
+   
+   e) Print the value of `value2`.
+   
+   f) Print the address of `value1`.
+   
+   g) Print the address stored in `longPtr`. Is the value printed the same as `value1`’s address?

# ### 8.10  *(Function Headers and Prototypes)*

Perform the task specified by each of the following statements:

+   a) Write the function header for function `zero` that takes a long integer array parameter `bigIntegers` and does not return a value.
+   
+   b) Write the function prototype for the function in part (a).
+   
+   c) Write the function header for function `add1AndSum` that takes an integer array parameter `oneTooSmall` and returns an integer.
+   
+   d) Write the function prototype for the function described in part (c).

# ### 8.11  *(Find the Code Errors)*

Find the error in each of the following segments. If the error can be corrected, explain how.

```
a)  int *number;
    cout << number << endl;

b)  double *realPtr;
    long *integerPtr;
    integerPtr = realPtr;

c)  int *x, y;
    x = y;

d)  char s[] = "this is a character array";
    for ( ; *s != '\0'; ++s)
        cout << *s << ' ';

e)  short *numPtr, result;
    void *genericPtr = numPtr;
    result = *genericPtr + 7;

f)  double x = 19.34;
    double xPtr = &x;
    cout << xPtr << endl;
```

# ### 8.12  *(Simulation: The Tortoise and the Hare)*

In this exercise, you'll re-create the classic race of the tortoise and the hare. You’ll use random number generation to develop a simulation of this memorable event.