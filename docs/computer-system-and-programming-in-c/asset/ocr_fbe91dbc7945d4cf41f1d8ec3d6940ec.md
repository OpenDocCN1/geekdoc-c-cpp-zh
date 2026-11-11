The general form of a multidimensional array is

**type array_name[s1][s2][s3]...[sm];**

The total number of elements in any dimension of arrays is the product of all sizes included in the declaration. So it becomes `s1*s2*s3*...*sm`.

For most applications, two dimension arrays serve. Three dimension is maximum that you can anticipate to go in normal applications. Still higher dimension arrays are needed in the field of scientific computing, weather forecasting, time-space analysis, etc.

# **DYNAMIC ALLOCATION OF ARRAYS OR ARRAYS OF UNKNOWN OR VARYING SIZE**

If we want to allocate the memory dynamically then we have to use the concept of dynamic allocation of arrays.

**The problems with fixed size arrays**
Declaring an array with a fixed size like `int a[10000];` has two typical problems:

+   - **Exceeding maximum.** Selecting a real maximum is often impossible because the programmer has no control over the size of the data sets the user is interested in. Erroneous assumptions that a maximum will never be exceeded are the source of many programming errors. Declaring very big arrays can be extremely wasteful of memory, and if there are many such arrays, may prevent the program from running in some systems.
+   - **No expansion.** Using a little size may be more efficient for the typical data set, but prevents the program from running with larger data sets. If array limits are not checked, large data sets will run over the end of an array with disastrous effects. Fixed size arrays cannot elaborate as needed.

These troubles can be avoided by dynamically allocating an array of the right size, or reallocating an array when it demands to expand. Both of these are done by declaring an array as a pointer and using the malloc/calloc function to allocate memory, and free function to free memory that is no longer needed.

The detail of this topic will be discussed in the Pointer chapter.

# **PASSING ARRAYS TO FUNCTIONS**

We can pass the single dimensional arrays as well as multidimensional arrays to the function. We will discuss these concepts one by one.

# *Single Dimensional Arrays*

Sometimes it is inconvenient to call a function that requires a long list of arguments.

One way around this, is to accumulate your variables into an array, then pass a **POINTER** to the array to the function. This method will be described in a great detail in the pointers section, but for now you need to know that the array is not actually passed to the function—just the array’s location in the memory. This is experienced as **PASS BY REFERENCE**. The name of an array references the array’s location in the memory, its **ADDRESS**.

If we write in max (int *) or int max (int []) the meaning of this line is that max is a function in which we pass the integer type of pointer, i.e. the complete array and according to that array it returns an integer type of variable.

# *Programming Problems*

# **Problem 1**

Write a program to input 5 numbers and print the sum of five numbers with the help of function.

# **Solution**

```
```c
#include <stdio.h>
int addNumbers(int fiveNumbers[]); /* declare function */
void main()
{
int array[5];
int i;
printf("Enter 5 integers separated by spaces: ");
for(i=0; i<5; i++)
{
scanf("%d", &array[i]);
```
```