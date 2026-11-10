+   - 12.4 Can we use the following statements?
+   
+         int i = 50; int *p = &i; p[4] = 100;
+   
+   - 12.5 The following code doesn't always fail. Why?
+   
+         int *p;
+         printf("%d", *p);
+   
+   - 12.6 If the pointer p points to the array arr, explain how pointer arithmetic works better with p than with arr.
+   - 12.7 How can two pointers be swapped using a function? Why can't the standard technique of using two pointers as arguments work here?
+   - 12.8 Explain how the use of **const** differs between the declaration of a variable in **main** and a parameter of a function.

# ## PROGRAMMING & DEBUGGING SKILLS

+   - 12.1 Write a program that declares and initializes two variables x and y to 10 and 20, respectively. Use two pointers to sum these values and print the result.
+   - 12.2 Write a program that declares three pointers of type `short *`, `int *` and `float *` pointing to regular variables. Prove that the size of the pointer has no relation to the size of the variable pointed to.
+   - 12.3 Use pointer arithmetic to prove that the size of the `char` data type is 1 byte.
+   - 12.4 Use a pointer to print the lowercase letters of the English alphabet.
+   - 12.5 Write a program that declares an `int` array of 10 elements. Using only pointer notation, populate the array with **scanf** and print the elements with **printf**.
+   - 12.6 Write a program where an `int` pointer `p` points to a variable `x` which is initialized to 10. Using only the `*`, `++` and `--` operators with `p`, (i) add 1 to the address of `x`, (ii) subtract 1 from `x`, (iii) add 1 to `x`.
+   - 12.7 Write a program that uses **scanf** to accept a word as string input. Using a pointer to a character array and without using array notation, compute the length of the string, i.e. until the NUL character is encountered.
+   - 12.8 Write a program to compute the sum of all elements of an `int` array using only pointers.

12.9 Correct the following program which issues a warning on compilation but fails at runtime. Does the **create_array** function return an array?

```
    #include <stdio.h>
    short * create_array(void);
    int main(void)
    {
        short i;
        short *brr;
        brr = create_array();
```